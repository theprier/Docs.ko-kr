---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
title: 마스터/세부 DropDownList (VB)를 사용 하 여 필터링 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 displ 하려면 'master' 레코드와 DataList를 표시 하려면 dropdownlist 활용을 사용 하 여 단일 웹 페이지에서 마스터/세부 보고서를 표시 하는 방법을 표시 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/18/2007
ms.topic: article
ms.assetid: ad0f1014-1eff-465f-bdc6-93058de00e44
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: e4ece466319e268a74bbe8c4ed96ffc33cff432f
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30880689"
---
<a name="masterdetail-filtering-with-a-dropdownlist-vb"></a><span data-ttu-id="91c84-103">마스터/세부 DropDownList (VB)를 사용 하 여 필터링</span><span class="sxs-lookup"><span data-stu-id="91c84-103">Master/Detail Filtering With a DropDownList (VB)</span></span>
====================
<span data-ttu-id="91c84-104">으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="91c84-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="91c84-105">[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_VB.exe) 또는 [PDF 다운로드](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/datatutorial33vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="91c84-105">[Download Sample App](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_VB.exe) or [Download PDF](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/datatutorial33vb1.pdf)</span></span>

> <span data-ttu-id="91c84-106">이 자습서에서는 dropdownlist 활용을 사용 하 여 "마스터" 레코드와 "정보"를 표시 하려면 DataList 표시 하려면 단일 웹 페이지에서 마스터/세부 보고서를 표시 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-106">In this tutorial we see how to display master/detail reports in a single web page using DropDownLists to display the "master" records and a DataList to display the "details".</span></span>


## <a name="introduction"></a><span data-ttu-id="91c84-107">소개</span><span class="sxs-lookup"><span data-stu-id="91c84-107">Introduction</span></span>

<span data-ttu-id="91c84-108">마스터/세부 정보 보고서에는 먼저는 GridView를 사용 하 여 이전에 만든 [마스터/세부 정보 필터링 된 정도 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) 자습서에서는 몇 가지 "마스터" 레코드 집합을 표시 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-108">The master/detail report, which we first created using a GridView in the earlier [Master/Detail Filtering With a DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) tutorial, begins by showing some set of "master" records.</span></span> <span data-ttu-id="91c84-109">사용자는 다음으로 드릴 다운할 수 마스터 레코드 중 하나 함으로써 해당 마스터 레코드의 세부 정보를 "." 보기</span><span class="sxs-lookup"><span data-stu-id="91c84-109">The user can then drill down into one of the master records, thereby viewing that master record's "details."</span></span> <span data-ttu-id="91c84-110">마스터/세부 정보 보고서는 일 대 다 관계를 시각화 하 고 (더 많은 열이 있는)는 특히 "와이드" 테이블에서 자세한 정보를 표시 하는 것에 대 한 적합 한 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-110">Master/detail reports are an ideal choice for visualizing one-to-many relationships and for displaying detailed information from particularly "wide" tables (ones that have a lot of columns).</span></span> <span data-ttu-id="91c84-111">이전 자습서에서 GridView 및 DetailsView 컨트롤을 사용 하 여 마스터/세부 보고서를 구현 하는 방법에서 살펴본 했습니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-111">We've explored how to implement master/detail reports using the GridView and DetailsView controls in previous tutorials.</span></span> <span data-ttu-id="91c84-112">이 자습서에는 다음 두 DataList를 사용 하 여에 집중 되지만 이러한 개념을 다시 검사할 수 우리 및 반복기 대신 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-112">In this tutorial and the next two, we'll reexamine these concepts, but focus on using DataList and Repeater controls instead.</span></span>

<span data-ttu-id="91c84-113">이 자습서에서는 DropDownList를 사용 하 여 DataList에 표시 된 "details" 레코드 "마스터" 레코드를 포함 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-113">In this tutorial, we'll look at using a DropDownList to contain the "master" records, with the "details" records displayed in a DataList.</span></span>

## <a name="step-1-adding-the-masterdetail-tutorial-web-pages"></a><span data-ttu-id="91c84-114">1 단계: 마스터/세부 자습서 웹 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="91c84-114">Step 1: Adding the Master/Detail Tutorial Web Pages</span></span>

<span data-ttu-id="91c84-115">이 자습서를 시작 하기 전에 먼저 간단히 살펴보겠습니다 폴더와이 자습서와 다음 두 DataList 및 반복기 제어를 사용 하 여 마스터/세부 보고서 처리에 대 한 사용 해야 하는 ASP.NET 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-115">Before we start this tutorial, let's first take a moment to add the folder and ASP.NET pages we'll need for this tutorial and the next two dealing with master/detail reports using the DataList and Repeater controls.</span></span> <span data-ttu-id="91c84-116">시작 이라는 프로젝트에 새 폴더를 만들어서 `DataListRepeaterFiltering`합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-116">Start by creating a new folder in the project named `DataListRepeaterFiltering`.</span></span> <span data-ttu-id="91c84-117">다음으로 마스터 페이지를 사용 하도록 구성 된 모두이 폴더에 다음과 같은 5 개의 ASP.NET 페이지를 추가 `Site.master`:</span><span class="sxs-lookup"><span data-stu-id="91c84-117">Next, add the following five ASP.NET pages to this folder, having all of them configured to use the master page `Site.master`:</span></span>

- `Default.aspx`
- `FilterByDropDownList.aspx`
- `CategoryListMaster.aspx`
- `ProductsForCategoryDetails.aspx`
- `CategoriesAndProducts.aspx`


![DataListRepeaterFiltering 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image1.png)

<span data-ttu-id="91c84-119">**그림 1**: 만들기는 `DataListRepeaterFiltering` 폴더 자습서 ASP.NET 페이지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-119">**Figure 1**: Create a `DataListRepeaterFiltering` Folder and Add the Tutorial ASP.NET Pages</span></span>


<span data-ttu-id="91c84-120">을 열고는 `Default.aspx` 끌어서 페이지는 `SectionLevelTutorialListing.ascx` 에서 사용자 정의 컨트롤의 `UserControls` 디자인 화면으로 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-120">Next, open the `Default.aspx` page and drag the `SectionLevelTutorialListing.ascx` User Control from the `UserControls` folder onto the Design surface.</span></span> <span data-ttu-id="91c84-121">만든이 사용자 정의 컨트롤의 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-vb.md) 자습서에서는 사이트 맵을 열거 하 고 글머리 기호 목록에서 현재 섹션의 자습서를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-121">This User Control, which we created in the [Master Pages and Site Navigation](../introduction/master-pages-and-site-navigation-vb.md) tutorial, enumerates the site map and displays the tutorials from the current section in a bulleted list.</span></span>


<span data-ttu-id="91c84-122">[![Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="91c84-122">[![Add the SectionLevelTutorialListing.ascx User Control to Default.aspx](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image2.png)</span></span>

<span data-ttu-id="91c84-123">**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="91c84-123">**Figure 2**: Add the `SectionLevelTutorialListing.ascx` User Control to `Default.aspx` ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image4.png))</span></span>


<span data-ttu-id="91c84-124">글머리 기호 목록을 표시 하기 위해 म 만들게 됩니다, 마스터/세부 자습서 해야 사이트 맵에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-124">In order to have the bulleted list display the master/detail tutorials we'll be creating, we need to add them to the site map.</span></span> <span data-ttu-id="91c84-125">열기는 `Web.sitemap` 파일을 "표시 데이터와 the DataList 및 반복기" 사이트 맵 노드 태그 뒤에 다음 태그를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-125">Open the `Web.sitemap` file and add the following markup after the "Displaying Data with the DataList and Repeater" site map node markup:</span></span>

[!code-xml[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample1.xml)]


![새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image5.png)

<span data-ttu-id="91c84-127">**그림 3**: 새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트</span><span class="sxs-lookup"><span data-stu-id="91c84-127">**Figure 3**: Update the Site Map to Include the New ASP.NET Pages</span></span>


## <a name="step-2-displaying-the-categories-in-a-dropdownlist"></a><span data-ttu-id="91c84-128">2 단계: DropDownList에 범주를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-128">Step 2: Displaying the Categories in a DropDownList</span></span>

<span data-ttu-id="91c84-129">마스터/세부 정보 보고서는 선택한 목록 항목의 제품이 표시와 DropDownList에서 범주별 나열 됩니다 아래로 DataList의 페이지에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-129">Our master/detail report will list the categories in a DropDownList, with the selected list item's products displayed further down in the page in a DataList.</span></span> <span data-ttu-id="91c84-130">그런 다음 미리 us, 첫 번째 작업 범주 DropDownList에 표시 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-130">The first task ahead of us, then, is to have the categories displayed in a DropDownList.</span></span> <span data-ttu-id="91c84-131">열어 시작는 `FilterByDropDownList.aspx` 페이지에 `DataListRepeaterFiltering` 폴더와 페이지의 디자이너 도구 상자에서 끌어서 DropDownList 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-131">Start by opening the `FilterByDropDownList.aspx` page in the `DataListRepeaterFiltering` folder and drag a DropDownList from the Toolbox onto the page's designer.</span></span> <span data-ttu-id="91c84-132">다음으로 DropDownList 설정 `ID` 속성을 `Categories`합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-132">Next, set the DropDownList's `ID` property to `Categories`.</span></span> <span data-ttu-id="91c84-133">DropDownList의 스마트 태그에서 데이터 소스 선택 링크를 클릭 하 고 라는 새 ObjectDataSource 만들 `CategoriesDataSource`합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-133">Click on the Choose Data Source link from the DropDownList's smart tag and create a new ObjectDataSource named `CategoriesDataSource`.</span></span>


<span data-ttu-id="91c84-134">[![CategoriesDataSource 라는 새 ObjectDataSource를 추가 합니다.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="91c84-134">[![Add a New ObjectDataSource Named CategoriesDataSource](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image6.png)</span></span>

<span data-ttu-id="91c84-135">**그림 4**: 새 ObjectDataSource 라는 추가 `CategoriesDataSource` ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="91c84-135">**Figure 4**: Add a New ObjectDataSource Named `CategoriesDataSource` ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image8.png))</span></span>


<span data-ttu-id="91c84-136">새 ObjectDataSource 호출 갖도록 구성 해야는 `CategoriesBLL` 클래스의 `GetCategories()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="91c84-136">Configure the new ObjectDataSource such that it invokes the `CategoriesBLL` class's `GetCategories()` method.</span></span> <span data-ttu-id="91c84-137">드롭다운 목록에서 어떤 데이터 소스 필드를 표시 해야 하와 지정 해야 ObjectDataSource를 구성한 후 각 목록 항목에 대 한 값으로 연결 해야 하나 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-137">After configuring the ObjectDataSource we still need to specify what data source field should be displayed in the DropDownList and which one should be associated as the value for each list item.</span></span> <span data-ttu-id="91c84-138">있어야는 `CategoryName` 디스플레이와 필드 및 `CategoryID` 각 목록 항목에 대 한 값으로.</span><span class="sxs-lookup"><span data-stu-id="91c84-138">Have the `CategoryName` field as the display and `CategoryID` as the value for each list item.</span></span>


<span data-ttu-id="91c84-139">[![DropDownList 표시 범주 필드와 사용 하 여 CategoryID는는 값으로](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="91c84-139">[![Have the DropDownList Display the CategoryName Field and Use CategoryID as the Value](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image9.png)</span></span>

<span data-ttu-id="91c84-140">**그림 5**: DropDownList 디스플레이 `CategoryName` 필드 및 사용 `CategoryID` 값으로 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image11.png))</span><span class="sxs-lookup"><span data-stu-id="91c84-140">**Figure 5**: Have the DropDownList Display the `CategoryName` Field and Use `CategoryID` as the Value ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image11.png))</span></span>


<span data-ttu-id="91c84-141">이 시점에서의 레코드와 채워지는 DropDownList 컨트롤이 `Categories` 테이블 (모두 약 6 초 후에 수행).</span><span class="sxs-lookup"><span data-stu-id="91c84-141">At this point we have a DropDownList control that's populated with the records from the `Categories` table (all accomplished in about six seconds).</span></span> <span data-ttu-id="91c84-142">그림 6 브라우저를 통해 표시 될 때까지 진행률을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-142">Figure 6 shows our progress thus far when viewed through a browser.</span></span>


<span data-ttu-id="91c84-143">[![드롭 다운 현재 범주를 나열합니다.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="91c84-143">[![A Drop-Down Lists the Current Categories](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image12.png)</span></span>

<span data-ttu-id="91c84-144">**그림 6**: A 드롭다운 목록이 현재 범주 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="91c84-144">**Figure 6**: A Drop-Down Lists the Current Categories ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image14.png))</span></span>


## <a name="step-2-adding-the-products-datalist"></a><span data-ttu-id="91c84-145">2 단계: 추가 제품 DataList</span><span class="sxs-lookup"><span data-stu-id="91c84-145">Step 2: Adding the Products DataList</span></span>

<span data-ttu-id="91c84-146">마스터/세부 정보 보고서의 마지막 단계는 선택한 범주와 관련 된 제품을 나열 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-146">The last step in our master/detail report is to list the products associated with the selected category.</span></span> <span data-ttu-id="91c84-147">이를 위해 DataList 페이지에 추가 하 고 라는 새 ObjectDataSource 만들 `ProductsByCategoryDataSource`합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-147">To accomplish this, add a DataList to the page and create a new ObjectDataSource named `ProductsByCategoryDataSource`.</span></span> <span data-ttu-id="91c84-148">있어야는 `ProductsByCategoryDataSource` 컨트롤에서 데이터를 검색 된 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드.</span><span class="sxs-lookup"><span data-stu-id="91c84-148">Have the `ProductsByCategoryDataSource` control retrieve its data from the `ProductsBLL` class's `GetProductsByCategoryID(categoryID)` method.</span></span> <span data-ttu-id="91c84-149">이 마스터/세부 보고서 읽기 전용 이므로 (없음)는 INSERT, UPDATE 및 DELETE 탭에서 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-149">Since this master/detail report is read-only, choose the (None) option in the INSERT, UPDATE, and DELETE tabs.</span></span>


<span data-ttu-id="91c84-150">[![GetProductsByCategoryID(categoryID) 방법 선택](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="91c84-150">[![Select the GetProductsByCategoryID(categoryID) Method](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image15.png)</span></span>

<span data-ttu-id="91c84-151">**그림 7**: 선택 된 `GetProductsByCategoryID(categoryID)` 메서드 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image17.png))</span><span class="sxs-lookup"><span data-stu-id="91c84-151">**Figure 7**: Select the `GetProductsByCategoryID(categoryID)` Method ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image17.png))</span></span>


<span data-ttu-id="91c84-152">다음을 클릭 한 후 ObjectDataSource 마법사 라는 메시지가 나타납니다에 대 한 값의 출처는 `GetProductsByCategoryID(categoryID)` 메서드의 *`categoryID`* 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-152">After clicking Next, the ObjectDataSource wizard prompts us for the source of the value for the `GetProductsByCategoryID(categoryID)` method's *`categoryID`* parameter.</span></span> <span data-ttu-id="91c84-153">선택 된 값을 사용 하려면 `categories` DropDownList 항목 매개 변수 소스 제어 및에 ControlID를 설정 `Categories`합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-153">To use the value of the selected `categories` DropDownList item set the Parameter source to Control and the ControlID to `Categories`.</span></span>


<span data-ttu-id="91c84-154">[![매개 변수 categoryID 범주 DropDownList의 값으로 설정](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="91c84-154">[![Set the categoryID Parameter to the Value of the Categories DropDownList](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image18.png)</span></span>

<span data-ttu-id="91c84-155">**그림 8**: 설정의 *`categoryID`* 의 값에 대 한 매개 변수는 `Categories` DropDownList ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image20.png))</span><span class="sxs-lookup"><span data-stu-id="91c84-155">**Figure 8**: Set the *`categoryID`* Parameter to the Value of the `Categories` DropDownList ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image20.png))</span></span>


<span data-ttu-id="91c84-156">Visual Studio에서 자동으로 데이터 소스 구성 마법사를 완료 될 때 생성 된 `ItemTemplate` DataList 이름 및 각 데이터 필드의 값을 표시 하는 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-156">Upon completing the Configure Data Source wizard, Visual Studio will automatically generate an `ItemTemplate` for the DataList that displays the name and value of each data field.</span></span> <span data-ttu-id="91c84-157">대신 사용 하 여 DataList을 향상 해 보겠습니다는 `ItemTemplate` 제품의 이름, 범주, 공급 업체, 단위 테스트와 함께 가격 및 수량만 표시 하는 `SeparatorTemplate` 삽입 하는 `<hr>` 각 항목 사이 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-157">Let's enhance the DataList to instead use an `ItemTemplate` that displays just the product's name, category, supplier, quantity per unit, and price along with a `SeparatorTemplate` that injects an `<hr>` element between each item.</span></span> <span data-ttu-id="91c84-158">사용 하도록 하겠습니다는 `ItemTemplate` 의 예제에서는 [DataList 및 반복기 컨트롤을 사용 하 여 데이터 표시](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb.md) 자습서 하지만 느낌 매력적인 시각적으로 가장 찾을 어떤 템플릿 태그 있습니다 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-158">I'm going to use the `ItemTemplate` from an example in the [Displaying Data with the DataList and Repeater Controls](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb.md) tutorial, but feel free to use whatever template markup you find most visually appealing.</span></span>

<span data-ttu-id="91c84-159">다음과 같이 변경한 후 여 DataList 및 해당 ObjectDataSource 태그 다음과 비슷하게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-159">After making these changes, your DataList and its ObjectDataSource's markup should look similar to the following:</span></span>

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample2.aspx)]

<span data-ttu-id="91c84-160">브라우저에서 진행률을 확인해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="91c84-160">Take a moment to check out our progress in a browser.</span></span> <span data-ttu-id="91c84-161">페이지를 처음 방문 하는 경우 (음료) 선택한 범주에 속하는 제품 같이 표시 됩니다 (그림 9에서), 하지만 DropDownList 변경 데이터를 업데이트 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-161">When first visiting the page, those products belonging to the selected category (Beverages) are displayed (as shown in Figure 9), but changing the DropDownList doesn't update the data.</span></span> <span data-ttu-id="91c84-162">업데이트 하려면 DataList 포스트백 발생 해야 발생 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-162">This is because a postback must occur for the DataList to update.</span></span> <span data-ttu-id="91c84-163">활용해 서 하거나이를 위해 설정 DropDownList의 `AutoPostBack` 속성을 `true` 또는 페이지에 단추 웹 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-163">To accomplish this we can either set the DropDownList's `AutoPostBack` property to `true` or add a Button Web control to the page.</span></span> <span data-ttu-id="91c84-164">이 자습서에서는 선택한 이유는 DropDownList를 설정 하려면 `AutoPostBack` 속성을 `true`합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-164">For this tutorial, I've opted to set the DropDownList's `AutoPostBack` property to `true`.</span></span>

<span data-ttu-id="91c84-165">그림 9와 10 작업에서 마스터/세부 정보 보고서를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-165">Figures 9 and 10 illustrate the master/detail report in action.</span></span>


<span data-ttu-id="91c84-166">[![처음 방문 하 여 페이지 음료 제품 표시 됩니다.](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="91c84-166">[![When First Visiting the Page, the Beverage Products are Displayed](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image21.png)</span></span>

<span data-ttu-id="91c84-167">**그림 9**: 처음 방문 하 여 페이지 음료 제품 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image23.png))</span><span class="sxs-lookup"><span data-stu-id="91c84-167">**Figure 9**: When First Visiting the Page, the Beverage Products are Displayed ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image23.png))</span></span>


<span data-ttu-id="91c84-168">[![DataList 업데이트의 포스트백을 사용 하면 새 제품 (생성)을 선택 하면 자동으로](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image24.png)</span><span class="sxs-lookup"><span data-stu-id="91c84-168">[![Selecting a New Product (Produce) Automatically Causes a PostBack, Updating the DataList](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image24.png)</span></span>

<span data-ttu-id="91c84-169">**그림 10**: DataList 업데이트 포스트백 신제품 (생성)를 자동으로 선택 하면 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image26.png))</span><span class="sxs-lookup"><span data-stu-id="91c84-169">**Figure 10**: Selecting a New Product (Produce) Automatically Causes a PostBack, Updating the DataList ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image26.png))</span></span>


## <a name="adding-a----choose-a-category----list-item"></a><span data-ttu-id="91c84-170">"-범주 선택-" 목록 항목 추가</span><span class="sxs-lookup"><span data-stu-id="91c84-170">Adding a "-- Choose a Category --" List Item</span></span>

<span data-ttu-id="91c84-171">처음 방문할 때는 `FilterByDropDownList.aspx` DropDownList의 첫 번째 목록 항목 (음료) DataList 음료 제품을 보여 주는 기본적으로 선택 되어 범주 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-171">When first visiting the `FilterByDropDownList.aspx` page the categories DropDownList's first list item (Beverages) is selected by default, showing the beverage products in the DataList.</span></span> <span data-ttu-id="91c84-172">에 *마스터/세부 정보 필터링 된 정도 DropDownList* 자습서 "-범주 선택-" 옵션을 기본적으로 선택 되었으며 옵션을 선택 하면 표시 되는 드롭다운 목록에 추가한 *모든* 의 데이터베이스에서 제품입니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-172">In the *Master/Detail Filtering With a DropDownList* tutorial we added a "-- Choose a Category --" option to the DropDownList that was selected by default and, when selected, displayed *all* of the products in the database.</span></span> <span data-ttu-id="91c84-173">이러한 접근 방식은 관리할 수는 GridView에 제품을 나열 하는 경우 각 제품 행 적은 양의 화면 자원을를 걸렸습니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-173">Such an approach was manageable when listing the products in a GridView, as each product row took up a small amount of screen real estate.</span></span> <span data-ttu-id="91c84-174">그러나 datalist, 각 제품 정보를이 훨씬 더 큰 청크 화면을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-174">With the DataList, however, each product's information consumes a much larger chunk of the screen.</span></span> <span data-ttu-id="91c84-175">여전히 보겠습니다 "-범주 선택-" 옵션을 추가 하 고 기본적으로 선택 하 게 이지만 모든 제품을 표시 하지 않고 옵션을 선택 하면 보겠습니다 구성할 제품이 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-175">Let's still add a "-- Choose a Category --" option and have it selected by default, but instead of having it show all products when selected, let's configure it so that it shows no products.</span></span>

<span data-ttu-id="91c84-176">DropDownList를 새 목록 항목을 추가 하려면 속성 창으로 이동 하 고의 줄임표를 클릭 하 고 `Items` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-176">To add a new list item to the DropDownList, go to the Properties window and click on the ellipses in the `Items` property.</span></span> <span data-ttu-id="91c84-177">추가 된 새 목록 항목의 `Text` "-범주 선택-" 및 `Value` `0`합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-177">Add a new list item with the `Text` "-- Choose a Category --" and the `Value` `0`.</span></span>


![추가](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image27.png)

<span data-ttu-id="91c84-179">**그림 11**: "-범주 선택-" 목록 항목 추가</span><span class="sxs-lookup"><span data-stu-id="91c84-179">**Figure 11**: Add a "-- Choose a Category --" List Item</span></span>


<span data-ttu-id="91c84-180">또는 드롭다운 목록에 다음 태그를 추가 하 여 목록 항목을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-180">Alternatively, you can add the list item by adding the following markup to the DropDownList:</span></span>

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample3.aspx)]

<span data-ttu-id="91c84-181">또한 DropDownList 제어를 설정 하려면 할 `AppendDataBoundItems` 를 `true` 때문에로 설정 되어 있으면 `false` (기본값), 수동으로 추가 하는 모든 목록 덮어씁니다 범주는 ObjectDataSource에서 드롭다운 목록에 바인딩되는 경우 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-181">Additionally, we need to set the DropDownList control's `AppendDataBoundItems` to `true` because if it's set to `false` (the default), when the categories are bound to the DropDownList from the ObjectDataSource they'll overwrite any manually-added list items.</span></span>


![AppendDataBoundItems 속성이 True로 설정](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image28.png)

<span data-ttu-id="91c84-183">**그림 12**: 설정의 `AppendDataBoundItems` 속성을 True로</span><span class="sxs-lookup"><span data-stu-id="91c84-183">**Figure 12**: Set the `AppendDataBoundItems` Property to True</span></span>


<span data-ttu-id="91c84-184">값 선택 이유 `0` "-범주 선택-" 목록에 대 한 항목은 범주가 있는 시스템의 값에 있기 때문에 `0`, 따라서 "-범주 선택-" 목록 항목을 선택 하는 경우 제품 레코드가 없습니다 항목이 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-184">The reason we chose the value `0` for the "-- Choose a Category --" list item is because there are no categories in the system with a value of `0`, hence no product records will be returned when the "-- Choose a Category --" list item is selected.</span></span> <span data-ttu-id="91c84-185">이 확인 하려면 브라우저를 통해 페이지를 방문 하 여 보십시오.</span><span class="sxs-lookup"><span data-stu-id="91c84-185">To confirm this, take a moment to visit the page through a browser.</span></span> <span data-ttu-id="91c84-186">그림 13에서는 처음 페이지 보기 "-범주 선택-" 목록 항목을 선택 하면 제품이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-186">As Figure 13 shows, when initially viewing the page the "-- Choose a Category --" list item is selected and no products are displayed.</span></span>


<span data-ttu-id="91c84-187">[![경우는](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="91c84-187">[![When the](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image29.png)</span></span>

<span data-ttu-id="91c84-188">**그림 13**: "-범주 선택-" 목록 항목을 선택 하면 No 제품 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image31.png))</span><span class="sxs-lookup"><span data-stu-id="91c84-188">**Figure 13**: When the "-- Choose a Category --" List Item is Selected, No Products are Displayed ([Click to view full-size image](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image31.png))</span></span>


<span data-ttu-id="91c84-189">대신 표시 하는 경우 *모든* 제품 "-범주 선택-" 옵션을 선택 하면 값이 사용 됩니다. `-1` 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-189">If you'd rather display *all* of the products when the "-- Choose a Category --" option is selected, use a value of `-1` instead.</span></span> <span data-ttu-id="91c84-190">예리한 독자에 그 뒤로 다시 호출 됩니다는 *마스터/세부 정보 필터링 된 정도 DropDownList* 을 업데이트 했습니다. 자습서는 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드 되도록 하는 경우는 *`categoryID`* 값 `-1` 반환 된 레코드가 모든 제품에 전달 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-190">The astute reader will recall that back in the *Master/Detail Filtering With a DropDownList* tutorial we updated the `ProductsBLL` class's `GetProductsByCategoryID(categoryID)` method so that if a *`categoryID`* value of `-1` was passed in, all product records were returned.</span></span>

## <a name="summary"></a><span data-ttu-id="91c84-191">요약</span><span class="sxs-lookup"><span data-stu-id="91c84-191">Summary</span></span>

<span data-ttu-id="91c84-192">계층적으로 관련 데이터를 표시할 때 종종 사용자 계층의 최상위에서 데이터를 읽는 데 시작 하 고 세부 정보로 드릴 다운는 마스터/세부 보고서를 사용 하 여 데이터를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-192">When displaying hierarchically-related data, it often helps to present the data using master/detail reports, from which the user can start perusing the data from the top of the hierarchy and drill down into details.</span></span> <span data-ttu-id="91c84-193">이 자습서에서는 선택한 범주의 제품을 보여 주는 간단한 마스터/세부 보고서 작성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-193">In this tutorial we examined building a simple master/detail report showing a selected category's products.</span></span> <span data-ttu-id="91c84-194">이 범주에는 선택한 범주에 속한 제품에 대 한 DataList의 목록과 DropDownList를 사용 하 여 수행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-194">This was accomplished by using a DropDownList for the list of categories and a DataList for the products belonging to the selected category.</span></span>

<span data-ttu-id="91c84-195">다음 자습서 두 페이지에 걸쳐 마스터 및 세부 정보 레코드를 구분 하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-195">In the next tutorial we'll look at separating the master and details records across two pages.</span></span> <span data-ttu-id="91c84-196">첫 번째 페이지에서 "마스터" 레코드 목록이 표시 됩니다, 정보를 보려면 해당 링크.</span><span class="sxs-lookup"><span data-stu-id="91c84-196">In the first page, a list of "master" records will be displayed, with a link to view the details.</span></span> <span data-ttu-id="91c84-197">링크를 클릭 하면 사용자는 선택된 된 마스터 레코드에 대 한 정보를 표시 하는 두 번째 페이지를 whisk 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-197">Clicking on the link will whisk the user to the second page, which will display the details for the selected master record.</span></span>

<span data-ttu-id="91c84-198">만족도 매우 프로그래밍!</span><span class="sxs-lookup"><span data-stu-id="91c84-198">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="91c84-199">작성자 정보</span><span class="sxs-lookup"><span data-stu-id="91c84-199">About the Author</span></span>

<span data-ttu-id="91c84-200">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-200">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="91c84-201">Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-201">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="91c84-202">그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-202">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="91c84-203">에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-203">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="91c84-204">특히 감사 드립니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-204">Special Thanks To…</span></span>

<span data-ttu-id="91c84-205">이 자습서 시리즈 많은 유용한 검토자가 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-205">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="91c84-206">이 자습서에 대 한 선행 검토자 Randy Schmidt 했습니다.</span><span class="sxs-lookup"><span data-stu-id="91c84-206">Lead reviewer for this tutorial was Randy Schmidt.</span></span> <span data-ttu-id="91c84-207">향후 내 MSDN 문서를 검토에 관심이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="91c84-207">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="91c84-208">이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="91c84-208">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="91c84-209">[이전](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)
> [다음](master-detail-filtering-acess-two-pages-datalist-vb.md)</span><span class="sxs-lookup"><span data-stu-id="91c84-209">[Previous](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)
[Next](master-detail-filtering-acess-two-pages-datalist-vb.md)</span></span>
