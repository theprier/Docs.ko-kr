---
uid: aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: "사용자 지정 HTML 도우미 (C#) 만들기 | Microsoft Docs"
author: microsoft
description: "이 자습서의 목표를 사용해 MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주기 위한 것입니다. HTML 도우미를 활용 하면..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: a0b6d67eb7aab51ba2b422fab0788e34255f2c8c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="creating-custom-html-helpers-c"></a><span data-ttu-id="b9f55-104">사용자 지정 HTML 도우미 (C#) 만들기</span><span class="sxs-lookup"><span data-stu-id="b9f55-104">Creating Custom HTML Helpers (C#)</span></span>
====================
<span data-ttu-id="b9f55-105">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b9f55-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="b9f55-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="b9f55-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="b9f55-107">이 자습서의 목표를 사용해 MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="b9f55-108">HTML 도우미 활용 함으로써 표준 HTML 페이지를 만들기 위해 수행 해야 하는 HTML 태그의 번거로운 입력의 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>


<span data-ttu-id="b9f55-109">이 자습서의 목표를 사용해 MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="b9f55-110">HTML 도우미 활용 함으로써 표준 HTML 페이지를 만들기 위해 수행 해야 하는 HTML 태그의 번거로운 입력의 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="b9f55-111">이 자습서의 첫 번째 부분에서 설명 기존 ASP.NET MVC 프레임 워크에 포함 된 HTML 도우미 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="b9f55-112">다음으로, 사용자 지정 HTML 도우미를 작성 하는 두 가지 방법 설명: 정적 메서드를 작성 하 고 확장 메서드를 만들어 사용자 지정 HTML 도우미를 만드는 방법을 설명할 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="b9f55-113">HTML 도우미 이해</span><span class="sxs-lookup"><span data-stu-id="b9f55-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="b9f55-114">HTML 도우미는 문자열을 반환 하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="b9f55-115">문자열에는 모든 유형의 원하는 콘텐츠를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="b9f55-116">예를 들어 HTML와 같은 표준 HTML 태그를 렌더링할 HTML 도우미를 사용할 수 있습니다 `<input>` 및 `<img>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="b9f55-117">탭 스트립 또는 데이터베이스 데이터의 HTML 테이블 등의 보다 복잡 한 콘텐츠를 렌더링할 HTML 도우미를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="b9f55-118">ASP.NET MVC 프레임 워크에는 다음과 같은 표준 HTML 도우미 (이것은 전체 목록이 아님) 집합이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="b9f55-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="b9f55-119">Html.ActionLink()</span></span>
- <span data-ttu-id="b9f55-120">Html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="b9f55-120">Html.BeginForm()</span></span>
- <span data-ttu-id="b9f55-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="b9f55-121">Html.CheckBox()</span></span>
- <span data-ttu-id="b9f55-122">Html.DropDownList()</span><span class="sxs-lookup"><span data-stu-id="b9f55-122">Html.DropDownList()</span></span>
- <span data-ttu-id="b9f55-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="b9f55-123">Html.EndForm()</span></span>
- <span data-ttu-id="b9f55-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="b9f55-124">Html.Hidden()</span></span>
- <span data-ttu-id="b9f55-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="b9f55-125">Html.ListBox()</span></span>
- <span data-ttu-id="b9f55-126">Html.Password()</span><span class="sxs-lookup"><span data-stu-id="b9f55-126">Html.Password()</span></span>
- <span data-ttu-id="b9f55-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="b9f55-127">Html.RadioButton()</span></span>
- <span data-ttu-id="b9f55-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="b9f55-128">Html.TextArea()</span></span>
- <span data-ttu-id="b9f55-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="b9f55-129">Html.TextBox()</span></span>

<span data-ttu-id="b9f55-130">폼 목록 1의 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="b9f55-131">이 양식은 두 (그림 1 참조)는 표준 HTML 도우미를 사용 하 여 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="b9f55-132">이 양식에서 사용 하 여 `Html.BeginForm()` 및 `Html.TextBox()` 양식을 렌더링 하는 간단한 HTML 도우미 메서드.</span><span class="sxs-lookup"><span data-stu-id="b9f55-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>


<span data-ttu-id="b9f55-133">[![HTML 도우미를 사용 하 여 페이지 렌더링](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b9f55-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="b9f55-134">**그림 01**: HTML 도우미를 사용 하 여 페이지 렌더링 ([전체 크기 이미지를 보려면 클릭](creating-custom-html-helpers-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="b9f55-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>


<span data-ttu-id="b9f55-135">**1 – 나열`Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="b9f55-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="b9f55-136">열기 및 닫기 HTML을 만들기 위해 Html.BeginForm() 도우미 메서드는 `<form>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="b9f55-137">다음에 유의 `Html.BeginForm()` using 내에서 메서드는 문입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="b9f55-138">문을 사용 하면는 `<form>` 태그를 사용 하 여 끝에 닫힐 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="b9f55-139">사용 하 여 만드는 대신 선호 하는 경우 블록을 닫는 Html.EndForm() 도우미 메서드를 호출할 수 있습니다는 `<form>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="b9f55-140">여는 만들기 및 닫기에 어떤 방법을 사용 하 여 `<form>` 가장 직관적으로 보이는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="b9f55-141">`Html.TextBox()` 도우미 메서드 목록 1의 HTML을 렌더링 하는 데 사용 됩니다 `<input>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="b9f55-142">선택 하면 소스 보기 브라우저에서 목록 2의 HTML 소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="b9f55-143">소스 표준 HTML 태그가 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9f55-144">에 `Html.TextBox()`HTML 도우미와 함께 렌더링 된 `<%= %>` 대신 태그 `<% %>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="b9f55-145">등호 기호를 포함 하지 않는 경우 브라우저에 렌더링 가져옵니다 nothing입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="b9f55-146">ASP.NET MVC 프레임 워크 도우미 중 작은 부분만 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="b9f55-147">대부분의 경우 사용자 지정 HTML 도우미와 MVC 프레임 워크를 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="b9f55-148">이 자습서의 나머지 부분에서는 사용자 지정 HTML 도우미를 작성 하는 두 가지 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="b9f55-149">**2 – 나열`Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="b9f55-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="b9f55-150">정적 메서드를 사용 하 여 HTML 도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="b9f55-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="b9f55-151">새 HTML 도우미를 만드는 가장 쉬운 방법은 문자열을 반환 하는 정적 메서드를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="b9f55-152">한다고 가정, 예를 들어 HTML을 렌더링 하는 새 HTML 도우미 만들려는 `<label>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="b9f55-153">목록 2 클래스를 사용 하 여 렌더링 하는 수는 `<label>` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="b9f55-154">**2 – 나열`Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="b9f55-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="b9f55-155">목록 2의 클래스에 대 한 특별 한 일은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="b9f55-156">`Label()` 메서드는 단순히 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="b9f55-157">목록 3에서 수정 된 인덱스 뷰를 사용 하는 `LabelHelper` HTML을 렌더링 하 `<label>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="b9f55-158">공지 보기를 포함 하는 `<%@ imports %>` 가져오는 지시문의 `Application1.Helpers` 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="b9f55-159">**2 – 나열`Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="b9f55-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="b9f55-160">확장 메서드를 사용 하 여 HTML 도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="b9f55-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="b9f55-161">만들려는 경우에 작동 하는 HTML 도우미 확장 메서드를 만들어야 하는 다음 ASP.NET MVC 프레임 워크에 포함 된 표준 HTML 도우미 같은입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="b9f55-162">확장 메서드를 사용 하 여 기존 클래스에 새 메서드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="b9f55-163">HTML 도우미 메서드를 만들 때 뷰의 Html 속성으로 표현 HtmlHelper 클래스에 새 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="b9f55-164">확장 메서드를 추가 하는 보기 3의 클래스는 `HtmlHelper` 라는 클래스 `Label()`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="b9f55-165">이 클래스에 대 한 주의 해야 하는 것의 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="b9f55-166">첫째, 클래스는 정적 클래스 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="b9f55-167">정적 클래스와 확장 메서드를 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="b9f55-168">둘째, 알 수 있듯이 첫 번째 매개 변수에 `Label()` 메서드 키워드에 의해 앞 `this`합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="b9f55-169">확장 메서드의 첫 번째 매개 변수는 확장 메서드를 확장 하는 클래스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="b9f55-170">**3 – 나열`Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="b9f55-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="b9f55-171">확장 메서드 같은 모든 클래스의 다른 메서드에서 Visual Studio Intellisense에 표시 되는 확장 메서드를 만들고 응용 프로그램을 성공적으로 작성 한 후 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="b9f55-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="b9f55-172">유일한 차이점은 해당 확장 메서드는 특수 기호가 옆에 (아래쪽 화살표 아이콘)와 함께 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>


<span data-ttu-id="b9f55-173">[![Html.Label() 확장 메서드를 사용 하 여](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="b9f55-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="b9f55-174">**그림 02**: Html.Label() 확장 메서드를 사용 하 여 ([전체 크기 이미지를 보려면 클릭](creating-custom-html-helpers-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="b9f55-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>


<span data-ttu-id="b9f55-175">수정한 인덱스 뷰 목록 4에서의 모든 렌더링를 Html.Label() 확장 메서드를 사용 하 여 해당 `<label>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="b9f55-176">**4 – 나열`Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="b9f55-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="b9f55-177">요약</span><span class="sxs-lookup"><span data-stu-id="b9f55-177">Summary</span></span>

<span data-ttu-id="b9f55-178">이 자습서에서는 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="b9f55-179">사용자 지정을 만드는 방법을 배웠습니다 먼저 `Label()` 정적 메서드를 만들어 HTML 도우미는 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="b9f55-180">다음으로, 사용자 지정을 만드는 방법을 배웠습니다 `Label()` 에 확장 메서드를 만들어 HTML 도우미 메서드는 `HtmlHelper` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="b9f55-181">이 자습서에서는 매우 간단한 HTML 도우미 메서드는 구축에 집중 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="b9f55-182">참고로, 하는 HTML 도우미는 원하는 만큼 복잡 해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="b9f55-183">트리 뷰, 메뉴 또는 데이터베이스 데이터 테이블 같은 풍부한 콘텐츠를 렌더링 하는 HTML 도우미를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9f55-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="b9f55-184">[이전](asp-net-mvc-views-overview-cs.md)
[다음](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="b9f55-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>
