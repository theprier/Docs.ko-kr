---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
title: '3 부 Entity Framework 4.0 및 ObjectDataSource 컨트롤 사용: 정렬 및 필터링 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈의 Entity Framework 4.0 자습서 시리즈를 사용 하 여 시작 하 여 만든 Contoso University 웹 응용 프로그램 기반으로 합니다. 필자는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/26/2011
ms.topic: article
ms.assetid: 2990bd10-590d-43d5-9529-6b503ce5455d
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering
msc.type: authoredcontent
ms.openlocfilehash: 48d859191877ba951e233f19873d52625fe180ac
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378912"
---
<a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-3-sorting-and-filtering"></a><span data-ttu-id="0b708-104">3 부 Entity Framework 4.0 및 ObjectDataSource 컨트롤 사용: 정렬 및 필터링</span><span class="sxs-lookup"><span data-stu-id="0b708-104">Using the Entity Framework 4.0 and the ObjectDataSource Control, Part 3: Sorting and Filtering</span></span>
====================
<span data-ttu-id="0b708-105">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="0b708-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="0b708-106">이 자습서 시리즈에서 만든 Contoso University 웹 응용 프로그램 빌드를 [Entity Framework 4.0을 사용 하 여 시작](https://asp.net/entity-framework/tutorials#Getting%20Started) 자습서 시리즈입니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) tutorial series.</span></span> <span data-ttu-id="0b708-107">이전 자습서를 완료 하지 않은 경우이 자습서에 대 한 시작 지점으로 할 수 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 만들어졌을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="0b708-108">할 수도 있습니다 [응용 프로그램을 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 전체 자습서 시리즈에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="0b708-109">이 자습서에 대 한 질문이 있으면 하기를 게시할 수 있습니다 합니다 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>


<span data-ttu-id="0b708-110">이전 자습서에서 Entity Framework를 사용 하는 n 계층 웹 응용 프로그램에서 리포지토리 패턴을 구현 하 고 `ObjectDataSource` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-110">In the previous tutorial you implemented the repository pattern in an n-tier web application that uses the Entity Framework and the `ObjectDataSource` control.</span></span> <span data-ttu-id="0b708-111">이 자습서에서는 정렬 및 필터링을 수행 하 여 마스터-세부 시나리오를 처리 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-111">This tutorial shows how to do sorting and filtering and handle master-detail scenarios.</span></span> <span data-ttu-id="0b708-112">다음과 같은 향상 된 기능을 추가 합니다 *Departments.aspx* 페이지:</span><span class="sxs-lookup"><span data-stu-id="0b708-112">You'll add the following enhancements to the *Departments.aspx* page:</span></span>

- <span data-ttu-id="0b708-113">입력란을 이름으로 부서를 선택할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-113">A text box to allow users to select departments by name.</span></span>
- <span data-ttu-id="0b708-114">목록 표에 표시 되는 각 부서에 대 한 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-114">A list of courses for each department that's shown in the grid.</span></span>
- <span data-ttu-id="0b708-115">열 머리글을 클릭 하 여 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-115">The ability to sort by clicking column headings.</span></span>

<span data-ttu-id="0b708-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="0b708-116">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image1.png)</span></span>

## <a name="adding-the-ability-to-sort-gridview-columns"></a><span data-ttu-id="0b708-117">GridView 열 정렬 하는 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-117">Adding the Ability to Sort GridView Columns</span></span>

<span data-ttu-id="0b708-118">엽니다는 *Departments.aspx* 페이지 및 추가 `SortParameterName="sortExpression"` 특성을 `ObjectDataSource` 라는 컨트롤 `DepartmentsObjectDataSource`합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-118">Open the *Departments.aspx* page and add a `SortParameterName="sortExpression"` attribute to the `ObjectDataSource` control named `DepartmentsObjectDataSource`.</span></span> <span data-ttu-id="0b708-119">(만들어 나중에 `GetDepartments` 라는 매개 변수를 갖는 메서드의 `sortExpression`.) 컨트롤의 여는 태그에 대 한 태그에는 이제 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-119">(Later you'll create a `GetDepartments` method that takes a parameter named `sortExpression`.) The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample1.aspx)]

<span data-ttu-id="0b708-120">추가 된 `AllowSorting="true"` 특성을 여는 태그를 `GridView` 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-120">Add the `AllowSorting="true"` attribute to the opening tag of the `GridView` control.</span></span> <span data-ttu-id="0b708-121">컨트롤의 여는 태그에 대 한 태그에는 이제 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-121">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample2.aspx)]

<span data-ttu-id="0b708-122">*Departments.aspx.cs*를 호출 하 여 기본 정렬 순서를 설정 합니다 `GridView` 컨트롤의 `Sort` 메서드에서 `Page_Load` 메서드:</span><span class="sxs-lookup"><span data-stu-id="0b708-122">In *Departments.aspx.cs*, set the default sort order by calling the `GridView` control's `Sort` method from the `Page_Load` method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample3.cs)]

<span data-ttu-id="0b708-123">비즈니스 논리 클래스 또는 해당 리포지토리 클래스를 정렬 하거나 필터링 하는 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-123">You can add code that sorts or filters in either the business logic class or the repository class.</span></span> <span data-ttu-id="0b708-124">비즈니스 논리 클래스에서 수행 하는 경우 정렬 또는 필터링 작업은 데이터베이스에서 데이터를 검색 한 후 있기 때문에 가능는 비즈니스 논리 클래스가 사용 되는 `IEnumerable` 저장소에서 반환 된 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-124">If you do it in the business logic class, the sorting or filtering work will be done after the data is retrieved from the database, because the business logic class is working with an `IEnumerable` object returned by the repository.</span></span> <span data-ttu-id="0b708-125">정렬 및 필터링 리포지토리 클래스의 코드를 추가 하 고 그렇게 하는 LINQ 식 앞 또는 개체 쿼리 변환 된 경우는 `IEnumerable` 개체, 일반적으로 더 효율적인 처리를 위해 데이터베이스에 명령을 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-125">If you add sorting and filtering code in the repository class and you do it before a LINQ expression or object query has been converted to an `IEnumerable` object, your commands will be passed through to the database for processing, which is typically more efficient.</span></span> <span data-ttu-id="0b708-126">이 자습서에서는 정렬 및 데이터베이스에서 완료 해야 하는 처리를 발생 시키는 방식으로 필터링를 구현 하-즉, 리포지토리에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-126">In this tutorial you'll implement sorting and filtering in a way that causes the processing to be done by the database — that is, in the repository.</span></span>

<span data-ttu-id="0b708-127">정렬 기능을 추가 하 고 리포지토리 인터페이스는 비즈니스 논리 클래스에 대 한 리포지토리 클래스를도 새 메서드를 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-127">To add sorting capability, you must add a new method to the repository interface and repository classes as well as to the business logic class.</span></span> <span data-ttu-id="0b708-128">에 *ISchoolRepository.cs* 파일에서 새 `GetDepartments` 메서드를는 `sortExpression` 반환 되는 부서 목록을 정렬 하는 데 사용할 수 있는 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="0b708-128">In the *ISchoolRepository.cs* file, add a new `GetDepartments` method that takes a `sortExpression` parameter that will be used to sort the list of departments that's returned:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample4.cs)]

<span data-ttu-id="0b708-129">`sortExpression` 매개 변수 열을 기준으로 정렬 및 정렬 방향을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-129">The `sortExpression` parameter will specify the column to sort on and the sort direction.</span></span>

<span data-ttu-id="0b708-130">새 메서드를 위한 코드를 추가 합니다 *SchoolRepository.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="0b708-130">Add code for the new method to the *SchoolRepository.cs* file:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample5.cs)]

<span data-ttu-id="0b708-131">매개 변수가 없는 기존 변경 `GetDepartments` 새 메서드를 호출 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="0b708-131">Change the existing parameterless `GetDepartments` method to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample6.cs)]

<span data-ttu-id="0b708-132">테스트 프로젝트에서 다음 새 메서드를 추가 합니다 *MockSchoolRepository.cs*:</span><span class="sxs-lookup"><span data-stu-id="0b708-132">In the test project, add the following new method to *MockSchoolRepository.cs*:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample7.cs)]

<span data-ttu-id="0b708-133">정렬 된 목록을 반환 합니다.이 메서드를 종속 되어 있는 모든 단위 테스트를 만드는 것을 사용 하는 경우에 반환 하기 전에 목록을 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-133">If you were going to create any unit tests that depended on this method returning a sorted list, you would need to sort the list before returning it.</span></span> <span data-ttu-id="0b708-134">않습니다 만드시겠습니까 테스트는이 자습서에서는 메서드 수 정렬 되지 않은 부서 목록을 반환 하므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-134">You won't be creating tests like that in this tutorial, so the method can just return the unsorted list of departments.</span></span>

<span data-ttu-id="0b708-135">에 *SchoolBL.cs* 파일에서 다음 새 메서드는 비즈니스 논리 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-135">In the *SchoolBL.cs* file, add the following new method to the business logic class:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample8.cs)]

<span data-ttu-id="0b708-136">이 코드는 리포지토리 메서드로 정렬 매개 변수를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-136">This code passes the sort parameter to the repository method.</span></span>

<span data-ttu-id="0b708-137">실행 합니다 *Departments.aspx* 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-137">Run the *Departments.aspx* page.</span></span>

<span data-ttu-id="0b708-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="0b708-138">[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image3.png)</span></span>

<span data-ttu-id="0b708-139">이제 해당 열으로 정렬 하려면 열 머리글을 클릭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-139">You can now click any column heading to sort by that column.</span></span> <span data-ttu-id="0b708-140">열이 이미 정렬 하는 경우 제목을 클릭 하는 정렬 방향을 반대로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-140">If the column is already sorted, clicking the heading reverses the sort direction.</span></span>

## <a name="adding-a-search-box"></a><span data-ttu-id="0b708-141">검색 상자 추가</span><span class="sxs-lookup"><span data-stu-id="0b708-141">Adding a Search Box</span></span>

<span data-ttu-id="0b708-142">이 섹션의 검색 텍스트 상자 추가, 연결할 수는 `ObjectDataSource` 제어 매개 변수를 사용 하 여 제어 하 고 필터링을 지원 하도록 비즈니스 논리 클래스에 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-142">In this section you'll add a search text box, link it to the `ObjectDataSource` control using a control parameter, and add a method to the business logic class to support filtering.</span></span>

<span data-ttu-id="0b708-143">엽니다는 *Departments.aspx* 첫 번째 머리글 사이 다음 태그를 추가한 페이지 `ObjectDataSource` 컨트롤:</span><span class="sxs-lookup"><span data-stu-id="0b708-143">Open the *Departments.aspx* page and add the following markup between the heading and the first `ObjectDataSource` control:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample9.aspx)]

<span data-ttu-id="0b708-144">`ObjectDataSource` 라는 컨트롤 `DepartmentsObjectDataSource`, 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-144">In the `ObjectDataSource` control named `DepartmentsObjectDataSource`, do the following:</span></span>

- <span data-ttu-id="0b708-145">추가 `SelectParameters` 라는 매개 변수 요소 `nameSearchString` 에 입력 된 값을 가져옵니다는 `SearchTextBox` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-145">Add a `SelectParameters` element for a parameter named `nameSearchString` that gets the value entered in the `SearchTextBox` control.</span></span>
- <span data-ttu-id="0b708-146">변경 된 `SelectMethod` 특성 값을 `GetDepartmentsByName`입니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-146">Change the `SelectMethod` attribute value to `GetDepartmentsByName`.</span></span> <span data-ttu-id="0b708-147">(나중에 만들이 메서드가 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="0b708-147">(You'll create this method later.)</span></span>

<span data-ttu-id="0b708-148">에 대 한 태그는 `ObjectDataSource` 컨트롤에는 이제 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-148">The markup for the `ObjectDataSource` control now resembles the following example:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample10.aspx)]

<span data-ttu-id="0b708-149">*ISchoolRepository.cs*, 추가 된 `GetDepartmentsByName` 둘 다 사용 하는 메서드 `sortExpression` 및 `nameSearchString` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="0b708-149">In *ISchoolRepository.cs*, add a `GetDepartmentsByName` method that takes both `sortExpression` and `nameSearchString` parameters:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample11.cs)]

<span data-ttu-id="0b708-150">*SchoolRepository.cs*, 다음 새 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-150">In *SchoolRepository.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample12.cs)]

<span data-ttu-id="0b708-151">이 코드에 사용 된 `Where` 검색 문자열이 포함 된 항목을 선택 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-151">This code uses a `Where` method to select items that contain the search string.</span></span> <span data-ttu-id="0b708-152">검색 문자열이 비어 있으면 모든 레코드 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-152">If the search string is empty, all records will be selected.</span></span> <span data-ttu-id="0b708-153">메서드를 다음과 같이 하나의 문에서 함께 호출을 지정 하는 경우 사용자에 게 유의 (`Include`, 한 다음 `OrderBy`, 다음 `Where`), `Where` 메서드 항상 마지막 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-153">Note that when you specify method calls together in one statement like this (`Include`, then `OrderBy`, then `Where`), the `Where` method must always be last.</span></span>

<span data-ttu-id="0b708-154">기존 변경 `GetDepartments` 사용 하는 메서드를 `sortExpression` 새 메서드를 호출 하는 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="0b708-154">Change the existing `GetDepartments` method that takes a `sortExpression` parameter to call the new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample13.cs)]

<span data-ttu-id="0b708-155">*MockSchoolRepository.cs* 테스트 프로젝트에서 다음 새 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-155">In *MockSchoolRepository.cs* in the test project, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample14.cs)]

<span data-ttu-id="0b708-156">*SchoolBL.cs*, 다음 새 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-156">In *SchoolBL.cs*, add the following new method:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample15.cs)]

<span data-ttu-id="0b708-157">실행 합니다 *Departments.aspx* 페이지 및 선택 논리 작동 하는지 확인 하려면 검색 문자열을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-157">Run the *Departments.aspx* page and enter a search string to make sure that the selection logic works.</span></span> <span data-ttu-id="0b708-158">텍스트 상자를 비워 두고 모든 레코드가 반환 되도록 검색을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="0b708-158">Leave the text box empty and try a search to make sure that all records are returned.</span></span>

<span data-ttu-id="0b708-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="0b708-159">[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image5.png)</span></span>

## <a name="adding-a-details-column-for-each-grid-row"></a><span data-ttu-id="0b708-160">각 그리드 행에 대 한 세부 정보 열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-160">Adding a Details Column for Each Grid Row</span></span>

<span data-ttu-id="0b708-161">다음으로, 모든 그리드의 오른쪽 셀에 표시 되는 각 부서에 대 한 강의 참조 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-161">Next, you want to see all of the courses for each department displayed in the right-hand cell of the grid.</span></span> <span data-ttu-id="0b708-162">이 위해 사용 하 여 중첩 된 `GridView` 컨트롤과 databind 데이터로 하는 `Courses` 의 탐색 속성을 `Department` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="0b708-162">To do this, you'll use a nested `GridView` control and databind it to data from the `Courses` navigation property of the `Department` entity.</span></span>

<span data-ttu-id="0b708-163">열기 *Departments.aspx* 및 태그에는 `GridView` 컨트롤을 처리기를 지정에 대 한는 `RowDataBound` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-163">Open *Departments.aspx* and in the markup for the `GridView` control, specify a handler for the `RowDataBound` event.</span></span> <span data-ttu-id="0b708-164">컨트롤의 여는 태그에 대 한 태그에는 이제 다음 예제와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-164">The markup for the opening tag of the control now resembles the following example.</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample16.aspx)]

<span data-ttu-id="0b708-165">새 `TemplateField` 요소 뒤의 `Administrator` 템플릿 필드:</span><span class="sxs-lookup"><span data-stu-id="0b708-165">Add a new `TemplateField` element after the `Administrator` template field:</span></span>

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample17.aspx)]

<span data-ttu-id="0b708-166">이 태그는 중첩 된 만듭니다 `GridView` 강좌 번호 및 제목 목록은 과정을 보여주는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-166">This markup creates a nested `GridView` control that shows the course number and title of a list of courses.</span></span> <span data-ttu-id="0b708-167">Databind 해야 하기 때문에 데이터 소스를 지정 하지에서 코드에는 `RowDataBound` 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-167">It does not specify a data source because you'll databind it in code in the `RowDataBound` handler.</span></span>

<span data-ttu-id="0b708-168">오픈 *Departments.aspx.cs* 에 대 한 다음 처리기를 추가 하 고는 `RowDataBound` 이벤트:</span><span class="sxs-lookup"><span data-stu-id="0b708-168">Open *Departments.aspx.cs* and add the following handler for the `RowDataBound` event:</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample18.cs)]

<span data-ttu-id="0b708-169">이 코드는 `Department` 이벤트 인수에서 엔터티 변환 합니다 `Courses` 탐색 속성을를 `List` 컬렉션 및 중첩 된 계열을 `GridView` 컬렉션에.</span><span class="sxs-lookup"><span data-stu-id="0b708-169">This code gets the `Department` entity from the event arguments, converts the `Courses` navigation property to a `List` collection, and databinds the nested `GridView` to the collection.</span></span>

<span data-ttu-id="0b708-170">열기는 *SchoolRepository.cs* 파일과 대해 즉시 로드를 지정 합니다 `Courses` 호출 하 여 탐색 속성을 `Include` 에서 만든 개체 쿼리에서 메서드를 `GetDepartmentsByName` 메서드.</span><span class="sxs-lookup"><span data-stu-id="0b708-170">Open the *SchoolRepository.cs* file and specify eager loading for the `Courses` navigation property by calling the `Include` method in the object query that you create in the `GetDepartmentsByName` method.</span></span> <span data-ttu-id="0b708-171">합니다 `return` 문에서 `GetDepartmentsByName` 메서드에는 이제 다음 예제와 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-171">The `return` statement in the `GetDepartmentsByName` method now resembles the following example.</span></span>

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/samples/sample19.cs)]

<span data-ttu-id="0b708-172">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-172">Run the page.</span></span> <span data-ttu-id="0b708-173">정렬 및 필터링 위에서 추가한 기능을 하는 것 외에도 GridView 컨트롤은 이제 각 부서에 대 한 중첩 된 강좌 세부 정보 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-173">In addition to the sorting and filtering capability that you added earlier, the GridView control now shows nested course details for each department.</span></span>

<span data-ttu-id="0b708-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="0b708-174">[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering/_static/image7.png)</span></span>

<span data-ttu-id="0b708-175">정렬, 필터링 및 마스터-세부 시나리오에 대 한 소개를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-175">This completes the introduction to sorting, filtering, and master-detail scenarios.</span></span> <span data-ttu-id="0b708-176">다음 자습서에서는 동시성을 처리 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="0b708-176">In the next tutorial, you'll see how to handle concurrency.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0b708-177">[이전](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
> [다음](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span><span class="sxs-lookup"><span data-stu-id="0b708-177">[Previous](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
[Next](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)</span></span>
