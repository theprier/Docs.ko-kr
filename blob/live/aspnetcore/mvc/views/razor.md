---
title: "ASP.NET Core에 대 한 razor 구문 참조"
author: rick-anderson
description: "웹 페이지에 서버 기반 코드를 포함 하는 것에 대 한 Razor 태그 구문에 알아봅니다."
ms.author: riande
manager: wpickett
ms.date: 10/18/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: mvc/views/razor
ms.openlocfilehash: d932e28246998c60e2b3f9c77a2521fe55991e85
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="razor-syntax-for-aspnet-core"></a><span data-ttu-id="33087-103">ASP.NET Core에 대 한 razor 구문</span><span class="sxs-lookup"><span data-stu-id="33087-103">Razor syntax for ASP.NET Core</span></span>

<span data-ttu-id="33087-104">여 [Rick Anderson](https://twitter.com/RickAndMSFT), [Luke Latham](https://github.com/guardrex), [Taylor Mullen](https://twitter.com/ntaylormullen), 및 [Dan Vicarel](https://github.com/Rabadash8820)</span><span class="sxs-lookup"><span data-stu-id="33087-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Luke Latham](https://github.com/guardrex), [Taylor Mullen](https://twitter.com/ntaylormullen), and [Dan Vicarel](https://github.com/Rabadash8820)</span></span>

<span data-ttu-id="33087-105">Razor은 웹 페이지에 서버 기반 코드를 포함 하는 것에 대 한 태그 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="33087-105">Razor is a markup syntax for embedding server-based code into webpages.</span></span> <span data-ttu-id="33087-106">Razor 구문 Razor 태그, C#, 및 HTML로 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-106">The Razor syntax consists of Razor markup, C#, and HTML.</span></span> <span data-ttu-id="33087-107">Razor를 일반적으로 들어 있는 파일을 *.cshtml* 파일 확장명입니다.</span><span class="sxs-lookup"><span data-stu-id="33087-107">Files containing Razor generally have a *.cshtml* file extension.</span></span>

## <a name="rendering-html"></a><span data-ttu-id="33087-108">HTML 렌더링</span><span class="sxs-lookup"><span data-stu-id="33087-108">Rendering HTML</span></span>

<span data-ttu-id="33087-109">기본 Razor 언어 HTML입니다.</span><span class="sxs-lookup"><span data-stu-id="33087-109">The default Razor language is HTML.</span></span> <span data-ttu-id="33087-110">렌더링 HTML Razor 태그에서이 HTML 파일에서 HTML을 렌더링 하는 방법과 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-110">Rendering HTML from Razor markup is no different than rendering HTML from an HTML file.</span></span> <span data-ttu-id="33087-111">HTML 태그에서 *.cshtml* Razor 파일은 변경 하지 않고 서버에서 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-111">HTML markup in *.cshtml* Razor files is rendered by the server unchanged.</span></span>

## <a name="razor-syntax"></a><span data-ttu-id="33087-112">Razor 구문</span><span class="sxs-lookup"><span data-stu-id="33087-112">Razor syntax</span></span>

<span data-ttu-id="33087-113">Razor C# 지원 및 사용 하 여는 `@` C#으로 HTML에서 전환 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="33087-113">Razor supports C# and uses the `@` symbol to transition from HTML to C#.</span></span> <span data-ttu-id="33087-114">Razor C# 식을 계산 하 고 HTML 출력에이 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-114">Razor evaluates C# expressions and renders them in the HTML output.</span></span>

<span data-ttu-id="33087-115">경우는 `@` 기호 뒤는 [Razor 예약 키워드](#razor-reserved-keywords), Razor 특정 태그에 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-115">When an `@` symbol is followed by a [Razor reserved keyword](#razor-reserved-keywords), it transitions into Razor-specific markup.</span></span> <span data-ttu-id="33087-116">그렇지 않은 경우 일반 C# 식으로 전환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-116">Otherwise, it transitions into plain C#.</span></span>

<span data-ttu-id="33087-117">이스케이프할는 `@` Razor 태그에서 기호, 초를 사용 하 여 `@` 기호:</span><span class="sxs-lookup"><span data-stu-id="33087-117">To escape an `@` symbol in Razor markup, use a second `@` symbol:</span></span>

```cshtml
<p>@@Username</p>
```

<span data-ttu-id="33087-118">코드는 단일 HTML로 렌더링은 `@` 기호:</span><span class="sxs-lookup"><span data-stu-id="33087-118">The code is rendered in HTML with a single `@` symbol:</span></span>

```html
<p>@Username</p>
```

<span data-ttu-id="33087-119">HTML 특성 및 전자 메일 주소를 포함 하는 내용을 처리 하지 않습니다는 `@` 전환 문자로 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="33087-119">HTML attributes and content containing email addresses don't treat the `@` symbol as a transition character.</span></span> <span data-ttu-id="33087-120">다음 예제에서 전자 메일 주소 Razor 구문 분석 하 여 그대로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-120">The email addresses in the following example are untouched by Razor parsing:</span></span>

```cshtml
<a href="mailto:Support@contoso.com">Support@contoso.com</a>
```

## <a name="implicit-razor-expressions"></a><span data-ttu-id="33087-121">암시적 Razor 식</span><span class="sxs-lookup"><span data-stu-id="33087-121">Implicit Razor expressions</span></span>

<span data-ttu-id="33087-122">암시적 Razor 식은로 시작 `@` C# 코드가 뒤에 오는:</span><span class="sxs-lookup"><span data-stu-id="33087-122">Implicit Razor expressions start with `@` followed by C# code:</span></span>

```cshtml
<p>@DateTime.Now</p>
<p>@DateTime.IsLeapYear(2016)</p>
```

<span data-ttu-id="33087-123">C# 제외 하 고 `await` 키워드, 암시적 식 공백을 포함 해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-123">With the exception of the C# `await` keyword, implicit expressions must not contain spaces.</span></span> <span data-ttu-id="33087-124">C# 문에 명확한 종료 있으면 공백은 혼합 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-124">If the C# statement has a clear ending, spaces can be intermingled:</span></span>

```cshtml
<p>@await DoSomething("hello", "world")</p>
```

<span data-ttu-id="33087-125">암시적 식 **없습니다** C# 제네릭, 대괄호 내의 문자가 포함 (`<>`) HTML 태그로 해석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-125">Implicit expressions **cannot** contain C# generics, as the characters inside the brackets (`<>`) are interpreted as an HTML tag.</span></span> <span data-ttu-id="33087-126">다음 코드는 **하지** 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-126">The following code is **not** valid:</span></span>

```cshtml
<p>@GenericMethod<int>()</p>
```

<span data-ttu-id="33087-127">위의 코드에서는 다음 중 하 나와 비슷한 컴파일러 오류가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-127">The preceding code generates a compiler error similar to one of the following:</span></span>

 * <span data-ttu-id="33087-128">"Int" 요소가 닫히지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-128">The "int" element was not closed.</span></span> <span data-ttu-id="33087-129">모든 요소가 하나 있어야 자체 닫거나는 짝이 되는 끝 태그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-129">All elements must be either self-closing or have a matching end tag.</span></span>
 * <span data-ttu-id="33087-130">메서드 그룹을 비 대리자 형식 'object' ' GenericMethod'으로 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-130">Cannot convert method group 'GenericMethod' to non-delegate type 'object'.</span></span> <span data-ttu-id="33087-131">메서드를 호출 하 시겠습니까?'</span><span class="sxs-lookup"><span data-stu-id="33087-131">Did you intend to invoke the method?\`</span></span> 
 
<span data-ttu-id="33087-132">제네릭 메서드 호출에 래핑되어야는 [명시적 Razor 식](#explicit-razor-expressions) 또는 [Razor 코드 블록](#razor-code-blocks)합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-132">Generic method calls must be wrapped in an [explicit Razor expression](#explicit-razor-expressions) or a [Razor code block](#razor-code-blocks).</span></span>

## <a name="explicit-razor-expressions"></a><span data-ttu-id="33087-133">명시적 Razor 식</span><span class="sxs-lookup"><span data-stu-id="33087-133">Explicit Razor expressions</span></span>

<span data-ttu-id="33087-134">Razor 식은 명시적으로 구성 될는 `@` 균형 잡힌 괄호 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="33087-134">Explicit Razor expressions consist of an `@` symbol with balanced parenthesis.</span></span> <span data-ttu-id="33087-135">지난 주 시간을 렌더링 하려면 다음 Razor 태그 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-135">To render last week's time, the following Razor markup is used:</span></span>

```cshtml
<p>Last week this time: @(DateTime.Now - TimeSpan.FromDays(7))</p>
```

<span data-ttu-id="33087-136">내에서 모든 콘텐츠는 `@()` 괄호 평가 되 고 출력에 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-136">Any content within the `@()` parenthesis is evaluated and rendered to the output.</span></span>

<span data-ttu-id="33087-137">일반적으로 이전 섹션에 설명 된 암시적 식, 공백을 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-137">Implicit expressions, described in the previous section, generally can't contain spaces.</span></span> <span data-ttu-id="33087-138">다음 코드에서 1 주일 현재 시간에서 차감 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-138">In the following code, one week isn't subtracted from the current time:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact.cshtml?range=17)]

<span data-ttu-id="33087-139">코드는 다음과 같은 HTML을 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-139">The code renders the following HTML:</span></span>

```html
<p>Last week: 7/7/2016 4:39:52 PM - TimeSpan.FromDays(7)</p>
```

<span data-ttu-id="33087-140">명시적 식은 연결 된 식 결과 텍스트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-140">Explicit expressions can be used to concatenate text with an expression result:</span></span>

```cshtml
@{
    var joe = new Person("Joe", 33);
}

<p>Age@(joe.Age)</p>
```

<span data-ttu-id="33087-141">명시적 식 없이 `<p>Age@joe.Age</p>` 전자 메일 주소로 처리 및 `<p>Age@joe.Age</p>` 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-141">Without the explicit expression, `<p>Age@joe.Age</p>` is treated as an email address, and `<p>Age@joe.Age</p>` is rendered.</span></span> <span data-ttu-id="33087-142">명시적 식을으로 쓸 때 `<p>Age33</p>` 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-142">When written as an explicit expression, `<p>Age33</p>` is rendered.</span></span>


<span data-ttu-id="33087-143">제네릭 메서드의 입력에서 출력을 렌더링 하는 명시적 식을 사용할 수 있습니다 *.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="33087-143">Explicit expressions can be used to render output from generic methods in *.cshtml* files.</span></span> <span data-ttu-id="33087-144">대괄호 내의 문자가 암시적 식에서 (`<>`) HTML 태그로 해석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-144">In an implicit expression, the characters inside the brackets (`<>`) are interpreted as an HTML tag.</span></span> <span data-ttu-id="33087-145">다음 태그는 **하지** 유효한 Razor:</span><span class="sxs-lookup"><span data-stu-id="33087-145">The following markup is **not** valid Razor:</span></span>

```cshtml
<p>@GenericMethod<int>()</p>
```

<span data-ttu-id="33087-146">위의 코드에서는 다음 중 하 나와 비슷한 컴파일러 오류가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-146">The preceding code generates a compiler error similar to one of the following:</span></span>

 * <span data-ttu-id="33087-147">"Int" 요소가 닫히지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-147">The "int" element was not closed.</span></span> <span data-ttu-id="33087-148">모든 요소가 하나 있어야 자체 닫거나는 짝이 되는 끝 태그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-148">All elements must be either self-closing or have a matching end tag.</span></span>
 * <span data-ttu-id="33087-149">메서드 그룹을 비 대리자 형식 'object' ' GenericMethod'으로 변환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-149">Cannot convert method group 'GenericMethod' to non-delegate type 'object'.</span></span> <span data-ttu-id="33087-150">메서드를 호출 하 시겠습니까?'</span><span class="sxs-lookup"><span data-stu-id="33087-150">Did you intend to invoke the method?\`</span></span> 
 
 <span data-ttu-id="33087-151">다음 태그는 올바른 방법은 쓰기가이 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="33087-151">The following markup shows the correct way write this code.</span></span> <span data-ttu-id="33087-152">명시적 식으로 코드를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-152">The code is written as an explicit expression:</span></span>

```cshtml
<p>@(GenericMethod<int>())</p>
```

## <a name="expression-encoding"></a><span data-ttu-id="33087-153">식 인코딩</span><span class="sxs-lookup"><span data-stu-id="33087-153">Expression encoding</span></span>

<span data-ttu-id="33087-154">C# 식을 문자열로 평가 하는 인코딩된 HTML입니다.</span><span class="sxs-lookup"><span data-stu-id="33087-154">C# expressions that evaluate to a string are HTML encoded.</span></span> <span data-ttu-id="33087-155">C# 식을 계산 하는 `IHtmlContent` 통해 직접 렌더링 되는 `IHtmlContent.WriteTo`합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-155">C# expressions that evaluate to `IHtmlContent` are rendered directly through `IHtmlContent.WriteTo`.</span></span> <span data-ttu-id="33087-156">C# 식으로 계산 하지는 `IHtmlContent` 하 여 문자열로 변환 `ToString` 되 고 렌더링 하는 전에 인코딩된 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-156">C# expressions that don't evaluate to `IHtmlContent` are converted to a string by `ToString` and encoded before they're rendered.</span></span>

```cshtml
@("<span>Hello World</span>")
```

<span data-ttu-id="33087-157">코드는 다음과 같은 HTML을 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-157">The code renders the following HTML:</span></span>

```html
&lt;span&gt;Hello World&lt;/span&gt;
```

<span data-ttu-id="33087-158">HTML은 브라우저에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-158">The HTML is shown in the browser as:</span></span>

```
<span>Hello World</span>
```

<span data-ttu-id="33087-159">`HtmlHelper.Raw`출력 인코딩된 않지만 HTML 태그로 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-159">`HtmlHelper.Raw` output isn't encoded but rendered as HTML markup.</span></span>

> [!WARNING]
> <span data-ttu-id="33087-160">사용 하 여 `HtmlHelper.Raw` unsanitized 사용자 입력은 보안상 위험 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-160">Using `HtmlHelper.Raw` on unsanitized user input is a security risk.</span></span> <span data-ttu-id="33087-161">사용자 입력에는 악의적인 JavaScript 또는 다른 악용 기법 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-161">User input might contain malicious JavaScript or other exploits.</span></span> <span data-ttu-id="33087-162">사용자 입력을 정리 하는 것은 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-162">Sanitizing user input is difficult.</span></span> <span data-ttu-id="33087-163">사용 하지 않도록 `HtmlHelper.Raw` 사용자 입력을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-163">Avoid using `HtmlHelper.Raw` with user input.</span></span>

```cshtml
@Html.Raw("<span>Hello World</span>")
```

<span data-ttu-id="33087-164">코드는 다음과 같은 HTML을 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-164">The code renders the following HTML:</span></span>

```html
<span>Hello World</span>
```

## <a name="razor-code-blocks"></a><span data-ttu-id="33087-165">Razor 코드 블록</span><span class="sxs-lookup"><span data-stu-id="33087-165">Razor code blocks</span></span>

<span data-ttu-id="33087-166">Razor 코드 블록 시작 `@` 묶여 및 `{}`합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-166">Razor code blocks start with `@` and are enclosed by `{}`.</span></span> <span data-ttu-id="33087-167">식에서와 달리 C# 코드 블록 내부에서 코드 렌더링 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-167">Unlike expressions, C# code inside code blocks isn't rendered.</span></span> <span data-ttu-id="33087-168">코드 블록 및 뷰의 식에서에서 같은 범위를 공유 및 순서에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-168">Code blocks and expressions in a view share the same scope and are defined in order:</span></span>

```cshtml
@{
    var quote = "The future depends on what you do today. - Mahatma Gandhi";
}

<p>@quote</p>

@{
    quote = "Hate cannot drive out hate, only love can do that. - Martin Luther King, Jr.";
}

<p>@quote</p>
```

<span data-ttu-id="33087-169">코드는 다음과 같은 HTML을 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-169">The code renders the following HTML:</span></span>

```html
<p>The future depends on what you do today. - Mahatma Gandhi</p>
<p>Hate cannot drive out hate, only love can do that. - Martin Luther King, Jr.</p>
```

### <a name="implicit-transitions"></a><span data-ttu-id="33087-170">암시적 변환</span><span class="sxs-lookup"><span data-stu-id="33087-170">Implicit transitions</span></span>

<span data-ttu-id="33087-171">코드 블록에 기본 언어는 C#, 하지만 Razor 페이지를 HTML로 다시 전환 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-171">The default language in a code block is C#, but the Razor Page can transition back to HTML:</span></span>

```cshtml
@{
    var inCSharp = true;
    <p>Now in HTML, was in C# @inCSharp</p>
}
```

### <a name="explicit-delimited-transition"></a><span data-ttu-id="33087-172">명시적 구분 기호로 분리 된 전환</span><span class="sxs-lookup"><span data-stu-id="33087-172">Explicit delimited transition</span></span>

<span data-ttu-id="33087-173">HTML 렌더링 해야 하는 코드 블록의 하위 섹션을 정의 하려면 코드 감싸기 렌더링 하기 위한 문자 Razor  **\<텍스트 >** 태그:</span><span class="sxs-lookup"><span data-stu-id="33087-173">To define a subsection of a code block that should render HTML, surround the characters for rendering with the Razor **\<text>** tag:</span></span>

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    <text>Name: @person.Name</text>
}
```

<span data-ttu-id="33087-174">HTML 태그로 묶인 없는 HTML 렌더링 하기 위한이 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-174">Use this approach to render HTML that isn't surrounded by an HTML tag.</span></span> <span data-ttu-id="33087-175">HTML 또는 Razor 태그가 없는 Razor 런타임 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-175">Without an HTML or Razor tag, a Razor runtime error occurs.</span></span>

<span data-ttu-id="33087-176">**\<텍스트 >** 태그는 콘텐츠를 렌더링할 때 공백을 제어 하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-176">The **\<text>** tag is useful to control whitespace when rendering content:</span></span>

* <span data-ttu-id="33087-177">사이 있는 내용을는  **\<텍스트 >** 태그를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-177">Only the content between the **\<text>** tag is rendered.</span></span> 
* <span data-ttu-id="33087-178">앞 이나 뒤에 공백이 없어야는  **\<텍스트 >** 태그가 HTML 출력에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="33087-178">No whitespace before or after the **\<text>** tag appears in the HTML output.</span></span>

### <a name="explicit-line-transition-with-"></a><span data-ttu-id="33087-179">명시적 줄 전환을 @:</span><span class="sxs-lookup"><span data-stu-id="33087-179">Explicit Line Transition with @:</span></span>

<span data-ttu-id="33087-180">코드 블록 안에 줄의 나머지 부분을 HTML로 렌더링, 사용 된 `@:` 구문:</span><span class="sxs-lookup"><span data-stu-id="33087-180">To render the rest of an entire line as HTML inside a code block, use the `@:` syntax:</span></span>

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    @:Name: @person.Name
}
```

<span data-ttu-id="33087-181">없이 `@:` 코드에서는 Razor 런타임 오류가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-181">Without the `@:` in the code, a Razor runtime error is generated.</span></span>

<span data-ttu-id="33087-182">경고: 추가 `@` Razor 파일의 문자는 블록의 뒷부분에 나오는 문에서 발생 한 컴파일러 오류 원인 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-182">Warning: Extra `@` characters in a Razor file can cause cause compiler errors at statements later in the block.</span></span> <span data-ttu-id="33087-183">이러한 컴파일러 오류 보고 된 오류 하기 전에 실제 오류가 발생 하기 때문에 이해 하기 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-183">These compiler errors can be difficult to understand because the actual error occurs before the reported error.</span></span> <span data-ttu-id="33087-184">이 오류는 단일 코드 블록으로 여러 암시적/명시적 식을 결합 이후에 자주 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-184">This error is common after combining multiple implicit/explicit expressions into a single code block.</span></span>

## <a name="control-structures"></a><span data-ttu-id="33087-185">제어 구조</span><span class="sxs-lookup"><span data-stu-id="33087-185">Control Structures</span></span>

<span data-ttu-id="33087-186">제어 구조는 코드 블록의 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="33087-186">Control structures are an extension of code blocks.</span></span> <span data-ttu-id="33087-187">코드 블록 (인라인 C# 태그로 전환)도의 모든 측면은 다음 구조에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-187">All aspects of code blocks (transitioning to markup, inline C#) also apply to the following structures:</span></span>

### <a name="conditionals-if-else-if-else-and-switch"></a><span data-ttu-id="33087-188">조건부 @if, else if else, 및@switch</span><span class="sxs-lookup"><span data-stu-id="33087-188">Conditionals @if, else if, else, and @switch</span></span>

<span data-ttu-id="33087-189">`@if`코드를 실행할 때 컨트롤:</span><span class="sxs-lookup"><span data-stu-id="33087-189">`@if` controls when code runs:</span></span>

```cshtml
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
```

<span data-ttu-id="33087-190">`else`및 `else if` 필요 하지 않습니다는 `@` 기호:</span><span class="sxs-lookup"><span data-stu-id="33087-190">`else` and `else if` don't require the `@` symbol:</span></span>

```cshtml
@if (value % 2 == 0)
{
    <p>The value was even.</p>
}
else if (value >= 1337)
{
    <p>The value is large.</p>
}
else
{
    <p>The value is odd and small.</p>
}
```

<span data-ttu-id="33087-191">다음 태그 switch 문을 사용 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="33087-191">The following markup shows how to use a switch statement:</span></span>

```cshtml
@switch (value)
{
    case 1:
        <p>The value is 1!</p>
        break;
    case 1337:
        <p>Your number is 1337!</p>
        break;
    default:
        <p>Your number wasn't 1 or 1337.</p>
        break;
}
```

### <a name="looping-for-foreach-while-and-do-while"></a><span data-ttu-id="33087-192">반복 @for, @foreach, @while, 및 @do 동안</span><span class="sxs-lookup"><span data-stu-id="33087-192">Looping @for, @foreach, @while, and @do while</span></span>

<span data-ttu-id="33087-193">템플릿 기반 HTML 제어 문을 반복 해 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-193">Templated HTML can be rendered with looping control statements.</span></span> <span data-ttu-id="33087-194">사람 목록이 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-194">To render a list of people:</span></span>

```cshtml
@{
    var people = new Person[]
    {
          new Person("Weston", 33),
          new Person("Johnathon", 41),
          ...
    };
}
```

<span data-ttu-id="33087-195">다음 반복 문이 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-195">The following looping statements are supported:</span></span>

`@for`

```cshtml
@for (var i = 0; i < people.Length; i++)
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>
}
```

`@foreach`

```cshtml
@foreach (var person in people)
{
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>
}
```

`@while`

```cshtml
@{ var i = 0; }
@while (i < people.Length)
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>

    i++;
}
```

`@do while`

```cshtml
@{ var i = 0; }
@do
{
    var person = people[i];
    <p>Name: @person.Name</p>
    <p>Age: @person.Age</p>

    i++;
} while (i < people.Length);
```

### <a name="compound-using"></a><span data-ttu-id="33087-196">복합@using</span><span class="sxs-lookup"><span data-stu-id="33087-196">Compound @using</span></span>

<span data-ttu-id="33087-197">C#에서는 `using` 문을 사용 하는 개체가 삭제 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-197">In C#, a `using` statement is used to ensure an object is disposed.</span></span> <span data-ttu-id="33087-198">Razor, 동일한 메커니즘 추가 콘텐츠를 포함 하는 HTML 도우미 만들기에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-198">In Razor, the same mechanism is used to create HTML Helpers that contain additional content.</span></span> <span data-ttu-id="33087-199">다음 코드에서는 HTML 도우미와 form 태그를 렌더링는 `@using` 문:</span><span class="sxs-lookup"><span data-stu-id="33087-199">In the following code, HTML Helpers render a form tag with the `@using` statement:</span></span>


```cshtml
@using (Html.BeginForm())
{
    <div>
        email:
        <input type="email" id="Email" value="">
        <button>Register</button>
    </div>
}
```

<span data-ttu-id="33087-200">범위 수준 작업을 수행할 수 있습니다 [태그 도우미](xref:mvc/views/tag-helpers/intro)합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-200">Scope-level actions can be performed with [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

### <a name="try-catch-finally"></a><span data-ttu-id="33087-201">@trycatch, finally</span><span class="sxs-lookup"><span data-stu-id="33087-201">@try, catch, finally</span></span>

<span data-ttu-id="33087-202">예외 처리는 C# 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-202">Exception handling is similar to C#:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact7.cshtml)]

### <a name="lock"></a>@lock

<span data-ttu-id="33087-203">Razor에 임계 섹션 lock 문을 보호 하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-203">Razor has the capability to protect critical sections with lock statements:</span></span>

```cshtml
@lock (SomeLock)
{
    // Do critical section work
}
```

### <a name="comments"></a><span data-ttu-id="33087-204">설명</span><span class="sxs-lookup"><span data-stu-id="33087-204">Comments</span></span>

<span data-ttu-id="33087-205">Razor 주석 C# 및 HTML을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-205">Razor supports C# and HTML comments:</span></span>

```cshtml
@{
    /* C# comment */
    // Another C# comment
}
<!-- HTML comment -->
```

<span data-ttu-id="33087-206">코드는 다음과 같은 HTML을 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-206">The code renders the following HTML:</span></span>

```html
<!-- HTML comment -->
```

<span data-ttu-id="33087-207">Razor 주석 웹 페이지를 렌더링 하기 전에 서버에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-207">Razor comments are removed by the server before the webpage is rendered.</span></span> <span data-ttu-id="33087-208">Razor를 사용 하 여 `@*  *@` 를 주석을 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-208">Razor uses `@*  *@` to delimit comments.</span></span> <span data-ttu-id="33087-209">다음 코드 주석 처리 되어, 서버에서 태그를 렌더링 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-209">The following code is commented out, so the server doesn't render any markup:</span></span>

```cshtml
@*
    @{
        /* C# comment */
        // Another C# comment
    }
    <!-- HTML comment -->
*@
```

## <a name="directives"></a><span data-ttu-id="33087-210">지시문</span><span class="sxs-lookup"><span data-stu-id="33087-210">Directives</span></span>

<span data-ttu-id="33087-211">Razor 지시문 다음 예약 된 키워드를 사용 하 여 암시적 식으로 표시 됩니다는 `@` 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="33087-211">Razor directives are represented by implicit expressions with reserved keywords following the `@` symbol.</span></span> <span data-ttu-id="33087-212">지시문에는 일반적으로 보기를 구문 분석 또는 다른 기능을 활성화 하는 방법을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-212">A directive typically changes the way a view is parsed or enables different functionality.</span></span>

<span data-ttu-id="33087-213">Razor 뷰의 코드를 생성 하는 방법을 이해 쉽게 지시문의 작동 방식을 이해 하려면 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-213">Understanding how Razor generates code for a view makes it easier to understand how directives work.</span></span>

[!code-html[Main](razor/sample/Views/Home/Contact8.cshtml)]

<span data-ttu-id="33087-214">코드에서는 클래스에는 다음과 유사한 오류가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-214">The code generates a class similar to the following:</span></span>

```csharp
public class _Views_Something_cshtml : RazorPage<dynamic>
{
    public override async Task ExecuteAsync()
    {
        var output = "Getting old ain't for wimps! - Anonymous";

        WriteLiteral("/r/n<div>Quote of the Day: ");
        Write(output);
        WriteLiteral("</div>");
    }
}
```

<span data-ttu-id="33087-215">이 문서의 섹션의 뒷부분에 나오는 [보기에 대해 생성 된 Razor C# 클래스 보기](#viewing-the-razor-c-class-generated-for-a-view) 이렇게 생성 된 클래스를 확인 하는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-215">Later in this article, the section [Viewing the Razor C# class generated for a view](#viewing-the-razor-c-class-generated-for-a-view) explains how to view this generated class.</span></span>

### <a name="using"></a>@using

<span data-ttu-id="33087-216">`@using` 지시문 추가 하는 C# `using` 지시문을 생성 된 보기에:</span><span class="sxs-lookup"><span data-stu-id="33087-216">The `@using` directive adds the C# `using` directive to the generated view:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact9.cshtml)]

### <a name="model"></a>@model

<span data-ttu-id="33087-217">`@model` 지시문 보기에 전달 된 모델의 유형을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-217">The `@model` directive specifies the type of the model passed to a view:</span></span>

```cshtml
@model TypeNameOfModel
```

<span data-ttu-id="33087-218">개별 사용자 계정을 사용 하 여 만든 ASP.NET Core MVC 응용 프로그램에 *Views/Account/Login.cshtml* 보기 모델 선언이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-218">In an ASP.NET Core MVC app created with individual user accounts, the *Views/Account/Login.cshtml* view contains the following model declaration:</span></span>

```cshtml
@model LoginViewModel
```

<span data-ttu-id="33087-219">생성 된 클래스에서 상속 `RazorPage<dynamic>`:</span><span class="sxs-lookup"><span data-stu-id="33087-219">The class generated inherits from `RazorPage<dynamic>`:</span></span>

```csharp
public class _Views_Account_Login_cshtml : RazorPage<LoginViewModel>
```

<span data-ttu-id="33087-220">Razor를 노출 한 `Model` 보기에 전달 된 모델에 액세스 하기 위한 속성:</span><span class="sxs-lookup"><span data-stu-id="33087-220">Razor exposes a `Model` property for accessing the model passed to the view:</span></span>

```cshtml
<div>The Login Email: @Model.Email</div>
```

<span data-ttu-id="33087-221">`@model` 지시문이이 속성의 유형을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-221">The `@model` directive specifies the type of this property.</span></span> <span data-ttu-id="33087-222">지시문에 지정 된 `T` 에 `RazorPage<T>` 뷰는 생성 된 클래스에서 파생 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-222">The directive specifies the `T` in `RazorPage<T>` that the generated class that the view derives from.</span></span> <span data-ttu-id="33087-223">경우는 `@model` 지시문 iisn't 지정는 `Model` 속성은 형식이 `dynamic`합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-223">If the `@model` directive iisn't specified, the `Model` property is of type `dynamic`.</span></span> <span data-ttu-id="33087-224">모델의 값은 컨트롤러에서 뷰에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-224">The value of the model is passed from the controller to the view.</span></span> <span data-ttu-id="33087-225">자세한 내용은 참조 하십시오. [강력한 형식 모델 및 @model 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="33087-225">For more information, see [Strongly typed models and the @model keyword.</span></span>

### <a name="inherits"></a>@inherits

<span data-ttu-id="33087-226">`@inherits` 지시문이 뷰가 상속 된 클래스의 모든 권한을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-226">The `@inherits` directive provides full control of the class the view inherits:</span></span>

```cshtml
@inherits TypeNameOfClassToInheritFrom
```

<span data-ttu-id="33087-227">다음 코드는 사용자 지정 Razor 페이지 유형:</span><span class="sxs-lookup"><span data-stu-id="33087-227">The following code is a custom Razor page type:</span></span>

[!code-csharp[Main](razor/sample/Classes/CustomRazorPage.cs)]

<span data-ttu-id="33087-228">`CustomText` 는 보기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-228">The `CustomText` is displayed in a view:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact10.cshtml)]

<span data-ttu-id="33087-229">코드는 다음과 같은 HTML을 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-229">The code renders the following HTML:</span></span>

```html
<div>Custom text: Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.</div>
```

 <span data-ttu-id="33087-230">`@model`및 `@inherits` 동일한 보기에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-230">`@model` and `@inherits` can be used in the same view.</span></span> <span data-ttu-id="33087-231">`@inherits`에 있을 수 있습니다는 *_ViewImports.cshtml* 파일을 가져오므로 보기:</span><span class="sxs-lookup"><span data-stu-id="33087-231">`@inherits` can be in a *_ViewImports.cshtml* file that the view imports:</span></span>

[!code-cshtml[Main](razor/sample/Views/_ViewImportsModel.cshtml)]

<span data-ttu-id="33087-232">다음 코드는 강력한 형식의 뷰의 예:</span><span class="sxs-lookup"><span data-stu-id="33087-232">The following code is an example of a strongly-typed view:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Login1.cshtml)]

<span data-ttu-id="33087-233">경우 "rick@contoso.com" 전달 보기 모델에서는 다음과 같은 HTML 태그를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-233">If "rick@contoso.com" is passed in the model, the view generates the following HTML markup:</span></span>

```html
<div>The Login Email: rick@contoso.com</div>
<div>Custom text: Gardyloo! - A Scottish warning yelled from a window before dumping a slop bucket on the street below.</div>
```

### <a name="inject"></a>@inject


<span data-ttu-id="33087-234">`@inject` 지시문을 사용 하면 Razor 페이지에서 서비스를 삽입 하는 [서비스 컨테이너](xref:fundamentals/dependency-injection) 보기에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-234">The `@inject` directive enables the Razor Page to inject a service from the [service container](xref:fundamentals/dependency-injection) into a view.</span></span> <span data-ttu-id="33087-235">자세한 내용은 참조 [뷰로 종속성 주입](xref:mvc/views/dependency-injection)합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-235">For more information, see [Dependency injection into views](xref:mvc/views/dependency-injection).</span></span>

### <a name="functions"></a>@functions

<span data-ttu-id="33087-236">`@functions` 지시문 Razor 페이지 보기에 기능 수준 콘텐츠를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-236">The `@functions` directive enables a Razor Page to add function-level content to a view:</span></span>

```cshtml
@functions { // C# Code }
```

<span data-ttu-id="33087-237">예:</span><span class="sxs-lookup"><span data-stu-id="33087-237">For example:</span></span>

[!code-cshtml[Main](razor/sample/Views/Home/Contact6.cshtml)]

<span data-ttu-id="33087-238">코드에서는 다음 HTML 태그를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-238">The code generates the following HTML markup:</span></span>

```html
<div>From method: Hello</div>
```

<span data-ttu-id="33087-239">다음 코드는 생성된 된 Razor C# 클래스:</span><span class="sxs-lookup"><span data-stu-id="33087-239">The following code is the generated Razor C# class:</span></span>

[!code-csharp[Main](razor/sample/Classes/Views_Home_Test_cshtml.cs?range=1-19)]

### <a name="section"></a>@section

<span data-ttu-id="33087-240">`@section` 지시어와 함께 사용 되는 [레이아웃](xref:mvc/views/layout) HTML 페이지의 서로 다른 부분에 콘텐츠를 렌더링할 뷰를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-240">The `@section` directive is used in conjunction with the [layout](xref:mvc/views/layout) to enable views to render content in different parts of the HTML page.</span></span> <span data-ttu-id="33087-241">자세한 내용은 참조 [섹션](xref:mvc/views/layout#layout-sections-label)합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-241">For more information, see [Sections](xref:mvc/views/layout#layout-sections-label).</span></span>

## <a name="tag-helpers"></a><span data-ttu-id="33087-242">태그 도우미</span><span class="sxs-lookup"><span data-stu-id="33087-242">Tag Helpers</span></span>

<span data-ttu-id="33087-243">와 관련 된 세 가지 지시문 없는 [태그 도우미](xref:mvc/views/tag-helpers/intro)합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-243">There are three directives that pertain to [Tag Helpers](xref:mvc/views/tag-helpers/intro).</span></span>

| <span data-ttu-id="33087-244">지시문</span><span class="sxs-lookup"><span data-stu-id="33087-244">Directive</span></span> | <span data-ttu-id="33087-245">함수</span><span class="sxs-lookup"><span data-stu-id="33087-245">Function</span></span> |
| --------- | -------- |
| [@addTagHelper](xref:mvc/views/tag-helpers/intro#add-helper-label) | <span data-ttu-id="33087-246">태그 도우미 보기를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-246">Makes Tag Helpers available to a view.</span></span> |
| [@removeTagHelper](xref:mvc/views/tag-helpers/intro#remove-razor-directives-label) | <span data-ttu-id="33087-247">보기에서 이전에 추가 된 태그 도우미를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-247">Removes Tag Helpers previously added from a view.</span></span> |
| [@tagHelperPrefix](xref:mvc/views/tag-helpers/intro#prefix-razor-directives-label) | <span data-ttu-id="33087-248">태그 도우미 지원 기능이 사용 하 고 명시적 태그 도우미 사용을 확인 하려면 태그 접두사를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-248">Specifies a tag prefix to enable Tag Helper support and to make Tag Helper usage explicit.</span></span> |

## <a name="razor-reserved-keywords"></a><span data-ttu-id="33087-249">Razor 예약 키워드</span><span class="sxs-lookup"><span data-stu-id="33087-249">Razor reserved keywords</span></span>

### <a name="razor-keywords"></a><span data-ttu-id="33087-250">Razor 키워드</span><span class="sxs-lookup"><span data-stu-id="33087-250">Razor keywords</span></span>

* <span data-ttu-id="33087-251">페이지 (ASP.NET Core 2.0 이상 필요)</span><span class="sxs-lookup"><span data-stu-id="33087-251">page (Requires ASP.NET Core 2.0 and later)</span></span>
* <span data-ttu-id="33087-252">함수</span><span class="sxs-lookup"><span data-stu-id="33087-252">functions</span></span>
* <span data-ttu-id="33087-253">상속</span><span class="sxs-lookup"><span data-stu-id="33087-253">inherits</span></span>
* <span data-ttu-id="33087-254">모델</span><span class="sxs-lookup"><span data-stu-id="33087-254">model</span></span>
* <span data-ttu-id="33087-255">section</span><span class="sxs-lookup"><span data-stu-id="33087-255">section</span></span>
* <span data-ttu-id="33087-256">(현재 지원 하지 않는 ASP.NET Core) 도우미</span><span class="sxs-lookup"><span data-stu-id="33087-256">helper (Not currently supported by ASP.NET Core)</span></span>

<span data-ttu-id="33087-257">Razor 키워드로 이스케이프 `@(Razor Keyword)` (예를 들어 `@(functions)`).</span><span class="sxs-lookup"><span data-stu-id="33087-257">Razor keywords are escaped with `@(Razor Keyword)` (for example, `@(functions)`).</span></span>

### <a name="c-razor-keywords"></a><span data-ttu-id="33087-258">C# Razor 키워드</span><span class="sxs-lookup"><span data-stu-id="33087-258">C# Razor keywords</span></span>

* <span data-ttu-id="33087-259">case</span><span class="sxs-lookup"><span data-stu-id="33087-259">case</span></span>
* <span data-ttu-id="33087-260">do</span><span class="sxs-lookup"><span data-stu-id="33087-260">do</span></span>
* <span data-ttu-id="33087-261">default</span><span class="sxs-lookup"><span data-stu-id="33087-261">default</span></span>
* <span data-ttu-id="33087-262">for</span><span class="sxs-lookup"><span data-stu-id="33087-262">for</span></span>
* <span data-ttu-id="33087-263">foreach</span><span class="sxs-lookup"><span data-stu-id="33087-263">foreach</span></span>
* <span data-ttu-id="33087-264">if</span><span class="sxs-lookup"><span data-stu-id="33087-264">if</span></span>
* <span data-ttu-id="33087-265">else</span><span class="sxs-lookup"><span data-stu-id="33087-265">else</span></span>
* <span data-ttu-id="33087-266">잠금</span><span class="sxs-lookup"><span data-stu-id="33087-266">lock</span></span>
* <span data-ttu-id="33087-267">switch</span><span class="sxs-lookup"><span data-stu-id="33087-267">switch</span></span>
* <span data-ttu-id="33087-268">try</span><span class="sxs-lookup"><span data-stu-id="33087-268">try</span></span>
* <span data-ttu-id="33087-269">catch</span><span class="sxs-lookup"><span data-stu-id="33087-269">catch</span></span>
* <span data-ttu-id="33087-270">finally</span><span class="sxs-lookup"><span data-stu-id="33087-270">finally</span></span>
* <span data-ttu-id="33087-271">using</span><span class="sxs-lookup"><span data-stu-id="33087-271">using</span></span>
* <span data-ttu-id="33087-272">while</span><span class="sxs-lookup"><span data-stu-id="33087-272">while</span></span>

<span data-ttu-id="33087-273">C# Razor 키워드와 이중 이스케이프 해야 `@(@C# Razor Keyword)` (예를 들어 `@(@case)`).</span><span class="sxs-lookup"><span data-stu-id="33087-273">C# Razor keywords must be double-escaped with `@(@C# Razor Keyword)` (for example, `@(@case)`).</span></span> <span data-ttu-id="33087-274">첫 번째 `@` Razor 구문 분석기를 이스케이프 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-274">The first `@` escapes the Razor parser.</span></span> <span data-ttu-id="33087-275">두 번째 `@` C# 파서를 이스케이프 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-275">The second `@` escapes the C# parser.</span></span>

### <a name="reserved-keywords-not-used-by-razor"></a><span data-ttu-id="33087-276">Razor에서 사용 하지 않는 예약 된 키워드</span><span class="sxs-lookup"><span data-stu-id="33087-276">Reserved keywords not used by Razor</span></span>

* <span data-ttu-id="33087-277">네임스페이스(namespace)</span><span class="sxs-lookup"><span data-stu-id="33087-277">namespace</span></span>
* <span data-ttu-id="33087-278">클래스</span><span class="sxs-lookup"><span data-stu-id="33087-278">class</span></span>

## <a name="viewing-the-razor-c-class-generated-for-a-view"></a><span data-ttu-id="33087-279">보기에 대해 생성 된 Razor C# 클래스 보기</span><span class="sxs-lookup"><span data-stu-id="33087-279">Viewing the Razor C# class generated for a view</span></span>

<span data-ttu-id="33087-280">ASP.NET Core MVC 프로젝트에 다음 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-280">Add the following class to the ASP.NET Core MVC project:</span></span>

[!code-csharp[Main](razor/sample/Utilities/CustomTemplateEngine.cs)]

<span data-ttu-id="33087-281">재정의 `RazorTemplateEngine` 와 MVC에서 추가 `CustomTemplateEngine` 클래스:</span><span class="sxs-lookup"><span data-stu-id="33087-281">Override the `RazorTemplateEngine` added by MVC with the `CustomTemplateEngine` class:</span></span>

[!code-csharp[Main](razor/sample/Startup.cs?highlight=4&range=10-14)]

<span data-ttu-id="33087-282">중단점을 설정한는 `return csharpDocument` 의 문은 `CustomTemplateEngine`합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-282">Set a break point on the `return csharpDocument` statement of `CustomTemplateEngine`.</span></span> <span data-ttu-id="33087-283">프로그램 실행이 중단점에서 중지 되는 경우의 값을 보려면 `generatedCode`합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-283">When program execution stops at the break point, view the value of `generatedCode`.</span></span>

![GeneratedCode의 텍스트 시각화 도우미 보기](razor/_static/tvr.png)

## <a name="view-lookups-and-case-sensitivity"></a><span data-ttu-id="33087-285">보기 조회 및 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="33087-285">View lookups and case sensitivity</span></span>

<span data-ttu-id="33087-286">Razor 뷰 엔진 뷰에 대 한 대/소문자 구분 조회를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-286">The Razor view engine performs case-sensitive lookups for views.</span></span> <span data-ttu-id="33087-287">그러나 실제 조회는 기본 파일 시스템에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="33087-287">However, the actual lookup is determined by the underlying file system:</span></span>

* <span data-ttu-id="33087-288">소스를 기반으로 하는 파일:</span><span class="sxs-lookup"><span data-stu-id="33087-288">File based source:</span></span> 
  * <span data-ttu-id="33087-289">대/소문자 구분 파일 시스템 (예: Windows), 운영 체제에서 실제 파일 공급자 조회는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-289">On operating systems with case insensitive file systems (for example, Windows), physical file provider lookups are case insensitive.</span></span> <span data-ttu-id="33087-290">예를 들어 `return View("Test")` 일치 하는 항목으로 인해 */Views/Home/Test.cshtml*, */Views/home/test.cshtml*, 및 기타 대/소문자 구분 변형 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-290">For example, `return View("Test")` results in matches for */Views/Home/Test.cshtml*, */Views/home/test.cshtml*, and any other casing variant.</span></span>
  * <span data-ttu-id="33087-291">대/소문자 구분 파일 시스템에 (예: Linux, OSX와 `EmbeddedFileProvider`), 조회는 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-291">On case-sensitive file systems (for example, Linux, OSX, and with `EmbeddedFileProvider`), lookups are case-sensitive.</span></span> <span data-ttu-id="33087-292">예를 들어 `return View("Test")` 구체적으로 일치 하는 항목 */Views/Home/Test.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-292">For example, `return View("Test")` specifically matches */Views/Home/Test.cshtml*.</span></span>
* <span data-ttu-id="33087-293">뷰 미리 컴파일된: ASP.NET 2.0 이상 코어, 미리 컴파일된 뷰를 조회는 대/소문자 구분 모든 운영 체제에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-293">Precompiled views: With ASP.NET Core 2.0 and later, looking up precompiled views is case insensitive on all operating systems.</span></span> <span data-ttu-id="33087-294">동작은 Windows에서 물리적 파일 공급자의 동작과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-294">The behavior is identical to physical file provider's behavior on Windows.</span></span> <span data-ttu-id="33087-295">미리 컴파일된 뷰를 두 가지 경우에만 다른 경우 조회 명확 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-295">If two precompiled views differ only in case, the result of lookup is non-deterministic.</span></span>

<span data-ttu-id="33087-296">개발자는의 대/소문자를 파일 및 디렉터리 이름의 대/소문자와 일치 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="33087-296">Developers are encouraged to match the casing of file and directory names to the casing of:</span></span>

    * <span data-ttu-id="33087-297">영역, 컨트롤러 및 작업 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="33087-297">Area, controller, and action names.</span></span> 
    * <span data-ttu-id="33087-298">Razor 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="33087-298">Razor Pages.</span></span>
    
<span data-ttu-id="33087-299">대/소문자와 일치 하는 배포는 내부 파일 시스템에 관계 없이 해당 보기를 찾을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="33087-299">Matching case ensures the deployments find their views regardless of the underlying file system.</span></span>
