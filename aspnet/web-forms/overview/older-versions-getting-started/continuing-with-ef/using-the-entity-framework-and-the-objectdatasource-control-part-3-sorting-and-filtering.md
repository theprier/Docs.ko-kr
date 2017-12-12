---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: "Entity Framework 4.0 및 ObjectDataSource 컨트롤을 사용 하 여 단계 3: 정렬 및 필터링 | Microsoft Docs"
author: tdykstra
description: "이 자습서 시리즈의 Entity Framework 4.0 자습서 시리즈 시작 하기에 의해 만들어진 Contoso 대학 웹 응용 프로그램 기반으로 합니다. I 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2011
ms.topic: article
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 4accd3381a66bde1f87f0dc7dd95beeb54fcc6a2
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a><span data-ttu-id="23207-104">Entity Framework 4.0 및 ObjectDataSource 컨트롤을 사용 하 여 단계 3: 정렬 및 필터링</span><span class="sxs-lookup"><span data-stu-id="23207-104">Using the Entity Framework 4.0 and the ObjectDataSource Control, Part 3: Sorting and Filtering</span></span>
====================
<span data-ttu-id="23207-105">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="23207-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="23207-106">에 의해 만들어진 Contoso 대학 웹 응용 프로그램을 기반으로 하는이 자습서 시리즈의 [Entity Framework 4.0이 있는 시작](https://asp.net/entity-framework/tutorials#Getting%20Started) 자습서 시리즈 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) tutorial series.</span></span> <span data-ttu-id="23207-107">이전 자습서를 완료 하지 않은 경우이 자습서에 대 한 시작 점으로 하면 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 만들어졌을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="23207-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="23207-108">수도 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 완료 하는 자습서 시리즈에서 만들어진 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="23207-109">이 자습서에 대 한 질문이 있으면에 게시할 수 있습니다는 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>


<span data-ttu-id="23207-110">Entity Framework를 사용 하는 n 계층 웹 응용 프로그램에서 리포지토리 패턴을 구현 하기 이전 자습서에서 및 `ObjectDataSource` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-110">In the previous tutorial you implemented the repository pattern in an n-tier web application that uses the Entity Framework and the `ObjectDataSource` control.</span></span> <span data-ttu-id="23207-111">이 자습서에서는 정렬 및 필터링을 수행 하 고 마스터-세부 정보 시나리오를 처리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="23207-111">This tutorial shows how to do sorting and filtering and handle master-detail scenarios.</span></span> <span data-ttu-id="23207-112">다음과 같은 향상 기능이 추가 된 *Departments.aspx* 페이지:</span><span class="sxs-lookup"><span data-stu-id="23207-112">You'll add the following enhancements to the *Departments.aspx* page:</span></span>

- <span data-ttu-id="23207-113">부서 이름으로 선택할 수 있도록 하려면 텍스트 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="23207-113">A text box to allow users to select departments by name.</span></span>
- <span data-ttu-id="23207-114">눈금에 표시 되는 각 부서에 대 한 교육 과정의 목록.</span><span class="sxs-lookup"><span data-stu-id="23207-114">A list of courses for each department that's shown in the grid.</span></span>
- <span data-ttu-id="23207-115">열 머리글을 클릭 하 여 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23207-115">The ability to sort by clicking column headings.</span></span>

<span data-ttu-id="23207-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="23207-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span></span>

## <a name="adding-the-ability-to-sort-gridview-columns"></a><span data-ttu-id="23207-117">GridView 열을 정렬 하는 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-117">Adding the Ability to Sort GridView Columns</span></span>

<span data-ttu-id="23207-118">열기는 *Departments.aspx* 페이지 및 추가 `SortParameterName="sortExpression"` 특성을 `ObjectDataSource` 라는 컨트롤 `DepartmentsObjectDataSource`합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-118">Open the *Departments.aspx* page and add a `SortParameterName="sortExpression"` attribute to the `ObjectDataSource` control named `DepartmentsObjectDataSource`.</span></span> <span data-ttu-id="23207-119">(만들어 나중에 `GetDepartments` 라는 매개 변수를 갖는 메서드의 `sortExpression`.) 컨트롤의 여는 태그에 대 한 태그에는 이제 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-119">(Later you'll create a `GetDepartments` method that takes a parameter named `sortExpression`.) The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

<span data-ttu-id="23207-120">추가 `AllowSorting="true"` 특성을 여는 태그는 `GridView` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-120">Add the `AllowSorting="true"` attribute to the opening tag of the `GridView` control.</span></span> <span data-ttu-id="23207-121">컨트롤의 여는 태그에 대 한 태그에는 이제 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-121">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

<span data-ttu-id="23207-122">*Departments.aspx.cs*를 호출 하 여 기본 정렬 순서를 설정의 `GridView` 컨트롤의 `Sort` 에서 메서드는 `Page_Load` 메서드:</span><span class="sxs-lookup"><span data-stu-id="23207-122">In *Departments.aspx.cs*, set the default sort order by calling the `GridView` control's `Sort` method from the `Page_Load` method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

<span data-ttu-id="23207-123">비즈니스 논리 클래스 또는 저장소 클래스 중 하나에서 정렬 또는 필터 하는 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23207-123">You can add code that sorts or filters in either the business logic class or the repository class.</span></span> <span data-ttu-id="23207-124">비즈니스 논리 클래스에서 하면 정렬 또는 필터링 작업 수행 됩니다, 데이터베이스에서 데이터를 검색 후 비즈니스 논리 클래스 사용 하기 때문에 프로그램 `IEnumerable` 저장소에서 반환 된 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="23207-124">If you do it in the business logic class, the sorting or filtering work will be done after the data is retrieved from the database, because the business logic class is working with an `IEnumerable` object returned by the repository.</span></span> <span data-ttu-id="23207-125">정렬 및 필터링 저장소 클래스의 코드를 추가 LINQ 식 앞 그렇게 또는 개체 쿼리 변환 된 경우는 `IEnumerable` 개체는 일반적으로 보다 효율적 처리를 위해 데이터베이스에 명령을 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23207-125">If you add sorting and filtering code in the repository class and you do it before a LINQ expression or object query has been converted to an `IEnumerable` object, your commands will be passed through to the database for processing, which is typically more efficient.</span></span> <span data-ttu-id="23207-126">이 자습서에서는 데이터베이스에서 수행 해야 하는 처리 하는 방법으로에서 정렬 및 필터링을 구현 합니다-즉, 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23207-126">In this tutorial you'll implement sorting and filtering in a way that causes the processing to be done by the database — that is, in the repository.</span></span>

<span data-ttu-id="23207-127">정렬 기능을 추가 하려면 리포지토리 인터페이스와 비즈니스 논리 클래스에 대 한 저장소 클래스를 에서도에 새 메서드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-127">To add sorting capability, you must add a new method to the repository interface and repository classes as well as to the business logic class.</span></span> <span data-ttu-id="23207-128">에 *ISchoolRepository.cs* 파일, 새 추가 `GetDepartments` 를 받는 메서드에 `sortExpression` 반환 되는 부서 목록을 정렬 하는 데 사용할 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="23207-128">In the *ISchoolRepository.cs* file, add a new `GetDepartments` method that takes a `sortExpression` parameter that will be used to sort the list of departments that's returned:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

<span data-ttu-id="23207-129">`sortExpression` 매개 변수에서 정렬할 열과 정렬 방향을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-129">The `sortExpression` parameter will specify the column to sort on and the sort direction.</span></span>

<span data-ttu-id="23207-130">새로운 메서드를 위한 코드를 추가 *SchoolRepository.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="23207-130">Add code for the new method to the *SchoolRepository.cs* file:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

<span data-ttu-id="23207-131">매개 변수가 없는 기존 변경 `GetDepartments` 새 메서드를 호출 하는 메서드:</span><span class="sxs-lookup"><span data-stu-id="23207-131">Change the existing parameterless `GetDepartments` method to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

<span data-ttu-id="23207-132">테스트 프로젝트에서 다음과 같은 새로운 메서드를 추가 *MockSchoolRepository.cs*:</span><span class="sxs-lookup"><span data-stu-id="23207-132">In the test project, add the following new method to *MockSchoolRepository.cs*:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

<span data-ttu-id="23207-133">이 메서드는 정렬 된 목록 반환에 의존 하는 모든 단위 테스트를 만드는 하려던 목록을 반환 하기 전에 정렬 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-133">If you were going to create any unit tests that depended on this method returning a sorted list, you would need to sort the list before returning it.</span></span> <span data-ttu-id="23207-134">않습니다 만드시겠습니까 테스트 그렇게이 자습서에서는 메서드가 정렬 되지 않은 부서 목록을 반환할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-134">You won't be creating tests like that in this tutorial, so the method can just return the unsorted list of departments.</span></span>

<span data-ttu-id="23207-135">에 *SchoolBL.cs* 파일, 비즈니스 논리 클래스에 다음과 같은 새 메서드 추가:</span><span class="sxs-lookup"><span data-stu-id="23207-135">In the *SchoolBL.cs* file, add the following new method to the business logic class:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

<span data-ttu-id="23207-136">이 코드는 저장소 메서드를 정렬 매개 변수를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-136">This code passes the sort parameter to the repository method.</span></span>

<span data-ttu-id="23207-137">실행 된 *Departments.aspx* 페이지.</span><span class="sxs-lookup"><span data-stu-id="23207-137">Run the *Departments.aspx* page.</span></span>

<span data-ttu-id="23207-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="23207-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span></span>

<span data-ttu-id="23207-139">해당 열으로 정렬 하려면 열 머리글을 클릭할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23207-139">You can now click any column heading to sort by that column.</span></span> <span data-ttu-id="23207-140">열이 이미 정렬, 머리글을 클릭 하면 정렬 방향을 취소 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23207-140">If the column is already sorted, clicking the heading reverses the sort direction.</span></span>

## <a name="adding-a-search-box"></a><span data-ttu-id="23207-141">검색 상자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-141">Adding a Search Box</span></span>

<span data-ttu-id="23207-142">이 섹션의 검색 텍스트 상자를 추가, 연결 합니다는 `ObjectDataSource` 제어 매개 변수를 사용 하 여 제어 하 고 필터링을 지원 하려면 비즈니스 논리 클래스는 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-142">In this section you'll add a search text box, link it to the `ObjectDataSource` control using a control parameter, and add a method to the business logic class to support filtering.</span></span>

<span data-ttu-id="23207-143">열기는 *Departments.aspx* 페이지 머리글 및 첫 번째 사이 다음 태그를 추가 하 고 `ObjectDataSource` 제어:</span><span class="sxs-lookup"><span data-stu-id="23207-143">Open the *Departments.aspx* page and add the following markup between the heading and the first `ObjectDataSource` control:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

<span data-ttu-id="23207-144">에 `ObjectDataSource` 라는 컨트롤 `DepartmentsObjectDataSource`에서 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-144">In the `ObjectDataSource` control named `DepartmentsObjectDataSource`, do the following:</span></span>

- <span data-ttu-id="23207-145">추가 `SelectParameters` 매개 변수 이름에 대 한 요소 `nameSearchString` 를 가져옴에 입력 된 값은 `SearchTextBox` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-145">Add a `SelectParameters` element for a parameter named `nameSearchString` that gets the value entered in the `SearchTextBox` control.</span></span>
- <span data-ttu-id="23207-146">변경 된 `SelectMethod` 특성 값을 `GetDepartmentsByName`합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-146">Change the `SelectMethod` attribute value to `GetDepartmentsByName`.</span></span> <span data-ttu-id="23207-147">(나중에 만들이 이렇게 합니다.)</span><span class="sxs-lookup"><span data-stu-id="23207-147">(You'll create this method later.)</span></span>

<span data-ttu-id="23207-148">에 대 한 태그는 `ObjectDataSource` 컨트롤에는 이제 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-148">The markup for the `ObjectDataSource` control now resembles the following example:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

<span data-ttu-id="23207-149">*ISchoolRepository.cs*, 추가 `GetDepartmentsByName` 메서드 둘 다 사용 `sortExpression` 및 `nameSearchString` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="23207-149">In *ISchoolRepository.cs*, add a `GetDepartmentsByName` method that takes both `sortExpression` and `nameSearchString` parameters:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

<span data-ttu-id="23207-150">*SchoolRepository.cs*, 다음 새 메서드 추가:</span><span class="sxs-lookup"><span data-stu-id="23207-150">In *SchoolRepository.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

<span data-ttu-id="23207-151">사용 하 여이 코드는 `Where` 메서드 검색 문자열이 포함 된 항목을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-151">This code uses a `Where` method to select items that contain the search string.</span></span> <span data-ttu-id="23207-152">검색 문자열이 비어 있으면 모든 레코드는 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23207-152">If the search string is empty, all records will be selected.</span></span> <span data-ttu-id="23207-153">메서드를 다음과 같이 하나의 문에서 함께 호출을 지정 하는 경우 유의 (`Include`, 다음 `OrderBy`, 다음 `Where`), `Where` 메서드가 항상 마지막 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-153">Note that when you specify method calls together in one statement like this (`Include`, then `OrderBy`, then `Where`), the `Where` method must always be last.</span></span>

<span data-ttu-id="23207-154">기존 변경 `GetDepartments` 를 받는 메서드에 `sortExpression` 새 메서드를 호출 하는 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="23207-154">Change the existing `GetDepartments` method that takes a `sortExpression` parameter to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

<span data-ttu-id="23207-155">*MockSchoolRepository.cs* 테스트 프로젝트에서 다음과 같은 새 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-155">In *MockSchoolRepository.cs* in the test project, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

<span data-ttu-id="23207-156">*SchoolBL.cs*, 다음 새 메서드 추가:</span><span class="sxs-lookup"><span data-stu-id="23207-156">In *SchoolBL.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

<span data-ttu-id="23207-157">실행 된 *Departments.aspx* 페이지 하 고 선택 논리 작동 하는지 확인 하는 검색 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-157">Run the *Departments.aspx* page and enter a search string to make sure that the selection logic works.</span></span> <span data-ttu-id="23207-158">텍스트 상자를 비워 두고 모든 레코드가 반환 되도록 검색을 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-158">Leave the text box empty and try a search to make sure that all records are returned.</span></span>

<span data-ttu-id="23207-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="23207-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span></span>

## <a name="adding-a-details-column-for-each-grid-row"></a><span data-ttu-id="23207-160">각 그리드 행에 대 한 세부 정보 열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-160">Adding a Details Column for Each Grid Row</span></span>

<span data-ttu-id="23207-161">다음으로 눈금의 오른쪽 셀에 표시 되는 각 부서에 대 한 교육 과정의 모든 참조 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-161">Next, you want to see all of the courses for each department displayed in the right-hand cell of the grid.</span></span> <span data-ttu-id="23207-162">이 작업을 수행 하려면 중첩 된 사용 합니다 `GridView` 컨트롤과 databind에서 데이터에는 `Courses` 의 탐색 속성은 `Department` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="23207-162">To do this, you'll use a nested `GridView` control and databind it to data from the `Courses` navigation property of the `Department` entity.</span></span>

<span data-ttu-id="23207-163">열기 *Departments.aspx* 및에 대 한 태그는 `GridView` 제어 처리기를 지정에 대 한는 `RowDataBound` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="23207-163">Open *Departments.aspx* and in the markup for the `GridView` control, specify a handler for the `RowDataBound` event.</span></span> <span data-ttu-id="23207-164">컨트롤의 여는 태그에 대 한 태그에는 이제 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-164">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

<span data-ttu-id="23207-165">새로 추가 `TemplateField` 요소 뒤의 `Administrator` 템플릿 필드:</span><span class="sxs-lookup"><span data-stu-id="23207-165">Add a new `TemplateField` element after the `Administrator` template field:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

<span data-ttu-id="23207-166">이 태그는 중첩 된 만듭니다 `GridView` 과정 번호 및 courses 목록 제목 표시 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="23207-166">This markup creates a nested `GridView` control that shows the course number and title of a list of courses.</span></span> <span data-ttu-id="23207-167">Databind 것 때문에 데이터 소스를 지정 하지의 코드에는 `RowDataBound` 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="23207-167">It does not specify a data source because you'll databind it in code in the `RowDataBound` handler.</span></span>

<span data-ttu-id="23207-168">열기 *Departments.aspx.cs* 에 대 한 다음 처리기를 추가 하 고는 `RowDataBound` 이벤트:</span><span class="sxs-lookup"><span data-stu-id="23207-168">Open *Departments.aspx.cs* and add the following handler for the `RowDataBound` event:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

<span data-ttu-id="23207-169">이 코드는 `Department` 이벤트 인수에서 엔터티를 변환는 `Courses` 탐색 속성을는 `List` 컬렉션 및 중첩 된 데이터 바인딩합니다 `GridView` 컬렉션에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23207-169">This code gets the `Department` entity from the event arguments, converts the `Courses` navigation property to a `List` collection, and databinds the nested `GridView` to the collection.</span></span>

<span data-ttu-id="23207-170">열기는 *SchoolRepository.cs* 파일을 즉시 로드에 대 한 지정는 `Courses` 호출 하 여 탐색 속성은 `Include` 에서 만드는 개체 쿼리에 대 한 메서드는 `GetDepartmentsByName` 메서드.</span><span class="sxs-lookup"><span data-stu-id="23207-170">Open the *SchoolRepository.cs* file and specify eager loading for the `Courses` navigation property by calling the `Include` method in the object query that you create in the `GetDepartmentsByName` method.</span></span> <span data-ttu-id="23207-171">`return` 의 문에서 `GetDepartmentsByName` 메서드에는 이제 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-171">The `return` statement in the `GetDepartmentsByName` method now resembles the following example.</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

<span data-ttu-id="23207-172">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-172">Run the page.</span></span> <span data-ttu-id="23207-173">정렬 및 필터링 이전에 추가한 기능을 실행 하는 것 외에도 GridView 컨트롤 이제 각 부서에 대 한 중첩된 강좌 세부 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-173">In addition to the sorting and filtering capability that you added earlier, the GridView control now shows nested course details for each department.</span></span>

<span data-ttu-id="23207-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="23207-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span></span>

<span data-ttu-id="23207-175">이로써 정렬, 필터링, 및 마스터-세부 정보 시나리오를 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="23207-175">This completes the introduction to sorting, filtering, and master-detail scenarios.</span></span> <span data-ttu-id="23207-176">다음 자습서에서는 동시성을 처리 하는 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23207-176">In the next tutorial, you'll see how to handle concurrency.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="23207-177">[이전](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
[다음](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="23207-177">[Previous](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span></span>
