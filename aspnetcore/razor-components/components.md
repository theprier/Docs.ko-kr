---
title: 만들기 및 Razor 구성 요소를 사용 합니다.
author: guardrex
description: 만들기 및 데이터 바인딩, 이벤트를 처리 및 구성 요소 수명 주기를 관리 하는 방법을 비롯 하 여 Razor 구성 요소를 사용 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 04/08/2019
uid: razor-components/components
ms.openlocfilehash: f8ac7f3844b94a162e8d1c45f80ae153d89536ee
ms.sourcegitcommit: 948e533e02c2a7cb6175ada20b2c9cabb7786d0b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2019
ms.locfileid: "59515695"
---
# <a name="create-and-use-razor-components"></a>만들기 및 Razor 구성 요소를 사용 합니다.

하 여 [Luke Latham](https://github.com/guardrex)하십시오 [Daniel Roth](https://github.com/danroth27), 및 [Morné Zaayman](https://github.com/MorneZaayman)

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([다운로드 방법](xref:index#how-to-download-a-sample)) 필수 구성 요소는 [시작](xref:razor-components/get-started) 항목을 참조하세요.

Razor 구성 요소 앱을 사용 하 여 빌드됩니다 *구성 요소*합니다. 구성 요소는 UI (사용자 인터페이스), 페이지, 대화 상자, 폼 등의 자체 포함 된 청크입니다. 구성 요소는 HTML 태그 및 데이터를 삽입 하거나 UI 이벤트에 응답 하는 데 필요한 처리 논리를 포함 합니다. 구성 요소는 유연 하 고 간단 합니다. 중첩 된, 다시 사용 하 고 수 프로젝트 간에 공유 합니다.

## <a name="component-classes"></a>구성 요소 클래스

구성 요소는 일반적으로 구성 요소 Razor 파일에서 구현 됩니다 (*.razor*)를 조합 하 여 C# 와 HTML 태그 (*.cshtml* Blazor 앱에서는 파일을 사용).

구성 요소를 사용 하 여 Razor 구성 요소 앱에 작성 될 수 있습니다 합니다 *.cshtml* 파일 확장명으로 파일을 사용 하 여 구성 요소 Razor 파일으로 식별 됩니다는 `_RazorComponentInclude` MSBuild 속성입니다. 예를 들어, Razor 구성 요소 템플릿을 사용 하 여 만든 앱을 지정 하는 모든 *.cshtml* 아래에서 파일을 *구성 요소* Razor 구성 요소 파일과 폴더를 처리할지:

```xml
<_RazorComponentInclude>Components\**\*.cshtml</_RazorComponentInclude>
```

구성 요소에 대 한 UI는 HTML을 사용 하 여 정의 됩니다. 동적 렌더링 논리(예: 루프, 조건, 식)는 [Razor](xref:mvc/views/razor)라는 포함된 C# 구문을 사용하여 추가됩니다. 구성 요소 Razor 앱을 컴파일할 때, HTML 태그 및 C# 렌더링 논리 구성 요소 클래스 변환 됩니다. 파일의 이름과 일치 하는 생성된 된 클래스의 이름입니다.

에 정의 된 구성 요소 클래스의 멤버는 `@functions` 블록 (둘 이상의 `@functions` 블록은 허용). 에 `@functions` 이벤트 처리를 위해 또는 다른 구성 요소 논리를 정의 하기 위한 메서드를 사용 하 여 지정 된 블록에 구성 요소 상태 (속성, 필드).

구성 요소 멤버 논리를 사용 하 여 구성 요소의 파트의 렌더링 처럼 사용할 수 있습니다 C# 로 시작 하는 식을 `@`합니다. 예를 들어는 C# 접두사로 사용 하 여 필드가 렌더링 되는지 `@` 필드 이름입니다. 다음 예제에서는 평가 하 고 렌더링 합니다.

* `_headingFontStyle` CSS 속성 값으로 `font-style`입니다.
* `_headingText` 내용에는 `<h1>` 요소입니다.

```cshtml
<h1 style="font-style:@_headingFontStyle">@_headingText</h1>

@functions {
    private string _headingFontStyle = "italic";
    private string _headingText = "Put on your new Blazor!";
}
```

처음에 구성 요소를 렌더링 한 후 이벤트에 대 한 응답에 렌더링 트리에서 해당 구성 요소에 다시 생성 합니다. 다음 razor 구성 요소는 이전에 대 한 새로운 렌더링 트리를 비교 하 고 브라우저의 문서 개체 모델 (DOM)에 대 한 수정은 적용 됩니다.

## <a name="integrate-components-into-razor-pages-and-mvc-apps"></a>구성 요소 Razor 페이지 및 MVC 앱에 통합

기존 Razor 페이지 및 MVC 앱과 구성 요소를 사용 합니다. 기존 페이지 또는 Razor 구성 요소를 사용 하는 뷰를 다시 작성할 필요가 없는 경우 페이지 또는 보기를 렌더링할 때 구성 요소는 미리 렌더링 된&dagger; 동시에 합니다. 

> [!NOTE]
> &dagger;기본적으로 Razor 구성 요소 앱에 대 한 사전 서버 쪽 렌더링이 가능 합니다. 클라이언트 쪽 Blazor 앱 향후 Preview 4 릴리스에서 사전 렌더링이 지원 합니다. 자세한 내용은 [MapFallbackToPage/파일을 사용 하도록 템플릿을/미들웨어 업데이트](https://github.com/aspnet/AspNetCore/issues/8852)합니다.

페이지 또는 보기에서 구성 요소를 렌더링 하려면 사용는 `RenderComponentAsync<TComponent>` HTML 도우미 메서드입니다.

```cshtml
<div id="Counter">
    @(await Html.RenderComponentAsync<Counter>(new { IncrementAmount = 10 }))
</div>
```

페이지 뷰를 렌더링 하는 구성 요소에서 대화형으로 미리 보기 3 릴리스에 아직 없습니다. 예를 들어, 단추를 선택 하는 메서드 호출이 트리거되지 않습니다. 향후 미리 보기는이 제한 사항을 해결를 일반 요소 및 특성 구문을 사용 하 여 렌더링 구성 요소에 대 한 지원을 추가 합니다.

페이지 및 뷰 구성 요소를 사용할 수 있지만 그 반대도 마찬가지로 true 아닙니다. 구성 요소는 부분 뷰 섹션 등의 보기 및 페이지 관련 시나리오를 사용할 수 없습니다. 에 구성 요소에 구성 요소에서 부분 뷰, 부분 뷰 논리 비율에서 논리를 사용 합니다.

## <a name="using-components"></a>구성 요소를 사용 하 여

구성 요소는 선언 하 여 다른 구성 요소는 HTML 요소 구문을 사용 하 여 합니다. 구성 요소 사용을 위한 태그는 태그 이름이 구성 요소 유형인 HTML 태그처럼 보입니다.

다음 태그를 렌더링 한 `HeadingComponent` (*HeadingComponent.cshtml*) 인스턴스:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/Index.cshtml?name=snippet_HeadingComponent)]

## <a name="component-parameters"></a>구성 요소 매개 변수

구성 요소를 가질 수 있습니다 *구성 요소 매개 변수*를 사용 하 여 정의 된 *public이 아닌* 구성 요소 클래스의 속성으로 데코 레이트 `[Parameter]`합니다. 특성을 사용하여 태그에서 구성 요소의 인수를 지정합니다.

다음 예에서 `ParentComponent` 의 값을 설정 합니다 `Title` 의 속성을 `ChildComponent`:

*ParentComponent.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ParentComponent.cshtml?name=snippet_ParentComponent&highlight=5)]

*ChildComponent.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ChildComponent.cshtml?highlight=7-8)]

## <a name="child-content"></a>자식 콘텐츠

구성 요소는 다른 구성 요소의 콘텐츠를 설정할 수 있습니다. 할당의 수신 구성 요소를 지정 하는 태그 사이 있는 내용을 제공 합니다. 예를 들어, 한 `ParentComponent` 여 제공할 수 있습니다 콘텐츠 렌더링에 대 한 하위 구성 요소 내에서 콘텐츠를 배치 하 여 `<ChildComponent>` 태그입니다.

*ParentComponent.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ParentComponent.cshtml?name=snippet_ParentComponent&highlight=6-7)]

자식 구성 요소에는 `ChildContent` 나타내는 속성을 `RenderFragment`입니다. 변수의 `ChildContent` 콘텐츠 렌더링할지 자식 요소의 태그에 배치 됩니다. 다음 예제에서는 변수의 `ChildContent` 부모 구성 요소에서 수신 되 고 부트스트랩 패널 내에서 렌더링 `panel-body`합니다.

*ChildComponent.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ChildComponent.cshtml?highlight=3,10-11)]

> [!NOTE]
> 속성 수신 합니다 `RenderFragment` 콘텐츠 이름은 `ChildContent` 규칙에 따라 합니다.

## <a name="data-binding"></a>데이터 바인딩

구성 요소와 DOM 요소에 대 한 데이터 바인딩을 사용 하 여 수행 됩니다는 `bind` 특성입니다. 다음 예제에서는 `ItalicsCheck` 속성 확인란의 상태를 확인 합니다.

```cshtml
<input type="checkbox" class="form-check-input" id="italicsCheck" 
    bind="@_italicsCheck">
```

확인란을 선택 하 고 지울, 속성의 값으로 업데이트 됩니다 `true` 고 `false`, 각각.

속성의 값 변경에 대 한 응답에 없는 구성 요소를 렌더링 하는 경우에 확인란 UI에서 업데이트 됩니다. 구성 요소 렌더링 이벤트 처리기 코드를 실행 한 후, 이후 속성 업데이트 UI에 즉시 반영 일반적으로 됩니다.

사용 하 여 `bind` 사용 하 여는 `CurrentValue` 속성 (`<input bind="@CurrentValue">`) 다음 기본적으로 동일 합니다.

```cshtml
<input value="@CurrentValue" 
    onchange="@((UIChangeEventArgs __e) => CurrentValue = __e.Value)">
```

구성 요소를 렌더링할 때 합니다 `value` 에서 가져온 입력 요소를 `CurrentValue` 속성입니다. 사용자가 텍스트 상자에는 `onchange` 이벤트가 발생 및 `CurrentValue` 속성 변경 된 값으로 설정 됩니다. 사실에서 코드 생성은 조금 더 복잡 한 `bind` 형식 변환이 수행 되는 몇 가지 경우를 처리 합니다. 원칙적으로 `bind` 연결 된 식의 현재 값을 `value` 등록 된 처리기를 사용 하 여 특성 및 처리 변경 합니다.

외에 `onchange`와 같은 다른 이벤트를 사용 하 여 속성에 바인딩할 수 있습니다 `oninput` 바인딩할 항목에 대해 더 명확히 하 여:

```cshtml
<input type="text" bind-value-oninput="@CurrentValue">
```

와 달리 `onchange`, `oninput` 텍스트 상자에 입력 된 모든 문자에 대해 발생 합니다.

**형식 문자열**

데이터 바인딩을 사용 하 여 작동 <xref:System.DateTime> 형식 문자열입니다. 이 이번에 통화 또는 숫자 형식과 같은 다른 형식으로 식을 사용할 수 없습니다.

```cshtml
<input bind="@StartDate" format-value="yyyy-MM-dd">

@functions {
    [Parameter]
    private DateTime StartDate { get; set; } = new DateTime(2020, 1, 1);
}
```

`format-value` 특성을 적용할 날짜 형식을 지정 합니다 `value` 의 `input` 요소입니다. 형식 값을 구문 분석 하는 또한 때는 `onchange` 이벤트가 발생 합니다.

**구성 요소 매개 변수**

바인딩 구성 요소 매개 변수를 인식 여기서 `bind-{property}` 구성 요소에서 속성 값을 바인딩할 수 있습니다.

다음 구성 요소에서는 `ChildComponent` 바인딩합니다 합니다 `ParentYear` 부모에서 매개 변수는 `Year` 자식 구성 요소에 대 한 매개 변수:

부모 구성 요소입니다.

```cshtml
@page "/ParentComponent"

<h1>Parent Component</h1>

<p>ParentYear: @ParentYear</p>

<ChildComponent bind-Year="@ParentYear" />

<button class="btn btn-primary" onclick="@ChangeTheYear">
    Change Year to 1986
</button>

@functions {
    [Parameter]
    private int ParentYear { get; set; } = 1978;

    private void ChangeTheYear()
    {
        ParentYear = 1986;
    }
}
```

자식 구성 요소입니다.

```cshtml
<h2>Child Component</h2>

<p>Year: @Year</p>

@functions {
    [Parameter]
    private int Year { get; set; }

    [Parameter]
    private Action<int> YearChanged { get; set; }
}
```

로드 된 `ParentComponent` 다음 태그를 생성 합니다.

```html
<h1>Parent Component</h1>

<p>ParentYear: 1978</p>

<h2>Child Component</h2>

<p>Year: 1978</p>
```

경우의 값을 `ParentYear` 에서 단추를 선택 하 여 속성이 변경 될를 `ParentComponent`, `Year` 의 속성은 `ChildComponent` 업데이트 됩니다. 새 값 `Year` UI에서 렌더링 될 때를 `ParentComponent` 렌더링은:

```html
<h1>Parent Component</h1>

<p>ParentYear: 1986</p>

<h2>Child Component</h2>

<p>Year: 1986</p>
```

`Year` 동반 있기 때문에 매개 변수를 바인딩할 수 `YearChanged` 유형과 일치 하는 이벤트를 `Year` 매개 변수입니다.

규칙에 따라 `<ChildComponent bind-Year="@ParentYear" />` 기본적으로 해당 문서를 작성 하는

```cshtml
    <ChildComponent bind-Year-YearChanged="@ParentYear" />
```

속성을 사용 하 여 해당 이벤트 처리기는 일반적으로 바인딩될 수 `bind-property-event` 특성입니다.

## <a name="event-handling"></a>이벤트 처리

Razor 구성 요소는 이벤트 처리 기능을 제공 합니다. HTML 요소 특성에 대 한 명명 된 `on<event>` (예를 들어 `onclick`, `onsubmit`) 대리자 형식의 값을 사용 하 여 Razor 구성 요소는 이벤트 처리기로 특성의 값을 처리 합니다. 특성의 이름이 항상 시작 `on`합니다.

다음 코드는 호출 된 `UpdateHeading` 메서드 UI의 단추를 선택한 경우:

```cshtml
<button class="btn btn-primary" onclick="@UpdateHeading">
    Update heading
</button>

@functions {
    private void UpdateHeading(UIMouseEventArgs e)
    {
        ...
    }
}
```

다음 코드는 호출 된 `CheckboxChanged` 확인란 UI에서 변경 되 면 메서드:

```cshtml
<input type="checkbox" class="form-check-input" onchange="@CheckboxChanged">

@functions {
    private void CheckboxChanged()
    {
        ...
    }
}
```

이벤트 처리기는 비동기 및 반환 될 수도 있습니다는 <xref:System.Threading.Tasks.Task>합니다. 수동으로 호출할 필요가 없습니다 `StateHasChanged()`합니다. 예외가 발생할 때 기록 됩니다.

```cshtml
<button class="btn btn-primary" onclick="@UpdateHeading">
    Update heading
</button>

@functions {
    private async Task UpdateHeading(UIMouseEventArgs e)
    {
        ...
    }
}
```

일부 이벤트에 대 한 이벤트 관련 이벤트 인수 형식은 허용 됩니다. 이러한 이벤트 유형 중 하나에 대 한 액세스 필요 없으면 그럴 메서드 호출에 필요 합니다.

지원 되는 이벤트 인수의 목록이입니다.

* UIEventArgs
* UIChangeEventArgs
* UIKeyboardEventArgs
* UIMouseEventArgs

람다 식을 사용할 수도 있습니다.

```cshtml
<button onclick="@(e => Console.WriteLine("Hello, world!"))">Say hello</button>
```

와 같은 추가 값에 대해 닫기 하면 편리한 경우가 요소의 집합을 반복 하는 경우. 다음 예제에서는 세 개의 단추를 호출 하는 각 `UpdateHeading` 이벤트 인수를 전달 (`UIMouseEventArgs`) 단추 번호 (`buttonNumber`) UI에서 선택한 경우:

```cshtml
<h2>@message</h2>

@for (var i = 1; i < 4; i++)
{
    var buttonNumber = i;

    <button class="btn btn-primary"
            onclick="@(e => UpdateHeading(e, buttonNumber))">
        Button #@i
    </button>
}

@functions {
    private string message = "Select a button to learn its position.";

    private void UpdateHeading(UIMouseEventArgs e, int buttonNumber)
    {
        message = $"You selected Button #{buttonNumber} at " +
            "mouse position: {e.ClientX} X {e.ClientY}.";
    }
}
```

> [!NOTE]
> 수행 **되지** 루프 변수를 사용 하 여 (`i`)에 `for` 람다 식에 직접 루프입니다. 그렇지 않으면 같은 변수 발생 하는 모든 람다 식에 의해 사용 됩니다 `i`의 모든 람다 식에서 동일한 값입니다. 지역 변수에 해당 값을 항상 캡처하지 (`buttonNumber` 앞의 예제에서) 다음 사용 하 여 합니다.

## <a name="capture-references-to-components"></a>구성 요소에 대 한 참조를 캡처

구성 요소 참조를 가져올 참조를 제공할 구성 요소 인스턴스를 해당 인스턴스를 같은 명령을 실행할 수 있도록 `Show` 또는 `Reset`합니다. 추가 구성 요소 참조를 캡처하려면는 `ref` 자식 구성 요소에 특성 및 다음 하위 구성 요소와 동일한 이름과 동일한 형식을 사용 하 여 필드를 정의 합니다.

```cshtml
<MyLoginDialog ref="loginDialog" ... />

@functions {
    private MyLoginDialog loginDialog;

    private void OnSomething()
    {
        loginDialog.Show();
    }
}
```

구성 요소를 렌더링할 때 합니다 `loginDialog` 필드가 채워집니다는 `MyLoginDialog` 자식 구성 요소 인스턴스. 다음 구성 요소 인스턴스에 대 한.NET 메서드를 호출할 수 있습니다.

> [!IMPORTANT]
> 합니다 `loginDialog` 변수는 구성 요소에서 렌더링 되 고 해당 출력을 포함 한 후에 채워집니다는 `MyLoginDialog` 요소입니다. 그때까지 참조할 것이 없습니다. 구성 요소 렌더링을 마친 후 구성 요소 참조를 조작 하려면 사용 합니다 `OnAfterRenderAsync` 또는 `OnAfterRender` 메서드.

하는 유사한 구문을 사용 하 여 구성 요소 참조를 캡처하는 동안 [요소 참조를 캡처](xref:razor-components/javascript-interop#capture-references-to-elements), 되어 있지는 [JavaScript interop](xref:razor-components/javascript-interop) 기능입니다. JavaScript 코드에 전달 된 구성 요소 참조 되지 않습니다. 해당 하는.NET 코드에만 사용 됩니다.

> [!NOTE]
> 수행할 **되지** 자식 구성 요소의 상태를 변경할 구성 요소 참조를 사용 합니다. 대신, 자식 구성 요소에 데이터를 전달할 일반 선언적 매개 변수를 사용 합니다. 이렇게 하면 정확한 시간에 자동으로 렌더링할 자식 구성 요소입니다.

## <a name="lifecycle-methods"></a>수명 주기 메서드

`OnInitAsync` 및 `OnInit` 구성 요소를 초기화 하는 코드를 실행 합니다. 비동기 작업을 수행 하려면 사용할 `OnInitAsync` 하며 `await` 작업 키워드:

```csharp
protected override async Task OnInitAsync()
{
    await ...
}
```

동기 작업을 사용 하 여 `OnInit`:

```csharp
protected override void OnInit()
{
    ...
}
```

`OnParametersSetAsync` 및 `OnParametersSet` 구성 요소를 부모에서 매개 변수를 수신 했 고 값 속성에 할당 된 때 호출 됩니다. 이러한 메서드는 구성 요소를 초기화 한 후 실행 하 고 때마다 구성 요소는 렌더링 후:

```csharp
protected override async Task OnParametersSetAsync()
{
    await ...
}
```

```csharp
protected override void OnParametersSet()
{
    ...
}
```

`OnAfterRenderAsync` 및 `OnAfterRender` 구성 요소는 렌더링을 완료 된 후 호출 됩니다. 요소 및 구성 요소에 대 한 참조에 대 한 연결이 시점에서 채워집니다. 이 단계를 사용 하 여 렌더링 된 DOM 요소에서 작동 하는 타사 JavaScript 라이브러리를 활성화 하는 등의 렌더링된 된 콘텐츠를 사용 하 여 추가 초기화 단계를 수행 합니다.

```csharp
protected override async Task OnAfterRenderAsync()
{
    await ...
}
```

```csharp
protected override void OnAfterRender()
{
    ...
}
```

`SetParameters` 매개 변수를 설정 하기 전에 코드를 실행 하 여 재정의할 수 있습니다.

```csharp
public override void SetParameters(ParameterCollection parameters)
{
    ...

    base.SetParameters(parameters);
}
```

경우 `base.SetParameters` 되지 호출 사용자 지정 코드를 해석할 수 있는 방식으로 필요한 들어오는 매개 변수 값입니다. 예를 들어, 들어오는 매개 변수는 클래스의 속성에 할당할 필요 하지 않습니다.

`ShouldRender` ui 새로 고침 표시 하지 않으려면 재정의할 수 있습니다. 구현을 반환 하는 경우 `true`, UI 새로 고쳐집니다. 경우에 `ShouldRender` 는 재정의 된 구성 요소는 항상 처음 렌더링 됩니다.

```csharp
protected override bool ShouldRender()
{
    var renderUI = true;

    return renderUI;
}
```

## <a name="component-disposal-with-idisposable"></a>IDisposable 사용 하 여 구성 요소 삭제

구성 요소를 구현 하는 경우 <xref:System.IDisposable>서 [Dispose 메서드](/dotnet/standard/garbage-collection/implementing-dispose) UI에서 구성 요소가 제거 될 때 호출 됩니다. 다음 구성 요소 `@implements IDisposable` 하며 `Dispose` 메서드:

```csharp
@using System
@implements IDisposable

...

@functions {
    public void Dispose()
    {
        ...
    }
}
```

## <a name="routing"></a>라우팅

라우팅 Razor 구성 요소에는 앱에서 액세스할 수 있는 각 구성 요소에 경로 템플릿을 제공 하 여 수행 됩니다.

때를 *.cshtml* 파일을 `@page` 지시문 컴파일됩니다, 생성된 된 클래스는 지정 된을 <xref:Microsoft.AspNetCore.Mvc.RouteAttribute> 경로 템플릿을 지정 합니다. 런타임 시 사용 하 여 구성 요소 클래스에 대 한 라우터 찾습니다는 `RouteAttribute` 하 고 어떤 구성 요소는 요청 된 URL과 일치 하는 경로 템플릿을 렌더링 합니다.

여러 경로 템플릿 구성 요소에 적용할 수 있습니다. 다음 구성 요소에 대 한 요청에 응답할 `/BlazorRoute` 고 `/DifferentBlazorRoute`:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRoute.cshtml?name=snippet_BlazorRoute)]

## <a name="route-parameters"></a>경로 매개 변수

구성 요소에 제공 된 경로 템플릿에서 경로 매개 변수를 받을 수는 `@page` 지시문입니다. 라우터 경로 매개 변수를 사용 하 여 해당 구성 요소 매개 변수를 채웁니다.

*RouteParameter.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/RouteParameter.cshtml?name=snippet_RouteParameter)]

선택적 매개 변수 지원 되지 않으며, 따라서 두 `@page` 지시문 위의 예제에 적용 됩니다. 첫 번째 매개 변수 없이 구성 요소에 대 한 탐색을 허용합니다. 두 번째 `@page` 지시문은 합니다 `{text}` 경로 매개 변수 및 값을 할당 합니다 `Text` 속성입니다.

## <a name="base-class-inheritance-for-a-code-behind-experience"></a>"코드 숨김" 환경에 대 한 기본 클래스 상속

구성 요소 파일 (*.cshtml*) HTML 태그를 혼합 하 고 C# 같은 파일에서 코드를 처리 합니다. `@inherits` Razor 구성 요소 앱 구성 요소 태그 처리 코드와 분리 하는 "코드 숨김" 환경을 제공할 수 지시문을 사용할 수 있습니다.

[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) 구성 요소는 기본 클래스를 상속할 수 있습니다 하는 방법을 보여 줍니다. `BlazorRocksBase`, 구성 요소의 속성과 메서드를 제공 합니다.

*BlazorRocks.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRocks.cshtml?name=snippet_BlazorRocks)]

*BlazorRocksBase.cs*:

[!code-csharp[](common/samples/3.x/BlazorSample/Pages/BlazorRocksBase.cs)]

기본 클래스에서 파생 되어야 `ComponentBase`합니다.

## <a name="razor-support"></a>Razor 지원

**Razor 지시문**

Razor 지시문은 다음 표에 표시 됩니다.

| 지시문 | 설명 |
| --------- | ----------- |
| [\@functions](xref:mvc/views/razor#section-5) | 추가 된 C# 구성 요소에 대 한 코드 블록입니다. |
| `@implements` | 생성 된 구성 요소 클래스에 대 한 인터페이스를 구현합니다. |
| [\@상속](xref:mvc/views/razor#section-3) | 구성 요소가 상속 된 클래스의 모든 권한을 제공 합니다. |
| [\@삽입](xref:mvc/views/razor#section-4) | 서비스에서 주입 수 있도록 합니다 [서비스 컨테이너](xref:fundamentals/dependency-injection)합니다. 자세한 내용은 [보기에 종속성 주입](xref:mvc/views/dependency-injection)을 참조하세요. |
| `@layout` | 레이아웃 구성 요소를 지정합니다. 레이아웃 구성 요소 코드 중복 및 불일치를 방지 하는 데 사용 됩니다. |
| [\@page](xref:razor-pages/index#razor-pages) | 구성 요소가 요청을 직접 처리 해야 지정 합니다. `@page` 경로 및 선택적 매개 변수를 사용 하 여 지시문을 지정할 수 있습니다. Razor 페이지와 달리는 `@page` 지시문 파일의 맨 위에 있는 첫 번째 지시문을 사용할 필요가 없습니다. 자세한 내용은 [라우팅](xref:razor-components/routing)을 참고하시기 바랍니다. |
| [\@using](xref:mvc/views/razor#using) | 추가 된 C# `using` 지시문을 생성 된 구성 요소 클래스입니다. |
| [\@addTagHelper](xref:mvc/views/razor#tag-helpers) | 사용 하 여 `@addTagHelper` 앱의 어셈블리 보다 다른 어셈블리의 구성 요소를 사용 하도록 합니다. |

**조건부 특성**

특성은.NET 값에 따라 조건부로 렌더링 됩니다. 값이 `false` 또는 `null`, 특성 렌더링 되지 않습니다. 값이 `true`, 특성이 렌더링 되 최소화 합니다.

다음 예에서 `IsCompleted` 있는지 여부를 확인 `checked` 컨트롤의 태그 렌더링 됩니다.

```cshtml
<input type="checkbox" checked="@IsCompleted">

@functions {
    [Parameter]
    private bool IsCompleted { get; set; }
}
```

하는 경우 `IsCompleted` 는 `true`, 확인란으로 렌더링 됩니다.

```html
<input type="checkbox" checked>
```

하는 경우 `IsCompleted` 는 `false`, 확인란으로 렌더링 됩니다.

```html
<input type="checkbox">
```

**Razor에 대 한 추가 정보**

Razor에 대 한 자세한 내용은 참조는 [Razor 구문 참조](xref:mvc/views/razor)합니다.

## <a name="raw-html"></a>원시 HTML

문자열은 일반적으로 렌더링 됩니다 DOM 텍스트 노드를 사용 하 여 포함할 수 있는 태그는 무시 되 고 리터럴 텍스트로 처리 하는 것을 의미 합니다. 원시 HTML을 렌더링 하에 HTML 콘텐츠를 래핑하는 `MarkupString` 값입니다. 값이 HTML 또는 SVG로 구문 분석 하 고 DOM에 삽입

> [!WARNING]
> 소스는 신뢰할 수 없는 원시 HTML에서 생성 된 렌더링을 **보안 위험** 않아야 합니다.

다음 예제에서는 사용 하 여는 `MarkupString` 요소의 렌더링 된 출력은 정적 HTML 콘텐츠 블록을 추가할 형식입니다.

```html
@((MarkupString)myMarkup)

@functions {
    private string myMarkup = 
        "<p class='markup'>This is a <em>markup string</em>.</p>";
}
```

## <a name="templated-components"></a>템플릿 기반 구성 요소

템플릿 기반 구성 요소는 하나 이상의 UI 템플릿 요소의 렌더링 논리의 일부로 사용할 수 있는 매개 변수로 허용 하는 구성 요소입니다. 템플릿 기반 구성 요소를 사용 하 여 일반 구성 요소 보다 더 다시 사용할 수 있는 더 높은 수준의 구성 요소를 작성할 수 있습니다. 몇 가지 예는 다음과 같습니다.

* 테이블의 머리글, 행 및 바닥글에 대 한 템플릿을 지정할 수 있도록 허용 하는 테이블 구성 요소입니다.
* 사용자가 목록에 항목 렌더링에 대 한 템플릿을 지정할 수 있도록 목록 구성 요소입니다.

### <a name="template-parameters"></a>템플릿 매개 변수

템플릿 기반 구성 요소 형식의 하나 이상의 구성 요소 매개 변수를 지정 하 여 정의 됩니다 `RenderFragment` 또는 `RenderFragment<T>`합니다. 렌더링 조각 구성 요소에 의해 렌더링 되는 UI의 세그먼트를 나타냅니다. 필요에 따라 렌더링 조각 렌더링 조각 호출 될 때 지정 될 수 있는 매개 변수를 사용 합니다.

*Components/TableTemplate.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/TableTemplate.cshtml)]

템플릿 기반 구성 요소를 사용 하는 경우 템플릿 매개 변수를 지정할 수 있습니다 매개 변수의 이름과 일치 하는 자식 요소를 사용 하 여 (`TableHeader` 고 `RowTemplate` 다음 예제의):

```cshtml
<TableTemplate Items="@pets">
    <TableHeader>
        <th>ID</th>
        <th>Name</th>
    </TableHeader>
    <RowTemplate>
        <td>@context.PetId</td>
        <td>@context.Name</td>
    </RowTemplate>
</TableTemplate>
```

### <a name="template-context-parameters"></a>템플릿 상황에 맞는 매개 변수

형식의 인수를 구성 요소 `RenderFragment<T>` 요소가 있는 라는 암시적 매개 변수 전달 `context` (예를 들어 위의 코드 샘플에서에서 `@context.PetId`)를 사용 하 여 매개 변수 이름을 변경할 수 있습니다는 `Context` 자식 특성 요소입니다. 다음 예제에서는 `RowTemplate` 요소의 `Context` 특성을 지정 합니다 `pet` 매개 변수:

```cshtml
<TableTemplate Items="@pets">
    <TableHeader>
        <th>ID</th>
        <th>Name</th>
    </TableHeader>
    <RowTemplate Context="pet">
        <td>@pet.PetId</td>
        <td>@pet.Name</td>
    </RowTemplate>
</TableTemplate>
```

지정할 수 있습니다는 `Context` component 요소 특성입니다. 지정 된 `Context` 특성이 지정 된 템플릿 매개 변수를 모두에 적용 됩니다. 암시적 자식 콘텐츠를 콘텐츠 매개 변수 이름을 지정 하려는 경우 유용할 수 있습니다 (모든 줄 바꿈 없이 자식 요소). 다음 예제에서는 `Context` 특성에 표시 되는 `TableTemplate` 요소 모든 템플릿 매개 변수를 적용:

```cshtml
<TableTemplate Items="@pets" Context="pet">
    <TableHeader>
        <th>ID</th>
        <th>Name</th>
    </TableHeader>
    <RowTemplate>
        <td>@pet.PetId</td>
        <td>@pet.Name</td>
    </RowTemplate>
</TableTemplate>
```

### <a name="generic-typed-components"></a>제네릭 형식의 구성 요소

템플릿 기반 구성 요소가 일반적으로 자주 형식화 됩니다. 렌더링 하는 제네릭 목록 보기 템플릿에서 구성 요소를 사용할 수 예를 들어 `IEnumerable<T>` 값입니다. 일반 구성 요소를 정의 하기 위해 사용 하 여는 `@typeparam` 지시문 형식 매개 변수를 지정 합니다.

*Components/ListViewTemplate.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/ListViewTemplate.cshtml)]

제네릭 형식의 구성 요소를 사용 하는 경우 형식 매개 변수에 가능한 경우 유추 됩니다.

```cshtml
<ListViewTemplate Items="@pets">
    <ItemTemplate Context="pet">
        <li>@pet.Name</li>
    </ItemTemplate>
</ListViewTemplate>
```

그렇지 않은 경우 형식 매개 변수 지정 되어야 합니다 명시적으로 형식 매개 변수의 이름과 일치 하는 특성을 사용 하 여. 다음 예에서 `TItem="Pet"` 형식을 지정 합니다.

```cshtml
<ListViewTemplate Items="@pets" TItem="Pet">
    <ItemTemplate Context="pet">
        <li>@pet.Name</li>
    </ItemTemplate>
</ListViewTemplate>
```

## <a name="cascading-values-and-parameters"></a>연계 값 및 매개 변수

일부 시나리오에서는 하기가 불편 데이터가 흐르도록 지정 하는 상위 구성 요소를 사용 하 여 하위 구성 요소에서 [구성 요소 매개 변수](#component-parameters)여러 구성 요소 계층 필요한 경우에 특히, 합니다. 연계 값 및 매개 변수는 상위 구성 요소의 모든 하위 구성 요소에 값을 제공 하는 편리한 방법을 제공 하 여이 문제를 해결 합니다. 연계 값 및 매개 변수 구성 요소를 조정 하는 방법을 제공 합니다.

### <a name="theme-example"></a>테마 예제

다음과에서 *테마* 샘플 앱의 예제는 `ThemeInfo` 클래스는 동일한 스타일을 공유할 앱의 특정된 부분 내에서 단추의 모든 구성 요소 계층 구조 아래로 흐름 테마 정보를 지정 합니다.

*UIThemeClasses/ThemeInfo.cs*:

```csharp
public class ThemeInfo
{
    public string ButtonClass { get; set; }
}
```

상위 구성 요소를 연계 값 구성 요소를 사용 하 여 연계 값을 제공할 수 있습니다. 연계 값 구성 요소는 구성 요소 계층 구조의 하위 트리를 래핑하고 해당 하위 트리 내에서 모든 구성 요소에 단일 값을 제공 합니다.

샘플 앱에서 테마 정보를 지정 하는 예를 들어, (`ThemeInfo`)의 레이아웃 본문을 구성 하는 모든 구성 요소에 대 한 연계 매개 변수로 앱의 레이아웃 중 하나에 `@Body` 속성입니다. `ButtonClass` 값이 할당은 `btn-success` 레이아웃 구성 요소에 있습니다. 하위 구성 요소를 통해이 속성을 사용할 수는 `ThemeInfo` 연계 개체입니다.

*Shared/CascadingValuesParametersLayout.cshtml*:

```cshtml
@inherits LayoutComponentBase
@using BlazorSample.UIThemeClasses

<div class="container-fluid">
    <div class="row">
        <div class="col-sm-3">
            <NavMenu />
        </div>
        <div class="col-sm-9">
            <CascadingValue Value="@theme">
                <div class="content px-4">
                    @Body
                </div>
            </CascadingValue>
        </div>
    </div>
</div>

@functions {
    private ThemeInfo theme = new ThemeInfo { ButtonClass = "btn-success" };
}
```

있도록 연계 값을 사용 하 여 연계 매개 변수를 선언 하는 구성 요소는 `[CascadingParameter]` 특성 또는 문자열 이름 값을 기준으로:

```cshtml
<CascadingValue Value=@PermInfo Name="UserPermissions">...</CascadingValue>

[CascadingParameter(Name = "UserPermissions")]
private PermInfo Permissions { get; set; }
```

문자열 이름 값을 사용 하 여 바인딩을 동일한 형식의 여러 연계 값이 있는 동일한 하위 트리 내와 구분 해야 하는 경우 관련이 있습니다.

연계 값 형식으로 연계 매개 변수에 바인딩됩니다.

샘플 앱에서 연계 값 매개 변수 테마 구성 요소에 바인딩하는 `ThemeInfo` 연계 연계 매개 변수 값입니다. 매개 변수를 사용 하 여 구성 요소에 의해 표시 되는 단추 중 하나에 대 한 CSS 클래스를 설정 합니다.

*Pages/CascadingValuesParametersTheme.cshtml*:

```cshtml
@page "/cascadingvaluesparameterstheme"
@layout CascadingValuesParametersLayout
@using BlazorSample.UIThemeClasses

<h1>Cascading Values & Parameters</h1>

<p>Current count: @currentCount</p>

<p>
    <button class="btn" onclick="@IncrementCount">
        Increment Counter (Unthemed)
    </button>
</p>

<p>
    <button class="btn @ThemeInfo.ButtonClass" onclick="@IncrementCount">
        Increment Counter (Themed)
    </button>
</p>

@functions {
    private int currentCount = 0;

    [CascadingParameter] protected ThemeInfo ThemeInfo { get; set; }

    private void IncrementCount()
    {
        currentCount++;
    }
}
```

### <a name="tabset-example"></a>TabSet 예제

연계 매개 변수 구성 요소 구성 요소 계층 전체에서 공동 작업을 사용 하도록 설정할 수도 있습니다. 예를 들어, 다음 사항을 고려 *TabSet* 샘플 앱의 예제입니다.

샘플 앱에는 `ITab` 인터페이스 구현 탭입니다.

[!code-cs[](common/samples/3.x/BlazorSample/UIInterfaces/ITab.cs)]

값 매개 변수 TabSet 연계 구성 요소에서는 여러 탭 구성 요소를 포함 하는 탭 설정 구성:

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/CascadingValuesParametersTabSet.cshtml?name=snippet_TabSet)]

명시적으로 자식 탭 구성 되지 탭 설정에 매개 변수로 전달 됩니다. 대신, 자식 탭 구성 요소는 일부 탭 집합의 자식 내용입니다. 그러나 탭 설정 해야 헤더와 활성 탭을 렌더링할 수 있도록 각 탭 구성 요소에 대해 알아야 합니다. 탭 설정 구성 요소 추가 코드 없이이 조정을 사용할 수 있도록 *연계 값으로 자체를 제공할 수 있습니다* 다음 선택 하는 하위 탭 구성 요소입니다.

*Components/TabSet.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/TabSet.cshtml)]

하위 탭 구성 캡처를 연계 매개 변수로 포함 된 탭 설정 탭 구성 요소 탭 설정 및 좌표에 추가 되도록 하므로 어떤 탭에서 활성화 됩니다.

*Components/Tab.cshtml*:

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/Tab.cshtml)]

## <a name="razor-templates"></a>Razor 템플릿

렌더링 조각 Razor 템플릿 구문을 사용 하 여 정의할 수 있습니다. Razor 템플릿 UI 코드 조각을 정의 하 고 다음 형식으로 가정 하는 방법을 같습니다.

```cshtml
@<tag>...</tag>
```

다음 예제에서는 지정 하는 방법을 보여 줍니다 `RenderFragment` 고 `RenderFragment<T>` 값입니다.

*RazorTemplates.cshtml*:

```cshtml
@{
    RenderFragment template = @<p>The time is @DateTime.Now.</p>;
    RenderFragment<Pet> petTemplate = (pet) => @<p>Your pet's name is @pet.Name.</p>;
}
```

Razor 템플릿 템플릿 구성 요소에 인수로 전달 하거나 나중에 직접 렌더링할 수를 사용 하 여 정의 조각을 렌더링 합니다. 예를 들어 이전 서식 파일에 다음 Razor 태그를 사용 하 여 직접 렌더링 됩니다.

```cshtml
@template

@petTemplate(new Pet { Name = "Rex" })
```

렌더링된 출력:

```
The time is 10/04/2018 01:26:52.

Your pet's name is Rex.
```

## <a name="manual-rendertreebuilder-logic"></a>수동 RenderTreeBuilder 논리

`Microsoft.AspNetCore.Components.RenderTree` 구성 요소 및 구성 요소에 수동으로 빌드를 포함 하 여 요소를 조작 하기 위한 메서드를 제공 합니다. C# 코드입니다.

> [!NOTE]
> 사용 `RenderTreeBuilder` 은 고급 시나리오 구성 요소를 만듭니다. 잘못 된 구성 요소 (예: 닫히지 않은 태그 태그) 정의 되지 않은 동작이 발생할 수 있습니다.

애완 동물 정보 구성 요소는 것이 좋습니다 (*PetDetails.razor* Razor 구성 요소에서 *PetDetails.cshtml* Blazor에서), 다른 구성 요소를 수동으로 빌드할 수입니다.

```cshtml
<h2>Pet Details Component</h2>

<p>@PetDetailsQuote<p>

@functions
{
    [Parameter]
    string PetDetailsQuote { get; set; }
}
```

다음 예에서 루프는 `CreateComponent` 메서드는 세 가지 애완 동물 정보 구성 요소를 생성 합니다. 호출할 때 `RenderTreeBuilder` 구성 요소를 만드는 방법 (`OpenComponent` 고 `AddAttribute`), 시퀀스 번호는 소스 코드 줄 번호입니다. 해당 고유 줄의 코드만으로 고유 하지 하는 시퀀스 번호 차이 알고리즘은 Razor 구성 요소 호출을 호출 합니다. 구성 요소를 만들 때 `RenderTreeBuilder` 방법, 하드 코드 시퀀스 번호에 대 한 인수입니다. **시퀀스 번호를 생성 하는 계산 또는 카운터를 사용 하 여 성능이 저하 될 수 있습니다.**

구성 요소 작성 (*BuiltContent.razor* Razor 구성 요소에서 *BuiltContent.cshtml* Blazor에서):

```cshtml
@page "/BuiltContent"

<h1>Build a component</h1>

@CustomRender

<button type="button" onclick="@RenderComponent">
    Create three Pet Details components
</button>

@functions {
    private RenderFragment CustomRender { get; set; }
    
    private RenderFragment CreateComponent() => builder =>
    {
        for (var i = 0; i < 3; i++) 
        {
            builder.OpenComponent(0, typeof(PetDetails));
            builder.AddAttribute(1, "PetDetailsQuote", "Someone's best friend!");
            builder.CloseComponent();
        }
    };    
    
    private void RenderComponent()
    {
        CustomRender = CreateComponent();
    }
}
```
