---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: 먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-4 부 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은...
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/03/2010
ms.topic: article
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: 6bea5f4faeb0a9c11a406a7e4e87c4929eda6a18
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30886871"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a><span data-ttu-id="cb5c6-104">먼저 Entity Framework 4.0 데이터베이스와 시작 및 ASP.NET 4 Web Forms-4 부</span><span class="sxs-lookup"><span data-stu-id="cb5c6-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 4</span></span>
====================
<span data-ttu-id="cb5c6-105">으로 [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="cb5c6-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="cb5c6-106">Contoso 대학 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="cb5c6-107">자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="cb5c6-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>


## <a name="working-with-related-data"></a><span data-ttu-id="cb5c6-108">관련된 데이터 작업</span><span class="sxs-lookup"><span data-stu-id="cb5c6-108">Working with Related Data</span></span>

<span data-ttu-id="cb5c6-109">이전 자습서에서 사용 되는 `EntityDataSource` 필터, 정렬 및 그룹 데이터를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-109">In the previous tutorial you used the `EntityDataSource` control to filter, sort, and group data.</span></span> <span data-ttu-id="cb5c6-110">이 자습서에서는 표시 하 고 관련된 데이터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-110">In this tutorial you'll display and update related data.</span></span>

<span data-ttu-id="cb5c6-111">강사의 목록을 보여 주는 강사 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-111">You'll create the Instructors page that shows a list of instructors.</span></span> <span data-ttu-id="cb5c6-112">강사를 선택 하면 해당 강사 여 courses 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-112">When you select an instructor, you see a list of courses taught by that instructor.</span></span> <span data-ttu-id="cb5c6-113">과정을 선택 하면 등록 과정에 학생의 목록과 과정에 대 한 세부 정보 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-113">When you select a course, you see details for the course and a list of students enrolled in the course.</span></span> <span data-ttu-id="cb5c6-114">강사 이름, 고용 날짜 및 사무실 할당을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-114">You can edit the instructor name, hire date, and office assignment.</span></span> <span data-ttu-id="cb5c6-115">Office 할당 탐색 속성을 통해 액세스 하는 별도 엔터티 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-115">The office assignment is a separate entity set that you access through a navigation property.</span></span>

<span data-ttu-id="cb5c6-116">마스터 데이터는 세부 데이터 또는 코드에서 태그를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-116">You can link master data to detail data in markup or in code.</span></span> <span data-ttu-id="cb5c6-117">자습서의이 부분에서는 두 방법 모두를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-117">In this part of the tutorial, you'll use both methods.</span></span>

<span data-ttu-id="cb5c6-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cb5c6-118">[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)</span></span>

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a><span data-ttu-id="cb5c6-119">표시 및 GridView 컨트롤에서 관련된 엔터티를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-119">Displaying and Updating Related Entities in a GridView Control</span></span>

<span data-ttu-id="cb5c6-120">라는 새 웹 페이지 생성 *Instructors.aspx* 를 사용 하는 *Site.Master* 마스터 페이지, 다음 태그를 추가 하 고는 `Content` 라는 컨트롤 `Content2`:</span><span class="sxs-lookup"><span data-stu-id="cb5c6-120">Create a new web page named *Instructors.aspx* that uses the *Site.Master* master page, and add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

<span data-ttu-id="cb5c6-121">이 태그를 만듭니다는 `EntityDataSource` 강사를 선택 하 고 업데이트 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-121">This markup creates an `EntityDataSource` control that selects instructors and enables updates.</span></span> <span data-ttu-id="cb5c6-122">`div` 요소 오른쪽에 나중에 열을 추가할 수 있도록 왼쪽 렌더링 하도록 태그를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-122">The `div` element configures markup to render on the left so that you can add a column on the right later.</span></span>

<span data-ttu-id="cb5c6-123">사이 `EntityDataSource` 태그와 닫는 `</div>` 태그에 다음 태그를 만드는 추가 `GridView` 제어 및 `Label` 제어 하는 오류 메시지에 대해 사용할:</span><span class="sxs-lookup"><span data-stu-id="cb5c6-123">Between the `EntityDataSource` markup and the closing `</div>` tag, add the following markup that creates a `GridView` control and a `Label` control that you'll use for error messages:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

<span data-ttu-id="cb5c6-124">이 `GridView` 행을 선택할 수, 선택 된 행을 밝은 회색 배경 색으로 강조 표시 및 지정 하는 처리기 (나중에 만들)에 대 한 제어는 `SelectedIndexChanged` 및 `Updating` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-124">This `GridView` control enables row selection, highlights the selected row with a light gray background color, and specifies handlers (which you'll create later) for the `SelectedIndexChanged` and `Updating` events.</span></span> <span data-ttu-id="cb5c6-125">또한 지정 `PersonID` 에 대 한는 `DataKeyNames` 속성을 나중에 추가할 다른 컨트롤에 선택된 된 행의 키 값을 전달 될 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-125">It also specifies `PersonID` for the `DataKeyNames` property, so that the key value of the selected row can be passed to another control that you'll add later.</span></span>

<span data-ttu-id="cb5c6-126">마지막 열이 포함 되어 강의 사무실 할당의 탐색 속성에 저장 되는 `Person` 엔터티 연결 된 엔터티의 있기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-126">The last column contains the instructor's office assignment, which is stored in a navigation property of the `Person` entity because it comes from an associated entity.</span></span> <span data-ttu-id="cb5c6-127">다음에 유의 `EditItemTemplate` 요소 지정 `Eval` 대신 `Bind`때문에 `GridView` 컨트롤을 업데이트 하려면 탐색 속성에 바인딩할 직접 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-127">Notice that the `EditItemTemplate` element specifies `Eval` instead of `Bind`, because the `GridView` control cannot directly bind to navigation properties in order to update them.</span></span> <span data-ttu-id="cb5c6-128">코드에서 사무실 할당을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-128">You'll update the office assignment in code.</span></span> <span data-ttu-id="cb5c6-129">이렇게 하려면에 대 한 참조 해야 합니다는 `TextBox` 제어를 가져오고 저장에서 하는 것은 `TextBox` 컨트롤의 `Init` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-129">To do that, you'll need a reference to the `TextBox` control, and you'll get and save that in the `TextBox` control's `Init` event.</span></span>

<span data-ttu-id="cb5c6-130">다음은 `GridView` 컨트롤은 한 `Label` 오류 메시지에 사용 되는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-130">Following the `GridView` control is a `Label` control that's used for error messages.</span></span> <span data-ttu-id="cb5c6-131">컨트롤의 `Visible` 속성은 `false`, 및 뷰 상태 꺼져만 때 코드 표시 되도록 오류에 대 한 응답으로 레이블이 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-131">The control's `Visible` property is `false`, and view state is turned off, so that the label will appear only when code makes it visible in response to an error.</span></span>

<span data-ttu-id="cb5c6-132">열기는 *Instructors.aspx.cs* 파일을 다음 추가 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="cb5c6-132">Open the *Instructors.aspx.cs* file and add the following `using` statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

<span data-ttu-id="cb5c6-133">Office 할당 텍스트 상자에 대 한 참조를 보유 하는 partial 클래스 이름 선언 바로 뒤 전용 클래스 필드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-133">Add a private class field immediately after the partial-class name declaration to hold a reference to the office assignment text box.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

<span data-ttu-id="cb5c6-134">에 대 한 스텁 추가 `SelectedIndexChanged` 이벤트 처리기를 나중에 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-134">Add a stub for the `SelectedIndexChanged` event handler that you'll add code for later.</span></span> <span data-ttu-id="cb5c6-135">또한 사무실 할당에 대 한 처리기를 추가 `TextBox` 컨트롤의 `Init` 이벤트에 대 한 참조를 저장할 수 있도록는 `TextBox` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-135">Also add a handler for the office assignment `TextBox` control's `Init` event so that you can store a reference to the `TextBox` control.</span></span> <span data-ttu-id="cb5c6-136">사용자가 탐색 속성에 연결 된 엔터티를 업데이트 하기 위해 입력 한 값을이 참조를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-136">You'll use this reference to get the value the user entered in order to update the entity associated with the navigation property.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

<span data-ttu-id="cb5c6-137">사용 하 여는 `GridView` 컨트롤의 `Updating` 업데이트 하는 이벤트는 `Location` 속성은 연결 된 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-137">You'll use the `GridView` control's `Updating` event to update the `Location` property of the associated `OfficeAssignment` entity.</span></span> <span data-ttu-id="cb5c6-138">에 대 한 다음 처리기를 추가 `Updating` 이벤트:</span><span class="sxs-lookup"><span data-stu-id="cb5c6-138">Add the following handler for the `Updating` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

<span data-ttu-id="cb5c6-139">이 코드를 클릭할 때 실행 **업데이트** 에 `GridView` 행입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-139">This code is run when the user clicks **Update** in a `GridView` row.</span></span> <span data-ttu-id="cb5c6-140">코드는 LINQ to Entities 사용 하 여 검색 된 `OfficeAssignment` 현재와 관련 된 엔터티 `Person` 엔터티를 사용 하 여는 `PersonID` 이벤트 인수에서 선택한 행의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-140">The code uses LINQ to Entities to retrieve the `OfficeAssignment` entity that's associated with the current `Person` entity, using the `PersonID` of the selected row from the event argument.</span></span>

<span data-ttu-id="cb5c6-141">값에 따라 다음 작업 중 하나는 코드는 다음 됩니다는 `InstructorOfficeTextBox` 제어:</span><span class="sxs-lookup"><span data-stu-id="cb5c6-141">The code then takes one of the following actions depending on the value in the `InstructorOfficeTextBox` control:</span></span>

- <span data-ttu-id="cb5c6-142">텍스트 상자에 값이 되 고 없습니다 `OfficeAssignment` 를 업데이트 하려면 엔터티 하나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-142">If the text box has a value and there's no `OfficeAssignment` entity to update, it creates one.</span></span>
- <span data-ttu-id="cb5c6-143">텍스트 상자에 값이 되 고는 `OfficeAssignment` 업데이트 엔터티에 `Location` 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-143">If the text box has a value and there's an `OfficeAssignment` entity, it updates the `Location` property value.</span></span>
- <span data-ttu-id="cb5c6-144">텍스트 상자가 비어 고 `OfficeAssignment` 엔터티, 엔터티를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-144">If the text box is empty and an `OfficeAssignment` entity exists, it deletes the entity.</span></span>

<span data-ttu-id="cb5c6-145">이후에 데이터베이스에 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-145">After this, it saves the changes to the database.</span></span> <span data-ttu-id="cb5c6-146">예외가 발생 하면 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-146">If an exception occurs, it displays an error message.</span></span>

<span data-ttu-id="cb5c6-147">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-147">Run the page.</span></span>

<span data-ttu-id="cb5c6-148">[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="cb5c6-148">[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)</span></span>

<span data-ttu-id="cb5c6-149">클릭 **편집** 하 고 텍스트 상자에 모든 필드를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-149">Click **Edit** and all fields change to text boxes.</span></span>

<span data-ttu-id="cb5c6-150">[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="cb5c6-150">[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)</span></span>

<span data-ttu-id="cb5c6-151">이러한 값을 포함 하 여 변경 **사무실 할당**합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-151">Change any of these values, including **Office Assignment**.</span></span> <span data-ttu-id="cb5c6-152">클릭 **업데이트** 목록에 반영 된 변경 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-152">Click **Update** and you'll see the changes reflected in the list.</span></span>

## <a name="displaying-related-entities-in-a-separate-control"></a><span data-ttu-id="cb5c6-153">별도 컨트롤에 관련된 엔터티를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-153">Displaying Related Entities in a Separate Control</span></span>

<span data-ttu-id="cb5c6-154">각 강사를 추가할 수 있도록 하나 이상의 과정을 학습 시킬 수 있습니다는 `EntityDataSource` 제어 및 `GridView` 컨트롤을 나오든 이들 강사 강사에서 선택 된 연관 courses 목록 `GridView` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-154">Each instructor can teach one or more courses, so you'll add an `EntityDataSource` control and a `GridView` control to list the courses associated with whichever instructor is selected in the instructors `GridView` control.</span></span> <span data-ttu-id="cb5c6-155">제목을 만들려면 및 `EntityDataSource` courses 엔터티에 대 한 제어, 오류 메시지 사이 다음 태그를 추가 `Label` 제어 및 닫는 `</div>` 태그:</span><span class="sxs-lookup"><span data-stu-id="cb5c6-155">To create a heading and the `EntityDataSource` control for courses entities, add the following markup between the error message `Label` control and the closing `</div>` tag:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

<span data-ttu-id="cb5c6-156">`Where` 의 값을 포함 하는 매개 변수는 `PersonID` 의 해당 행을 선택한 강사는 `InstructorsGridView` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-156">The `Where` parameter contains the value of the `PersonID` of the instructor whose row is selected in the `InstructorsGridView` control.</span></span> <span data-ttu-id="cb5c6-157">`Where` 속성을 가져오는 연결 된 모든 하위 select 명령을 포함 `Person` 에서 엔터티는 `Course` 엔터티의 `People` 탐색 속성을 선택은 `Course` 엔터티 경우에만 관련된 중`Person`엔터티 포함 선택한 `PersonID` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-157">The `Where` property contains a subselect command that gets all associated `Person` entities from a `Course` entity's `People` navigation property and selects the `Course` entity only if one of the associated `Person` entities contains the selected `PersonID` value.</span></span>

<span data-ttu-id="cb5c6-158">만들려는 `GridView` 컨트롤입니다. 바로 뒤에 다음 태그를 추가 `CoursesEntityDataSource` 컨트롤 (닫는 앞 `</div>` 태그):</span><span class="sxs-lookup"><span data-stu-id="cb5c6-158">To create the `GridView` control., add the following markup immediately following the `CoursesEntityDataSource` control (before the closing `</div>` tag):</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

<span data-ttu-id="cb5c6-159">없는 courses 없는 강사를 선택 하면 표시 됩니다 때문에 프로그램 `EmptyDataTemplate` 요소가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-159">Because no courses will be displayed if no instructor is selected, an `EmptyDataTemplate` element is included.</span></span>

<span data-ttu-id="cb5c6-160">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-160">Run the page.</span></span>

<span data-ttu-id="cb5c6-161">[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="cb5c6-161">[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)</span></span>

<span data-ttu-id="cb5c6-162">에 할당 하는 하나 이상의 과정을 가진 강사 선택한 과정 또는 courses 목록에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-162">Select an instructor who has one or more courses assigned, and the course or courses appear in the list.</span></span> <span data-ttu-id="cb5c6-163">(참고: 데이터베이스 스키마에서는 여러 강좌를 수 있지만 데이터베이스와 함께 제공 되는 테스트 데이터의 없는 강사 권한이 실제로 둘 이상의 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-163">(Note: although the database schema allows multiple courses, in the test data supplied with the database no instructor actually has more than one course.</span></span> <span data-ttu-id="cb5c6-164">추가할 수 있습니다 courses 데이터베이스에 직접 사용 하는 **서버 탐색기** 창 또는 *CoursesAdd.aspx* 페이지 자습서의 뒷부분에 추가 합니다.)</span><span class="sxs-lookup"><span data-stu-id="cb5c6-164">You can add courses to the database yourself using the **Server Explorer** window or the *CoursesAdd.aspx* page, which you'll add in a later tutorial.)</span></span>

<span data-ttu-id="cb5c6-165">[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="cb5c6-165">[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)</span></span>

<span data-ttu-id="cb5c6-166">`CoursesGridView` 컨트롤 과정 필드를 몇 개만 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-166">The `CoursesGridView` control shows only a few course fields.</span></span> <span data-ttu-id="cb5c6-167">과정에 대 한 모든 세부 정보를 표시 하려면 사용 합니다는 `DetailsView` 사용자가을 선택 하는 과정에 대 한 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-167">To display all the details for a course, you'll use a `DetailsView` control for the course that the user selects.</span></span> <span data-ttu-id="cb5c6-168">*Instructors.aspx*를 닫은 후 다음 태그를 추가 `</div>` 태그 (이 태그를 배치 해야 **후** 닫는 div 태그, 날짜부터 해당):</span><span class="sxs-lookup"><span data-stu-id="cb5c6-168">In *Instructors.aspx*, add the following markup after the closing `</div>` tag (make sure you place this markup **after** the closing div tag, not before it):</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

<span data-ttu-id="cb5c6-169">이 태그를 만듭니다는 `EntityDataSource` 에 바인딩되는 컨트롤은 `Courses` 엔터티 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-169">This markup creates an `EntityDataSource` control that's bound to the `Courses` entity set.</span></span> <span data-ttu-id="cb5c6-170">`Where` 를 사용 하 여 과정을 선택 하는 속성의 `CourseID` 코스에서 선택한 행의 값 `GridView` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-170">The `Where` property selects a course using the `CourseID` value of the selected row in the courses `GridView` control.</span></span> <span data-ttu-id="cb5c6-171">에 대 한 처리기를 지정 하는 태그는 `Selected` 이벤트를 나중에 사용할 학생 등급을 표시 하기 위한을 하위 계층에 다른 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-171">The markup specifies a handler for the `Selected` event, which you'll use later for displaying student grades, which is another level lower in the hierarchy.</span></span>

<span data-ttu-id="cb5c6-172">*Instructors.aspx.cs*에 대 한 다음 스텁을 `CourseDetailsEntityDataSource_Selected` 메서드.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-172">In *Instructors.aspx.cs*, create the following stub for the `CourseDetailsEntityDataSource_Selected` method.</span></span> <span data-ttu-id="cb5c6-173">(이 자습서의 뒷부분에 나오는이 스텁을 채우는 속도가; 지금은 필요한 페이지를 컴파일하고 실행 되도록 합니다.)</span><span class="sxs-lookup"><span data-stu-id="cb5c6-173">(You'll fill this stub out later in the tutorial; for now, you need it so that the page will compile and run.)</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

<span data-ttu-id="cb5c6-174">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-174">Run the page.</span></span>

<span data-ttu-id="cb5c6-175">[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="cb5c6-175">[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)</span></span>

<span data-ttu-id="cb5c6-176">처음에 없는 과정 선택 되었기 때문에 과정 세부 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-176">Initially there are no course details because no course is selected.</span></span> <span data-ttu-id="cb5c6-177">할당 하는 과정을 가진 강사를 선택한 다음 세부 정보를 과정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-177">Select an instructor who has a course assigned, and then select a course to see the details.</span></span>

<span data-ttu-id="cb5c6-178">[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="cb5c6-178">[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)</span></span>

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a><span data-ttu-id="cb5c6-179">EntityDataSource를 사용 하 여 "선택" 이벤트 관련된 데이터 표시</span><span class="sxs-lookup"><span data-stu-id="cb5c6-179">Using the EntityDataSource "Selected" Event to Display Related Data</span></span>

<span data-ttu-id="cb5c6-180">마지막으로 등록 된 학생 및 선택한 과정에 대 한 자신의 등급을 모두 표시 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-180">Finally, you want to show all of the enrolled students and their grades for the selected course.</span></span> <span data-ttu-id="cb5c6-181">이 작업을 수행 하려면을 사용 합니다는 `Selected` 의 이벤트는 `EntityDataSource` 과정에 바인딩된 컨트롤 `DetailsView`합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-181">To do this, you'll use the `Selected` event of the `EntityDataSource` control bound to the course `DetailsView`.</span></span>

<span data-ttu-id="cb5c6-182">*Instructors.aspx*, 다음 태그 뒤에 추가 `DetailsView` 제어:</span><span class="sxs-lookup"><span data-stu-id="cb5c6-182">In *Instructors.aspx*, add the following markup after the `DetailsView` control:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

<span data-ttu-id="cb5c6-183">이 태그를 만듭니다는 `ListView` 학생 선택한 과정에 대 한 자신의 등급의 목록을 표시 하는 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-183">This markup creates a `ListView` control that displays a list of students and their grades for the selected course.</span></span> <span data-ttu-id="cb5c6-184">데이터 원본이 없는 databind 코드에서 컨트롤 수 때문에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-184">No data source is specified because you'll databind the control in code.</span></span> <span data-ttu-id="cb5c6-185">`EmptyDataTemplate` 없는 과정을 선택 하는 경우 표시할 메시지를 제공 하는 요소-경우에 표시 하는 학생은 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-185">The `EmptyDataTemplate` element provides a message to display when no course is selected—in that case, there are no students to display.</span></span> <span data-ttu-id="cb5c6-186">`LayoutTemplate` 요소 목록을 표시 하는 HTML 테이블을 만듭니다 및 `ItemTemplate` 표시할 열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-186">The `LayoutTemplate` element creates an HTML table to display the list, and the `ItemTemplate` specifies the columns to display.</span></span> <span data-ttu-id="cb5c6-187">학생 ID와 학생 등급이는 `StudentGrade` 엔터티와 학생 이름에서이 `Person` Entity Framework에서 사용할 수 있도록 하는 엔터티는 `Person` 의 탐색 속성은 `StudentGrade` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-187">The student ID and the student grade are from the `StudentGrade` entity, and the student name is from the `Person` entity that the Entity Framework makes available in the `Person` navigation property of the `StudentGrade` entity.</span></span>

<span data-ttu-id="cb5c6-188">*Instructors.aspx.cs*, 대체 스텁 아웃 `CourseDetailsEntityDataSource_Selected` 메서드를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="cb5c6-188">In *Instructors.aspx.cs*, replace the stubbed-out `CourseDetailsEntityDataSource_Selected` method with the following code:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

<span data-ttu-id="cb5c6-189">이 이벤트에 대 한 이벤트 인수 형식 아무것도 선택 하지 않으면 항목이 0 또는 1 개의 항목 포함 하는 컬렉션으로 선택한 데이터를 제공 하는 경우는 `Course` 엔터티를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-189">The event argument for this event provides the selected data in the form of a collection, which will have zero items if nothing is selected or one item if a `Course` entity is selected.</span></span> <span data-ttu-id="cb5c6-190">경우는 `Course` 엔터티가 선택 되었는지, 코드를 사용 하 여는 `First` 메서드를 단일 개체 컬렉션으로 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-190">If a `Course` entity is selected, the code uses the `First` method to convert the collection to a single object.</span></span> <span data-ttu-id="cb5c6-191">그런 다음 가져옵니다 `StudentGrade` 탐색 속성에서 엔터티 컬렉션으로 변환 및 바인딩하는 `GradesListView` 컨트롤 컬렉션을 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-191">It then gets `StudentGrade` entities from the navigation property, converts them to a collection, and binds the `GradesListView` control to the collection.</span></span>

<span data-ttu-id="cb5c6-192">표시 하려면 등급, 하지만 빈 데이터 서식 파일에 메시지 페이지는 처음으로 표시 되는지 확인 하려면 충분 한 며이 과정을 선택 하지 않으면 때마다입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-192">This is sufficient to display grades, but you want to make sure that the message in the empty data template is displayed the first time the page is displayed and whenever a course is not selected.</span></span> <span data-ttu-id="cb5c6-193">이렇게 하려면 두 위치에서 호출 하는 다음 메서드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-193">To do that, create the following method, which you'll call from two places:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

<span data-ttu-id="cb5c6-194">이 새 메서드를 호출 하는 `Page_Load` 메서드를 페이지가 표시 되는 빈 데이터 템플릿을 처음 시간을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-194">Call this new method from the `Page_Load` method to display the empty data template the first time the page is displayed.</span></span> <span data-ttu-id="cb5c6-195">호출에서 `InstructorsGridView_SelectedIndexChanged` 메서드 강사 선택 된 경우 해당 이벤트가 발생 하기 때문에 새 과정을 의미 하는 강의에 로드 `GridView` 컨트롤과 none 아직 선택 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-195">And call it from the `InstructorsGridView_SelectedIndexChanged` method because that event is raised when an instructor is selected, which means new courses are loaded into the courses `GridView` control and none is selected yet.</span></span> <span data-ttu-id="cb5c6-196">다음은 두 번 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-196">Here are the two calls:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

<span data-ttu-id="cb5c6-197">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-197">Run the page.</span></span>

<span data-ttu-id="cb5c6-198">[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="cb5c6-198">[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)</span></span>

<span data-ttu-id="cb5c6-199">할당 하는 과정을 가진 강사를 선택 하 고 과정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-199">Select an instructor that has a course assigned, and then select the course.</span></span>

<span data-ttu-id="cb5c6-200">[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="cb5c6-200">[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)</span></span>

<span data-ttu-id="cb5c6-201">관련 된 데이터로 작업 하는 몇 가지 방법을 살펴 보았습니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-201">You have now seen a few ways to work with related data.</span></span> <span data-ttu-id="cb5c6-202">다음 자습서에서는 기존 엔터티 간의 관계를 추가 하는 방법을 알아봅니다 관계를 제거 하는 방법 및 기존 엔터티와 관계를 맺고 있는 새 엔터티를 추가 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cb5c6-202">In the following tutorial, you'll learn how to add relationships between existing entities, how to remove relationships, and how to add a new entity that has a relationship to an existing entity.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cb5c6-203">[이전](the-entity-framework-and-aspnet-getting-started-part-3.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="cb5c6-203">[Previous](the-entity-framework-and-aspnet-getting-started-part-3.md)
[Next](the-entity-framework-and-aspnet-getting-started-part-5.md)</span></span>
