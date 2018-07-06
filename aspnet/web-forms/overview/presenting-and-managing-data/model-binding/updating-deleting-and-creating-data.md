---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: 업데이트, 삭제 및 데이터 모델 바인딩 및 web forms를 사용 하 여 만들기 | Microsoft Docs
author: tfitzmac
description: 이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩을 통해 데이터 상호 작용 자세한 직선-...
ms.author: aspnetcontent
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 1cf9873db177b67927b579def1eedd08e3e9a762
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37821634"
---
<a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a><span data-ttu-id="44623-104">업데이트, 삭제 및 데이터 모델 바인딩 및 web forms를 사용 하 여 만들기</span><span class="sxs-lookup"><span data-stu-id="44623-104">Updating, deleting, and creating data with model binding and web forms</span></span>
====================
<span data-ttu-id="44623-105">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="44623-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="44623-106">이 자습서 시리즈에서는 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="44623-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="44623-107">모델 바인딩 보다 직관적인 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 데이터 상호 작용 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="44623-108">이 시리즈 소개 자료를 사용 하 여 시작 하 고 나중에 자습서에서 고급 개념을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="44623-109">이 자습서에는 만들기, 업데이트 및 모델 바인딩을 사용 하 여 데이터를 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="44623-109">This tutorial shows how to create, update, and delete data with model binding.</span></span> <span data-ttu-id="44623-110">다음 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-110">You will set the following properties:</span></span>
> 
> - <span data-ttu-id="44623-111">DeleteMethod</span><span class="sxs-lookup"><span data-stu-id="44623-111">DeleteMethod</span></span>
> - <span data-ttu-id="44623-112">InsertMethod</span><span class="sxs-lookup"><span data-stu-id="44623-112">InsertMethod</span></span>
> - <span data-ttu-id="44623-113">UpdateMethod</span><span class="sxs-lookup"><span data-stu-id="44623-113">UpdateMethod</span></span>
> 
> <span data-ttu-id="44623-114">이러한 속성에서 해당 작업을 처리 하는 메서드의 이름을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-114">These properties receive the name of the method that handles the corresponding operation.</span></span> <span data-ttu-id="44623-115">이 메서드 내에서 데이터 상호 작용 하기 위한 논리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-115">Within that method, you provide the logic for interacting with the data.</span></span>
> 
> <span data-ttu-id="44623-116">첫 번째 범위에서 만든 프로젝트를 기반으로 한이 자습서 [파트](retrieving-data.md) 계열의 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-116">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="44623-117">할 수 있습니다 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) C# 또는 VB. 전체 프로젝트</span><span class="sxs-lookup"><span data-stu-id="44623-117">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="44623-118">다운로드 가능한 코드를 Visual Studio 2012 또는 Visual Studio 2013을 사용 하 여 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-118">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="44623-119">이 자습서에 표시 된 Visual Studio 2013 서식 파일 보다 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-119">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="44623-120">만들 내용</span><span class="sxs-lookup"><span data-stu-id="44623-120">What you'll build</span></span>

<span data-ttu-id="44623-121">이 자습서에서는 다음을 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-121">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="44623-122">동적 데이터 템플릿을 추가합니다</span><span class="sxs-lookup"><span data-stu-id="44623-122">Add dynamic data templates</span></span>
2. <span data-ttu-id="44623-123">모델 바인딩 메서드를 통해 데이터 업데이트 및 삭제를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="44623-123">Enable updating and deleting data through model binding methods</span></span>
3. <span data-ttu-id="44623-124">데이터 유효성 검사 규칙을 적용-데이터베이스에 새 레코드를 만드는 사용</span><span class="sxs-lookup"><span data-stu-id="44623-124">Apply data validation rules - Enable creating a new record in the database</span></span>

## <a name="add-dynamic-data-templates"></a><span data-ttu-id="44623-125">동적 데이터 템플릿을 추가합니다</span><span class="sxs-lookup"><span data-stu-id="44623-125">Add dynamic data templates</span></span>

<span data-ttu-id="44623-126">최상의 사용자 환경을 제공 하 고 코드 반복을 최소화 하려면 동적 데이터 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-126">To provide the best user experience and minimize code repetition, you will use dynamic data templates.</span></span> <span data-ttu-id="44623-127">NuGet 패키지를 설치 하 여 기존 사이트를 미리 작성된 된 동적 데이터 템플릿을 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44623-127">You can easily integrate pre-built dynamic data templates into your existing site by installing a NuGet package.</span></span>

<span data-ttu-id="44623-128">**NuGet 패키지 관리**를 설치 합니다 **DynamicDataTemplatesCS**합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-128">From the **Manage NuGet Packages**, install the **DynamicDataTemplatesCS**.</span></span>

![동적 데이터 템플릿](updating-deleting-and-creating-data/_static/image1.png)

<span data-ttu-id="44623-130">프로젝트에 이제 라는 폴더에 통지 **DynamicData**합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-130">Notice that your project now includes a folder named **DynamicData**.</span></span> <span data-ttu-id="44623-131">해당 폴더에 있는 웹 폼에서 동적 컨트롤에 자동으로 적용 되는 템플릿을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44623-131">In that folder, you will find the templates that are automatically applied to dynamic controls in your web forms.</span></span>

![동적 데이터 폴더](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a><span data-ttu-id="44623-133">설정 업데이트 및 삭제</span><span class="sxs-lookup"><span data-stu-id="44623-133">Enable updating and deleting</span></span>

<span data-ttu-id="44623-134">사용자 데이터베이스에서 레코드를 업데이트 및 삭제를 사용 하는 것은 데이터를 검색 하기 위한 프로세스와 매우 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-134">Enabling users to update and delete records in the database is very similar to the process for retrieving data.</span></span> <span data-ttu-id="44623-135">에 **UpdateMethod** 하 고 **DeleteMethod** 속성을 해당 작업을 수행 하는 메서드의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-135">In the **UpdateMethod** and **DeleteMethod** properties, you specify the names of the methods that perform those operations.</span></span> <span data-ttu-id="44623-136">GridView 컨트롤을 사용 하 여 편집의 자동 생성을 지정 하 고 단추를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-136">With a GridView control, you can also specify the automatic generation of edit and delete buttons.</span></span> <span data-ttu-id="44623-137">다음 강조 표시 된 코드를 GridView 코드의 추가 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="44623-137">The following highlighted code shows the additions to the GridView code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

<span data-ttu-id="44623-138">코드 숨김 파일에 추가 하 여 문을 **System.Data.Entity.Infrastructure**합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-138">In the code-behind file, add a using statement for **System.Data.Entity.Infrastructure**.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

<span data-ttu-id="44623-139">그런 다음 다음 업데이트를 추가 하 고 메서드를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-139">Then, add the following update and delete methods.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

<span data-ttu-id="44623-140">합니다 **tryupdatemodel에 전달** 메서드 웹 폼에서 데이터 항목에 일치 하는 데이터 바인딩된 값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-140">The **TryUpdateModel** method applies the matching data-bound values from the web form to the data item.</span></span> <span data-ttu-id="44623-141">데이터 항목의 id 매개 변수 값에 따라 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44623-141">The data item is retrieved based on the value of the id parameter.</span></span>

## <a name="enforce-validation-requirements"></a><span data-ttu-id="44623-142">유효성 검사 요구 사항을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-142">Enforce validation requirements</span></span>

<span data-ttu-id="44623-143">FirstName, LastName 및 Year 속성 Student 클래스에 적용 하는 유효성 검사 특성은 데이터를 업데이트할 때 자동으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44623-143">The validation attributes that you applied to the FirstName, LastName, and Year properties in the Student class are automatically enforced when updating the data.</span></span> <span data-ttu-id="44623-144">DynamicField 컨트롤 유효성 검사 특성을 기반으로 하는 클라이언트 및 서버 유효성 검사기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-144">The DynamicField controls add client and server validators based on the validation attributes.</span></span> <span data-ttu-id="44623-145">FirstName 및 LastName 속성은 모두 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-145">The FirstName and LastName properties are both required.</span></span> <span data-ttu-id="44623-146">FirstName 길이가 20 자를 초과할 수 없습니다 및 LastName 40 자를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="44623-146">FirstName cannot exceed 20 characters in length, and LastName cannot exceed 40 characters.</span></span> <span data-ttu-id="44623-147">연도는 AcademicYear 열거형에 대 한 유효한 값 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-147">Year must be a valid value for the AcademicYear enumeration.</span></span>

<span data-ttu-id="44623-148">사용자 유효성 검사 요구 사항의 위반 하면 업데이트가 진행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="44623-148">If the user violates one of the validation requirements, the update does not proceed.</span></span> <span data-ttu-id="44623-149">오류 메시지를 보려면 위에서 GridView ValidationSummary 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-149">To see the error message, add a ValidationSummary control above the GridView.</span></span> <span data-ttu-id="44623-150">모델 바인딩에서 유효성 검사 오류를 표시 하려면 설정 합니다 **ShowModelStateErrors** 속성으로 설정 **true**합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-150">To display the validation errors from model binding, set the **ShowModelStateErrors** property set to **true**.</span></span> 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

<span data-ttu-id="44623-151">웹 응용 프로그램을 실행 하 고 업데이트 하 고 레코드를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-151">Run the web application, and update and delete any of the records.</span></span>

![업데이트 데이터](updating-deleting-and-creating-data/_static/image3.png)

<span data-ttu-id="44623-153">편집 모드에서 Year 속성에 대 한 값을 자동으로 렌더링할 때 드롭다운 목록으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-153">Notice that when in the edit mode the value for the Year property is automatically rendered as a drop down list.</span></span> <span data-ttu-id="44623-154">Year 속성은 열거 값을 하 고 열거형 값에 대 한 동적 데이터 템플릿을 편집할 수 있도록 목록 드롭다운을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-154">The Year property is an enumeration value, and the dynamic data template for an enumeration value specifies a drop down list for editing.</span></span> <span data-ttu-id="44623-155">열어 해당 템플릿을 찾을 수 있습니다는 **열거형\_Edit.ascx** 파일을 **DynamicData**/**FieldTemplates** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="44623-155">You can find that template by opening the **Enumeration\_Edit.ascx** file in the **DynamicData**/**FieldTemplates** folder.</span></span>

<span data-ttu-id="44623-156">유효한 값을 제공 하는 경우 업데이트를 성공적으로 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-156">If you provide valid values, the update completes successfully.</span></span> <span data-ttu-id="44623-157">유효성 검사 요구 사항 중 하나를 위반 하면 업데이트가 진행 되지 않습니다 하 고 오류 메시지를 표 형태 위에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44623-157">If you violate one of the validation requirements, the update does not proceed and an error message is displayed above the grid.</span></span>

![오류 메시지](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a><span data-ttu-id="44623-159">새 레코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-159">Add new records</span></span>

<span data-ttu-id="44623-160">GridView 컨트롤을 다루지 않습니다 합니다 **InsertMethod** 속성 모델 바인딩을 사용 하 여 새 레코드를 추가 하는 것에 대 한 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="44623-160">The GridView control does not include the **InsertMethod** property and therefore cannot be used for adding a new record with model binding.</span></span> <span data-ttu-id="44623-161">InsertMethod 속성을 찾을 수 있습니다 합니다 **FormView**를 **DetailsView**, 또는 **ListView** 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="44623-161">You can find the InsertMethod property in the **FormView**, **DetailsView**, or **ListView** controls.</span></span> <span data-ttu-id="44623-162">이 자습서에서는 새 레코드를 추가 하려면 FormView 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-162">In this tutorial, you will use a FormView control to add a new record.</span></span>

<span data-ttu-id="44623-163">첫째, 만든 새 레코드를 추가 하는 것에 대 한 새 페이지에 링크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-163">First, add a link to the new page you will create for adding a new record.</span></span> <span data-ttu-id="44623-164">ValidationSummary, 위에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-164">Above the ValidationSummary, add:</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

<span data-ttu-id="44623-165">학생 페이지에 대 한 콘텐츠의 맨 위에 있는 새 링크 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44623-165">The new link will appear at the top of the content for the Students page.</span></span>

![새 링크](updating-deleting-and-creating-data/_static/image5.png)

<span data-ttu-id="44623-167">그런 다음 마스터 페이지를 사용 하 여 새 web form을 추가 하 고 이름을 **AddStudent**합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-167">Then, add a new web form using a master page, and name it **AddStudent**.</span></span> <span data-ttu-id="44623-168">마스터 페이지와 Site.Master를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-168">Select Site.Master as the master page.</span></span>

<span data-ttu-id="44623-169">사용 하 여 새 학생을 추가 하기 위한 필드를 렌더링 합니다는 **DynamicEntity** 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-169">You will render the fields for adding a new student by using a **DynamicEntity** control.</span></span> <span data-ttu-id="44623-170">DynamicEntity 컨트롤 ItemType 속성에 지정 된 클래스에는 편집 가능한 속성을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-170">The DynamicEntity control renders that editable properties in the class specified in the ItemType property.</span></span> <span data-ttu-id="44623-171">StudentID 속성으로 표시 되어 있으므로 합니다 **[ScaffoldColumn(false)]** 특성 사용 하므로 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="44623-171">The StudentID property was marked with the **[ScaffoldColumn(false)]** attribute so it is not rendered.</span></span> <span data-ttu-id="44623-172">AddStudent 페이지의 MainContent 자리 표시자를 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-172">In the MainContent placeholder of the AddStudent page, add the following code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

<span data-ttu-id="44623-173">코드 숨김 파일 (AddStudent.aspx.cs)에서 추가 **를 사용 하 여** 문을 합니다 **ContosoUniversityModelBinding.Models** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="44623-173">In the code-behind file (AddStudent.aspx.cs), add a **using** statement for the **ContosoUniversityModelBinding.Models** namespace.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

<span data-ttu-id="44623-174">새 레코드 및 취소 단추에 대 한 이벤트 처리기를 삽입 하는 방법을 지정 하려면 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-174">Then, add the following methods to specify how to insert a new record and an event handler for the cancel button.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

<span data-ttu-id="44623-175">모든 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-175">Save all of the changes.</span></span>

<span data-ttu-id="44623-176">웹 응용 프로그램을 실행 하 고 새 학생을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44623-176">Run the web application and create a new student.</span></span>

![새 학생을 추가 합니다.](updating-deleting-and-creating-data/_static/image6.png)

<span data-ttu-id="44623-178">클릭 **삽입** 새 학생을 만들었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-178">Click **Insert** and notice the new student has been created.</span></span>

![새 학생을 표시 합니다.](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a><span data-ttu-id="44623-180">결론</span><span class="sxs-lookup"><span data-stu-id="44623-180">Conclusion</span></span>

<span data-ttu-id="44623-181">이 자습서에서는 업데이트, 삭제 및 만드는 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-181">In this tutorial, you enabled updating, deleting, and creating data.</span></span> <span data-ttu-id="44623-182">하면 확인 데이터와 상호 작용할 때 유효성 검사 규칙이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44623-182">You ensured validation rules are applied when interacting with the data.</span></span>

<span data-ttu-id="44623-183">다음에 [자습서](sorting-paging-and-filtering-data.md) 이 시리즈에서는 정렬, 페이징 및 필터링 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44623-183">In the next [tutorial](sorting-paging-and-filtering-data.md) in this series, you will enable sorting, paging, and filtering data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="44623-184">[이전](retrieving-data.md)
> [다음](sorting-paging-and-filtering-data.md)</span><span class="sxs-lookup"><span data-stu-id="44623-184">[Previous](retrieving-data.md)
[Next](sorting-paging-and-filtering-data.md)</span></span>
