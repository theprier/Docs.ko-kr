---
title: Razor 구성 요소 폼 및 유효성 검사
author: guardrex
description: Razor 구성 요소에서 폼 및 필드 유효성 검사 시나리오를 사용 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 04/08/2019
uid: razor-components/forms-validation
ms.openlocfilehash: a4ed75efc6b5a733ce4ff4e82f354a8e2fd48500
ms.sourcegitcommit: 948e533e02c2a7cb6175ada20b2c9cabb7786d0b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2019
ms.locfileid: "59515670"
---
# <a name="razor-components-forms-and-validation"></a><span data-ttu-id="9f4ba-103">Razor 구성 요소 폼 및 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="9f4ba-103">Razor Components forms and validation</span></span>

<span data-ttu-id="9f4ba-104">작성자: [Daniel Roth](https://github.com/danroth27) 및 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="9f4ba-104">By [Daniel Roth](https://github.com/danroth27) and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="9f4ba-105">폼 및 유효성 검사를 사용 하 여 Razor 구성 요소에서 지원 됩니다 [데이터 주석](xref:mvc/models/validation)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-105">Forms and validation are supported in Razor Components using [data annotations](xref:mvc/models/validation).</span></span>

> [!NOTE]
> <span data-ttu-id="9f4ba-106">폼 및 유효성 검사 시나리오에는 각 미리 보기 릴리스를 사용 하 여 변경할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-106">Forms and validation scenarios are likely to change with each preview release.</span></span>

<span data-ttu-id="9f4ba-107">다음 `ExampleModel` 형식 데이터 주석을 사용 하는 유효성 검사 논리를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-107">The following `ExampleModel` type defines validation logic using data annotations:</span></span>

```csharp
using System.ComponentModel.DataAnnotations;

public class ExampleModel
{
    [Required]
    [StringLength(10, ErrorMessage = "Name is too long.")]
    public string Name { get; set; }
}
```

<span data-ttu-id="9f4ba-108">폼을 사용 하 여 정의 되는 `<EditForm>` 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-108">A form is defined using the `<EditForm>` component.</span></span> <span data-ttu-id="9f4ba-109">다음 형식의 일반적인 요소, 구성 요소 및 Razor 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-109">The following form demonstrates typical elements, components, and Razor code:</span></span>

```csharp
<EditForm Model="@exampleModel" OnValidSubmit="@HandleValidSubmit">
    <DataAnnotationsValidator />
    <ValidationSummary />

    <InputText id="name" bind-Value="@exampleModel.Name" />

    <button type="submit">Submit</button>
</EditForm>

@functions {
    private ExampleModel exampleModel = new ExampleModel();

    private void HandleValidSubmit()
    {
        Console.WriteLine("OnValidSubmit");
    }
}
```

* <span data-ttu-id="9f4ba-110">폼에서 사용자 입력의 유효성을 검사 합니다 `name` 에 정의 된 유효성 검사를 사용 하 여 필드를 `ExampleModel` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-110">The form validates user input in the `name` field using the validation defined in the `ExampleModel` type.</span></span> <span data-ttu-id="9f4ba-111">구성 요소에서 모델을 만들 `@functions` 차단 및 private 필드에 저장 된 (`exampleModel`).</span><span class="sxs-lookup"><span data-stu-id="9f4ba-111">The model is created in the component's `@functions` block and held in a private field (`exampleModel`).</span></span> <span data-ttu-id="9f4ba-112">필드에 할당 된 합니다 `Model` 특성을 `<EditForm>`입니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-112">The field is assigned to the `Model` attribute of the `<EditForm>`.</span></span>
* <span data-ttu-id="9f4ba-113">데이터 주석 유효성 검사기 구성 요소 (`<DataAnnotationsValidator>`) 유효성 검사 지원 데이터 주석을 사용 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-113">The Data Annotations Validator component (`<DataAnnotationsValidator>`) attaches validation support using data annotations.</span></span>
* <span data-ttu-id="9f4ba-114">유효성 검사 요약 구성 요소 (`<ValidationSummary>`) 유효성 검사 메시지를 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-114">The Validation Summary component (`<ValidationSummary>`) summarizes validation messages.</span></span>
* `HandleValidSubmit` <span data-ttu-id="9f4ba-115">폼 (전달 유효성 검사)를 성공적으로 제출 하는 경우 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-115">is triggered when the form successfully submits (passes validation).</span></span>

<span data-ttu-id="9f4ba-116">기본 제공 입력된 구성 요소 집합을 수신 하 고 사용자 입력 유효성 검사에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-116">A set of built-in input components are available to receive and validate user input.</span></span> <span data-ttu-id="9f4ba-117">입력에는 변경 하는 시간과 양식이 제출 될 때 유효성이 검사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-117">Inputs are validated when they're changed and when a form is submitted.</span></span> <span data-ttu-id="9f4ba-118">사용 가능한 입력된 구성 요소는 다음 표에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-118">Available input components are shown in the following table.</span></span>

| <span data-ttu-id="9f4ba-119">입력된 구성 요소</span><span class="sxs-lookup"><span data-stu-id="9f4ba-119">Input component</span></span>   | <span data-ttu-id="9f4ba-120">로 렌더링&hellip;</span><span class="sxs-lookup"><span data-stu-id="9f4ba-120">Rendered as&hellip;</span></span>       |
| ----------------- | ------------------------- |
| `<InputText>`     | `<input>`                 |
| `<InputTextArea>` | `<textarea>`              |
| `<InputSelect>`   | `<select>`                |
| `<InputNumber>`   | `<input type="number">`   |
| `<InputCheckbox>` | `<input type="checkbox">` |
| `<InputDate>`     | `<input type="date">`     |

<span data-ttu-id="9f4ba-121">입력된 구성 요소 편집에 유효성 검사 및 해당 CSS 클래스 필드 상태를 반영 하도록 변경에 대 한 기본 동작을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-121">Input components provide default behavior for validating on edit and changing their CSS class to reflect the field state.</span></span> <span data-ttu-id="9f4ba-122">일부 구성 요소는 유용한 구문 분석 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-122">Some components include useful parsing logic.</span></span> <span data-ttu-id="9f4ba-123">예를 들어 `<InputDate>` 고 `<InputNumber>` 유효성 검사 오류로 등록 하 여 구문 분석할 수 없는 값을 정상적으로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-123">For example, `<InputDate>` and `<InputNumber>` handle unparseable values gracefully by registering them as validation errors.</span></span> <span data-ttu-id="9f4ba-124">지원 대상 필드의 null 허용 여부가 null 값을 허용할 수 있는 형식 (예를 들어 `int?`).</span><span class="sxs-lookup"><span data-stu-id="9f4ba-124">Types that can accept null values also support nullability of the target field (for example, `int?`).</span></span>

<span data-ttu-id="9f4ba-125">다음 `Starship` 형식은 속성 집합을 사용 하 여 유효성 검사 논리를 정의 하 고 [데이터 주석](xref:mvc/models/validation) 이전 보다 `ExampleModel`:</span><span class="sxs-lookup"><span data-stu-id="9f4ba-125">The following `Starship` type defines validation logic using a larger set of properties and [data annotations](xref:mvc/models/validation) than the earlier `ExampleModel`:</span></span>

```csharp
using System;
using System.ComponentModel.DataAnnotations;

public class Starship
{
    [Required]
    [StringLength(16, 
        ErrorMessage = "Identifier too long (16 character limit).")]
    public string Identifier { get; set; }

    // Optional (no data annotations)
    public string Description { get; set; }

    [Required]
    public string Classification { get; set; }

    [Range(1, 100000, ErrorMessage = "Accommodation invalid (1-100000).")]
    public int MaximumAccommodation { get; set; }

    [Required]
    [Range(typeof(bool), "true", "true", 
        ErrorMessage = "Form disallowed for unapproved ships.")]
    public bool IsValidatedDesign { get; set; }

    [Required]
    public DateTime ProductionDate { get; set; }
}
```

<span data-ttu-id="9f4ba-126">다음 형식에 정의 된 유효성 검사를 통한 사용자 입력의 유효성을 검사 합니다 `Starship` 모델:</span><span class="sxs-lookup"><span data-stu-id="9f4ba-126">The following form validates user input using the validation defined in the `Starship` model:</span></span>

```cshtml
@page "/FormsValidation"

<h1>Starfleet Starship Database</h1>

<h2>New Ship Entry Form</h2>

<EditForm Model="@starship" OnValidSubmit="@HandleValidSubmit">
    <DataAnnotationsValidator />
    <ValidationSummary />

    <p>
        <label for="identifier">Identifier: </label>
        <InputText id="identifier" bind-Value="@starship.Identifier" />
    </p>
    <p>
        <label for="description">Description (optional): </label>
        <InputTextArea Id="description" bind-Value="@starship.Description" />
    </p>
    <p>
        <label for="classification">Primary Classification: </label>
        <InputSelect id="classification" bind-Value="@starship.Classification">
            <option value"">Select classification ...</option>
            <option value="Defense">Defense</option>
            <option value="Exploration">Exploration</option>
            <option value="Diplomacy">Diplomacy</option>
        </InputSelect>
    </p>
    <p>
        <label for="accommodation">Maximum Accommodation: </label>
        <InputNumber id="accommodation" 
            bind-Value="@starship.MaximumAccommodation" />
    </p>
    <p>
        <label for="valid">Engineering Approval: </label>
        <InputCheckbox id="valid" bind-Value="@starship.IsValidatedDesign" />
    </p>
    <p>
        <label for="productionDate">Production Date: </label>
        <InputDate Id="productionDate" bind-Value="@starship.ProductionDate" />
    </p>

    <button type="submit">Submit</button>

    <p>
        <a href="http://www.startrek.com/">Star Trek</a>, 
        &copy;1966-2019 CBS Studios, Inc. and 
        <a href="http://www.paramount.com">Paramount Pictures</a>
    </p>
</EditForm>

@functions {
    private Starship starship = new Starship();

    private void HandleValidSubmit()
    {
        Console.WriteLine("OnValidSubmit");
    }
}
```

<span data-ttu-id="9f4ba-127">합니다 `<EditForm>` 만듭니다는 `EditContext` 으로 [연계 값](xref:razor-components/components#cascading-values-and-parameters) 수정 된 필드를 포함 하 여 편집 프로세스에 대 한 메타 데이터 및 현재 유효성 검사 메시지를 추적 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-127">The `<EditForm>` creates an `EditContext` as a [cascading value](xref:razor-components/components#cascading-values-and-parameters) that tracks metadata about the edit process, including what fields have been modified and the current validation messages.</span></span> <span data-ttu-id="9f4ba-128">합니다 `<EditForm>` 편리한 이벤트도 제공 유효 하 고 잘못 된 제출에 대 한 (`OnValidSubmit`, `OnInvalidSubmit`).</span><span class="sxs-lookup"><span data-stu-id="9f4ba-128">The `<EditForm>` also provides convenient events for valid and invalid submits (`OnValidSubmit`, `OnInvalidSubmit`).</span></span> <span data-ttu-id="9f4ba-129">또는 사용 하 여 `OnSubmit` 유효성 검사 트리거 및 사용자 지정 유효성 검사 코드를 사용 하 여 필드 값을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-129">Alternatively, use `OnSubmit` to trigger the validation and check field values with custom validation code.</span></span>

<span data-ttu-id="9f4ba-130">데이터 주석 유효성 검사기 구성 요소 (`<DataAnnotationsValidator>`)를 연계 데이터 주석을 사용 하 여 유효성 검사 지원을 연결 `EditContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-130">The Data Annotations Validator component (`<DataAnnotationsValidator>`) attaches validation support using data annotations to the cascaded `EditContext`.</span></span> <span data-ttu-id="9f4ba-131">현재 데이터 주석을 사용 하 여 유효성 검사에 대 한 지원을 사용 하도록 설정 하면이 명시적 제스처 하는데이 재정의할 수 있습니다 하는 기본 동작을 수행 하는 것이 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-131">Enabling support for validation using data annotations currently requires this explicit gesture, but we're considering making this the default behavior that you can then override.</span></span> <span data-ttu-id="9f4ba-132">데이터 주석 보다는 서로 다른 유효성 검사 시스템을 사용 하려면 데이터 주석 유효성 검사기는 사용자 지정 구현으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-132">To use a different validation system than data annotations, replace the Data Annotations Validator with a custom implementation.</span></span> <span data-ttu-id="9f4ba-133">ASP.NET Core 구현은 참조 소스에서 검사를 위해 사용할 수 있습니다. [DataAnnotationsValidator](https://github.com/aspnet/AspNetCore/blob/master/src/Components/Components/src/Forms/DataAnnotationsValidator.cs)/[AddDataAnnotationsValidation](https://github.com/aspnet/AspNetCore/blob/master/src/Components/Components/src/Forms/EditContextDataAnnotationsExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="9f4ba-133">The ASP.NET Core implementation is available for inspection in the reference source: [DataAnnotationsValidator](https://github.com/aspnet/AspNetCore/blob/master/src/Components/Components/src/Forms/DataAnnotationsValidator.cs)/[AddDataAnnotationsValidation](https://github.com/aspnet/AspNetCore/blob/master/src/Components/Components/src/Forms/EditContextDataAnnotationsExtensions.cs).</span></span> *<span data-ttu-id="9f4ba-134">ASP.NET Core 구현은 미리 보기 릴리스 기간 동안 빠른 업데이트 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-134">The ASP.NET Core implementation is subject to rapid updates during the preview release period.</span></span>*

<span data-ttu-id="9f4ba-135">유효성 검사 요약 구성 요소 (`<ValidationSummary>`)는 비슷하지만 모든 유효성 검사 메시지를 요약 합니다 [유효성 검사 요약 태그 도우미](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-135">The Validation Summary component (`<ValidationSummary>`) summarizes all validation messages, which is similar to the [Validation Summary Tag Helper](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper).</span></span>

<span data-ttu-id="9f4ba-136">유효성 검사 메시지 구성 요소 (`<ValidationMessage>`)는 비슷합니다는 특정 필드에 대 한 유효성 검사 메시지를 표시 합니다 [유효성 검사 메시지 태그 도우미](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)합니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-136">The Validation Message component (`<ValidationMessage>`) displays validation messages for a specific field, which is similar to the [Validation Message Tag Helper](xref:mvc/views/working-with-forms#the-validation-message-tag-helper).</span></span> <span data-ttu-id="9f4ba-137">유효성 검사에 필드를 지정 합니다 `For` 특성 및 모델 속성 이름을 지정 하는 람다 식:</span><span class="sxs-lookup"><span data-stu-id="9f4ba-137">Specify the field for validation with the `For` attribute and a lambda expression naming the model property:</span></span>

```cshtml
<ValidationMessage For="@(() => starship.MaximumAccommodation)" />
```

> [!NOTE]
> <span data-ttu-id="9f4ba-138">기본 제공 입력된 구성 요소에는 이후 릴리스를 해결 하는 것으로 예상 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-138">Built-in input components have limitations that we expect to resolve in future releases.</span></span> <span data-ttu-id="9f4ba-139">생성 된 임의의 특성을 지정할 수 없습니다는 예를 들어 `<input>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-139">For example, you can't specify arbitrary attributes on the generated `<input>` tags.</span></span> <span data-ttu-id="9f4ba-140">사용할 수 없는 시나리오를 처리 하도록 사용자 고유의 구성 요소 하위 클래스를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="9f4ba-140">Build your own component subclasses to handle unavailable scenarios.</span></span>
