---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: 먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms-8 부 | Microsoft Docs
author: tdykstra
description: Contoso University 샘플 웹 응용 프로그램에는 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: 249677c9e0eca248710bf730e57a7aeca5a9b5ce
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835489"
---
<a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a><span data-ttu-id="2ee87-104">먼저 Entity Framework 4.0 Database를 사용 하 여 시작 및 ASP.NET 4 Web Forms-8 부</span><span class="sxs-lookup"><span data-stu-id="2ee87-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 8</span></span>
====================
<span data-ttu-id="2ee87-105">[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="2ee87-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="2ee87-106">Contoso University 샘플 웹 응용 프로그램에는 Entity Framework 4.0 및 Visual Studio 2010을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="2ee87-107">자습서 시리즈에 대 한 정보를 참조 하세요. [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="2ee87-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>


## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a><span data-ttu-id="2ee87-108">Dynamic Data 기능을 사용 하 여 서식을 지정 하 고 데이터 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="2ee87-108">Using Dynamic Data Functionality to Format and Validate Data</span></span>

<span data-ttu-id="2ee87-109">이전 자습서에서 저장된 프로시저를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-109">In the previous tutorial you implemented stored procedures.</span></span> <span data-ttu-id="2ee87-110">이 자습서에서는 보여줍니다 Dynamic Data 기능 다음과 같은 이점을 제공할 수 있습니다 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="2ee87-110">This tutorial will show you how Dynamic Data functionality can provide the following benefits:</span></span>

- <span data-ttu-id="2ee87-111">필드는 자동으로 해당 데이터 형식을 기반으로 하는 디스플레이에 서식이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-111">Fields are automatically formatted for display based on their data type.</span></span>
- <span data-ttu-id="2ee87-112">필드는 해당 데이터 형식을 기반으로 자동으로 유효성이 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-112">Fields are automatically validated based on their data type.</span></span>
- <span data-ttu-id="2ee87-113">서식 지정 및 유효성 검사 동작을 사용자 지정 데이터 모델에 메타 데이터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-113">You can add metadata to the data model to customize formatting and validation behavior.</span></span> <span data-ttu-id="2ee87-114">이렇게 하면 하나의 위치에서 서식 지정 및 유효성 검사 규칙을 추가할 수 있습니다 하 고 어디에서 나 자동으로 적용 되는 동적 데이터 컨트롤을 사용 하 여 필드에 액세스 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-114">When you do this, you can add the formatting and validation rules in just one place, and they're automatically applied everywhere you access the fields using Dynamic Data controls.</span></span>

<span data-ttu-id="2ee87-115">사용할 컨트롤을 표시 하 고 기존 필드를 편집 합니다.이 과정을 보려면 변경 *Students.aspx* 페이지에서 추가 서식 지정 및 유효성 검사 메타 데이터 이름 및 날짜 필드에는 `Student` 엔터티 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-115">To see how this works, you'll change the controls you use to display and edit fields in the existing *Students.aspx* page, and you'll add formatting and validation metadata to the name and date fields of the `Student` entity type.</span></span>

<span data-ttu-id="2ee87-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="2ee87-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span></span>

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a><span data-ttu-id="2ee87-117">DynamicField 및 DynamicControl 컨트롤을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2ee87-117">Using DynamicField and DynamicControl Controls</span></span>

<span data-ttu-id="2ee87-118">열기는 *Students.aspx* 페이지 및 합니다 `StudentsGridView` 제어 바꾸기는 **이름** 및 **등록 날짜** `TemplateField` 다음 태그를 사용 하 여 요소:</span><span class="sxs-lookup"><span data-stu-id="2ee87-118">Open the *Students.aspx* page and in the `StudentsGridView` control replace the **Name** and **Enrollment Date** `TemplateField` elements with the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

<span data-ttu-id="2ee87-119">이 태그를 사용 하 여 `DynamicControl` 대신 제어 `TextBox` 하 고 `Label` 학생에서 컨트롤 템플릿 필드 이름을 지정 하 고 사용 하 여는 `DynamicField` 등록 날짜에 대 한 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-119">This markup uses `DynamicControl` controls in place of `TextBox` and `Label` controls in the student name template field, and it uses a `DynamicField` control for the enrollment date.</span></span> <span data-ttu-id="2ee87-120">없는 형식 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-120">No format strings are specified.</span></span>

<span data-ttu-id="2ee87-121">추가 `ValidationSummary` 후에 컨트롤을 `StudentsGridView` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-121">Add a `ValidationSummary` control after the `StudentsGridView` control.</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

<span data-ttu-id="2ee87-122">에 `SearchGridView` 컨트롤에 대 한 태그를 바꿉니다는 **이름** 및 **등록 날짜** 에서 수행한 대로 열을 `StudentsGridView` 컨트롤을 생략 하는 제외는 `EditItemTemplate` 요소.</span><span class="sxs-lookup"><span data-stu-id="2ee87-122">In the `SearchGridView` control replace the markup for the **Name** and **Enrollment Date** columns as you did in the `StudentsGridView` control, except omit the `EditItemTemplate` element.</span></span> <span data-ttu-id="2ee87-123">`Columns` 의 요소는 `SearchGridView` 컨트롤은 이제 다음 태그를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-123">The `Columns` element of the `SearchGridView` control now contains the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

<span data-ttu-id="2ee87-124">오픈 *Students.aspx.cs* 추가한 다음 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="2ee87-124">Open *Students.aspx.cs* and add the following `using` statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

<span data-ttu-id="2ee87-125">페이지에 대 한 처리기를 추가 `Init` 이벤트:</span><span class="sxs-lookup"><span data-stu-id="2ee87-125">Add a handler for the page's `Init` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

<span data-ttu-id="2ee87-126">이 코드는 동적 데이터 서식 지정 및 유효성 검사의 필드에 대 한 이러한 데이터 바인딩된 컨트롤에서 제공 됩니다는 지정 된 `Student` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="2ee87-126">This code specifies that Dynamic Data will provide formatting and validation in these data-bound controls for fields of the `Student` entity.</span></span> <span data-ttu-id="2ee87-127">페이지를 실행 하는 경우 다음 예제와 같이 오류 메시지를 받게 되 면 일반적으로 의미를 호출 하지 않았습니다 합니다 `EnableDynamicData` 의 메서드 `Page_Init`:</span><span class="sxs-lookup"><span data-stu-id="2ee87-127">If you get an error message like the following example when you run the page, it typically means you've forgotten to call the `EnableDynamicData` method in `Page_Init`:</span></span>

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

<span data-ttu-id="2ee87-128">페이지를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-128">Run the page.</span></span>

<span data-ttu-id="2ee87-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="2ee87-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span></span>

<span data-ttu-id="2ee87-130">에 **Enrollment Date** 열에서 속성 형식이 이기 때문에 날짜와 함께 표시 됩니다 `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="2ee87-130">In the **Enrollment Date** column, the time is displayed along with the date because the property type is `DateTime`.</span></span> <span data-ttu-id="2ee87-131">나중에 수정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-131">You'll fix that later.</span></span>

<span data-ttu-id="2ee87-132">이제 동적 데이터가 기본 데이터 유효성 검사를 자동으로 제공 하는 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-132">For now, notice that Dynamic Data automatically provides basic data validation.</span></span> <span data-ttu-id="2ee87-133">예를 들어, 클릭 **편집**날짜 필드를 지우고, 클릭 **업데이트**는 동적 데이터 자동으로 수행이 필요한 필드 값이 데이터 모델에서 null을 허용 하기 때문에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-133">For example, click **Edit**, clear the date field, click **Update**, and you see that Dynamic Data automatically makes this a required field because the value is not nullable in the data model.</span></span> <span data-ttu-id="2ee87-134">필드에 오류 메시지가 후 별표를 표시 하는 페이지는 `ValidationSummary` 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-134">The page displays an asterisk after the field and an error message in the `ValidationSummary` control:</span></span>

<span data-ttu-id="2ee87-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="2ee87-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span></span>

<span data-ttu-id="2ee87-136">생략할 수 있습니다는 `ValidationSummary` 컨트롤, 오류 메시지를 보려면 별표 위에 마우스 포인터를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-136">You could omit the `ValidationSummary` control, because you can also hold the mouse pointer over the asterisk to see the error message:</span></span>

<span data-ttu-id="2ee87-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="2ee87-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span></span>

<span data-ttu-id="2ee87-138">동적 데이터는 입력 데이터 유효성 검사도 합니다 **Enrollment Date** 필드는 유효한 날짜:</span><span class="sxs-lookup"><span data-stu-id="2ee87-138">Dynamic Data will also validate that data entered in the **Enrollment Date** field is a valid date:</span></span>

<span data-ttu-id="2ee87-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="2ee87-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span></span>

<span data-ttu-id="2ee87-140">알 수 있듯이 일반 오류 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-140">As you can see, this is a generic error message.</span></span> <span data-ttu-id="2ee87-141">다음 섹션에서는 메시지와 유효성 검사 및 서식 지정 규칙을 사용자 지정 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-141">In the next section you'll see how to customize messages as well as validation and formatting rules.</span></span>

## <a name="adding-metadata-to-the-data-model"></a><span data-ttu-id="2ee87-142">데이터 모델에 대 한 메타 데이터 추가</span><span class="sxs-lookup"><span data-stu-id="2ee87-142">Adding Metadata to the Data Model</span></span>

<span data-ttu-id="2ee87-143">일반적으로 동적 데이터에서 제공한 기능을 사용자 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-143">Typically, you want to customize the functionality provided by Dynamic Data.</span></span> <span data-ttu-id="2ee87-144">예를 들어 데이터는 표시 하는 방법 및 오류 메시지의 콘텐츠를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-144">For example, you might change how data is displayed and the content of error messages.</span></span> <span data-ttu-id="2ee87-145">하면 일반적으로 데이터 유효성 검사 규칙을 사용자 지정 동적 데이터에서 제공 하는 것 보다 더 많은 기능을 제공 데이터 형식에 따라 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-145">You typically also customize data validation rules to provide more functionality than what Dynamic Data provides automatically based on data types.</span></span> <span data-ttu-id="2ee87-146">이 작업을 수행 하려면 엔터티 형식에 해당 하는 partial 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-146">To do this, you create partial classes that correspond to entity types.</span></span>

<span data-ttu-id="2ee87-147">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **ContosoUniversity** 프로젝트를 선택 **참조 추가**에 대 한 참조를 추가 하 고 `System.ComponentModel.DataAnnotations`입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-147">In **Solution Explorer**, right-click the **ContosoUniversity** project, select **Add Reference**, and add a reference to `System.ComponentModel.DataAnnotations`.</span></span>

<span data-ttu-id="2ee87-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="2ee87-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span></span>

<span data-ttu-id="2ee87-149">에 *DAL* 폴더에 새 클래스 파일을 만들고, 이름을 *Student.cs*에서 템플릿 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-149">In the *DAL* folder, create a new class file, name it *Student.cs*, and replace the template code in it with the following code.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

<span data-ttu-id="2ee87-150">이 코드에서는 partial 클래스는 `Student` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="2ee87-150">This code creates a partial class for the `Student` entity.</span></span> <span data-ttu-id="2ee87-151">`MetadataType` 이 partial 클래스에 적용 된 특성 메타 데이터를 지정 하는 데 사용 하는 클래스를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-151">The `MetadataType` attribute applied to this partial class identifies the class that you're using to specify metadata.</span></span> <span data-ttu-id="2ee87-152">메타 데이터 클래스 이름을 지정할 수 있지만 엔터티 이름과 "메타 데이터"를 사용 하는 경우가 잦다 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-152">The metadata class can have any name, but using the entity name plus "Metadata" is a common practice.</span></span>

<span data-ttu-id="2ee87-153">속성 메타 데이터 클래스에 적용 되는 특성 서식 지정, 유효성 검사, 규칙 및 오류 메시지를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-153">The attributes applied to properties in the metadata class specify formatting, validation, rules, and error messages.</span></span> <span data-ttu-id="2ee87-154">여기에 표시 된 특성에는 다음과 같은 결과가 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-154">The attributes shown here will have the following results:</span></span>

- <span data-ttu-id="2ee87-155">`EnrollmentDate` (시간)을 제외한 날짜가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-155">`EnrollmentDate` will display as a date (without a time).</span></span>
- <span data-ttu-id="2ee87-156">두 이름 필드에 25 자 여야 합니다. 또는 적게 길이 및 사용자 지정 오류 메시지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-156">Both name fields must be 25 characters or less in length, and a custom error message is provided.</span></span>
- <span data-ttu-id="2ee87-157">두 이름 필드는 필요 하 고 사용자 지정 오류 메시지를 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-157">Both name fields are required, and a custom error message is provided.</span></span>

<span data-ttu-id="2ee87-158">실행 합니다 *Students.aspx* 다시 페이지를 표시, 날짜 시간 없이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-158">Run the *Students.aspx* page again, and you see that the dates are now displayed without times:</span></span>

<span data-ttu-id="2ee87-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="2ee87-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span></span>

<span data-ttu-id="2ee87-160">행을 편집 하 고 이름 필드의 값을 선택 취소 해 보세요.</span><span class="sxs-lookup"><span data-stu-id="2ee87-160">Edit a row and try to clear the values in the name fields.</span></span> <span data-ttu-id="2ee87-161">필드 오류를 나타내는 별표 표시를 클릭 하기 전에 필드를 두면 즉시 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-161">The asterisks indicating field errors appear as soon as you leave a field, before you click **Update**.</span></span> <span data-ttu-id="2ee87-162">클릭 하면 **업데이트**, 지정한 오류 메시지 텍스트를 페이지에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-162">When you click **Update**, the page displays the error message text you specified.</span></span>

<span data-ttu-id="2ee87-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="2ee87-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span></span>

<span data-ttu-id="2ee87-164">25 자 보다 긴 이름을 입력, 클릭 **업데이트**, 페이지 지정한 오류 메시지 텍스트를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-164">Try to enter names that are longer than 25 characters, click **Update**, and the page displays the error message text you specified.</span></span>

<span data-ttu-id="2ee87-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="2ee87-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span></span>

<span data-ttu-id="2ee87-166">이제 데이터 모델 메타 데이터에서 이러한 서식 지정 및 유효성 검사 규칙을 설정한 규칙 적용 됨을 자동으로 표시 하거나 이러한 필드에 대 한 변경을 허용 하는 모든 페이지에서 사용 된다면 `DynamicControl` 또는 `DynamicField` 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-166">Now that you've set up these formatting and validation rules in the data model metadata, the rules will automatically be applied on every page that displays or allows changes to these fields, so long as you use `DynamicControl` or `DynamicField` controls.</span></span> <span data-ttu-id="2ee87-167">프로그래밍 및 테스트를 보다 쉽게 그러면를 작성 해야 하는 중복 코드의 양을 줄이고 데이터 서식 지정 및 유효성 검사는 응용 프로그램을 통해 일치 하는 것이 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-167">This reduces the amount of redundant code you have to write, which makes programming and testing easier, and it ensures that data formatting and validation are consistent throughout an application.</span></span>

## <a name="more-information"></a><span data-ttu-id="2ee87-168">추가 정보</span><span class="sxs-lookup"><span data-stu-id="2ee87-168">More Information</span></span>

<span data-ttu-id="2ee87-169">이 자습서 시리즈의 Entity Framework를 사용 하 여 시작을 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee87-169">This concludes this series of tutorials on Getting Started with the Entity Framework.</span></span> <span data-ttu-id="2ee87-170">Entity Framework를 사용 하는 방법을 배울 수 있도록 더 많은 리소스를 계속 진행 [다음 Entity Framework 자습서 시리즈의 첫 번째 자습서](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) 또는 다음 사이트를 방문 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2ee87-170">For more resources to help you learn how to use the Entity Framework, continue with [the first tutorial in the next Entity Framework tutorial series](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) or visit the following sites:</span></span>

- [<span data-ttu-id="2ee87-171">Entity Framework FAQ</span><span class="sxs-lookup"><span data-stu-id="2ee87-171">Entity Framework FAQ</span></span>](http://www.ef-faq.org/introduction.html)
- [<span data-ttu-id="2ee87-172">Entity Framework 팀 블로그</span><span class="sxs-lookup"><span data-stu-id="2ee87-172">The Entity Framework Team Blog</span></span>](https://blogs.msdn.com/b/adonet/)
- [<span data-ttu-id="2ee87-173">MSDN Library에서 entity Framework 사용</span><span class="sxs-lookup"><span data-stu-id="2ee87-173">Entity Framework in the MSDN Library</span></span>](https://msdn.microsoft.com/library/bb399572.aspx)
- [<span data-ttu-id="2ee87-174">MSDN 데이터 개발자 센터에서 entity Framework 사용</span><span class="sxs-lookup"><span data-stu-id="2ee87-174">Entity Framework in the MSDN Data Developer Center</span></span>](https://msdn.microsoft.com/data/ef.aspx)
- [<span data-ttu-id="2ee87-175">MSDN 라이브러리의 EntityDataSource 웹 서버 컨트롤 개요</span><span class="sxs-lookup"><span data-stu-id="2ee87-175">EntityDataSource Web Server Control Overview in the MSDN Library</span></span>](https://msdn.microsoft.com/library/cc488502.aspx)
- [<span data-ttu-id="2ee87-176">EntityDataSource 컨트롤 MSDN 라이브러리의 API 참조</span><span class="sxs-lookup"><span data-stu-id="2ee87-176">EntityDataSource control API reference in the MSDN Library</span></span>](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [<span data-ttu-id="2ee87-177">MSDN의 entity Framework 포럼</span><span class="sxs-lookup"><span data-stu-id="2ee87-177">Entity Framework Forums on MSDN</span></span>](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [<span data-ttu-id="2ee87-178">Julie Lerman의 블로그</span><span class="sxs-lookup"><span data-stu-id="2ee87-178">Julie Lerman's blog</span></span>](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> [<span data-ttu-id="2ee87-179">이전</span><span class="sxs-lookup"><span data-stu-id="2ee87-179">Previous</span></span>](the-entity-framework-and-aspnet-getting-started-part-7.md)
