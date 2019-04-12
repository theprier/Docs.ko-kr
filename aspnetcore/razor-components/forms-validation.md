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
# <a name="razor-components-forms-and-validation"></a>Razor 구성 요소 폼 및 유효성 검사

작성자: [Daniel Roth](https://github.com/danroth27) 및 [Luke Latham](https://github.com/guardrex)

폼 및 유효성 검사를 사용 하 여 Razor 구성 요소에서 지원 됩니다 [데이터 주석](xref:mvc/models/validation)합니다.

> [!NOTE]
> 폼 및 유효성 검사 시나리오에는 각 미리 보기 릴리스를 사용 하 여 변경할 가능성이 높습니다.

다음 `ExampleModel` 형식 데이터 주석을 사용 하는 유효성 검사 논리를 정의 합니다.

```csharp
using System.ComponentModel.DataAnnotations;

public class ExampleModel
{
    [Required]
    [StringLength(10, ErrorMessage = "Name is too long.")]
    public string Name { get; set; }
}
```

폼을 사용 하 여 정의 되는 `<EditForm>` 구성 요소입니다. 다음 형식의 일반적인 요소, 구성 요소 및 Razor 코드를 보여 줍니다.

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

* 폼에서 사용자 입력의 유효성을 검사 합니다 `name` 에 정의 된 유효성 검사를 사용 하 여 필드를 `ExampleModel` 형식입니다. 구성 요소에서 모델을 만들 `@functions` 차단 및 private 필드에 저장 된 (`exampleModel`). 필드에 할당 된 합니다 `Model` 특성을 `<EditForm>`입니다.
* 데이터 주석 유효성 검사기 구성 요소 (`<DataAnnotationsValidator>`) 유효성 검사 지원 데이터 주석을 사용 하 여 연결 합니다.
* 유효성 검사 요약 구성 요소 (`<ValidationSummary>`) 유효성 검사 메시지를 요약 합니다.
* `HandleValidSubmit` 폼 (전달 유효성 검사)를 성공적으로 제출 하는 경우 트리거됩니다.

기본 제공 입력된 구성 요소 집합을 수신 하 고 사용자 입력 유효성 검사에 사용할 수 있습니다. 입력에는 변경 하는 시간과 양식이 제출 될 때 유효성이 검사 됩니다. 사용 가능한 입력된 구성 요소는 다음 표에 표시 됩니다.

| 입력된 구성 요소   | 로 렌더링&hellip;       |
| ----------------- | ------------------------- |
| `<InputText>`     | `<input>`                 |
| `<InputTextArea>` | `<textarea>`              |
| `<InputSelect>`   | `<select>`                |
| `<InputNumber>`   | `<input type="number">`   |
| `<InputCheckbox>` | `<input type="checkbox">` |
| `<InputDate>`     | `<input type="date">`     |

입력된 구성 요소 편집에 유효성 검사 및 해당 CSS 클래스 필드 상태를 반영 하도록 변경에 대 한 기본 동작을 제공 합니다. 일부 구성 요소는 유용한 구문 분석 논리를 포함 합니다. 예를 들어 `<InputDate>` 고 `<InputNumber>` 유효성 검사 오류로 등록 하 여 구문 분석할 수 없는 값을 정상적으로 처리 합니다. 지원 대상 필드의 null 허용 여부가 null 값을 허용할 수 있는 형식 (예를 들어 `int?`).

다음 `Starship` 형식은 속성 집합을 사용 하 여 유효성 검사 논리를 정의 하 고 [데이터 주석](xref:mvc/models/validation) 이전 보다 `ExampleModel`:

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

다음 형식에 정의 된 유효성 검사를 통한 사용자 입력의 유효성을 검사 합니다 `Starship` 모델:

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

합니다 `<EditForm>` 만듭니다는 `EditContext` 으로 [연계 값](xref:razor-components/components#cascading-values-and-parameters) 수정 된 필드를 포함 하 여 편집 프로세스에 대 한 메타 데이터 및 현재 유효성 검사 메시지를 추적 하는 합니다. 합니다 `<EditForm>` 편리한 이벤트도 제공 유효 하 고 잘못 된 제출에 대 한 (`OnValidSubmit`, `OnInvalidSubmit`). 또는 사용 하 여 `OnSubmit` 유효성 검사 트리거 및 사용자 지정 유효성 검사 코드를 사용 하 여 필드 값을 확인 합니다.

데이터 주석 유효성 검사기 구성 요소 (`<DataAnnotationsValidator>`)를 연계 데이터 주석을 사용 하 여 유효성 검사 지원을 연결 `EditContext`합니다. 현재 데이터 주석을 사용 하 여 유효성 검사에 대 한 지원을 사용 하도록 설정 하면이 명시적 제스처 하는데이 재정의할 수 있습니다 하는 기본 동작을 수행 하는 것이 예정입니다. 데이터 주석 보다는 서로 다른 유효성 검사 시스템을 사용 하려면 데이터 주석 유효성 검사기는 사용자 지정 구현으로 대체 합니다. ASP.NET Core 구현은 참조 소스에서 검사를 위해 사용할 수 있습니다. [DataAnnotationsValidator](https://github.com/aspnet/AspNetCore/blob/master/src/Components/Components/src/Forms/DataAnnotationsValidator.cs)/[AddDataAnnotationsValidation](https://github.com/aspnet/AspNetCore/blob/master/src/Components/Components/src/Forms/EditContextDataAnnotationsExtensions.cs). *ASP.NET Core 구현은 미리 보기 릴리스 기간 동안 빠른 업데이트 될 수 있습니다.*

유효성 검사 요약 구성 요소 (`<ValidationSummary>`)는 비슷하지만 모든 유효성 검사 메시지를 요약 합니다 [유효성 검사 요약 태그 도우미](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)합니다.

유효성 검사 메시지 구성 요소 (`<ValidationMessage>`)는 비슷합니다는 특정 필드에 대 한 유효성 검사 메시지를 표시 합니다 [유효성 검사 메시지 태그 도우미](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)합니다. 유효성 검사에 필드를 지정 합니다 `For` 특성 및 모델 속성 이름을 지정 하는 람다 식:

```cshtml
<ValidationMessage For="@(() => starship.MaximumAccommodation)" />
```

> [!NOTE]
> 기본 제공 입력된 구성 요소에는 이후 릴리스를 해결 하는 것으로 예상 제한 사항이 있습니다. 생성 된 임의의 특성을 지정할 수 없습니다는 예를 들어 `<input>` 태그입니다. 사용할 수 없는 시나리오를 처리 하도록 사용자 고유의 구성 요소 하위 클래스를 빌드하십시오.
