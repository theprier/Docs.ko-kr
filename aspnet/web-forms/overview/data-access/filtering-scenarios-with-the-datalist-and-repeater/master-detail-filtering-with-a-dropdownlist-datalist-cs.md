---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-cs
title: 마스터/세부 정보 필터링 (C#) DropDownList 한 개로 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 단일 웹 페이지 'master' 레코드 및 DataList displ 표시할 Dropdownlist를 사용 하 여 마스터/세부 정보 보고서를 표시 하는 방법을 표시 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/18/2007
ms.topic: article
ms.assetid: 07fa47ae-e491-4a2f-b265-d342b9ddef46
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: 8af99dec92050f6d3b64919d06e7bc0ddc19e083
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389676"
---
<a name="masterdetail-filtering-with-a-dropdownlist-c"></a><span data-ttu-id="cb86c-103">마스터/세부 정보 (C#) DropDownList 한 개로 필터링</span><span class="sxs-lookup"><span data-stu-id="cb86c-103">Master/Detail Filtering With a DropDownList (C#)</span></span>
====================
<span data-ttu-id="cb86c-104">[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="cb86c-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="cb86c-105">[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_CS.exe) 또는 [PDF 다운로드](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/datatutorial33cs1.pdf)</span><span class="sxs-lookup"><span data-stu-id="cb86c-105">[Download Sample App](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_CS.exe) or [Download PDF](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/datatutorial33cs1.pdf)</span></span>

> <span data-ttu-id="cb86c-106">이 자습서 Dropdownlist를 사용 하 여 "마스터" 레코드와 "정보"를 표시 하는 DataList 표시 하려면 단일 웹 페이지에서 마스터/세부 정보 보고서를 표시 하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-106">In this tutorial we see how to display master/detail reports in a single web page using DropDownLists to display the "master" records and a DataList to display the "details".</span></span>


## <a name="introduction"></a><span data-ttu-id="cb86c-107">소개</span><span class="sxs-lookup"><span data-stu-id="cb86c-107">Introduction</span></span>

<span data-ttu-id="cb86c-108">마스터/세부 정보 보고서를 먼저 GridView를 사용 하 여 이전에 만든 [마스터/세부 정보 필터링으로 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) 일부 "마스터" 레코드 집합을 표시 하 여 자습서를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-108">The master/detail report, which we first created using a GridView in the earlier [Master/Detail Filtering With a DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) tutorial, begins by showing some set of "master" records.</span></span> <span data-ttu-id="cb86c-109">사용자를 살펴볼 수 아래로 마스터 레코드 중 하나 있으므로 해당 마스터 레코드의 세부 정보를 "." 보기</span><span class="sxs-lookup"><span data-stu-id="cb86c-109">The user can then drill down into one of the master records, thereby viewing that master record's "details."</span></span> <span data-ttu-id="cb86c-110">마스터/세부 정보 보고서는 이상적인에 일 대 다 관계를 시각화 하 고 (많은 열 임)는 특히 "와이드" 테이블에서 자세한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-110">Master/detail reports are an ideal choice for visualizing one-to-many relationships and for displaying detailed information from particularly "wide" tables (ones that have a lot of columns).</span></span> <span data-ttu-id="cb86c-111">이전 자습서에서 GridView 및 DetailsView 컨트롤을 사용 하 여 마스터/세부 정보 보고서를 구현 하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-111">We've explored how to implement master/detail reports using the GridView and DetailsView controls in previous tutorials.</span></span> <span data-ttu-id="cb86c-112">이 자습서에는 다음 두 DataList를 사용 하 여 포커스가 있지만 이러한 개념을 판별 됩니다 것 및 반복기 대신 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-112">In this tutorial and the next two, we'll reexamine these concepts, but focus on using DataList and Repeater controls instead.</span></span>

<span data-ttu-id="cb86c-113">이 자습서에서는 DropDownList를 사용 하 여 DataList에서 표시 되는 "details" 레코드를 사용 하 여 "마스터" 레코드를 포함 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-113">In this tutorial, we'll look at using a DropDownList to contain the "master" records, with the "details" records displayed in a DataList.</span></span>

## <a name="step-1-adding-the-masterdetail-tutorial-web-pages"></a><span data-ttu-id="cb86c-114">1 단계: 마스터/세부 자습서 웹 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="cb86c-114">Step 1: Adding the Master/Detail Tutorial Web Pages</span></span>

<span data-ttu-id="cb86c-115">이 자습서를 시작 하기 전에 먼저 살펴보겠습니다 폴더와이 자습서에는 다음 두 DataList 및 반복기 컨트롤을 사용 하 여 마스터/세부 정보 보고서를 사용 하 여 처리 해야 하는 ASP.NET 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-115">Before we start this tutorial, let's first take a moment to add the folder and ASP.NET pages we'll need for this tutorial and the next two dealing with master/detail reports using the DataList and Repeater controls.</span></span> <span data-ttu-id="cb86c-116">이라는 프로젝트에 새 폴더를 만들어 시작 `DataListRepeaterFiltering`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-116">Start by creating a new folder in the project named `DataListRepeaterFiltering`.</span></span> <span data-ttu-id="cb86c-117">다음으로 마스터 페이지를 사용 하도록 구성 된 모든 것이 폴더에 다음 5 개의 ASP.NET 페이지를 추가 `Site.master`:</span><span class="sxs-lookup"><span data-stu-id="cb86c-117">Next, add the following five ASP.NET pages to this folder, having all of them configured to use the master page `Site.master`:</span></span>

- `Default.aspx`
- `FilterByDropDownList.aspx`
- `CategoryListMaster.aspx`
- `ProductsForCategoryDetails.aspx`
- `CategoriesAndProducts.aspx`


![DataListRepeaterFiltering 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image1.png)

<span data-ttu-id="cb86c-119">**그림 1**: 만들기는 `DataListRepeaterFiltering` 폴더 및 자습서 ASP.NET 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="cb86c-119">**Figure 1**: Create a `DataListRepeaterFiltering` Folder and Add the Tutorial ASP.NET Pages</span></span>


<span data-ttu-id="cb86c-120">을 엽니다는 `Default.aspx` 끌어서 페이지를 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `UserControls` 디자인 화면으로 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-120">Next, open the `Default.aspx` page and drag the `SectionLevelTutorialListing.ascx` User Control from the `UserControls` folder onto the Design surface.</span></span> <span data-ttu-id="cb86c-121">만든이 사용자 정의 컨트롤을 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-cs.md) 자습서에서는 사이트 맵을 열거 하 고 글머리 기호 목록에 현재 섹션의 자습서를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-121">This User Control, which we created in the [Master Pages and Site Navigation](../introduction/master-pages-and-site-navigation-cs.md) tutorial, enumerates the site map and displays the tutorials from the current section in a bulleted list.</span></span>


<span data-ttu-id="cb86c-122">[![Default.aspx SectionLevelTutorialListing.ascx 사용자 컨트롤 추가](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="cb86c-122">[![Add the SectionLevelTutorialListing.ascx User Control to Default.aspx](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image2.png)</span></span>

<span data-ttu-id="cb86c-123">**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 `Default.aspx` ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="cb86c-123">**Figure 2**: Add the `SectionLevelTutorialListing.ascx` User Control to `Default.aspx` ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image4.png))</span></span>


<span data-ttu-id="cb86c-124">글머리 기호 목록을 표시 하기 위해 우리가 만들 것을 마스터/세부 자습서 해야 사이트 맵을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-124">In order to have the bulleted list display the master/detail tutorials we'll be creating, we need to add them to the site map.</span></span> <span data-ttu-id="cb86c-125">열기는 `Web.sitemap` 파일과 "표시 데이터와 the DataList 및 Repeater" 사이트 맵 노드 태그 뒤에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-125">Open the `Web.sitemap` file and add the following markup after the "Displaying Data with the DataList and Repeater" site map node markup:</span></span>

[!code-xml[Main](master-detail-filtering-with-a-dropdownlist-datalist-cs/samples/sample1.xml)]


![사이트 맵을 업데이트 하 여 새 ASP.NET 페이지를 포함 합니다.](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image5.png)

<span data-ttu-id="cb86c-127">**그림 3**: 사이트 맵을 업데이트 하 여 새 ASP.NET 페이지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-127">**Figure 3**: Update the Site Map to Include the New ASP.NET Pages</span></span>


## <a name="step-2-displaying-the-categories-in-a-dropdownlist"></a><span data-ttu-id="cb86c-128">2 단계: DropDownList에 범주를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-128">Step 2: Displaying the Categories in a DropDownList</span></span>

<span data-ttu-id="cb86c-129">마스터/세부 정보 보고서는 선택한 목록 항목의 제품이 표시를 사용 하 여 DropDownList, 범주 표시 페이지 DataList에서 더 아래쪽 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-129">Our master/detail report will list the categories in a DropDownList, with the selected list item's products displayed further down in the page in a DataList.</span></span> <span data-ttu-id="cb86c-130">첫 번째 작업을 미리 한는 DropDownList에 표시 되는 범주를 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-130">The first task ahead of us, then, is to have the categories displayed in a DropDownList.</span></span> <span data-ttu-id="cb86c-131">열어서 시작 합니다 `FilterByDropDownList.aspx` 페이지에 `DataListRepeaterFiltering` 폴더 및 페이지의 디자이너 도구 상자에서 끌어서 DropDownList.</span><span class="sxs-lookup"><span data-stu-id="cb86c-131">Start by opening the `FilterByDropDownList.aspx` page in the `DataListRepeaterFiltering` folder and drag a DropDownList from the Toolbox onto the page's designer.</span></span> <span data-ttu-id="cb86c-132">다음으로 DropDownList를 설정 `ID` 속성을 `Categories`입니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-132">Next, set the DropDownList's `ID` property to `Categories`.</span></span> <span data-ttu-id="cb86c-133">DropDownList의 스마트 태그의 데이터 소스 선택 링크를 클릭 하 고 라는 새로운 ObjectDataSource는 만들 `CategoriesDataSource`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-133">Click on the Choose Data Source link from the DropDownList's smart tag and create a new ObjectDataSource named `CategoriesDataSource`.</span></span>


<span data-ttu-id="cb86c-134">[![CategoriesDataSource 라는 새 ObjectDataSource를 추가 합니다.](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="cb86c-134">[![Add a New ObjectDataSource Named CategoriesDataSource](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image6.png)</span></span>

<span data-ttu-id="cb86c-135">**그림 4**: 새 ObjectDataSource 라는 추가 `CategoriesDataSource` ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="cb86c-135">**Figure 4**: Add a New ObjectDataSource Named `CategoriesDataSource` ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image8.png))</span></span>


<span data-ttu-id="cb86c-136">호출 되도록 새 ObjectDataSource를 구성 합니다 `CategoriesBLL` 클래스의 `GetCategories()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="cb86c-136">Configure the new ObjectDataSource such that it invokes the `CategoriesBLL` class's `GetCategories()` method.</span></span> <span data-ttu-id="cb86c-137">DropDownList에 어떤 데이터 원본 필드를 표시 해야 하 고는 지정 해야 하는 ObjectDataSource를 구성한 후 각 목록 항목에 대 한 값으로 연결 해야 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-137">After configuring the ObjectDataSource we still need to specify what data source field should be displayed in the DropDownList and which one should be associated as the value for each list item.</span></span> <span data-ttu-id="cb86c-138">있어야 합니다 `CategoryName` 필드를 표시 및 `CategoryID` 각 목록 항목에 대 한 값으로.</span><span class="sxs-lookup"><span data-stu-id="cb86c-138">Have the `CategoryName` field as the display and `CategoryID` as the value for each list item.</span></span>


<span data-ttu-id="cb86c-139">[![가 DropDownList 표시를 사용 하 여 CategoryID와 CategoryName 필드 값](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="cb86c-139">[![Have the DropDownList Display the CategoryName Field and Use CategoryID as the Value](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image9.png)</span></span>

<span data-ttu-id="cb86c-140">**그림 5**: DropDownList을 표시 합니다 `CategoryName` 필드 및 사용 `CategoryID` 값으로 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image11.png))</span><span class="sxs-lookup"><span data-stu-id="cb86c-140">**Figure 5**: Have the DropDownList Display the `CategoryName` Field and Use `CategoryID` as the Value ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image11.png))</span></span>


<span data-ttu-id="cb86c-141">이 시점에서 레코드를 사용 하 여 채워지는 DropDownList 컨트롤이 있습니다를 `Categories` 테이블 (모두 약 6 초 후에 수행).</span><span class="sxs-lookup"><span data-stu-id="cb86c-141">At this point we have a DropDownList control that's populated with the records from the `Categories` table (all accomplished in about six seconds).</span></span> <span data-ttu-id="cb86c-142">그림 6 브라우저를 통해 볼 때 지금 진행 상황을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-142">Figure 6 shows our progress thus far when viewed through a browser.</span></span>


<span data-ttu-id="cb86c-143">[![현재 범주를 나열 하는 드롭다운](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="cb86c-143">[![A Drop-Down Lists the Current Categories](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image12.png)</span></span>

<span data-ttu-id="cb86c-144">**그림 6**:는 드롭다운 목록이 현재 범주 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="cb86c-144">**Figure 6**: A Drop-Down Lists the Current Categories ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image14.png))</span></span>


## <a name="step-2-adding-the-products-datalist"></a><span data-ttu-id="cb86c-145">2 단계: 추가 제품 DataList</span><span class="sxs-lookup"><span data-stu-id="cb86c-145">Step 2: Adding the Products DataList</span></span>

<span data-ttu-id="cb86c-146">마스터/세부 정보 보고서의 마지막 단계는 선택한 범주와 관련 된 제품을 나열 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-146">The last step in our master/detail report is to list the products associated with the selected category.</span></span> <span data-ttu-id="cb86c-147">이렇게 하려면 페이지로 DataList를 추가 하 고 라는 새로운 ObjectDataSource는 만들 `ProductsByCategoryDataSource`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-147">To accomplish this, add a DataList to the page and create a new ObjectDataSource named `ProductsByCategoryDataSource`.</span></span> <span data-ttu-id="cb86c-148">가 합니다 `ProductsByCategoryDataSource` 컨트롤에서 해당 데이터를 검색 합니다 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드.</span><span class="sxs-lookup"><span data-stu-id="cb86c-148">Have the `ProductsByCategoryDataSource` control retrieve its data from the `ProductsBLL` class's `GetProductsByCategoryID(categoryID)` method.</span></span> <span data-ttu-id="cb86c-149">이 마스터/세부 정보 보고서 읽기 전용 이므로 INSERT, UPDATE 및 DELETE 탭 옵션 (없음)을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-149">Since this master/detail report is read-only, choose the (None) option in the INSERT, UPDATE, and DELETE tabs.</span></span>


<span data-ttu-id="cb86c-150">[![GetProductsByCategoryID(categoryID) 메서드를 선택 합니다.](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="cb86c-150">[![Select the GetProductsByCategoryID(categoryID) Method](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image15.png)</span></span>

<span data-ttu-id="cb86c-151">**그림 7**: 선택 된 `GetProductsByCategoryID(categoryID)` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image17.png))</span><span class="sxs-lookup"><span data-stu-id="cb86c-151">**Figure 7**: Select the `GetProductsByCategoryID(categoryID)` Method ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image17.png))</span></span>


<span data-ttu-id="cb86c-152">다음을 클릭 한 후 ObjectDataSource 마법사 요청에 대 한 값의 출처를 `GetProductsByCategoryID(categoryID)` 메서드의 *`categoryID`* 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-152">After clicking Next, the ObjectDataSource wizard prompts us for the source of the value for the `GetProductsByCategoryID(categoryID)` method's *`categoryID`* parameter.</span></span> <span data-ttu-id="cb86c-153">선택한 값을 사용 하도록 `categories` DropDownList 항목으로 매개 변수 원본 컨트롤과를 ControlID `Categories`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-153">To use the value of the selected `categories` DropDownList item set the Parameter source to Control and the ControlID to `Categories`.</span></span>


<span data-ttu-id="cb86c-154">[![CategoryID 매개 변수 범주 DropDownList의 값으로 설정](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="cb86c-154">[![Set the categoryID Parameter to the Value of the Categories DropDownList](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image18.png)</span></span>

<span data-ttu-id="cb86c-155">**그림 8**: 설정 합니다 *`categoryID`* 매개 변수 값으로는 `Categories` DropDownList ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="cb86c-155">**Figure 8**: Set the *`categoryID`* Parameter to the Value of the `Categories` DropDownList ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image20.png))</span></span>


<span data-ttu-id="cb86c-156">Visual Studio에서 자동으로 데이터 소스 구성 마법사를 완료 하면 생성 된 `ItemTemplate` 이름과 각 데이터 필드의 값을 표시 하는 DataList에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-156">Upon completing the Configure Data Source wizard, Visual Studio will automatically generate an `ItemTemplate` for the DataList that displays the name and value of each data field.</span></span> <span data-ttu-id="cb86c-157">대신 사용 하 여 DataList를 개선해 보겠습니다를 `ItemTemplate` 제품의 이름, 범주, 공급자, 단위 및 함께 가격 당 수량만을 표시 하는 `SeparatorTemplate` 삽입 하는 `<hr>` 각 항목 사이 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-157">Let's enhance the DataList to instead use an `ItemTemplate` that displays just the product's name, category, supplier, quantity per unit, and price along with a `SeparatorTemplate` that injects an `<hr>` element between each item.</span></span> <span data-ttu-id="cb86c-158">사용 하려는 `ItemTemplate` 에서 예제로는 [DataList 및 반복기 컨트롤을 사용 하 여 데이터 표시](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-cs.md) 자습서에서는 있지만 자유롭게 가장 좋고 찾아야는 어떤 템플릿 태그를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-158">I'm going to use the `ItemTemplate` from an example in the [Displaying Data with the DataList and Repeater Controls](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-cs.md) tutorial, but feel free to use whatever template markup you find most visually appealing.</span></span>

<span data-ttu-id="cb86c-159">다음과 같이 변경한 후에 DataList 및 해당 ObjectDataSource의 태그가 다음과 비슷하게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-159">After making these changes, your DataList and its ObjectDataSource's markup should look similar to the following:</span></span>

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-cs/samples/sample2.aspx)]

<span data-ttu-id="cb86c-160">시간을 내어 브라우저에서 진행 상황을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-160">Take a moment to check out our progress in a browser.</span></span> <span data-ttu-id="cb86c-161">페이지를 처음 방문 하는 경우 (음료) 선택한 범주에 속하는 제품 같이 표시 됩니다 (그림 9에서), 있지만 DropDownList 변경 데이터를 업데이트 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-161">When first visiting the page, those products belonging to the selected category (Beverages) are displayed (as shown in Figure 9), but changing the DropDownList doesn't update the data.</span></span> <span data-ttu-id="cb86c-162">즉, DataList 업데이트에 대 한 포스트백을 발생 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-162">This is because a postback must occur for the DataList to update.</span></span> <span data-ttu-id="cb86c-163">DropDownList의 설정에 이렇게 수행할 수 있습니다 `AutoPostBack` 속성을 `true` 또는 페이지에 단추 웹 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-163">To accomplish this we can either set the DropDownList's `AutoPostBack` property to `true` or add a Button Web control to the page.</span></span> <span data-ttu-id="cb86c-164">DropDownList의 설정에 여러분도이 자습서용 `AutoPostBack` 속성을 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-164">For this tutorial, I've opted to set the DropDownList's `AutoPostBack` property to `true`.</span></span>

<span data-ttu-id="cb86c-165">그림 9와 10 중인 마스터/세부 정보 보고서를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-165">Figures 9 and 10 illustrate the master/detail report in action.</span></span>


<span data-ttu-id="cb86c-166">[![먼저 페이지를 방문 하 고, 음료 제품 표시 됩니다.](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="cb86c-166">[![When First Visiting the Page, the Beverage Products are Displayed](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image21.png)</span></span>

<span data-ttu-id="cb86c-167">**그림 9**: 먼저 페이지를 방문 하 고, 음료 제품 표시 됩니다 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image23.png))</span><span class="sxs-lookup"><span data-stu-id="cb86c-167">**Figure 9**: When First Visiting the Page, the Beverage Products are Displayed ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image23.png))</span></span>


<span data-ttu-id="cb86c-168">[![새 제품 (생성)을 선택 하면 자동으로 포스트백, DataList를 업데이트 하는 중](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image24.png)</span><span class="sxs-lookup"><span data-stu-id="cb86c-168">[![Selecting a New Product (Produce) Automatically Causes a PostBack, Updating the DataList](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image24.png)</span></span>

<span data-ttu-id="cb86c-169">**그림 10**: 새 제품 (생성)을 선택 하면 자동으로 포스트백, DataList를 업데이트 하는 중 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="cb86c-169">**Figure 10**: Selecting a New Product (Produce) Automatically Causes a PostBack, Updating the DataList ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image26.png))</span></span>


## <a name="adding-a----choose-a-category----list-item"></a><span data-ttu-id="cb86c-170">"-범주-" 선택 목록 항목 추가</span><span class="sxs-lookup"><span data-stu-id="cb86c-170">Adding a "-- Choose a Category --" List Item</span></span>

<span data-ttu-id="cb86c-171">먼저 방문할 때는 `FilterByDropDownList.aspx` DropDownList의 첫 번째 목록 항목 (음료)는 선택, 기본적으로 DataList에서 음료 제품을 보여 주는 범주 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-171">When first visiting the `FilterByDropDownList.aspx` page the categories DropDownList's first list item (Beverages) is selected by default, showing the beverage products in the DataList.</span></span> <span data-ttu-id="cb86c-172">에 *마스터/세부 정보 필터링으로 DropDownList* "-범주 선택-" 옵션을 기본적으로 선택을 선택 하면 표시 DropDownList에 추가한 자습서 *모든* 의 데이터베이스에서 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-172">In the *Master/Detail Filtering With a DropDownList* tutorial we added a "-- Choose a Category --" option to the DropDownList that was selected by default and, when selected, displayed *all* of the products in the database.</span></span> <span data-ttu-id="cb86c-173">이러한 접근 방식을 처럼 관리할 수는 GridView에 제품을 나열 하는 경우 각 제품 행 적은 양의 화면 공간을 차지 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-173">Such an approach was manageable when listing the products in a GridView, as each product row took up a small amount of screen real estate.</span></span> <span data-ttu-id="cb86c-174">그러나 DataList를 사용 하 여 각 제품 정보가 훨씬 큰 청크의 화면을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-174">With the DataList, however, each product's information consumes a much larger chunk of the screen.</span></span> <span data-ttu-id="cb86c-175">여전히 보겠습니다 "-범주 선택-" 옵션을 추가 및 기본적으로 선택 게 이지만 모든 제품을 표시 하는 대신 옵션을 선택 하면 보겠습니다 구성할 제품이 없습니다. 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-175">Let's still add a "-- Choose a Category --" option and have it selected by default, but instead of having it show all products when selected, let's configure it so that it shows no products.</span></span>

<span data-ttu-id="cb86c-176">DropDownList에 새 목록 항목을 추가 하려면 속성 창으로 이동 하 고에서 줄임표를 클릭 합니다 `Items` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-176">To add a new list item to the DropDownList, go to the Properties window and click on the ellipses in the `Items` property.</span></span> <span data-ttu-id="cb86c-177">사용 하 여 새 목록 항목을 추가 합니다 `Text` "-범주 선택-" 및 `Value` `0`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-177">Add a new list item with the `Text` "-- Choose a Category --" and the `Value` `0`.</span></span>


![추가](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image27.png)

<span data-ttu-id="cb86c-179">**그림 11**: "-범주-" 선택 목록 항목 추가</span><span class="sxs-lookup"><span data-stu-id="cb86c-179">**Figure 11**: Add a "-- Choose a Category --" List Item</span></span>


<span data-ttu-id="cb86c-180">또는 드롭다운 목록에 다음 태그를 추가 하 여 목록 항목을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-180">Alternatively, you can add the list item by adding the following markup to the DropDownList:</span></span>

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-cs/samples/sample3.aspx)]

<span data-ttu-id="cb86c-181">또한 DropDownList 컨트롤을 설정 해야 `AppendDataBoundItems` 하 `true` 때문에로 설정 된 경우 `false` (기본값), 수동으로 추가 된 목록을 덮어씁니다 ObjectDataSource의 범주 DropDownList에 바인딩된 경우 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-181">Additionally, we need to set the DropDownList control's `AppendDataBoundItems` to `true` because if it's set to `false` (the default), when the categories are bound to the DropDownList from the ObjectDataSource they'll overwrite any manually-added list items.</span></span>


![AppendDataBoundItems 속성도 True로 설정](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image28.png)

<span data-ttu-id="cb86c-183">**그림 12**: 설정의 `AppendDataBoundItems` 속성을 true로</span><span class="sxs-lookup"><span data-stu-id="cb86c-183">**Figure 12**: Set the `AppendDataBoundItems` Property to True</span></span>


<span data-ttu-id="cb86c-184">값 선택 이유 `0` "-범주 선택-" 목록에 대 한 항목은에 있기 때문에 없는 범주 값을 사용 하 여 시스템 `0`, "-범주-" 선택 목록 항목이 선택 될 때 제품 레코드가 반환 될 따라서 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-184">The reason we chose the value `0` for the "-- Choose a Category --" list item is because there are no categories in the system with a value of `0`, hence no product records will be returned when the "-- Choose a Category --" list item is selected.</span></span> <span data-ttu-id="cb86c-185">이 확인 하려면 잠시 브라우저를 통해 페이지를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-185">To confirm this, take a moment to visit the page through a browser.</span></span> <span data-ttu-id="cb86c-186">와 같이 그림 13, 처음에 페이지를 보고 "-범주-" 선택 목록 항목을 선택 하면 제품이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-186">As Figure 13 shows, when initially viewing the page the "-- Choose a Category --" list item is selected and no products are displayed.</span></span>


<span data-ttu-id="cb86c-187">[![경우는](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="cb86c-187">[![When the](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image29.png)</span></span>

<span data-ttu-id="cb86c-188">**그림 13**: 아니요 제품이 표시 되는 "-범주-" 선택 목록 항목을 선택 하면 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image31.png))</span><span class="sxs-lookup"><span data-stu-id="cb86c-188">**Figure 13**: When the "-- Choose a Category --" List Item is Selected, No Products are Displayed ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-cs/_static/image31.png))</span></span>


<span data-ttu-id="cb86c-189">대신 표시 하는 경우 *모든* 제품 "-범주 선택-" 옵션을 선택 하면 값이 사용 됩니다. `-1` 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-189">If you'd rather display *all* of the products when the "-- Choose a Category --" option is selected, use a value of `-1` instead.</span></span> <span data-ttu-id="cb86c-190">예리한 독자는 다시 기억 하겠지만 합니다 *마스터/세부 정보 필터링으로 DropDownList* 업데이트 하는 자습서를 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드 있도록 경우를 *`categoryID`* 값 `-1` 레코드가 반환 된 모든 제품에 전달 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-190">The astute reader will recall that back in the *Master/Detail Filtering With a DropDownList* tutorial we updated the `ProductsBLL` class's `GetProductsByCategoryID(categoryID)` method so that if a *`categoryID`* value of `-1` was passed in, all product records were returned.</span></span>

## <a name="summary"></a><span data-ttu-id="cb86c-191">요약</span><span class="sxs-lookup"><span data-stu-id="cb86c-191">Summary</span></span>

<span data-ttu-id="cb86c-192">계층적으로 관련 데이터를 표시할 때 종종 사용자 계층의 최상위에서 데이터를 읽는 데 시작 하 고 세부 정보로 드릴 다운 하는 마스터/세부 정보 보고서를 사용 하 여 데이터를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-192">When displaying hierarchically-related data, it often helps to present the data using master/detail reports, from which the user can start perusing the data from the top of the hierarchy and drill down into details.</span></span> <span data-ttu-id="cb86c-193">이 자습서에서는 선택한 범주의 제품을 표시 하는 간단한 마스터/세부 정보 보고서 작성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-193">In this tutorial we examined building a simple master/detail report showing a selected category's products.</span></span> <span data-ttu-id="cb86c-194">이 작업은 범주 및 선택한 범주에 속하는 제품 DataList 목록은 DropDownList를 사용 하 여 수행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-194">This was accomplished by using a DropDownList for the list of categories and a DataList for the products belonging to the selected category.</span></span>

<span data-ttu-id="cb86c-195">다음 자습서 두 페이지에 걸쳐 마스터 및 세부 정보 레코드를 구분 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-195">In the next tutorial we'll look at separating the master and details records across two pages.</span></span> <span data-ttu-id="cb86c-196">첫 번째 페이지에서 "마스터" 레코드 목록을 표시할 세부 정보를 보려면 링크를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-196">In the first page, a list of "master" records will be displayed, with a link to view the details.</span></span> <span data-ttu-id="cb86c-197">링크를 클릭 하면 선택한 마스터 레코드의 세부 정보를 표시 하는 두 번째 페이지로 whisk 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-197">Clicking on the link will whisk the user to the second page, which will display the details for the selected master record.</span></span>

<span data-ttu-id="cb86c-198">즐거운 프로그래밍!</span><span class="sxs-lookup"><span data-stu-id="cb86c-198">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="cb86c-199">저자 소개</span><span class="sxs-lookup"><span data-stu-id="cb86c-199">About the Author</span></span>

<span data-ttu-id="cb86c-200">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-200">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="cb86c-201">Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-201">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="cb86c-202">최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-202">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="cb86c-203">그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="cb86c-203">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span> <span data-ttu-id="cb86c-204">찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-204">or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="cb86c-205">특별히 감사 하는 중...</span><span class="sxs-lookup"><span data-stu-id="cb86c-205">Special Thanks To…</span></span>

<span data-ttu-id="cb86c-206">이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-206">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="cb86c-207">이 자습서에 대 한 선행 검토자 Randy Schmidt 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cb86c-207">Lead reviewer for this tutorial was Randy Schmidt.</span></span> <span data-ttu-id="cb86c-208">내 향후 MSDN 문서를 검토에 관심이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="cb86c-208">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="cb86c-209">그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="cb86c-209">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="cb86c-210">다음</span><span class="sxs-lookup"><span data-stu-id="cb86c-210">Next</span></span>](master-detail-filtering-acess-two-pages-datalist-cs.md)
