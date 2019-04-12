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
# <a name="create-and-use-razor-components"></a><span data-ttu-id="f9057-103">만들기 및 Razor 구성 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-103">Create and use Razor Components</span></span>

<span data-ttu-id="f9057-104">하 여 [Luke Latham](https://github.com/guardrex)하십시오 [Daniel Roth](https://github.com/danroth27), 및 [Morné Zaayman](https://github.com/MorneZaayman)</span><span class="sxs-lookup"><span data-stu-id="f9057-104">By [Luke Latham](https://github.com/guardrex), [Daniel Roth](https://github.com/danroth27), and [Morné Zaayman](https://github.com/MorneZaayman)</span></span>

<span data-ttu-id="f9057-105">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="f9057-105">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) ([how to download](xref:index#how-to-download-a-sample)).</span></span> <span data-ttu-id="f9057-106">필수 구성 요소는 [시작](xref:razor-components/get-started) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9057-106">See the [Get started](xref:razor-components/get-started) topic for prerequisites.</span></span>

<span data-ttu-id="f9057-107">Razor 구성 요소 앱을 사용 하 여 빌드됩니다 *구성 요소*합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-107">Razor Components apps are built using *components*.</span></span> <span data-ttu-id="f9057-108">구성 요소는 UI (사용자 인터페이스), 페이지, 대화 상자, 폼 등의 자체 포함 된 청크입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-108">A component is a self-contained chunk of user interface (UI), such as a page, dialog, or form.</span></span> <span data-ttu-id="f9057-109">구성 요소는 HTML 태그 및 데이터를 삽입 하거나 UI 이벤트에 응답 하는 데 필요한 처리 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-109">A component includes HTML markup and the processing logic required to inject data or respond to UI events.</span></span> <span data-ttu-id="f9057-110">구성 요소는 유연 하 고 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-110">Components are flexible and lightweight.</span></span> <span data-ttu-id="f9057-111">중첩 된, 다시 사용 하 고 수 프로젝트 간에 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-111">They can be nested, reused, and shared among projects.</span></span>

## <a name="component-classes"></a><span data-ttu-id="f9057-112">구성 요소 클래스</span><span class="sxs-lookup"><span data-stu-id="f9057-112">Component classes</span></span>

<span data-ttu-id="f9057-113">구성 요소는 일반적으로 구성 요소 Razor 파일에서 구현 됩니다 (*.razor*)를 조합 하 여 C# 와 HTML 태그 (*.cshtml* Blazor 앱에서는 파일을 사용).</span><span class="sxs-lookup"><span data-stu-id="f9057-113">Components are typically implemented in Razor Component files (*.razor*) using a combination of C# and HTML markup (*.cshtml* files are used in Blazor apps).</span></span>

<span data-ttu-id="f9057-114">구성 요소를 사용 하 여 Razor 구성 요소 앱에 작성 될 수 있습니다 합니다 *.cshtml* 파일 확장명으로 파일을 사용 하 여 구성 요소 Razor 파일으로 식별 됩니다는 `_RazorComponentInclude` MSBuild 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-114">Components can be authored in Razor Components apps using the *.cshtml* file extension as long as the files are identified as Razor Component files using the `_RazorComponentInclude` MSBuild property.</span></span> <span data-ttu-id="f9057-115">예를 들어, Razor 구성 요소 템플릿을 사용 하 여 만든 앱을 지정 하는 모든 *.cshtml* 아래에서 파일을 *구성 요소* Razor 구성 요소 파일과 폴더를 처리할지:</span><span class="sxs-lookup"><span data-stu-id="f9057-115">For example, an app created using the Razor Component template specifies that all *.cshtml* files under the *Components* folder should be treated as Razor Components files:</span></span>

```xml
<_RazorComponentInclude>Components\**\*.cshtml</_RazorComponentInclude>
```

<span data-ttu-id="f9057-116">구성 요소에 대 한 UI는 HTML을 사용 하 여 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-116">The UI for a component is defined using HTML.</span></span> <span data-ttu-id="f9057-117">동적 렌더링 논리(예: 루프, 조건, 식)는 [Razor](xref:mvc/views/razor)라는 포함된 C# 구문을 사용하여 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-117">Dynamic rendering logic (for example, loops, conditionals, expressions) is added using an embedded C# syntax called [Razor](xref:mvc/views/razor).</span></span> <span data-ttu-id="f9057-118">구성 요소 Razor 앱을 컴파일할 때, HTML 태그 및 C# 렌더링 논리 구성 요소 클래스 변환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-118">When a Razor Components app is compiled, the HTML markup and C# rendering logic are converted into a component class.</span></span> <span data-ttu-id="f9057-119">파일의 이름과 일치 하는 생성된 된 클래스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-119">The name of the generated class matches the name of the file.</span></span>

<span data-ttu-id="f9057-120">에 정의 된 구성 요소 클래스의 멤버는 `@functions` 블록 (둘 이상의 `@functions` 블록은 허용).</span><span class="sxs-lookup"><span data-stu-id="f9057-120">Members of the component class are defined in a `@functions` block (more than one `@functions` block is permissible).</span></span> <span data-ttu-id="f9057-121">에 `@functions` 이벤트 처리를 위해 또는 다른 구성 요소 논리를 정의 하기 위한 메서드를 사용 하 여 지정 된 블록에 구성 요소 상태 (속성, 필드).</span><span class="sxs-lookup"><span data-stu-id="f9057-121">In the `@functions` block, component state (properties, fields) is specified with methods for event handling or for defining other component logic.</span></span>

<span data-ttu-id="f9057-122">구성 요소 멤버 논리를 사용 하 여 구성 요소의 파트의 렌더링 처럼 사용할 수 있습니다 C# 로 시작 하는 식을 `@`합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-122">Component members can then be used as part of the component's rendering logic using C# expressions that start with `@`.</span></span> <span data-ttu-id="f9057-123">예를 들어는 C# 접두사로 사용 하 여 필드가 렌더링 되는지 `@` 필드 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-123">For example, a C# field is rendered by prefixing `@` to the field name.</span></span> <span data-ttu-id="f9057-124">다음 예제에서는 평가 하 고 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-124">The following example evaluates and renders:</span></span>

* `_headingFontStyle` <span data-ttu-id="f9057-125">CSS 속성 값으로 `font-style`입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-125">to the CSS property value for `font-style`.</span></span>
* `_headingText` <span data-ttu-id="f9057-126">내용에는 `<h1>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-126">to the content of the `<h1>` element.</span></span>

```cshtml
<h1 style="font-style:@_headingFontStyle">@_headingText</h1>

@functions {
    private string _headingFontStyle = "italic";
    private string _headingText = "Put on your new Blazor!";
}
```

<span data-ttu-id="f9057-127">처음에 구성 요소를 렌더링 한 후 이벤트에 대 한 응답에 렌더링 트리에서 해당 구성 요소에 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-127">After the component is initially rendered, the component regenerates its render tree in response to events.</span></span> <span data-ttu-id="f9057-128">다음 razor 구성 요소는 이전에 대 한 새로운 렌더링 트리를 비교 하 고 브라우저의 문서 개체 모델 (DOM)에 대 한 수정은 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-128">Razor Components then compares the new render tree against the previous one and applies any modifications to the browser's Document Object Model (DOM).</span></span>

## <a name="integrate-components-into-razor-pages-and-mvc-apps"></a><span data-ttu-id="f9057-129">구성 요소 Razor 페이지 및 MVC 앱에 통합</span><span class="sxs-lookup"><span data-stu-id="f9057-129">Integrate components into Razor Pages and MVC apps</span></span>

<span data-ttu-id="f9057-130">기존 Razor 페이지 및 MVC 앱과 구성 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-130">Use components with existing Razor Pages and MVC apps.</span></span> <span data-ttu-id="f9057-131">기존 페이지 또는 Razor 구성 요소를 사용 하는 뷰를 다시 작성할 필요가 없는 경우</span><span class="sxs-lookup"><span data-stu-id="f9057-131">There's no need to rewrite existing pages or views to use Razor Components.</span></span> <span data-ttu-id="f9057-132">페이지 또는 보기를 렌더링할 때 구성 요소는 미리 렌더링 된&dagger; 동시에 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-132">When the page or view is rendered, components are prerendered&dagger; at the same time.</span></span> 

> [!NOTE]
> <span data-ttu-id="f9057-133">&dagger;기본적으로 Razor 구성 요소 앱에 대 한 사전 서버 쪽 렌더링이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-133">&dagger;Server-side prerendering is enabled for Razor Components apps by default.</span></span> <span data-ttu-id="f9057-134">클라이언트 쪽 Blazor 앱 향후 Preview 4 릴리스에서 사전 렌더링이 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-134">Client-side Blazor apps will support prerendering in the upcoming Preview 4 release.</span></span> <span data-ttu-id="f9057-135">자세한 내용은 [MapFallbackToPage/파일을 사용 하도록 템플릿을/미들웨어 업데이트](https://github.com/aspnet/AspNetCore/issues/8852)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-135">For more information, see [Update templates/middleware to use MapFallbackToPage/File](https://github.com/aspnet/AspNetCore/issues/8852).</span></span>

<span data-ttu-id="f9057-136">페이지 또는 보기에서 구성 요소를 렌더링 하려면 사용는 `RenderComponentAsync<TComponent>` HTML 도우미 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-136">To render a component from a page or view, use the `RenderComponentAsync<TComponent>` HTML helper method:</span></span>

```cshtml
<div id="Counter">
    @(await Html.RenderComponentAsync<Counter>(new { IncrementAmount = 10 }))
</div>
```

<span data-ttu-id="f9057-137">페이지 뷰를 렌더링 하는 구성 요소에서 대화형으로 미리 보기 3 릴리스에 아직 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-137">Components rendered from pages and views aren't yet interactive in the Preview 3 release.</span></span> <span data-ttu-id="f9057-138">예를 들어, 단추를 선택 하는 메서드 호출이 트리거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-138">For example, selecting a button doesn't trigger a method call.</span></span> <span data-ttu-id="f9057-139">향후 미리 보기는이 제한 사항을 해결를 일반 요소 및 특성 구문을 사용 하 여 렌더링 구성 요소에 대 한 지원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-139">A future preview will address this limitation and add support for rendering components using the normal element and attribute syntax.</span></span>

<span data-ttu-id="f9057-140">페이지 및 뷰 구성 요소를 사용할 수 있지만 그 반대도 마찬가지로 true 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-140">While pages and views can use components, the converse isn't true.</span></span> <span data-ttu-id="f9057-141">구성 요소는 부분 뷰 섹션 등의 보기 및 페이지 관련 시나리오를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-141">Components can't use view- and page-specific scenarios, such as partial views and sections.</span></span> <span data-ttu-id="f9057-142">에 구성 요소에 구성 요소에서 부분 뷰, 부분 뷰 논리 비율에서 논리를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-142">To use logic from partial view in a component, factor out the partial view logic into a component.</span></span>

## <a name="using-components"></a><span data-ttu-id="f9057-143">구성 요소를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f9057-143">Using components</span></span>

<span data-ttu-id="f9057-144">구성 요소는 선언 하 여 다른 구성 요소는 HTML 요소 구문을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-144">Components can include other components by declaring them using HTML element syntax.</span></span> <span data-ttu-id="f9057-145">구성 요소 사용을 위한 태그는 태그 이름이 구성 요소 유형인 HTML 태그처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-145">The markup for using a component looks like an HTML tag where the name of the tag is the component type.</span></span>

<span data-ttu-id="f9057-146">다음 태그를 렌더링 한 `HeadingComponent` (*HeadingComponent.cshtml*) 인스턴스:</span><span class="sxs-lookup"><span data-stu-id="f9057-146">The following markup renders a `HeadingComponent` (*HeadingComponent.cshtml*) instance:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/Index.cshtml?name=snippet_HeadingComponent)]

## <a name="component-parameters"></a><span data-ttu-id="f9057-147">구성 요소 매개 변수</span><span class="sxs-lookup"><span data-stu-id="f9057-147">Component parameters</span></span>

<span data-ttu-id="f9057-148">구성 요소를 가질 수 있습니다 *구성 요소 매개 변수*를 사용 하 여 정의 된 *public이 아닌* 구성 요소 클래스의 속성으로 데코 레이트 `[Parameter]`합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-148">Components can have *component parameters*, which are defined using *non-public* properties on the component class decorated with `[Parameter]`.</span></span> <span data-ttu-id="f9057-149">특성을 사용하여 태그에서 구성 요소의 인수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-149">Use attributes to specify arguments for a component in markup.</span></span>

<span data-ttu-id="f9057-150">다음 예에서 `ParentComponent` 의 값을 설정 합니다 `Title` 의 속성을 `ChildComponent`:</span><span class="sxs-lookup"><span data-stu-id="f9057-150">In the following example, the `ParentComponent` sets the value of the `Title` property of the `ChildComponent`:</span></span>

<span data-ttu-id="f9057-151">*ParentComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f9057-151">*ParentComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ParentComponent.cshtml?name=snippet_ParentComponent&highlight=5)]

<span data-ttu-id="f9057-152">*ChildComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f9057-152">*ChildComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ChildComponent.cshtml?highlight=7-8)]

## <a name="child-content"></a><span data-ttu-id="f9057-153">자식 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="f9057-153">Child content</span></span>

<span data-ttu-id="f9057-154">구성 요소는 다른 구성 요소의 콘텐츠를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-154">Components can set the content of another component.</span></span> <span data-ttu-id="f9057-155">할당의 수신 구성 요소를 지정 하는 태그 사이 있는 내용을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-155">The assigning component provides the content between the tags that specify the receiving component.</span></span> <span data-ttu-id="f9057-156">예를 들어, 한 `ParentComponent` 여 제공할 수 있습니다 콘텐츠 렌더링에 대 한 하위 구성 요소 내에서 콘텐츠를 배치 하 여 `<ChildComponent>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-156">For example, a `ParentComponent` can provide content for rendering by a Child component by placing the content inside `<ChildComponent>` tags.</span></span>

<span data-ttu-id="f9057-157">*ParentComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f9057-157">*ParentComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ParentComponent.cshtml?name=snippet_ParentComponent&highlight=6-7)]

<span data-ttu-id="f9057-158">자식 구성 요소에는 `ChildContent` 나타내는 속성을 `RenderFragment`입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-158">The Child component has a `ChildContent` property that represents a `RenderFragment`.</span></span> <span data-ttu-id="f9057-159">변수의 `ChildContent` 콘텐츠 렌더링할지 자식 요소의 태그에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-159">The value of `ChildContent` is positioned in the child component's markup where the content should be rendered.</span></span> <span data-ttu-id="f9057-160">다음 예제에서는 변수의 `ChildContent` 부모 구성 요소에서 수신 되 고 부트스트랩 패널 내에서 렌더링 `panel-body`합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-160">In the following example, the value of `ChildContent` is received from the parent component and rendered inside the Bootstrap panel's `panel-body`.</span></span>

<span data-ttu-id="f9057-161">*ChildComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f9057-161">*ChildComponent.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/ChildComponent.cshtml?highlight=3,10-11)]

> [!NOTE]
> <span data-ttu-id="f9057-162">속성 수신 합니다 `RenderFragment` 콘텐츠 이름은 `ChildContent` 규칙에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-162">The property receiving the `RenderFragment` content must be named `ChildContent` by convention.</span></span>

## <a name="data-binding"></a><span data-ttu-id="f9057-163">데이터 바인딩</span><span class="sxs-lookup"><span data-stu-id="f9057-163">Data binding</span></span>

<span data-ttu-id="f9057-164">구성 요소와 DOM 요소에 대 한 데이터 바인딩을 사용 하 여 수행 됩니다는 `bind` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-164">Data binding to both components and DOM elements is accomplished with the `bind` attribute.</span></span> <span data-ttu-id="f9057-165">다음 예제에서는 `ItalicsCheck` 속성 확인란의 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-165">The following example binds the `ItalicsCheck` property to the check box's checked state:</span></span>

```cshtml
<input type="checkbox" class="form-check-input" id="italicsCheck" 
    bind="@_italicsCheck">
```

<span data-ttu-id="f9057-166">확인란을 선택 하 고 지울, 속성의 값으로 업데이트 됩니다 `true` 고 `false`, 각각.</span><span class="sxs-lookup"><span data-stu-id="f9057-166">When the check box is selected and cleared, the property's value is updated to `true` and `false`, respectively.</span></span>

<span data-ttu-id="f9057-167">속성의 값 변경에 대 한 응답에 없는 구성 요소를 렌더링 하는 경우에 확인란 UI에서 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-167">The check box is updated in the UI only when the component is rendered, not in response to changing the property's value.</span></span> <span data-ttu-id="f9057-168">구성 요소 렌더링 이벤트 처리기 코드를 실행 한 후, 이후 속성 업데이트 UI에 즉시 반영 일반적으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-168">Since components render themselves after event handler code executes, property updates are usually reflected in the UI immediately.</span></span>

<span data-ttu-id="f9057-169">사용 하 여 `bind` 사용 하 여는 `CurrentValue` 속성 (`<input bind="@CurrentValue">`) 다음 기본적으로 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-169">Using `bind` with a `CurrentValue` property (`<input bind="@CurrentValue">`) is essentially equivalent to the following:</span></span>

```cshtml
<input value="@CurrentValue" 
    onchange="@((UIChangeEventArgs __e) => CurrentValue = __e.Value)">
```

<span data-ttu-id="f9057-170">구성 요소를 렌더링할 때 합니다 `value` 에서 가져온 입력 요소를 `CurrentValue` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-170">When the component is rendered, the `value` of the input element comes from the `CurrentValue` property.</span></span> <span data-ttu-id="f9057-171">사용자가 텍스트 상자에는 `onchange` 이벤트가 발생 및 `CurrentValue` 속성 변경 된 값으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-171">When the user types in the text box, the `onchange` event is fired and the `CurrentValue` property is set to the changed value.</span></span> <span data-ttu-id="f9057-172">사실에서 코드 생성은 조금 더 복잡 한 `bind` 형식 변환이 수행 되는 몇 가지 경우를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-172">In reality, the code generation is a little more complex because `bind` handles a few cases where type conversions are performed.</span></span> <span data-ttu-id="f9057-173">원칙적으로 `bind` 연결 된 식의 현재 값을 `value` 등록 된 처리기를 사용 하 여 특성 및 처리 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-173">In principle, `bind` associates the current value of an expression with a `value` attribute and handles changes using the registered handler.</span></span>

<span data-ttu-id="f9057-174">외에 `onchange`와 같은 다른 이벤트를 사용 하 여 속성에 바인딩할 수 있습니다 `oninput` 바인딩할 항목에 대해 더 명확히 하 여:</span><span class="sxs-lookup"><span data-stu-id="f9057-174">In addition to `onchange`, the property can be bound using other events like `oninput` by being more explicit about what to bind to:</span></span>

```cshtml
<input type="text" bind-value-oninput="@CurrentValue">
```

<span data-ttu-id="f9057-175">와 달리 `onchange`, `oninput` 텍스트 상자에 입력 된 모든 문자에 대해 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-175">Unlike `onchange`, `oninput` fires for every character that is input into the text box.</span></span>

**<span data-ttu-id="f9057-176">형식 문자열</span><span class="sxs-lookup"><span data-stu-id="f9057-176">Format strings</span></span>**

<span data-ttu-id="f9057-177">데이터 바인딩을 사용 하 여 작동 <xref:System.DateTime> 형식 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-177">Data binding works with <xref:System.DateTime> format strings.</span></span> <span data-ttu-id="f9057-178">이 이번에 통화 또는 숫자 형식과 같은 다른 형식으로 식을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-178">Other format expressions, such as currency or number formats, aren't available at this time.</span></span>

```cshtml
<input bind="@StartDate" format-value="yyyy-MM-dd">

@functions {
    [Parameter]
    private DateTime StartDate { get; set; } = new DateTime(2020, 1, 1);
}
```

<span data-ttu-id="f9057-179">`format-value` 특성을 적용할 날짜 형식을 지정 합니다 `value` 의 `input` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-179">The `format-value` attribute specifies the date format to apply to the `value` of the `input` element.</span></span> <span data-ttu-id="f9057-180">형식 값을 구문 분석 하는 또한 때는 `onchange` 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-180">The format is also used to parse the value when an `onchange` event occurs.</span></span>

**<span data-ttu-id="f9057-181">구성 요소 매개 변수</span><span class="sxs-lookup"><span data-stu-id="f9057-181">Component parameters</span></span>**

<span data-ttu-id="f9057-182">바인딩 구성 요소 매개 변수를 인식 여기서 `bind-{property}` 구성 요소에서 속성 값을 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-182">Binding also recognizes component parameters, where `bind-{property}` can bind a property value across components.</span></span>

<span data-ttu-id="f9057-183">다음 구성 요소에서는 `ChildComponent` 바인딩합니다 합니다 `ParentYear` 부모에서 매개 변수는 `Year` 자식 구성 요소에 대 한 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="f9057-183">The following component uses `ChildComponent` and binds the `ParentYear` parameter from the parent to the `Year` parameter on the child component:</span></span>

<span data-ttu-id="f9057-184">부모 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-184">Parent component:</span></span>

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

<span data-ttu-id="f9057-185">자식 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-185">Child component:</span></span>

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

<span data-ttu-id="f9057-186">로드 된 `ParentComponent` 다음 태그를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-186">Loading the `ParentComponent` produces the following markup:</span></span>

```html
<h1>Parent Component</h1>

<p>ParentYear: 1978</p>

<h2>Child Component</h2>

<p>Year: 1978</p>
```

<span data-ttu-id="f9057-187">경우의 값을 `ParentYear` 에서 단추를 선택 하 여 속성이 변경 될를 `ParentComponent`, `Year` 의 속성은 `ChildComponent` 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-187">If the value of the `ParentYear` property is changed by selecting the button in the `ParentComponent`, the `Year` property of the `ChildComponent` is updated.</span></span> <span data-ttu-id="f9057-188">새 값 `Year` UI에서 렌더링 될 때를 `ParentComponent` 렌더링은:</span><span class="sxs-lookup"><span data-stu-id="f9057-188">The new value of `Year` is rendered in the UI when the `ParentComponent` is rerendered:</span></span>

```html
<h1>Parent Component</h1>

<p>ParentYear: 1986</p>

<h2>Child Component</h2>

<p>Year: 1986</p>
```

<span data-ttu-id="f9057-189">`Year` 동반 있기 때문에 매개 변수를 바인딩할 수 `YearChanged` 유형과 일치 하는 이벤트를 `Year` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-189">The `Year` parameter is bindable because it has a companion `YearChanged` event that matches the type of the `Year` parameter.</span></span>

<span data-ttu-id="f9057-190">규칙에 따라 `<ChildComponent bind-Year="@ParentYear" />` 기본적으로 해당 문서를 작성 하는</span><span class="sxs-lookup"><span data-stu-id="f9057-190">By convention, `<ChildComponent bind-Year="@ParentYear" />` is essentially equivalent to writing,</span></span>

```cshtml
    <ChildComponent bind-Year-YearChanged="@ParentYear" />
```

<span data-ttu-id="f9057-191">속성을 사용 하 여 해당 이벤트 처리기는 일반적으로 바인딩될 수 `bind-property-event` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-191">In general, a property can be bound to a corresponding event handler using `bind-property-event` attribute.</span></span>

## <a name="event-handling"></a><span data-ttu-id="f9057-192">이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="f9057-192">Event handling</span></span>

<span data-ttu-id="f9057-193">Razor 구성 요소는 이벤트 처리 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-193">Razor Components provide event handling features.</span></span> <span data-ttu-id="f9057-194">HTML 요소 특성에 대 한 명명 된 `on<event>` (예를 들어 `onclick`, `onsubmit`) 대리자 형식의 값을 사용 하 여 Razor 구성 요소는 이벤트 처리기로 특성의 값을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-194">For an HTML element attribute named `on<event>` (for example, `onclick`, `onsubmit`) with a delegate-typed value, Razor Components treats the attribute's value as an event handler.</span></span> <span data-ttu-id="f9057-195">특성의 이름이 항상 시작 `on`합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-195">The attribute's name always starts with `on`.</span></span>

<span data-ttu-id="f9057-196">다음 코드는 호출 된 `UpdateHeading` 메서드 UI의 단추를 선택한 경우:</span><span class="sxs-lookup"><span data-stu-id="f9057-196">The following code calls the `UpdateHeading` method when the button is selected in the UI:</span></span>

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

<span data-ttu-id="f9057-197">다음 코드는 호출 된 `CheckboxChanged` 확인란 UI에서 변경 되 면 메서드:</span><span class="sxs-lookup"><span data-stu-id="f9057-197">The following code calls the `CheckboxChanged` method when the check box is changed in the UI:</span></span>

```cshtml
<input type="checkbox" class="form-check-input" onchange="@CheckboxChanged">

@functions {
    private void CheckboxChanged()
    {
        ...
    }
}
```

<span data-ttu-id="f9057-198">이벤트 처리기는 비동기 및 반환 될 수도 있습니다는 <xref:System.Threading.Tasks.Task>합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-198">Event handlers can also be asynchronous and return a <xref:System.Threading.Tasks.Task>.</span></span> <span data-ttu-id="f9057-199">수동으로 호출할 필요가 없습니다 `StateHasChanged()`합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-199">There's no need to manually call `StateHasChanged()`.</span></span> <span data-ttu-id="f9057-200">예외가 발생할 때 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-200">Exceptions are logged when they occur.</span></span>

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

<span data-ttu-id="f9057-201">일부 이벤트에 대 한 이벤트 관련 이벤트 인수 형식은 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-201">For some events, event-specific event argument types are permitted.</span></span> <span data-ttu-id="f9057-202">이러한 이벤트 유형 중 하나에 대 한 액세스 필요 없으면 그럴 메서드 호출에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-202">If access to one of these event types isn't necessary, it isn't required in the method call.</span></span>

<span data-ttu-id="f9057-203">지원 되는 이벤트 인수의 목록이입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-203">The list of supported event arguments is:</span></span>

* <span data-ttu-id="f9057-204">UIEventArgs</span><span class="sxs-lookup"><span data-stu-id="f9057-204">UIEventArgs</span></span>
* <span data-ttu-id="f9057-205">UIChangeEventArgs</span><span class="sxs-lookup"><span data-stu-id="f9057-205">UIChangeEventArgs</span></span>
* <span data-ttu-id="f9057-206">UIKeyboardEventArgs</span><span class="sxs-lookup"><span data-stu-id="f9057-206">UIKeyboardEventArgs</span></span>
* <span data-ttu-id="f9057-207">UIMouseEventArgs</span><span class="sxs-lookup"><span data-stu-id="f9057-207">UIMouseEventArgs</span></span>

<span data-ttu-id="f9057-208">람다 식을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-208">Lambda expressions can also be used:</span></span>

```cshtml
<button onclick="@(e => Console.WriteLine("Hello, world!"))">Say hello</button>
```

<span data-ttu-id="f9057-209">와 같은 추가 값에 대해 닫기 하면 편리한 경우가 요소의 집합을 반복 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="f9057-209">It's often convenient to close over additional values, such as when iterating over a set of elements.</span></span> <span data-ttu-id="f9057-210">다음 예제에서는 세 개의 단추를 호출 하는 각 `UpdateHeading` 이벤트 인수를 전달 (`UIMouseEventArgs`) 단추 번호 (`buttonNumber`) UI에서 선택한 경우:</span><span class="sxs-lookup"><span data-stu-id="f9057-210">The following example creates three buttons, each of which calls `UpdateHeading` passing an event argument (`UIMouseEventArgs`) and its button number (`buttonNumber`) when selected in the UI:</span></span>

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
> <span data-ttu-id="f9057-211">수행 **되지** 루프 변수를 사용 하 여 (`i`)에 `for` 람다 식에 직접 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-211">Do **not** use the loop variable (`i`) in a `for` loop directly in a lambda expression.</span></span> <span data-ttu-id="f9057-212">그렇지 않으면 같은 변수 발생 하는 모든 람다 식에 의해 사용 됩니다 `i`의 모든 람다 식에서 동일한 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-212">Otherwise the same variable is used by all lambda expressions causing `i`'s value to be the same in all lambdas.</span></span> <span data-ttu-id="f9057-213">지역 변수에 해당 값을 항상 캡처하지 (`buttonNumber` 앞의 예제에서) 다음 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-213">Always capture its value in a local variable (`buttonNumber` in the preceding example) and then use it.</span></span>

## <a name="capture-references-to-components"></a><span data-ttu-id="f9057-214">구성 요소에 대 한 참조를 캡처</span><span class="sxs-lookup"><span data-stu-id="f9057-214">Capture references to components</span></span>

<span data-ttu-id="f9057-215">구성 요소 참조를 가져올 참조를 제공할 구성 요소 인스턴스를 해당 인스턴스를 같은 명령을 실행할 수 있도록 `Show` 또는 `Reset`합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-215">Component references provide a way get a reference to a component instance so that you can issue commands to that instance, such as `Show` or `Reset`.</span></span> <span data-ttu-id="f9057-216">추가 구성 요소 참조를 캡처하려면는 `ref` 자식 구성 요소에 특성 및 다음 하위 구성 요소와 동일한 이름과 동일한 형식을 사용 하 여 필드를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-216">To capture a component reference, add a `ref` attribute to the child component and then define a field with the same name and the same type as the child component.</span></span>

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

<span data-ttu-id="f9057-217">구성 요소를 렌더링할 때 합니다 `loginDialog` 필드가 채워집니다는 `MyLoginDialog` 자식 구성 요소 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="f9057-217">When the component is rendered, the `loginDialog` field is populated with the `MyLoginDialog` child component instance.</span></span> <span data-ttu-id="f9057-218">다음 구성 요소 인스턴스에 대 한.NET 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-218">You can then invoke .NET methods on the component instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9057-219">합니다 `loginDialog` 변수는 구성 요소에서 렌더링 되 고 해당 출력을 포함 한 후에 채워집니다는 `MyLoginDialog` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-219">The `loginDialog` variable is only populated after the component is rendered and its output includes the `MyLoginDialog` element.</span></span> <span data-ttu-id="f9057-220">그때까지 참조할 것이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-220">Until that point, there's nothing to reference.</span></span> <span data-ttu-id="f9057-221">구성 요소 렌더링을 마친 후 구성 요소 참조를 조작 하려면 사용 합니다 `OnAfterRenderAsync` 또는 `OnAfterRender` 메서드.</span><span class="sxs-lookup"><span data-stu-id="f9057-221">To manipulate components references after the component has finished rendering, use the `OnAfterRenderAsync` or `OnAfterRender` methods.</span></span>

<span data-ttu-id="f9057-222">하는 유사한 구문을 사용 하 여 구성 요소 참조를 캡처하는 동안 [요소 참조를 캡처](xref:razor-components/javascript-interop#capture-references-to-elements), 되어 있지는 [JavaScript interop](xref:razor-components/javascript-interop) 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-222">While capturing component references uses a similar syntax to [capturing element references](xref:razor-components/javascript-interop#capture-references-to-elements), it isn't a [JavaScript interop](xref:razor-components/javascript-interop) feature.</span></span> <span data-ttu-id="f9057-223">JavaScript 코드에 전달 된 구성 요소 참조 되지 않습니다. 해당 하는.NET 코드에만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-223">Component references aren't passed to JavaScript code; they're only used in .NET code.</span></span>

> [!NOTE]
> <span data-ttu-id="f9057-224">수행할 **되지** 자식 구성 요소의 상태를 변경할 구성 요소 참조를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-224">Do **not** use component references to mutate the state of child components.</span></span> <span data-ttu-id="f9057-225">대신, 자식 구성 요소에 데이터를 전달할 일반 선언적 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-225">Instead, use normal declarative parameters to pass data to child components.</span></span> <span data-ttu-id="f9057-226">이렇게 하면 정확한 시간에 자동으로 렌더링할 자식 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-226">This causes child components to rerender at the correct times automatically.</span></span>

## <a name="lifecycle-methods"></a><span data-ttu-id="f9057-227">수명 주기 메서드</span><span class="sxs-lookup"><span data-stu-id="f9057-227">Lifecycle methods</span></span>

`OnInitAsync` <span data-ttu-id="f9057-228">및 `OnInit` 구성 요소를 초기화 하는 코드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-228">and `OnInit` execute code to initialize the component.</span></span> <span data-ttu-id="f9057-229">비동기 작업을 수행 하려면 사용할 `OnInitAsync` 하며 `await` 작업 키워드:</span><span class="sxs-lookup"><span data-stu-id="f9057-229">To perform an asynchronous operation, use `OnInitAsync` and the `await` keyword on the operation:</span></span>

```csharp
protected override async Task OnInitAsync()
{
    await ...
}
```

<span data-ttu-id="f9057-230">동기 작업을 사용 하 여 `OnInit`:</span><span class="sxs-lookup"><span data-stu-id="f9057-230">For a synchronous operation, use `OnInit`:</span></span>

```csharp
protected override void OnInit()
{
    ...
}
```

`OnParametersSetAsync` <span data-ttu-id="f9057-231">및 `OnParametersSet` 구성 요소를 부모에서 매개 변수를 수신 했 고 값 속성에 할당 된 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-231">and `OnParametersSet` are called when a component has received parameters from its parent and the values are assigned to properties.</span></span> <span data-ttu-id="f9057-232">이러한 메서드는 구성 요소를 초기화 한 후 실행 하 고 때마다 구성 요소는 렌더링 후:</span><span class="sxs-lookup"><span data-stu-id="f9057-232">These methods are executed after component initialization and then each time the component is rendered:</span></span>

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

`OnAfterRenderAsync` <span data-ttu-id="f9057-233">및 `OnAfterRender` 구성 요소는 렌더링을 완료 된 후 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-233">and `OnAfterRender` are called after a component has finished rendering.</span></span> <span data-ttu-id="f9057-234">요소 및 구성 요소에 대 한 참조에 대 한 연결이 시점에서 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-234">Element and component references are populated at this point.</span></span> <span data-ttu-id="f9057-235">이 단계를 사용 하 여 렌더링 된 DOM 요소에서 작동 하는 타사 JavaScript 라이브러리를 활성화 하는 등의 렌더링된 된 콘텐츠를 사용 하 여 추가 초기화 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-235">Use this stage to perform additional initialization steps using the rendered content, such as activating third-party JavaScript libraries that operate on the rendered DOM elements.</span></span>

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

`SetParameters` <span data-ttu-id="f9057-236">매개 변수를 설정 하기 전에 코드를 실행 하 여 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-236">can be overridden to execute code before parameters are set:</span></span>

```csharp
public override void SetParameters(ParameterCollection parameters)
{
    ...

    base.SetParameters(parameters);
}
```

<span data-ttu-id="f9057-237">경우 `base.SetParameters` 되지 호출 사용자 지정 코드를 해석할 수 있는 방식으로 필요한 들어오는 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-237">If `base.SetParameters` isn't invoked, the custom code can interpret the incoming parameters value in any way required.</span></span> <span data-ttu-id="f9057-238">예를 들어, 들어오는 매개 변수는 클래스의 속성에 할당할 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-238">For example, the incoming parameters aren't required to be assigned to the properties on the class.</span></span>

`ShouldRender` <span data-ttu-id="f9057-239">ui 새로 고침 표시 하지 않으려면 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-239">can be overridden to suppress refreshing of the UI.</span></span> <span data-ttu-id="f9057-240">구현을 반환 하는 경우 `true`, UI 새로 고쳐집니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-240">If the implementation returns `true`, the UI is refreshed.</span></span> <span data-ttu-id="f9057-241">경우에 `ShouldRender` 는 재정의 된 구성 요소는 항상 처음 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-241">Even if `ShouldRender` is overridden, the component is always initially rendered.</span></span>

```csharp
protected override bool ShouldRender()
{
    var renderUI = true;

    return renderUI;
}
```

## <a name="component-disposal-with-idisposable"></a><span data-ttu-id="f9057-242">IDisposable 사용 하 여 구성 요소 삭제</span><span class="sxs-lookup"><span data-stu-id="f9057-242">Component disposal with IDisposable</span></span>

<span data-ttu-id="f9057-243">구성 요소를 구현 하는 경우 <xref:System.IDisposable>서 [Dispose 메서드](/dotnet/standard/garbage-collection/implementing-dispose) UI에서 구성 요소가 제거 될 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-243">If a component implements <xref:System.IDisposable>, the [Dispose method](/dotnet/standard/garbage-collection/implementing-dispose) is called when the component is removed from the UI.</span></span> <span data-ttu-id="f9057-244">다음 구성 요소 `@implements IDisposable` 하며 `Dispose` 메서드:</span><span class="sxs-lookup"><span data-stu-id="f9057-244">The following component uses `@implements IDisposable` and the `Dispose` method:</span></span>

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

## <a name="routing"></a><span data-ttu-id="f9057-245">라우팅</span><span class="sxs-lookup"><span data-stu-id="f9057-245">Routing</span></span>

<span data-ttu-id="f9057-246">라우팅 Razor 구성 요소에는 앱에서 액세스할 수 있는 각 구성 요소에 경로 템플릿을 제공 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-246">Routing in Razor Components is achieved by providing a route template to each accessible component in the app.</span></span>

<span data-ttu-id="f9057-247">때를 *.cshtml* 파일을 `@page` 지시문 컴파일됩니다, 생성된 된 클래스는 지정 된을 <xref:Microsoft.AspNetCore.Mvc.RouteAttribute> 경로 템플릿을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-247">When a *.cshtml* file with an `@page` directive is compiled, the generated class is given a <xref:Microsoft.AspNetCore.Mvc.RouteAttribute> specifying the route template.</span></span> <span data-ttu-id="f9057-248">런타임 시 사용 하 여 구성 요소 클래스에 대 한 라우터 찾습니다는 `RouteAttribute` 하 고 어떤 구성 요소는 요청 된 URL과 일치 하는 경로 템플릿을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-248">At runtime, the router looks for component classes with a `RouteAttribute` and renders whichever component has a route template that matches the requested URL.</span></span>

<span data-ttu-id="f9057-249">여러 경로 템플릿 구성 요소에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-249">Multiple route templates can be applied to a component.</span></span> <span data-ttu-id="f9057-250">다음 구성 요소에 대 한 요청에 응답할 `/BlazorRoute` 고 `/DifferentBlazorRoute`:</span><span class="sxs-lookup"><span data-stu-id="f9057-250">The following component responds to requests for `/BlazorRoute` and `/DifferentBlazorRoute`:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRoute.cshtml?name=snippet_BlazorRoute)]

## <a name="route-parameters"></a><span data-ttu-id="f9057-251">경로 매개 변수</span><span class="sxs-lookup"><span data-stu-id="f9057-251">Route parameters</span></span>

<span data-ttu-id="f9057-252">구성 요소에 제공 된 경로 템플릿에서 경로 매개 변수를 받을 수는 `@page` 지시문입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-252">Components can receive route parameters from the route template provided in the `@page` directive.</span></span> <span data-ttu-id="f9057-253">라우터 경로 매개 변수를 사용 하 여 해당 구성 요소 매개 변수를 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-253">The router uses route parameters to populate the corresponding component parameters.</span></span>

<span data-ttu-id="f9057-254">*RouteParameter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f9057-254">*RouteParameter.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/RouteParameter.cshtml?name=snippet_RouteParameter)]

<span data-ttu-id="f9057-255">선택적 매개 변수 지원 되지 않으며, 따라서 두 `@page` 지시문 위의 예제에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-255">Optional parameters aren't supported, so two `@page` directives are applied in the example above.</span></span> <span data-ttu-id="f9057-256">첫 번째 매개 변수 없이 구성 요소에 대 한 탐색을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-256">The first permits navigation to the component without a parameter.</span></span> <span data-ttu-id="f9057-257">두 번째 `@page` 지시문은 합니다 `{text}` 경로 매개 변수 및 값을 할당 합니다 `Text` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-257">The second `@page` directive takes the `{text}` route parameter and assigns the value to the `Text` property.</span></span>

## <a name="base-class-inheritance-for-a-code-behind-experience"></a><span data-ttu-id="f9057-258">"코드 숨김" 환경에 대 한 기본 클래스 상속</span><span class="sxs-lookup"><span data-stu-id="f9057-258">Base class inheritance for a "code-behind" experience</span></span>

<span data-ttu-id="f9057-259">구성 요소 파일 (*.cshtml*) HTML 태그를 혼합 하 고 C# 같은 파일에서 코드를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-259">Component files (*.cshtml*) mix HTML markup and C# processing code in the same file.</span></span> <span data-ttu-id="f9057-260">`@inherits` Razor 구성 요소 앱 구성 요소 태그 처리 코드와 분리 하는 "코드 숨김" 환경을 제공할 수 지시문을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-260">The `@inherits` directive can be used to provide Razor Components apps with a "code-behind" experience that separates component markup from processing code.</span></span>

<span data-ttu-id="f9057-261">[샘플 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) 구성 요소는 기본 클래스를 상속할 수 있습니다 하는 방법을 보여 줍니다. `BlazorRocksBase`, 구성 요소의 속성과 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-261">The [sample app](https://github.com/aspnet/Docs/tree/master/aspnetcore/razor-components/common/samples/) shows how a component can inherit a base class, `BlazorRocksBase`, to provide the component's properties and methods.</span></span>

<span data-ttu-id="f9057-262">*BlazorRocks.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f9057-262">*BlazorRocks.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/BlazorRocks.cshtml?name=snippet_BlazorRocks)]

<span data-ttu-id="f9057-263">*BlazorRocksBase.cs*:</span><span class="sxs-lookup"><span data-stu-id="f9057-263">*BlazorRocksBase.cs*:</span></span>

[!code-csharp[](common/samples/3.x/BlazorSample/Pages/BlazorRocksBase.cs)]

<span data-ttu-id="f9057-264">기본 클래스에서 파생 되어야 `ComponentBase`합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-264">The base class should derive from `ComponentBase`.</span></span>

## <a name="razor-support"></a><span data-ttu-id="f9057-265">Razor 지원</span><span class="sxs-lookup"><span data-stu-id="f9057-265">Razor support</span></span>

**<span data-ttu-id="f9057-266">Razor 지시문</span><span class="sxs-lookup"><span data-stu-id="f9057-266">Razor directives</span></span>**

<span data-ttu-id="f9057-267">Razor 지시문은 다음 표에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-267">Razor directives are shown in the following table.</span></span>

| <span data-ttu-id="f9057-268">지시문</span><span class="sxs-lookup"><span data-stu-id="f9057-268">Directive</span></span> | <span data-ttu-id="f9057-269">설명</span><span class="sxs-lookup"><span data-stu-id="f9057-269">Description</span></span> |
| --------- | ----------- |
| [<span data-ttu-id="f9057-270">\@functions</span><span class="sxs-lookup"><span data-stu-id="f9057-270">\@functions</span></span>](xref:mvc/views/razor#section-5) | <span data-ttu-id="f9057-271">추가 된 C# 구성 요소에 대 한 코드 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-271">Adds a C# code block to a component.</span></span> |
| `@implements` | <span data-ttu-id="f9057-272">생성 된 구성 요소 클래스에 대 한 인터페이스를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-272">Implements an interface for the generated component class.</span></span> |
| [<span data-ttu-id="f9057-273">\@상속</span><span class="sxs-lookup"><span data-stu-id="f9057-273">\@inherits</span></span>](xref:mvc/views/razor#section-3) | <span data-ttu-id="f9057-274">구성 요소가 상속 된 클래스의 모든 권한을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-274">Provides full control of the class that the component inherits.</span></span> |
| [<span data-ttu-id="f9057-275">\@삽입</span><span class="sxs-lookup"><span data-stu-id="f9057-275">\@inject</span></span>](xref:mvc/views/razor#section-4) | <span data-ttu-id="f9057-276">서비스에서 주입 수 있도록 합니다 [서비스 컨테이너](xref:fundamentals/dependency-injection)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-276">Enables service injection from the [service container](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="f9057-277">자세한 내용은 [보기에 종속성 주입](xref:mvc/views/dependency-injection)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f9057-277">For more information, see [Dependency injection into views](xref:mvc/views/dependency-injection).</span></span> |
| `@layout` | <span data-ttu-id="f9057-278">레이아웃 구성 요소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-278">Specifies a layout component.</span></span> <span data-ttu-id="f9057-279">레이아웃 구성 요소 코드 중복 및 불일치를 방지 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-279">Layout components are used to avoid code duplication and inconsistency.</span></span> |
| [<span data-ttu-id="f9057-280">\@page</span><span class="sxs-lookup"><span data-stu-id="f9057-280">\@page</span></span>](xref:razor-pages/index#razor-pages) | <span data-ttu-id="f9057-281">구성 요소가 요청을 직접 처리 해야 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-281">Specifies that the component should handle requests directly.</span></span> <span data-ttu-id="f9057-282">`@page` 경로 및 선택적 매개 변수를 사용 하 여 지시문을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-282">The `@page` directive can be specified with a route and optional parameters.</span></span> <span data-ttu-id="f9057-283">Razor 페이지와 달리는 `@page` 지시문 파일의 맨 위에 있는 첫 번째 지시문을 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-283">Unlike Razor Pages, the `@page` directive doesn't need to be the first directive at the top of the file.</span></span> <span data-ttu-id="f9057-284">자세한 내용은 [라우팅](xref:razor-components/routing)을 참고하시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-284">For more information, see [Routing](xref:razor-components/routing).</span></span> |
| [<span data-ttu-id="f9057-285">\@using</span><span class="sxs-lookup"><span data-stu-id="f9057-285">\@using</span></span>](xref:mvc/views/razor#using) | <span data-ttu-id="f9057-286">추가 된 C# `using` 지시문을 생성 된 구성 요소 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-286">Adds the C# `using` directive to the generated component class.</span></span> |
| [<span data-ttu-id="f9057-287">\@addTagHelper</span><span class="sxs-lookup"><span data-stu-id="f9057-287">\@addTagHelper</span></span>](xref:mvc/views/razor#tag-helpers) | <span data-ttu-id="f9057-288">사용 하 여 `@addTagHelper` 앱의 어셈블리 보다 다른 어셈블리의 구성 요소를 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-288">Use `@addTagHelper` to use a component in a different assembly than the app's assembly.</span></span> |

**<span data-ttu-id="f9057-289">조건부 특성</span><span class="sxs-lookup"><span data-stu-id="f9057-289">Conditional attributes</span></span>**

<span data-ttu-id="f9057-290">특성은.NET 값에 따라 조건부로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-290">Attributes are conditionally rendered based on the .NET value.</span></span> <span data-ttu-id="f9057-291">값이 `false` 또는 `null`, 특성 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-291">If the value is `false` or `null`,  the attribute isn't rendered.</span></span> <span data-ttu-id="f9057-292">값이 `true`, 특성이 렌더링 되 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-292">If the value is `true`, the attribute is rendered minimized.</span></span>

<span data-ttu-id="f9057-293">다음 예에서 `IsCompleted` 있는지 여부를 확인 `checked` 컨트롤의 태그 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-293">In the following example, `IsCompleted` determines if `checked` is rendered in the control's markup:</span></span>

```cshtml
<input type="checkbox" checked="@IsCompleted">

@functions {
    [Parameter]
    private bool IsCompleted { get; set; }
}
```

<span data-ttu-id="f9057-294">하는 경우 `IsCompleted` 는 `true`, 확인란으로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-294">If `IsCompleted` is `true`, the check box is rendered as:</span></span>

```html
<input type="checkbox" checked>
```

<span data-ttu-id="f9057-295">하는 경우 `IsCompleted` 는 `false`, 확인란으로 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-295">If `IsCompleted` is `false`, the check box is rendered as:</span></span>

```html
<input type="checkbox">
```

**<span data-ttu-id="f9057-296">Razor에 대 한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="f9057-296">Additional information on Razor</span></span>**

<span data-ttu-id="f9057-297">Razor에 대 한 자세한 내용은 참조는 [Razor 구문 참조](xref:mvc/views/razor)합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-297">For more information on Razor, see the [Razor syntax reference](xref:mvc/views/razor).</span></span>

## <a name="raw-html"></a><span data-ttu-id="f9057-298">원시 HTML</span><span class="sxs-lookup"><span data-stu-id="f9057-298">Raw HTML</span></span>

<span data-ttu-id="f9057-299">문자열은 일반적으로 렌더링 됩니다 DOM 텍스트 노드를 사용 하 여 포함할 수 있는 태그는 무시 되 고 리터럴 텍스트로 처리 하는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-299">Strings are normally rendered using DOM text nodes, which means that any markup they may contain is ignored and treated as literal text.</span></span> <span data-ttu-id="f9057-300">원시 HTML을 렌더링 하에 HTML 콘텐츠를 래핑하는 `MarkupString` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-300">To render raw HTML, wrap the HTML content in a `MarkupString` value.</span></span> <span data-ttu-id="f9057-301">값이 HTML 또는 SVG로 구문 분석 하 고 DOM에 삽입</span><span class="sxs-lookup"><span data-stu-id="f9057-301">The value is parsed as HTML or SVG and inserted into the DOM.</span></span>

> [!WARNING]
> <span data-ttu-id="f9057-302">소스는 신뢰할 수 없는 원시 HTML에서 생성 된 렌더링을 **보안 위험** 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-302">Rendering raw HTML constructed from any untrusted source is a **security risk** and should be avoided!</span></span>

<span data-ttu-id="f9057-303">다음 예제에서는 사용 하 여는 `MarkupString` 요소의 렌더링 된 출력은 정적 HTML 콘텐츠 블록을 추가할 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-303">The following example shows using the `MarkupString` type to add a block of static HTML content to the rendered output of a component:</span></span>

```html
@((MarkupString)myMarkup)

@functions {
    private string myMarkup = 
        "<p class='markup'>This is a <em>markup string</em>.</p>";
}
```

## <a name="templated-components"></a><span data-ttu-id="f9057-304">템플릿 기반 구성 요소</span><span class="sxs-lookup"><span data-stu-id="f9057-304">Templated components</span></span>

<span data-ttu-id="f9057-305">템플릿 기반 구성 요소는 하나 이상의 UI 템플릿 요소의 렌더링 논리의 일부로 사용할 수 있는 매개 변수로 허용 하는 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-305">Templated components are components that accept one or more UI templates as parameters, which can then be used as part of the component's rendering logic.</span></span> <span data-ttu-id="f9057-306">템플릿 기반 구성 요소를 사용 하 여 일반 구성 요소 보다 더 다시 사용할 수 있는 더 높은 수준의 구성 요소를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-306">Templated components allow you to author higher-level components that are more reusable than regular components.</span></span> <span data-ttu-id="f9057-307">몇 가지 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-307">A couple of examples include:</span></span>

* <span data-ttu-id="f9057-308">테이블의 머리글, 행 및 바닥글에 대 한 템플릿을 지정할 수 있도록 허용 하는 테이블 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-308">A table component that allows a user to specify templates for the table's header, rows, and footer.</span></span>
* <span data-ttu-id="f9057-309">사용자가 목록에 항목 렌더링에 대 한 템플릿을 지정할 수 있도록 목록 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-309">A list component that allows a user to specify a template for rendering items in a list.</span></span>

### <a name="template-parameters"></a><span data-ttu-id="f9057-310">템플릿 매개 변수</span><span class="sxs-lookup"><span data-stu-id="f9057-310">Template parameters</span></span>

<span data-ttu-id="f9057-311">템플릿 기반 구성 요소 형식의 하나 이상의 구성 요소 매개 변수를 지정 하 여 정의 됩니다 `RenderFragment` 또는 `RenderFragment<T>`합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-311">A templated component is defined by specifying one or more component parameters of type `RenderFragment` or `RenderFragment<T>`.</span></span> <span data-ttu-id="f9057-312">렌더링 조각 구성 요소에 의해 렌더링 되는 UI의 세그먼트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-312">A render fragment represents a segment of UI that is rendered by the component.</span></span> <span data-ttu-id="f9057-313">필요에 따라 렌더링 조각 렌더링 조각 호출 될 때 지정 될 수 있는 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-313">A render fragment optionally takes a parameter that can be specified when the render fragment is invoked.</span></span>

<span data-ttu-id="f9057-314">*Components/TableTemplate.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f9057-314">*Components/TableTemplate.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/TableTemplate.cshtml)]

<span data-ttu-id="f9057-315">템플릿 기반 구성 요소를 사용 하는 경우 템플릿 매개 변수를 지정할 수 있습니다 매개 변수의 이름과 일치 하는 자식 요소를 사용 하 여 (`TableHeader` 고 `RowTemplate` 다음 예제의):</span><span class="sxs-lookup"><span data-stu-id="f9057-315">When using a templated component, the template parameters can be specified using child elements that match the names of the parameters (`TableHeader` and `RowTemplate` in the following example):</span></span>

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

### <a name="template-context-parameters"></a><span data-ttu-id="f9057-316">템플릿 상황에 맞는 매개 변수</span><span class="sxs-lookup"><span data-stu-id="f9057-316">Template context parameters</span></span>

<span data-ttu-id="f9057-317">형식의 인수를 구성 요소 `RenderFragment<T>` 요소가 있는 라는 암시적 매개 변수 전달 `context` (예를 들어 위의 코드 샘플에서에서 `@context.PetId`)를 사용 하 여 매개 변수 이름을 변경할 수 있습니다는 `Context` 자식 특성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-317">Component arguments of type `RenderFragment<T>` passed as elements have an implicit parameter named `context` (for example from the preceding code sample, `@context.PetId`), but you can change the parameter name using the `Context` attribute on the child element.</span></span> <span data-ttu-id="f9057-318">다음 예제에서는 `RowTemplate` 요소의 `Context` 특성을 지정 합니다 `pet` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="f9057-318">In the following example, the `RowTemplate` element's `Context` attribute specifies the `pet` parameter:</span></span>

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

<span data-ttu-id="f9057-319">지정할 수 있습니다는 `Context` component 요소 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-319">Alternatively, you can specify the `Context` attribute on the component element.</span></span> <span data-ttu-id="f9057-320">지정 된 `Context` 특성이 지정 된 템플릿 매개 변수를 모두에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-320">The specified `Context` attribute applies to all specified template parameters.</span></span> <span data-ttu-id="f9057-321">암시적 자식 콘텐츠를 콘텐츠 매개 변수 이름을 지정 하려는 경우 유용할 수 있습니다 (모든 줄 바꿈 없이 자식 요소).</span><span class="sxs-lookup"><span data-stu-id="f9057-321">This can be useful when you want to specify the content parameter name for implicit child content (without any wrapping child element).</span></span> <span data-ttu-id="f9057-322">다음 예제에서는 `Context` 특성에 표시 되는 `TableTemplate` 요소 모든 템플릿 매개 변수를 적용:</span><span class="sxs-lookup"><span data-stu-id="f9057-322">In the following example, the `Context` attribute appears on the `TableTemplate` element and applies to all template parameters:</span></span>

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

### <a name="generic-typed-components"></a><span data-ttu-id="f9057-323">제네릭 형식의 구성 요소</span><span class="sxs-lookup"><span data-stu-id="f9057-323">Generic-typed components</span></span>

<span data-ttu-id="f9057-324">템플릿 기반 구성 요소가 일반적으로 자주 형식화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-324">Templated components are often generically typed.</span></span> <span data-ttu-id="f9057-325">렌더링 하는 제네릭 목록 보기 템플릿에서 구성 요소를 사용할 수 예를 들어 `IEnumerable<T>` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-325">For example, a generic List View Template component can be used to render `IEnumerable<T>` values.</span></span> <span data-ttu-id="f9057-326">일반 구성 요소를 정의 하기 위해 사용 하 여는 `@typeparam` 지시문 형식 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-326">To define a generic component, use the `@typeparam` directive to specify type parameters.</span></span>

<span data-ttu-id="f9057-327">*Components/ListViewTemplate.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f9057-327">*Components/ListViewTemplate.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/ListViewTemplate.cshtml)]

<span data-ttu-id="f9057-328">제네릭 형식의 구성 요소를 사용 하는 경우 형식 매개 변수에 가능한 경우 유추 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-328">When using generic-typed components, the type parameter is inferred if possible:</span></span>

```cshtml
<ListViewTemplate Items="@pets">
    <ItemTemplate Context="pet">
        <li>@pet.Name</li>
    </ItemTemplate>
</ListViewTemplate>
```

<span data-ttu-id="f9057-329">그렇지 않은 경우 형식 매개 변수 지정 되어야 합니다 명시적으로 형식 매개 변수의 이름과 일치 하는 특성을 사용 하 여.</span><span class="sxs-lookup"><span data-stu-id="f9057-329">Otherwise, the type parameter must be explicitly specified using an attribute that matches the name of the type parameter.</span></span> <span data-ttu-id="f9057-330">다음 예에서 `TItem="Pet"` 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-330">In the following example, `TItem="Pet"` specifies the type:</span></span>

```cshtml
<ListViewTemplate Items="@pets" TItem="Pet">
    <ItemTemplate Context="pet">
        <li>@pet.Name</li>
    </ItemTemplate>
</ListViewTemplate>
```

## <a name="cascading-values-and-parameters"></a><span data-ttu-id="f9057-331">연계 값 및 매개 변수</span><span class="sxs-lookup"><span data-stu-id="f9057-331">Cascading values and parameters</span></span>

<span data-ttu-id="f9057-332">일부 시나리오에서는 하기가 불편 데이터가 흐르도록 지정 하는 상위 구성 요소를 사용 하 여 하위 구성 요소에서 [구성 요소 매개 변수](#component-parameters)여러 구성 요소 계층 필요한 경우에 특히, 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-332">In some scenarios, it's inconvenient to flow data from an ancestor component to a descendent component using [component parameters](#component-parameters), especially when there are several component layers.</span></span> <span data-ttu-id="f9057-333">연계 값 및 매개 변수는 상위 구성 요소의 모든 하위 구성 요소에 값을 제공 하는 편리한 방법을 제공 하 여이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-333">Cascading values and parameters solve this problem by providing a convenient way for an ancestor component to provide a value to all of its descendent components.</span></span> <span data-ttu-id="f9057-334">연계 값 및 매개 변수 구성 요소를 조정 하는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-334">Cascading values and parameters also provide an approach for components to coordinate.</span></span>

### <a name="theme-example"></a><span data-ttu-id="f9057-335">테마 예제</span><span class="sxs-lookup"><span data-stu-id="f9057-335">Theme example</span></span>

<span data-ttu-id="f9057-336">다음과에서 *테마* 샘플 앱의 예제는 `ThemeInfo` 클래스는 동일한 스타일을 공유할 앱의 특정된 부분 내에서 단추의 모든 구성 요소 계층 구조 아래로 흐름 테마 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-336">In the following *Theme* example from the sample app, the `ThemeInfo` class specifies the theme information to flow down the component hierarchy so that all of the buttons within a given part of the app share the same style.</span></span>

<span data-ttu-id="f9057-337">*UIThemeClasses/ThemeInfo.cs*:</span><span class="sxs-lookup"><span data-stu-id="f9057-337">*UIThemeClasses/ThemeInfo.cs*:</span></span>

```csharp
public class ThemeInfo
{
    public string ButtonClass { get; set; }
}
```

<span data-ttu-id="f9057-338">상위 구성 요소를 연계 값 구성 요소를 사용 하 여 연계 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-338">An ancestor component can provide a cascading value using the Cascading Value component.</span></span> <span data-ttu-id="f9057-339">연계 값 구성 요소는 구성 요소 계층 구조의 하위 트리를 래핑하고 해당 하위 트리 내에서 모든 구성 요소에 단일 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-339">The Cascading Value component wraps a subtree of the component hierarchy and supplies a single value to all components within that subtree.</span></span>

<span data-ttu-id="f9057-340">샘플 앱에서 테마 정보를 지정 하는 예를 들어, (`ThemeInfo`)의 레이아웃 본문을 구성 하는 모든 구성 요소에 대 한 연계 매개 변수로 앱의 레이아웃 중 하나에 `@Body` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-340">For example, the sample app specifies theme information (`ThemeInfo`) in one of the app's layouts as a cascading parameter for all components that make up the layout body of the `@Body` property.</span></span> `ButtonClass` <span data-ttu-id="f9057-341">값이 할당은 `btn-success` 레이아웃 구성 요소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-341">is assigned a value of `btn-success` in the layout component.</span></span> <span data-ttu-id="f9057-342">하위 구성 요소를 통해이 속성을 사용할 수는 `ThemeInfo` 연계 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-342">Any descendent component can consume this property through the `ThemeInfo` cascading object.</span></span>

<span data-ttu-id="f9057-343">*Shared/CascadingValuesParametersLayout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f9057-343">*Shared/CascadingValuesParametersLayout.cshtml*:</span></span>

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

<span data-ttu-id="f9057-344">있도록 연계 값을 사용 하 여 연계 매개 변수를 선언 하는 구성 요소는 `[CascadingParameter]` 특성 또는 문자열 이름 값을 기준으로:</span><span class="sxs-lookup"><span data-stu-id="f9057-344">To make use of cascading values, components declare cascading parameters using the `[CascadingParameter]` attribute or based on a string name value:</span></span>

```cshtml
<CascadingValue Value=@PermInfo Name="UserPermissions">...</CascadingValue>

[CascadingParameter(Name = "UserPermissions")]
private PermInfo Permissions { get; set; }
```

<span data-ttu-id="f9057-345">문자열 이름 값을 사용 하 여 바인딩을 동일한 형식의 여러 연계 값이 있는 동일한 하위 트리 내와 구분 해야 하는 경우 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-345">Binding with a string name value is relevant if you have multiple cascading values of the same type and need to differentiate them within the same subtree.</span></span>

<span data-ttu-id="f9057-346">연계 값 형식으로 연계 매개 변수에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-346">Cascading values are bound to cascading parameters by type.</span></span>

<span data-ttu-id="f9057-347">샘플 앱에서 연계 값 매개 변수 테마 구성 요소에 바인딩하는 `ThemeInfo` 연계 연계 매개 변수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-347">In the sample app, the Cascading Values Parameters Theme component binds to the `ThemeInfo` cascading value to a cascading parameter.</span></span> <span data-ttu-id="f9057-348">매개 변수를 사용 하 여 구성 요소에 의해 표시 되는 단추 중 하나에 대 한 CSS 클래스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-348">The parameter is used to set the CSS class for one of the buttons displayed by the component.</span></span>

<span data-ttu-id="f9057-349">*Pages/CascadingValuesParametersTheme.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f9057-349">*Pages/CascadingValuesParametersTheme.cshtml*:</span></span>

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

### <a name="tabset-example"></a><span data-ttu-id="f9057-350">TabSet 예제</span><span class="sxs-lookup"><span data-stu-id="f9057-350">TabSet example</span></span>

<span data-ttu-id="f9057-351">연계 매개 변수 구성 요소 구성 요소 계층 전체에서 공동 작업을 사용 하도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-351">Cascading parameters also enable components to collaborate across the component hierarchy.</span></span> <span data-ttu-id="f9057-352">예를 들어, 다음 사항을 고려 *TabSet* 샘플 앱의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-352">For example, consider the following *TabSet* example in the sample app.</span></span>

<span data-ttu-id="f9057-353">샘플 앱에는 `ITab` 인터페이스 구현 탭입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-353">The sample app has an `ITab` interface that tabs implement:</span></span>

[!code-cs[](common/samples/3.x/BlazorSample/UIInterfaces/ITab.cs)]

<span data-ttu-id="f9057-354">값 매개 변수 TabSet 연계 구성 요소에서는 여러 탭 구성 요소를 포함 하는 탭 설정 구성:</span><span class="sxs-lookup"><span data-stu-id="f9057-354">The Cascading Values Parameters TabSet component uses the Tab Set component, which contains several Tab components:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Pages/CascadingValuesParametersTabSet.cshtml?name=snippet_TabSet)]

<span data-ttu-id="f9057-355">명시적으로 자식 탭 구성 되지 탭 설정에 매개 변수로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-355">The child Tab components aren't explicitly passed as parameters to the Tab Set.</span></span> <span data-ttu-id="f9057-356">대신, 자식 탭 구성 요소는 일부 탭 집합의 자식 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-356">Instead, the child Tab components are part of the child content of the Tab Set.</span></span> <span data-ttu-id="f9057-357">그러나 탭 설정 해야 헤더와 활성 탭을 렌더링할 수 있도록 각 탭 구성 요소에 대해 알아야 합니다. 탭 설정 구성 요소 추가 코드 없이이 조정을 사용할 수 있도록 *연계 값으로 자체를 제공할 수 있습니다* 다음 선택 하는 하위 탭 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-357">However, the Tab Set still needs to know about each Tab component so that it can render the headers and the active tab. To enable this coordination without requiring additional code, the Tab Set component *can provide itself as a cascading value* that is then picked up by the descendent Tab components.</span></span>

<span data-ttu-id="f9057-358">*Components/TabSet.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f9057-358">*Components/TabSet.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/TabSet.cshtml)]

<span data-ttu-id="f9057-359">하위 탭 구성 캡처를 연계 매개 변수로 포함 된 탭 설정 탭 구성 요소 탭 설정 및 좌표에 추가 되도록 하므로 어떤 탭에서 활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-359">The descendent Tab components capture the containing Tab Set as a cascading parameter, so the Tab components add themselves to the Tab Set and coordinate on which tab is active.</span></span>

<span data-ttu-id="f9057-360">*Components/Tab.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f9057-360">*Components/Tab.cshtml*:</span></span>

[!code-cshtml[](common/samples/3.x/BlazorSample/Components/Tab.cshtml)]

## <a name="razor-templates"></a><span data-ttu-id="f9057-361">Razor 템플릿</span><span class="sxs-lookup"><span data-stu-id="f9057-361">Razor templates</span></span>

<span data-ttu-id="f9057-362">렌더링 조각 Razor 템플릿 구문을 사용 하 여 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-362">Render fragments can be defined using Razor template syntax.</span></span> <span data-ttu-id="f9057-363">Razor 템플릿 UI 코드 조각을 정의 하 고 다음 형식으로 가정 하는 방법을 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-363">Razor templates are a way to define a UI snippet and assume the following format:</span></span>

```cshtml
@<tag>...</tag>
```

<span data-ttu-id="f9057-364">다음 예제에서는 지정 하는 방법을 보여 줍니다 `RenderFragment` 고 `RenderFragment<T>` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-364">The following example illustrates how to specify `RenderFragment` and `RenderFragment<T>` values.</span></span>

<span data-ttu-id="f9057-365">*RazorTemplates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="f9057-365">*RazorTemplates.cshtml*:</span></span>

```cshtml
@{
    RenderFragment template = @<p>The time is @DateTime.Now.</p>;
    RenderFragment<Pet> petTemplate = (pet) => @<p>Your pet's name is @pet.Name.</p>;
}
```

<span data-ttu-id="f9057-366">Razor 템플릿 템플릿 구성 요소에 인수로 전달 하거나 나중에 직접 렌더링할 수를 사용 하 여 정의 조각을 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-366">Render fragments defined using Razor templates can be passed as arguments to templated components or rendered directly.</span></span> <span data-ttu-id="f9057-367">예를 들어 이전 서식 파일에 다음 Razor 태그를 사용 하 여 직접 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-367">For example, the previous templates are directly rendered with the following Razor markup:</span></span>

```cshtml
@template

@petTemplate(new Pet { Name = "Rex" })
```

<span data-ttu-id="f9057-368">렌더링된 출력:</span><span class="sxs-lookup"><span data-stu-id="f9057-368">Rendered output:</span></span>

```
The time is 10/04/2018 01:26:52.

Your pet's name is Rex.
```

## <a name="manual-rendertreebuilder-logic"></a><span data-ttu-id="f9057-369">수동 RenderTreeBuilder 논리</span><span class="sxs-lookup"><span data-stu-id="f9057-369">Manual RenderTreeBuilder logic</span></span>

`Microsoft.AspNetCore.Components.RenderTree` <span data-ttu-id="f9057-370">구성 요소 및 구성 요소에 수동으로 빌드를 포함 하 여 요소를 조작 하기 위한 메서드를 제공 합니다. C# 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-370">provides methods for manipulating components and elements, including building components manually in C# code.</span></span>

> [!NOTE]
> <span data-ttu-id="f9057-371">사용 `RenderTreeBuilder` 은 고급 시나리오 구성 요소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-371">Use of `RenderTreeBuilder` to create components is an advanced scenario.</span></span> <span data-ttu-id="f9057-372">잘못 된 구성 요소 (예: 닫히지 않은 태그 태그) 정의 되지 않은 동작이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-372">A malformed component (for example, an unclosed markup tag) can result in undefined behavior.</span></span>

<span data-ttu-id="f9057-373">애완 동물 정보 구성 요소는 것이 좋습니다 (*PetDetails.razor* Razor 구성 요소에서 *PetDetails.cshtml* Blazor에서), 다른 구성 요소를 수동으로 빌드할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-373">Consider the following Pet Details component (*PetDetails.razor* in Razor Components; *PetDetails.cshtml* in Blazor), which can be manually built into another component:</span></span>

```cshtml
<h2>Pet Details Component</h2>

<p>@PetDetailsQuote<p>

@functions
{
    [Parameter]
    string PetDetailsQuote { get; set; }
}
```

<span data-ttu-id="f9057-374">다음 예에서 루프는 `CreateComponent` 메서드는 세 가지 애완 동물 정보 구성 요소를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-374">In the following example, the loop in the `CreateComponent` method generates three Pet Details components.</span></span> <span data-ttu-id="f9057-375">호출할 때 `RenderTreeBuilder` 구성 요소를 만드는 방법 (`OpenComponent` 고 `AddAttribute`), 시퀀스 번호는 소스 코드 줄 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-375">When calling `RenderTreeBuilder` methods to create the components (`OpenComponent` and `AddAttribute`), sequence numbers are source code line numbers.</span></span> <span data-ttu-id="f9057-376">해당 고유 줄의 코드만으로 고유 하지 하는 시퀀스 번호 차이 알고리즘은 Razor 구성 요소 호출을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-376">The Razor Components difference algorithm relies on the sequence numbers corresponding to distinct lines of code, not distinct call invocations.</span></span> <span data-ttu-id="f9057-377">구성 요소를 만들 때 `RenderTreeBuilder` 방법, 하드 코드 시퀀스 번호에 대 한 인수입니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-377">When creating a component with `RenderTreeBuilder` methods, hardcode the arguments for sequence numbers.</span></span> **<span data-ttu-id="f9057-378">시퀀스 번호를 생성 하는 계산 또는 카운터를 사용 하 여 성능이 저하 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f9057-378">Using a calculation or counter to generate the sequence number can lead to poor performance.</span></span>**

<span data-ttu-id="f9057-379">구성 요소 작성 (*BuiltContent.razor* Razor 구성 요소에서 *BuiltContent.cshtml* Blazor에서):</span><span class="sxs-lookup"><span data-stu-id="f9057-379">Built component (*BuiltContent.razor* in Razor Components; *BuiltContent.cshtml* in Blazor):</span></span>

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
