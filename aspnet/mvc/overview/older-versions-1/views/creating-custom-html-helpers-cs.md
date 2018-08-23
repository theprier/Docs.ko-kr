---
uid: aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: 사용자 지정 HTML 도우미 (C#) 만들기 | Microsoft Docs
author: microsoft
description: MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주기 위해이 자습서의 목표가입니다. HTML 도우미를 활용 하는 중...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: a6a684e01b67c2ea139a50b568098d2dcf594272
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836373"
---
<a name="creating-custom-html-helpers-c"></a><span data-ttu-id="d6ace-104">사용자 지정 HTML 도우미 만들기 (C#)</span><span class="sxs-lookup"><span data-stu-id="d6ace-104">Creating Custom HTML Helpers (C#)</span></span>
====================
<span data-ttu-id="d6ace-105">[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d6ace-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="d6ace-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="d6ace-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="d6ace-107">MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주기 위해이 자습서의 목표가입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="d6ace-108">HTML 도우미를 활용 하 여 표준 HTML 페이지 만들기를 수행 해야 하는 HTML 태그의 지루한 작업 입력의 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>


<span data-ttu-id="d6ace-109">MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주기 위해이 자습서의 목표가입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="d6ace-110">HTML 도우미를 활용 하 여 표준 HTML 페이지 만들기를 수행 해야 하는 HTML 태그의 지루한 작업 입력의 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="d6ace-111">이 자습서의 첫 번째 부분에서는 설명 ASP.NET MVC framework에 포함 된 기존 HTML 도우미 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="d6ace-112">다음으로, 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 설명 합니다: 정적 메서드를 만들어 및 확장 메서드를 만들어 사용자 지정 HTML 도우미를 만드는 방법을 설명 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="d6ace-113">HTML 도우미 이해</span><span class="sxs-lookup"><span data-stu-id="d6ace-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="d6ace-114">HTML 도우미는 문자열을 반환 하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="d6ace-115">문자열에는 모든 유형의 콘텐츠를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="d6ace-116">예를 들어 HTML과 같은 표준 HTML 태그를 렌더링할 HTML 도우미를 사용할 수 있습니다 `<input>` 고 `<img>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="d6ace-117">탭 스트립 또는 데이터베이스 데이터의 HTML 테이블을 같은 더 복잡 한 콘텐츠를 렌더링 HTML 도우미를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="d6ace-118">ASP.NET MVC 프레임 워크에 (이 전체 목록은 아님)는 표준 HTML 도우미의 다음 집합에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="d6ace-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="d6ace-119">Html.ActionLink()</span></span>
- <span data-ttu-id="d6ace-120">Html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="d6ace-120">Html.BeginForm()</span></span>
- <span data-ttu-id="d6ace-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="d6ace-121">Html.CheckBox()</span></span>
- <span data-ttu-id="d6ace-122">Html.DropDownList()</span><span class="sxs-lookup"><span data-stu-id="d6ace-122">Html.DropDownList()</span></span>
- <span data-ttu-id="d6ace-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="d6ace-123">Html.EndForm()</span></span>
- <span data-ttu-id="d6ace-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="d6ace-124">Html.Hidden()</span></span>
- <span data-ttu-id="d6ace-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="d6ace-125">Html.ListBox()</span></span>
- <span data-ttu-id="d6ace-126">Html.Password()</span><span class="sxs-lookup"><span data-stu-id="d6ace-126">Html.Password()</span></span>
- <span data-ttu-id="d6ace-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="d6ace-127">Html.RadioButton()</span></span>
- <span data-ttu-id="d6ace-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="d6ace-128">Html.TextArea()</span></span>
- <span data-ttu-id="d6ace-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="d6ace-129">Html.TextBox()</span></span>

<span data-ttu-id="d6ace-130">예를 들어 목록 1에서 폼을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="d6ace-131">이 폼은 두 표준 HTML 도우미 (그림 1 참조)를 사용 하 여 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="d6ace-132">이 폼에서 사용 하는 `Html.BeginForm()` 및 `Html.TextBox()` 간단한 HTML 폼을 렌더링 하는 도우미 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>


<span data-ttu-id="d6ace-133">[![HTML 도우미를 사용 하 여 페이지 렌더링](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d6ace-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="d6ace-134">**그림 01**: HTML 도우미를 사용 하 여 렌더링 된 페이지 ([큰 이미지를 보려면 클릭](creating-custom-html-helpers-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="d6ace-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>


<span data-ttu-id="d6ace-135">**목록 1 – `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="d6ace-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="d6ace-136">Html.BeginForm() 도우미 메서드는 중괄호 및 닫는 HTML을 만드는 데 `<form>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="d6ace-137">`Html.BeginForm()` 메서드를 사용 하 여 내는 문입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="d6ace-138">문을 사용 하 여는 `<form>` 사용 하 여 끝 태그가 닫혀 가져옵니다 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="d6ace-139">사용 하 여 만드는 대신 선호 하는 경우 블록을 닫는 Html.EndForm() 도우미 메서드를 호출할 수 있습니다는 `<form>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="d6ace-140">어떤 방식을 선택 하 여 만들기 및 닫기 사용 `<form>` 가장 직관적인 보이는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="d6ace-141">합니다 `Html.TextBox()` 도우미 메서드는 목록 1에서 HTML을 렌더링 하는 데 사용 됩니다 `<input>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="d6ace-142">브라우저에서 소스 보기를 선택 하는 경우의 HTML 소스 목록 2에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="d6ace-143">소스 표준 HTML 태그가 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6ace-144">다음에 유의 합니다 `Html.TextBox()`HTML 도우미와 함께 렌더링 된 `<%= %>` 대신 태그 `<% %>` 태그.</span><span class="sxs-lookup"><span data-stu-id="d6ace-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="d6ace-145">등호 기호를 포함 하지 않으면 브라우저에 렌더링 가져옵니다 아무 작업도 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="d6ace-146">ASP.NET MVC 프레임 워크는 작은 도우미 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="d6ace-147">대부분의 경우 사용자 지정 HTML 도우미를 사용 하 여 MVC 프레임 워크를 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="d6ace-148">이 자습서의 나머지 부분에서는 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="d6ace-149">**2 – 나열 `Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="d6ace-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="d6ace-150">정적 메서드를 사용 하 여 HTML 도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="d6ace-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="d6ace-151">새 HTML 도우미를 만드는 가장 쉬운 방법은 문자열을 반환 하는 정적 메서드를 만드는 경우</span><span class="sxs-lookup"><span data-stu-id="d6ace-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="d6ace-152">Imagine, 예를 들어, HTML을 렌더링 하는 새 HTML 도우미 만들려는 `<label>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="d6ace-153">목록 2 클래스를 사용 하 여 렌더링 하는 수는 `<label>` 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="d6ace-154">**2 – 나열 `Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="d6ace-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="d6ace-155">목록 2에서 클래스에 대 한 특별 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="d6ace-156">`Label()` 메서드는 단순히 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="d6ace-157">목록 3에서 수정 된 인덱스 뷰를 사용 하 여 `LabelHelper` HTML을 렌더링 하 `<label>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="d6ace-158">보기 포함을 `<%@ imports %>` 가져오는 지시문을 `Application1.Helpers` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="d6ace-159">**2 – 나열 `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="d6ace-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="d6ace-160">확장 메서드를 사용 하 여 HTML 도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="d6ace-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="d6ace-161">만들려는 작동 하는 HTML 도우미와 같은 경우 확장 메서드를 만들려면 ASP.NET MVC 프레임 워크에 포함 하는 표준 HTML 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="d6ace-162">확장 메서드를 사용 하면 기존 클래스에 새 메서드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="d6ace-163">HTML 도우미 메서드를 만들 때에 새 메서드를 HtmlHelper 클래스는 뷰의 Html 속성으로 표현으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="d6ace-164">보기 3의 클래스에 확장 메서드를 추가 합니다 `HtmlHelper` 라는 클래스 `Label()`합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="d6ace-165">이 클래스에 대 한 유의 해야 하는 것 중 몇 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="d6ace-166">먼저 클래스는 정적 클래스는 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="d6ace-167">정적 클래스를 사용 하 여 확장 메서드를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="d6ace-168">둘째, 있음을의 첫 번째 매개 변수를 `Label()` 키워드를 메서드 앞에 `this`입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="d6ace-169">확장 메서드의 첫 번째 매개 변수는 확장 메서드를 확장 하는 클래스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="d6ace-170">**3 – 나열 `Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="d6ace-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="d6ace-171">확장 메서드는 모든 클래스의 다른 메서드 같은 Visual Studio Intellisense 확장 메서드를 만들고 응용 프로그램을 성공적으로 빌드 후 나타나는 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="d6ace-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="d6ace-172">유일한 차이점은 해당 확장명 메서드 (아래쪽 화살표 아이콘) 옆에 있는 특수 기호를 사용 하 여 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>


<span data-ttu-id="d6ace-173">[![Html.Label() 확장 메서드를 사용 하 여](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="d6ace-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="d6ace-174">**그림 02**: Html.Label() 확장 메서드를 사용 하 여 ([큰 이미지를 보려면 클릭](creating-custom-html-helpers-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="d6ace-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>


<span data-ttu-id="d6ace-175">목록 4에서 수정 된 인덱스 뷰 Html.Label() 확장 메서드를 사용 하 여 렌더링할 모든 해당 `<label>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="d6ace-176">**4-목록 `Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="d6ace-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="d6ace-177">요약</span><span class="sxs-lookup"><span data-stu-id="d6ace-177">Summary</span></span>

<span data-ttu-id="d6ace-178">이 자습서에서는 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="d6ace-179">사용자 지정 하는 방법과 먼저 `Label()` HTML 도우미를 만들어 정적 메서드는 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="d6ace-180">사용자 지정 하는 방법과 어 `Label()` 에 확장 메서드를 만들어 HTML 도우미 메서드는 `HtmlHelper` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="d6ace-181">이 자습서에서는 매우 간단한 HTML 도우미 메서드를 작성에 집중 합니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="d6ace-182">실현 하는 HTML 도우미는 원하는 만큼 복잡 해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="d6ace-183">트리 뷰, 메뉴 또는 데이터베이스 데이터의 테이블과 같은 다양 한 콘텐츠를 렌더링 하는 HTML 도우미를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6ace-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d6ace-184">[이전](asp-net-mvc-views-overview-cs.md)
> [다음](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="d6ace-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>
