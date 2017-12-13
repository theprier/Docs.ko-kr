---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: "업데이트, 삭제 및 모델 바인딩 및 web forms를 사용 하 여 데이터를 만들기 | Microsoft Docs"
author: tfitzmac
description: "이 자습서 시리즈 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다. 모델 바인딩 데이터 상호 작용 하 게 더 많은 직선-중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/27/2014
ms.topic: article
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 18c065b44524e7738c048b5908fa50c592188064
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a><span data-ttu-id="82be0-104">업데이트, 삭제 및 데이터 모델 바인딩 및 web forms를 사용 하 여 만들기</span><span class="sxs-lookup"><span data-stu-id="82be0-104">Updating, deleting, and creating data with model binding and web forms</span></span>
====================
<span data-ttu-id="82be0-105">으로 [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="82be0-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="82be0-106">이 자습서 시리즈 모델 바인딩을 사용 하 여 ASP.NET Web Forms 프로젝트의 기본 사항을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="82be0-107">모델 바인딩 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource) 처리 하는 보다 간단한 것 보다 데이터 상호 작용 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="82be0-108">이 시리즈 소개 자료로 시작 하 고 이후의 자습서의 보다 발전된 된 개념 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="82be0-109">이 자습서에서는 생성, 업데이트 및 데이터를 모델 바인딩을 삭제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-109">This tutorial shows how to create, update, and delete data with model binding.</span></span> <span data-ttu-id="82be0-110">다음 속성을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-110">You will set the following properties:</span></span>
> 
> - <span data-ttu-id="82be0-111">DeleteMethod</span><span class="sxs-lookup"><span data-stu-id="82be0-111">DeleteMethod</span></span>
> - <span data-ttu-id="82be0-112">InsertMethod</span><span class="sxs-lookup"><span data-stu-id="82be0-112">InsertMethod</span></span>
> - <span data-ttu-id="82be0-113">UpdateMethod</span><span class="sxs-lookup"><span data-stu-id="82be0-113">UpdateMethod</span></span>
> 
> <span data-ttu-id="82be0-114">이러한 속성에 해당 작업을 처리 하는 메서드의 이름을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-114">These properties receive the name of the method that handles the corresponding operation.</span></span> <span data-ttu-id="82be0-115">이 메서드 내에서 데이터와 상호 작용 하기 위한 논리를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-115">Within that method, you provide the logic for interacting with the data.</span></span>
> 
> <span data-ttu-id="82be0-116">첫 번째 범위에서 만든 프로젝트를 기반으로 한이 자습서 [부분](retrieving-data.md) 일련의 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-116">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="82be0-117">있습니다 수 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116) C# 또는 VB. 전체 프로젝트</span><span class="sxs-lookup"><span data-stu-id="82be0-117">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="82be0-118">다운로드 가능한 코드는 Visual Studio 2012 또는 Visual Studio 2013과 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-118">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="82be0-119">이 자습서에 표시 된 Visual Studio 2013 서식 파일 보다 약간 차이가 있는 Visual Studio 2012 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-119">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>


## <a name="what-youll-build"></a><span data-ttu-id="82be0-120">만들 것인지</span><span class="sxs-lookup"><span data-stu-id="82be0-120">What you'll build</span></span>

<span data-ttu-id="82be0-121">이 자습서에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-121">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="82be0-122">동적 데이터 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="82be0-122">Add dynamic data templates</span></span>
2. <span data-ttu-id="82be0-123">모델 바인딩 메서드를 통해 데이터 업데이트 및 삭제를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-123">Enable updating and deleting data through model binding methods</span></span>
3. <span data-ttu-id="82be0-124">데이터 유효성 검사 규칙을 적용-데이터베이스에서 새 레코드를 만드는 설정</span><span class="sxs-lookup"><span data-stu-id="82be0-124">Apply data validation rules - Enable creating a new record in the database</span></span>

## <a name="add-dynamic-data-templates"></a><span data-ttu-id="82be0-125">동적 데이터 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="82be0-125">Add dynamic data templates</span></span>

<span data-ttu-id="82be0-126">최상의 사용자 환경을 제공 하 고 코드 반복을 최소화, 동적 데이터 템플릿을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-126">To provide the best user experience and minimize code repetition, you will use dynamic data templates.</span></span> <span data-ttu-id="82be0-127">NuGet 패키지를 설치 하 여 기존 사이트에 동적 데이터를 미리 빌드된 템플릿을 쉽게 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-127">You can easily integrate pre-built dynamic data templates into your existing site by installing a NuGet package.</span></span>

<span data-ttu-id="82be0-128">**NuGet 패키지 관리**, 설치는 **DynamicDataTemplatesCS**합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-128">From the **Manage NuGet Packages**, install the **DynamicDataTemplatesCS**.</span></span>

![동적 데이터 템플릿](updating-deleting-and-creating-data/_static/image1.png)

<span data-ttu-id="82be0-130">프로젝트가 이제 라는 폴더를 포함 하는 알림 **DynamicData**합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-130">Notice that your project now includes a folder named **DynamicData**.</span></span> <span data-ttu-id="82be0-131">해당 폴더에 자동으로 web forms에서 동적 컨트롤에 적용 되는 템플릿이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-131">In that folder, you will find the templates that are automatically applied to dynamic controls in your web forms.</span></span>

![동적 데이터 폴더](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a><span data-ttu-id="82be0-133">Enable 업데이트 및 삭제</span><span class="sxs-lookup"><span data-stu-id="82be0-133">Enable updating and deleting</span></span>

<span data-ttu-id="82be0-134">사용자가을 업데이트 하 고 데이터베이스에서 레코드를 삭제 하는 것은 데이터를 검색 하기 위한 프로세스와 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-134">Enabling users to update and delete records in the database is very similar to the process for retrieving data.</span></span> <span data-ttu-id="82be0-135">에 **UpdateMethod** 및 **DeleteMethod** 속성, 이러한 작업을 수행 하는 방법의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-135">In the **UpdateMethod** and **DeleteMethod** properties, you specify the names of the methods that perform those operations.</span></span> <span data-ttu-id="82be0-136">GridView 컨트롤을 편집의 자동 생성을 지정 하 고 삭제 단추 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-136">With a GridView control, you can also specify the automatic generation of edit and delete buttons.</span></span> <span data-ttu-id="82be0-137">다음 강조 표시 된 코드는 GridView 코드에 대 한 추가 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-137">The following highlighted code shows the additions to the GridView code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

<span data-ttu-id="82be0-138">Using 추가 코드 숨김 파일에 대 한 문을 **System.Data.Entity.Infrastructure**합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-138">In the code-behind file, add a using statement for **System.Data.Entity.Infrastructure**.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

<span data-ttu-id="82be0-139">그런 다음, 다음 업데이트를 추가 하 고 메서드를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-139">Then, add the following update and delete methods.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

<span data-ttu-id="82be0-140">**TryUpdateModel** 메서드 web form에서 데이터 항목을 일치 하는 데이터 바인딩된 값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-140">The **TryUpdateModel** method applies the matching data-bound values from the web form to the data item.</span></span> <span data-ttu-id="82be0-141">데이터 항목의 id 매개 변수 값에 따라 검색 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-141">The data item is retrieved based on the value of the id parameter.</span></span>

## <a name="enforce-validation-requirements"></a><span data-ttu-id="82be0-142">유효성 검사 요구 사항을 적용합니다</span><span class="sxs-lookup"><span data-stu-id="82be0-142">Enforce validation requirements</span></span>

<span data-ttu-id="82be0-143">학생 클래스에서 FirstName, LastName 및 연도 속성에 적용 하는 유효성 검사 특성은 데이터를 업데이트할 때 자동으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-143">The validation attributes that you applied to the FirstName, LastName, and Year properties in the Student class are automatically enforced when updating the data.</span></span> <span data-ttu-id="82be0-144">DynamicField 컨트롤 유효성 검사 특성을 기반으로 하는 클라이언트 및 서버 유효성 검사기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-144">The DynamicField controls add client and server validators based on the validation attributes.</span></span> <span data-ttu-id="82be0-145">FirstName 및 LastName 속성은 모두 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-145">The FirstName and LastName properties are both required.</span></span> <span data-ttu-id="82be0-146">FirstName의 길이가 20 자를 초과할 수 없습니다 및 LastName 40 자를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-146">FirstName cannot exceed 20 characters in length, and LastName cannot exceed 40 characters.</span></span> <span data-ttu-id="82be0-147">연도는 AcademicYear 열거형에 대 한 유효한 값 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-147">Year must be a valid value for the AcademicYear enumeration.</span></span>

<span data-ttu-id="82be0-148">사용자 유효성 검사 요구 사항의 위반 하면 업데이트가 진행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-148">If the user violates one of the validation requirements, the update does not proceed.</span></span> <span data-ttu-id="82be0-149">오류 메시지를 보려면 GridView 위에 ValidationSummary 컨트롤을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-149">To see the error message, add a ValidationSummary control above the GridView.</span></span> <span data-ttu-id="82be0-150">모델 바인딩에서 유효성 검사 오류를 표시 하려면 설정는 **ShowModelStateErrors** 속성이로 설정 **true**합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-150">To display the validation errors from model binding, set the **ShowModelStateErrors** property set to **true**.</span></span> 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

<span data-ttu-id="82be0-151">웹 응용 프로그램을 실행 하 고 업데이트 하 고 레코드를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-151">Run the web application, and update and delete any of the records.</span></span>

![데이터 업데이트](updating-deleting-and-creating-data/_static/image3.png)

<span data-ttu-id="82be0-153">편집 모드에 Year 속성의 값은 자동으로으로 렌더링 되 면 드롭다운 목록에 유의 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-153">Notice that when in the edit mode the value for the Year property is automatically rendered as a drop down list.</span></span> <span data-ttu-id="82be0-154">연도 속성은 열거형 값을 하 고 열거형 값에 대 한 동적 데이터 서식 파일 드롭 다운 목록 편집을 위해를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-154">The Year property is an enumeration value, and the dynamic data template for an enumeration value specifies a drop down list for editing.</span></span> <span data-ttu-id="82be0-155">열어 해당 서식 파일을 찾을 수 있습니다는 **열거형\_Edit.ascx** 파일에 **DynamicData**/**FieldTemplates** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-155">You can find that template by opening the **Enumeration\_Edit.ascx** file in the **DynamicData**/**FieldTemplates** folder.</span></span>

<span data-ttu-id="82be0-156">유효한 값을 제공 하는 경우 업데이트가 성공적으로 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-156">If you provide valid values, the update completes successfully.</span></span> <span data-ttu-id="82be0-157">유효성 검사 요구 사항 중 하나를 위반할 경우 업데이트가 진행 되지 않습니다 및 표 형태 위에 있는 오류 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-157">If you violate one of the validation requirements, the update does not proceed and an error message is displayed above the grid.</span></span>

![오류 메시지](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a><span data-ttu-id="82be0-159">새 레코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-159">Add new records</span></span>

<span data-ttu-id="82be0-160">GridView 컨트롤에 포함 되지 않습니다는 **InsertMethod** 속성 모델 바인딩과 함께 새 레코드를 추가 하는 데 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-160">The GridView control does not include the **InsertMethod** property and therefore cannot be used for adding a new record with model binding.</span></span> <span data-ttu-id="82be0-161">InsertMethod 속성에서 찾을 수 있습니다는 **FormView**, **DetailsView**, 또는 **ListView** 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-161">You can find the InsertMethod property in the **FormView**, **DetailsView**, or **ListView** controls.</span></span> <span data-ttu-id="82be0-162">이 자습서에서는 새 레코드를 추가 하려면 FormView 컨트롤을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-162">In this tutorial, you will use a FormView control to add a new record.</span></span>

<span data-ttu-id="82be0-163">먼저 만들려는 새 레코드를 추가 하기 위한 새 페이지에 대 한 링크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-163">First, add a link to the new page you will create for adding a new record.</span></span> <span data-ttu-id="82be0-164">ValidationSummary, 위에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-164">Above the ValidationSummary, add:</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

<span data-ttu-id="82be0-165">새 링크 학생 페이지에 대 한 콘텐츠 위쪽에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-165">The new link will appear at the top of the content for the Students page.</span></span>

![새 링크](updating-deleting-and-creating-data/_static/image5.png)

<span data-ttu-id="82be0-167">그런 다음 마스터 페이지를 사용 하 여 새 web form을 추가 하 고 이름을 **AddStudent**합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-167">Then, add a new web form using a master page, and name it **AddStudent**.</span></span> <span data-ttu-id="82be0-168">Site.Master 마스터 페이지로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-168">Select Site.Master as the master page.</span></span>

<span data-ttu-id="82be0-169">사용 하 여 새 학생을 추가 하기 위한 필드를 렌더링 합니다는 **DynamicEntity** 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-169">You will render the fields for adding a new student by using a **DynamicEntity** control.</span></span> <span data-ttu-id="82be0-170">DynamicEntity 컨트롤 ItemType 속성에 지정 된 클래스에는 편집 가능한 속성을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-170">The DynamicEntity control renders that editable properties in the class specified in the ItemType property.</span></span> <span data-ttu-id="82be0-171">StudentID 속성으로 표시 되어 있으므로 **[ScaffoldColumn(false)]** 특성은 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-171">The StudentID property was marked with the **[ScaffoldColumn(false)]** attribute so it is not rendered.</span></span> <span data-ttu-id="82be0-172">AddStudent 페이지의 MainContent 자리 표시자에 다음 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-172">In the MainContent placeholder of the AddStudent page, add the following code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

<span data-ttu-id="82be0-173">코드 숨김 파일 (AddStudent.aspx.cs)에 추가 **를 사용 하 여** 문을 **ContosoUniversityModelBinding.Models** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-173">In the code-behind file (AddStudent.aspx.cs), add a **using** statement for the **ContosoUniversityModelBinding.Models** namespace.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

<span data-ttu-id="82be0-174">그런 다음 새 레코드 및 취소 단추에 대 한 이벤트 처리기를 삽입 하는 방법을 지정 하려면 다음 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-174">Then, add the following methods to specify how to insert a new record and an event handler for the cancel button.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

<span data-ttu-id="82be0-175">모든 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-175">Save all of the changes.</span></span>

<span data-ttu-id="82be0-176">웹 응용 프로그램을 실행 하 고 새 학생을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-176">Run the web application and create a new student.</span></span>

![새 학생 추가](updating-deleting-and-creating-data/_static/image6.png)

<span data-ttu-id="82be0-178">클릭 **삽입** 새 학생 만들어진 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-178">Click **Insert** and notice the new student has been created.</span></span>

![새 학생을 표시 합니다.](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a><span data-ttu-id="82be0-180">결론</span><span class="sxs-lookup"><span data-stu-id="82be0-180">Conclusion</span></span>

<span data-ttu-id="82be0-181">이 자습서에서는 업데이트, 삭제 및 데이터를 만드는 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-181">In this tutorial, you enabled updating, deleting, and creating data.</span></span> <span data-ttu-id="82be0-182">하면 확인 데이터와 상호 작용할 때 유효성 검사 규칙이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-182">You ensured validation rules are applied when interacting with the data.</span></span>

<span data-ttu-id="82be0-183">다음에서 [자습서](sorting-paging-and-filtering-data.md) 이 시리즈의 정렬, 페이징, 및 데이터를 필터링를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82be0-183">In the next [tutorial](sorting-paging-and-filtering-data.md) in this series, you will enable sorting, paging, and filtering data.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="82be0-184">[이전](retrieving-data.md)
[다음](sorting-paging-and-filtering-data.md)</span><span class="sxs-lookup"><span data-stu-id="82be0-184">[Previous](retrieving-data.md)
[Next](sorting-paging-and-filtering-data.md)</span></span>
