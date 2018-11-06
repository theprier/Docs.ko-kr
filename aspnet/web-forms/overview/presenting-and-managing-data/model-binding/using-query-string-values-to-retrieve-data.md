---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: 쿼리 문자열 값을 사용 하 여 모델 바인딩을 사용 하 여 데이터를 필터링 하 여 web forms | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩을 통해 데이터 상호 작용 자세한 직선-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 490279ec8457535031387e955e67550052764fff
ms.sourcegitcommit: 2d3e5422d530203efdaf2014d1d7df31f88d08d0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51021120"
---
<a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a><span data-ttu-id="0c50e-104">모델 바인딩 및 web forms를 사용 하 여 데이터를 필터링 하는 쿼리 문자열 값을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="0c50e-104">Using query string values to filter data with model binding and web forms</span></span>
====================
<span data-ttu-id="0c50e-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="0c50e-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="0c50e-106">이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="0c50e-107">모델 바인딩 보다 직관적인 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 데이터 상호 작용 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="0c50e-108">이 시리즈 소개 자료를 사용 하 여 시작 하 고 나중에 자습서에서 고급 개념을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="0c50e-109">이 자습서에서는 쿼리 문자열의 값을 전달 하 고 해당 값을 사용 하 여 모델 바인딩을 통해 데이터를 검색 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-109">This tutorial shows how to pass a value in the query string and use that value to retrieve data through model binding.</span></span>
> 
> <span data-ttu-id="0c50e-110">이 자습서에서 만든 프로젝트를 기반 합니다 [이전](retrieving-data.md) 시리즈의 파트입니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-110">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="0c50e-111">할 수 있습니다 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) C# 또는 VB. 전체 프로젝트</span><span class="sxs-lookup"><span data-stu-id="0c50e-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="0c50e-112">다운로드 가능한 코드를 Visual Studio 2012 또는 Visual Studio 2013을 사용 하 여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="0c50e-113">이 자습서에 표시 된 Visual Studio 2013 서식 파일 보다 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="0c50e-114">만들 내용</span><span class="sxs-lookup"><span data-stu-id="0c50e-114">What you'll build</span></span>

<span data-ttu-id="0c50e-115">이 자습서에서는 다음을 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="0c50e-116">학생에 대 한 등록된 과정을 표시할 새 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="0c50e-116">Add a new page to show the enrolled courses for a student</span></span>
2. <span data-ttu-id="0c50e-117">쿼리 문자열의 값을 기준으로 선택한 학생에 대 한 등록된 과정 검색</span><span class="sxs-lookup"><span data-stu-id="0c50e-117">Retrieve the enrolled courses for the selected student based on a value in the query string</span></span>
3. <span data-ttu-id="0c50e-118">새 페이지를 그리드 보기에서 쿼리 문자열 값을 사용 하 여 하이퍼링크 추가</span><span class="sxs-lookup"><span data-stu-id="0c50e-118">Add a hyperlink with a query string value from the grid view to the new page</span></span>

<span data-ttu-id="0c50e-119">이 자습서의 단계를 수행한 매우 비슷합니다 이전 [자습서](sorting-paging-and-filtering-data.md) 드롭다운 목록에서에서 사용자 선택에 따라 표시 된 학생을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-119">The steps in this tutorial are fairly similar to what you did in the earlier [tutorial](sorting-paging-and-filtering-data.md) to filter the displayed students based on the user selection in a drop down list.</span></span> <span data-ttu-id="0c50e-120">해당 자습서를 사용 하는 **제어** 특성 선택 메서드에서 매개 변수 값을 컨트롤에서 제공 됨을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-120">In that tutorial, you used the **Control** attribute in the select method to specify that the parameter value comes from a control.</span></span> <span data-ttu-id="0c50e-121">이 자습서에서는 사용 합니다 **QueryString** select 메서드 매개 변수 값은 쿼리 문자열에서 제공 됨을 지정 하려면 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-121">In this tutorial, you'll use the **QueryString** attribute in the select method to specify that the parameter value comes from the query string.</span></span>

## <a name="add-new-page-for-displaying-a-students-courses"></a><span data-ttu-id="0c50e-122">학생의 코스를 표시 하기 위한 새 페이지 추가</span><span class="sxs-lookup"><span data-stu-id="0c50e-122">Add new page for displaying a student's courses</span></span>

<span data-ttu-id="0c50e-123">Site.master 마스터 페이지를 사용 하는 새 web form을 추가 하 고 페이지의 이름을 **코스**합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-123">Add a new web form that uses the Site.master master page, and name the page **Courses**.</span></span>

<span data-ttu-id="0c50e-124">에 **Courses.aspx** 파일, 선택한 학생에 대 한 강좌를 표시 하는 그리드 보기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-124">In the **Courses.aspx** file, add a grid view to display the courses for the selected student.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a><span data-ttu-id="0c50e-125">Select 메서드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-125">Define the select method</span></span>

<span data-ttu-id="0c50e-126">**Courses.aspx.cs**, 그리드 보기에서 지정한 이름 가진 select 메서드를 추가 합니다 **SelectMethod** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-126">In **Courses.aspx.cs**, you will add the select method with the name you specified in the grid view's **SelectMethod** property.</span></span> <span data-ttu-id="0c50e-127">메서드는 학생의 코스를 검색 하는 것에 대 한 쿼리를 정의 하 고 매개 변수 이름이 같은 매개 변수를 사용 하 여 쿼리 문자열 값에서 제공 됨을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-127">In that method, you'll define the query for retrieving a student's courses, and specify that the parameter comes from a query string value with the same name as the parameter.</span></span>

<span data-ttu-id="0c50e-128">먼저 다음을 추가 해야 합니다 **를 사용 하 여** 문입니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-128">First, you must add the following **using** statements.</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

<span data-ttu-id="0c50e-129">그런 다음 Courses.aspx.cs에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-129">Then, add the following code to Courses.aspx.cs:</span></span>

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

<span data-ttu-id="0c50e-130">QueryString 특성 StudentID 라는 쿼리 문자열 값을이 메서드의 매개 변수를 자동으로 할당 됩니다 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-130">The QueryString attribute means that a query string value named StudentID is automatically assigned to the parameter in this method.</span></span>

## <a name="add-hyperlink-with-query-string-value"></a><span data-ttu-id="0c50e-131">쿼리 문자열 값을 사용 하 여 하이퍼링크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-131">Add hyperlink with query string value</span></span>

<span data-ttu-id="0c50e-132">Students.aspx에서 표 뷰에서 새 강좌 페이지에 링크 되는 하이퍼링크 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-132">In the grid view on Students.aspx, you will add a hyperlink field that links to your new Courses page.</span></span> <span data-ttu-id="0c50e-133">하이퍼링크는 학생의 id 사용 하 여 쿼리 문자열 값을 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-133">The hyperlink will include a query string value with the student's id.</span></span>

<span data-ttu-id="0c50e-134">Students.aspx에서 다음 필드를 총 크레딧 눈금 보기 열 필드 바로 아래에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-134">In Students.aspx, add the following field to the grid view columns just below the field for Total Credits.</span></span>

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

<span data-ttu-id="0c50e-135">응용 프로그램을 실행 및 그리드 보기에 이제 과정 링크를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-135">Run the application and notice that the grid view now includes the Courses link.</span></span>

![하이퍼링크 추가](using-query-string-values-to-retrieve-data/_static/image1.png)

<span data-ttu-id="0c50e-137">링크 중 하나를 클릭 하면 등록 된 해당 학생의 코스 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-137">When you click one of the links, you'll see that student's enrolled courses.</span></span>

![강좌를 표시 합니다.](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="0c50e-139">결론</span><span class="sxs-lookup"><span data-stu-id="0c50e-139">Conclusion</span></span>

<span data-ttu-id="0c50e-140">이 자습서에서는 쿼리 문자열 값을 사용 하 여 링크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-140">In this tutorial, you added a link with a query string value.</span></span> <span data-ttu-id="0c50e-141">Select 메서드 매개 변수 값에 대 한 쿼리 문자열 값을 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-141">You used that query string value for the parameter value in the select method.</span></span>

<span data-ttu-id="0c50e-142">다음에 [자습서](adding-business-logic-layer.md), 비즈니스 논리 계층 및 데이터 액세스 계층을 코드 숨김 파일에서 코드를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c50e-142">In the next [tutorial](adding-business-logic-layer.md), you will move the code from the code-behind files into a business logic layer and a data access layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0c50e-143">[이전](integrating-jquery-ui.md)
> [다음](adding-business-logic-layer.md)</span><span class="sxs-lookup"><span data-stu-id="0c50e-143">[Previous](integrating-jquery-ui.md)
[Next](adding-business-logic-layer.md)</span></span>
