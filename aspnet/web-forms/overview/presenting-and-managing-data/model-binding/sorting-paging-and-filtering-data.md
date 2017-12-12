---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: "정렬, 페이징 및 모델 바인딩 및 web forms를 사용 하 여 데이터를 필터링 합니다. | Microsoft Docs"
author: tfitzmac
description: "이 자습서 시리즈 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩 데이터 상호 작용 하 게 더 많은 직선-중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: 94fc84533be5fcbcf0612fcdcabea7dee738d89b
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a><span data-ttu-id="201c8-104">정렬, 페이징 및 모델 바인딩 및 web forms를 사용 하 여 데이터를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-104">Sorting, paging, and filtering data with model binding and web forms</span></span>
====================
<span data-ttu-id="201c8-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="201c8-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="201c8-106">이 자습서 시리즈 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="201c8-107">모델 바인딩 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 간단한 것 보다 데이터 상호 작용 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="201c8-108">이 시리즈 소개 자료로 시작 하 고 이후의 자습서의 보다 발전된 된 개념 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="201c8-109">이 자습서에는 추가 정렬, 페이징 및 모델 바인딩을 통해 데이터를 필터링 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-109">This tutorial shows how to add sorting, paging, and filtering of the data through model binding.</span></span>
> 
> <span data-ttu-id="201c8-110">첫 번째 범위에서 만든 프로젝트를 기반으로 한이 자습서 [부분](retrieving-data.md) 일련의 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-110">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="201c8-111">있습니다 수 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) C# 또는 VB. 전체 프로젝트</span><span class="sxs-lookup"><span data-stu-id="201c8-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="201c8-112">다운로드 가능한 코드는 Visual Studio 2012 또는 Visual Studio 2013과 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="201c8-113">이 자습서에 표시 된 Visual Studio 2013 서식 파일 보다 약간 차이가 있는 Visual Studio 2012 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="201c8-114">만들 것인지</span><span class="sxs-lookup"><span data-stu-id="201c8-114">What you'll build</span></span>

<span data-ttu-id="201c8-115">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="201c8-116">정렬 및 데이터의 페이징을 활성화합니다</span><span class="sxs-lookup"><span data-stu-id="201c8-116">Enable sorting and paging of the data</span></span>
2. <span data-ttu-id="201c8-117">사용자가 한 선택에 따라 데이터의 필터링을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="201c8-117">Enable filtering of the data based on a selection by the user</span></span>

## <a name="add-sorting"></a><span data-ttu-id="201c8-118">정렬 추가</span><span class="sxs-lookup"><span data-stu-id="201c8-118">Add sorting</span></span>

<span data-ttu-id="201c8-119">GridView에서 정렬 사용 하지 않는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-119">Enabling sorting in the GridView is very easy.</span></span> <span data-ttu-id="201c8-120">Student.aspx 파일 설정 하기만 하면 **AllowSorting** 를 **true** GridView에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-120">In the Student.aspx file, simply set **AllowSorting** to **true** in the GridView.</span></span> <span data-ttu-id="201c8-121">설정할 필요가 없습니다는 **SortExpression** DataField 자동으로 사용 되는 각 열에 대 한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-121">You do not need to set a **SortExpression** value for each column as the DataField is automatically used.</span></span> <span data-ttu-id="201c8-122">GridView 선택한 값에 의해 데이터 정렬 포함 하도록 쿼리를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-122">The GridView modifies the query to include ordering the data by the selected value.</span></span> <span data-ttu-id="201c8-123">아래에 강조 표시 된 코드 정렬 하기 위해 해야 할 추가 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-123">The highlighted code below shows the addition you need to make to enable sorting.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

<span data-ttu-id="201c8-124">웹 응용 프로그램을 실행 하 고 다른 열 값을 기준으로 정렬 학생 레코드를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-124">Run the web application, and test sorting student records by the values in different columns.</span></span>

![정렬 학생](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a><span data-ttu-id="201c8-126">페이징 추가</span><span class="sxs-lookup"><span data-stu-id="201c8-126">Add paging</span></span>

<span data-ttu-id="201c8-127">페이징 사용을 매우 쉽게 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-127">Enabling paging is also very easy.</span></span> <span data-ttu-id="201c8-128">GridView에서 설정는 **AllowPaging** 속성을 **true** 설정 하 고는 **PageSize** 속성을 각 페이지에 표시 하려는 레코드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-128">In the GridView, set the **AllowPaging** property to **true** and set the **PageSize** property to the number of records you wish to display on each page.</span></span> <span data-ttu-id="201c8-129">이 자습서에서는 4로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-129">In this tutorial, you can set it to 4.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

<span data-ttu-id="201c8-130">웹 응용 프로그램을 실행 하 고 단일 페이지에 표시 되는 4 개 이하의 레코드와 레코드 여러 페이지에 걸쳐 나뉩니다 이제 다음에 유의 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-130">Run the web application, and notice that now the records are divided over multiple pages with no more than 4 records displayed on a single page.</span></span>

![페이징 추가](sorting-paging-and-filtering-data/_static/image4.png)

<span data-ttu-id="201c8-132">지연 된 쿼리 실행에는 응용 프로그램 효율성이 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-132">Deferred query execution improves the application efficiency.</span></span> <span data-ttu-id="201c8-133">전체 데이터 집합을 검색 하는 대신 GridView 현재 페이지에 대 한 레코드만 검색 하려면 쿼리를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-133">Instead of retrieving the entire data set, the GridView modifies the query to retrieve only the records for the current page.</span></span>

## <a name="filter-records-by-user-selection"></a><span data-ttu-id="201c8-134">사용자 선택 하 여 레코드 필터링</span><span class="sxs-lookup"><span data-stu-id="201c8-134">Filter records by user selection</span></span>

<span data-ttu-id="201c8-135">모델 바인딩을 사용 하면 모델 바인딩 방법에는 매개 변수의 값을 설정 하는 방법을 지정 하는 몇 가지 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-135">Model binding adds several attributes which enable you to designate how to set the value for a parameter in a model binding method.</span></span> <span data-ttu-id="201c8-136">이러한 특성은는 **System.Web.ModelBinding** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-136">These attributes are in the **System.Web.ModelBinding** namespace.</span></span> <span data-ttu-id="201c8-137">다음과 같은 변경 내용이 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-137">They include:</span></span>

- <span data-ttu-id="201c8-138">컨트롤</span><span class="sxs-lookup"><span data-stu-id="201c8-138">Control</span></span>
- <span data-ttu-id="201c8-139">쿠키</span><span class="sxs-lookup"><span data-stu-id="201c8-139">Cookie</span></span>
- <span data-ttu-id="201c8-140">Form</span><span class="sxs-lookup"><span data-stu-id="201c8-140">Form</span></span>
- <span data-ttu-id="201c8-141">프로필</span><span class="sxs-lookup"><span data-stu-id="201c8-141">Profile</span></span>
- <span data-ttu-id="201c8-142">QueryString</span><span class="sxs-lookup"><span data-stu-id="201c8-142">QueryString</span></span>
- <span data-ttu-id="201c8-143">RouteData</span><span class="sxs-lookup"><span data-stu-id="201c8-143">RouteData</span></span>
- <span data-ttu-id="201c8-144">세션</span><span class="sxs-lookup"><span data-stu-id="201c8-144">Session</span></span>
- <span data-ttu-id="201c8-145">사용자 프로필</span><span class="sxs-lookup"><span data-stu-id="201c8-145">UserProfile</span></span>
- <span data-ttu-id="201c8-146">ViewState</span><span class="sxs-lookup"><span data-stu-id="201c8-146">ViewState</span></span>

<span data-ttu-id="201c8-147">이 자습서에서는 GridView에 표시 되는 레코드를 필터링 하는 컨트롤의 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-147">In this tutorial, you will use a control's value to filter which records are displayed in the GridView.</span></span> <span data-ttu-id="201c8-148">추가한는 **제어** 특성을 쿼리 메서드에 이전에 만든 했습니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-148">You will add the **Control** attribute to the query method you had created earlier.</span></span> <span data-ttu-id="201c8-149">에 [나중](using-query-string-values-to-retrieve-data.md) 자습서를 적용 하는 **QueryString** 특성을 매개 변수 값은 쿼리 문자열 값의 하도록 지정 하는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-149">In a [later](using-query-string-values-to-retrieve-data.md) tutorial, you will apply the **QueryString** attribute to a parameter to specify that the parameter value comes from a query string value.</span></span>

<span data-ttu-id="201c8-150">첫째, 위에서 ValidationSummary, 어떤 학생 표시 되는 필터링에 대 한 목록 드롭다운을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-150">First, above the ValidationSummary, add a drop down list for filtering which students are shown.</span></span>

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

<span data-ttu-id="201c8-151">코드 숨김 파일에서 값을 받도록 컨트롤에서 선택 메서드를 수정 하 고 매개 변수의 이름 값을 제공 하는 컨트롤의 이름으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-151">In the code-behind file, modify the select method to receive a value from the control, and set the name of the parameter to the name of the control that provides the value.</span></span>

<span data-ttu-id="201c8-152">추가 해야 합니다는 **를 사용 하 여** 문을 **System.Web.ModelBinding** 컨트롤 특성을 확인할 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-152">You must add a **using** statement for the **System.Web.ModelBinding** namespace to resolve the Control attribute.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

<span data-ttu-id="201c8-153">다음 코드는 드롭다운 목록 값에 따라 반환 된 데이터를 필터링 하는 데 사용 되 던 다시 select 메서드를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-153">The following code shows the select method re-worked to filter the returned data based on the value of the drop down list.</span></span> <span data-ttu-id="201c8-154">매개 변수 값이 매개이 변수에 대 한 동일한 이름의 컨트롤에서 제공 됨을 지정 하기 전에 컨트롤 특성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-154">Adding a control attribute before a parameter specifies that the value for this parameter comes from a control with the same name.</span></span>

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

<span data-ttu-id="201c8-155">웹 응용 프로그램을 실행 하 고 드롭다운 학생의 목록을 필터링 하려면 목록에서에서 다른 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-155">Run the web application and select different values from the drop down list to filter the list of students.</span></span>

![필터 학생](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a><span data-ttu-id="201c8-157">결론</span><span class="sxs-lookup"><span data-stu-id="201c8-157">Conclusion</span></span>

<span data-ttu-id="201c8-158">이 자습서에서는 정렬 및 데이터의 페이징을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-158">In this tutorial, you enabled sorting and paging of the data.</span></span> <span data-ttu-id="201c8-159">설정한 컨트롤의 값으로 데이터를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-159">You also enabled filtering the data by the value of a control.</span></span>

<span data-ttu-id="201c8-160">다음에서 [자습서](integrating-jquery-ui.md) JQuery UI 위젯 동적 데이터 서식 파일에 통합 하 여 UI를 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="201c8-160">In the next [tutorial](integrating-jquery-ui.md) you will enhance the UI by integrating a JQuery UI widget into the dynamic data template.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="201c8-161">[이전](updating-deleting-and-creating-data.md)
[다음](integrating-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="201c8-161">[Previous](updating-deleting-and-creating-data.md)
[Next](integrating-jquery-ui.md)</span></span>
