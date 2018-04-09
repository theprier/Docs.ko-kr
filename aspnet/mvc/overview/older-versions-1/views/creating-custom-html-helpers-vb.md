---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: 사용자 지정 HTML 도우미 (VB) 만들기 | Microsoft Docs
author: microsoft
description: 이 자습서의 목표를 사용해 MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주기 위한 것입니다. HTML 도우미를 활용 하면...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 6980026e2653eacb71697f9b34def9bc38638726
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="creating-custom-html-helpers-vb"></a><span data-ttu-id="02b68-104">사용자 지정 HTML 도우미 (VB) 만들기</span><span class="sxs-lookup"><span data-stu-id="02b68-104">Creating Custom HTML Helpers (VB)</span></span>
====================
<span data-ttu-id="02b68-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="02b68-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="02b68-106">PDF 다운로드</span><span class="sxs-lookup"><span data-stu-id="02b68-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> <span data-ttu-id="02b68-107">이 자습서의 목표를 사용해 MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="02b68-108">HTML 도우미 활용 함으로써 표준 HTML 페이지를 만들기 위해 수행 해야 하는 HTML 태그의 번거로운 입력의 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>


<span data-ttu-id="02b68-109">이 자습서의 목표를 사용해 MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만드는 방법을 보여 주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="02b68-110">HTML 도우미 활용 함으로써 표준 HTML 페이지를 만들기 위해 수행 해야 하는 HTML 태그의 번거로운 입력의 양을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="02b68-111">이 자습서의 첫 번째 부분에서 설명 기존 ASP.NET MVC 프레임 워크에 포함 된 HTML 도우미 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="02b68-112">다음으로, 사용자 지정 HTML 도우미를 작성 하는 두 가지 방법 설명: I 공유 메서드를 작성 하 고 확장 메서드를 만들어 사용자 지정 HTML 도우미를 만드는 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a shared method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="02b68-113">HTML 도우미 이해</span><span class="sxs-lookup"><span data-stu-id="02b68-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="02b68-114">HTML 도우미는 문자열을 반환 하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="02b68-115">문자열에는 모든 유형의 원하는 콘텐츠를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="02b68-116">예를 들어 HTML와 같은 표준 HTML 태그를 렌더링할 HTML 도우미를 사용할 수 있습니다 `<input>` 및 `<img>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="02b68-117">탭 스트립 또는 데이터베이스 데이터의 HTML 테이블 등의 보다 복잡 한 콘텐츠를 렌더링할 HTML 도우미를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="02b68-118">ASP.NET MVC 프레임 워크에는 다음과 같은 표준 HTML 도우미 (이것은 전체 목록이 아님) 집합이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="02b68-119">Html.ActionLink()</span><span class="sxs-lookup"><span data-stu-id="02b68-119">Html.ActionLink()</span></span>
- <span data-ttu-id="02b68-120">Html.BeginForm()</span><span class="sxs-lookup"><span data-stu-id="02b68-120">Html.BeginForm()</span></span>
- <span data-ttu-id="02b68-121">Html.CheckBox()</span><span class="sxs-lookup"><span data-stu-id="02b68-121">Html.CheckBox()</span></span>
- <span data-ttu-id="02b68-122">Html.DropDownList()</span><span class="sxs-lookup"><span data-stu-id="02b68-122">Html.DropDownList()</span></span>
- <span data-ttu-id="02b68-123">Html.EndForm()</span><span class="sxs-lookup"><span data-stu-id="02b68-123">Html.EndForm()</span></span>
- <span data-ttu-id="02b68-124">Html.Hidden()</span><span class="sxs-lookup"><span data-stu-id="02b68-124">Html.Hidden()</span></span>
- <span data-ttu-id="02b68-125">Html.ListBox()</span><span class="sxs-lookup"><span data-stu-id="02b68-125">Html.ListBox()</span></span>
- <span data-ttu-id="02b68-126">Html.Password()</span><span class="sxs-lookup"><span data-stu-id="02b68-126">Html.Password()</span></span>
- <span data-ttu-id="02b68-127">Html.RadioButton()</span><span class="sxs-lookup"><span data-stu-id="02b68-127">Html.RadioButton()</span></span>
- <span data-ttu-id="02b68-128">Html.TextArea()</span><span class="sxs-lookup"><span data-stu-id="02b68-128">Html.TextArea()</span></span>
- <span data-ttu-id="02b68-129">Html.TextBox()</span><span class="sxs-lookup"><span data-stu-id="02b68-129">Html.TextBox()</span></span>

<span data-ttu-id="02b68-130">폼 목록 1의 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="02b68-131">이 양식은 두 (그림 1 참조)는 표준 HTML 도우미를 사용 하 여 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="02b68-132">이 양식에서 사용 하 여 `Html.BeginForm()` 및 `Html.TextBox()` 도우미 메서드.</span><span class="sxs-lookup"><span data-stu-id="02b68-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods.</span></span>


<span data-ttu-id="02b68-133">[![HTML 도우미를 사용 하 여 페이지 렌더링](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="02b68-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="02b68-134">**그림 01**: HTML 도우미를 사용 하 여 페이지 렌더링 ([전체 크기 이미지를 보려면 클릭](creating-custom-html-helpers-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="02b68-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image3.png))</span></span>


<span data-ttu-id="02b68-135">**1 – 나열 `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="02b68-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

<span data-ttu-id="02b68-136">`Html.BeginForm()` 중괄호와 닫는 HTML을 만들기 위해 도우미 메서드는 `<form>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-136">The `Html.BeginForm()` Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="02b68-137">다음에 유의 `Html.BeginForm()` using 내에서 메서드는 문입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="02b68-138">문을 사용 하면는 `<form>` 태그를 사용 하 여 끝에 닫힐 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="02b68-139">사용 하 여 만드는 대신 선호 하는 경우 블록을 닫는 Html.EndForm() 도우미 메서드를 호출할 수 있습니다는 `<form>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="02b68-140">여는 만들기 및 닫기에 어떤 방법을 사용 하 여 `<form>` 가장 직관적으로 보이는 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="02b68-141">`Html.TextBox()` 도우미 메서드 목록 1의 HTML을 렌더링 하는 데 사용 됩니다 `<input>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="02b68-142">선택 하면 소스 보기 브라우저에서 목록 2의 HTML 소스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="02b68-143">소스 표준 HTML 태그가 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02b68-144">에 `Html.TextBox()`HTML 도우미와 함께 렌더링 된 `<%= %>` 대신 태그 `<% %>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="02b68-145">등호 기호를 포함 하지 않는 경우 브라우저에 렌더링 가져옵니다 nothing입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="02b68-146">ASP.NET MVC 프레임 워크 도우미 중 작은 부분만 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="02b68-147">대부분의 경우 사용자 지정 HTML 도우미와 MVC 프레임 워크를 확장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="02b68-148">이 자습서의 나머지 부분에서는 사용자 지정 HTML 도우미를 작성 하는 두 가지 방법에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="02b68-149">**2 – 나열 `Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="02b68-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a><span data-ttu-id="02b68-150">공유 메서드를 사용 하 여 HTML 도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="02b68-150">Creating HTML Helpers with Shared Methods</span></span>

<span data-ttu-id="02b68-151">새 HTML 도우미를 만드는 가장 쉬운 방법은 문자열을 반환 하는 공유 메서드를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-151">The easiest way to create a new HTML Helper is to create a shared method that returns a string.</span></span> <span data-ttu-id="02b68-152">한다고 가정, 예를 들어 HTML을 렌더링 하는 새 HTML 도우미 만들려는 `<label>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="02b68-153">목록 2 클래스를 사용 하 여 렌더링 하는 수는 `<label>`합니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-153">You can use the class in Listing 2 to render a `<label>`.</span></span>

<span data-ttu-id="02b68-154">**2 – 나열 `Helpers\LabelHelper.vb`**</span><span class="sxs-lookup"><span data-stu-id="02b68-154">**Listing 2 – `Helpers\LabelHelper.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

<span data-ttu-id="02b68-155">목록 2의 클래스에 대 한 특별 한 일은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="02b68-156">`Label()` 메서드는 단순히 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="02b68-157">목록 3에서 수정 된 인덱스 뷰를 사용 하는 `LabelHelper` HTML을 렌더링 하 `<label>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="02b68-158">공지 보기를 포함 하는 `<%@ imports %>` 지시문에 Application1.Helpers 네임 스페이스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-158">Notice that the view includes an `<%@ imports %>` directive that imports the Application1.Helpers namespace.</span></span>

<span data-ttu-id="02b68-159">**2 – 나열 `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="02b68-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="02b68-160">확장 메서드를 사용 하 여 HTML 도우미 만들기</span><span class="sxs-lookup"><span data-stu-id="02b68-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="02b68-161">만들려는 경우에 작동 하는 HTML 도우미 확장 메서드를 만들어야 하는 다음 ASP.NET MVC 프레임 워크에 포함 된 표준 HTML 도우미 같은입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="02b68-162">확장 메서드를 사용 하 여 기존 클래스에 새 메서드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="02b68-163">새 메서드를 추가 하는 HTML 도우미 메서드를 만들 때의 `HtmlHelper` 뷰의 Html 속성으로 표현 되는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-163">When creating an HTML Helper method, you add new methods to the `HtmlHelper` class represented by a view's Html property.</span></span>

<span data-ttu-id="02b68-164">라는 확장 메서드를 추가 하는 보기 3의 Visual Basic 모듈 `Label()` 에 `HtmlHelper` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-164">The Visual Basic module in Listing 3 adds an extension method named `Label()` to the `HtmlHelper` class.</span></span> <span data-ttu-id="02b68-165">이 모듈에 대 한 주의 해야 하는 것의 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-165">There are a couple of things that you should notice about this module.</span></span> <span data-ttu-id="02b68-166">첫째, 모듈으로 데코레이팅은 확인할 수는 `<Extension()>` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-166">First, notice that the module is decorated with the `<Extension()>` attribute.</span></span> <span data-ttu-id="02b68-167">이 특성을 사용 하려면 가져와야는 `System.Runtime.CompilerServices` 네임 스페이스</span><span class="sxs-lookup"><span data-stu-id="02b68-167">In order to use this attribute, you must import the `System.Runtime.CompilerServices` namespace</span></span>

<span data-ttu-id="02b68-168">둘째, 알 수 있듯이의 첫 번째 매개 변수는 `Label()` 메서드가 `HtmlHelper` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-168">Second, notice that the first parameter of the `Label()` method represents the `HtmlHelper` class.</span></span> <span data-ttu-id="02b68-169">확장 메서드의 첫 번째 매개 변수는 확장 메서드를 확장 하는 클래스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="02b68-170">**3 – 나열 `Helpers\LabelExtensions.vb`**</span><span class="sxs-lookup"><span data-stu-id="02b68-170">**Listing 3 – `Helpers\LabelExtensions.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

<span data-ttu-id="02b68-171">확장 메서드 같은 모든 클래스의 다른 메서드에서 Visual Studio Intellisense에 표시 되는 확장 메서드를 만들고 응용 프로그램을 성공적으로 작성 한 후 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="02b68-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="02b68-172">유일한 차이점은 해당 확장 메서드는 특수 기호가 옆에 (아래쪽 화살표 아이콘)와 함께 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>


<span data-ttu-id="02b68-173">[![Html.Label() 확장 메서드를 사용 하 여](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="02b68-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span></span>

<span data-ttu-id="02b68-174">**그림 02**: Html.Label() 확장 메서드를 사용 하 여 ([전체 크기 이미지를 보려면 클릭](creating-custom-html-helpers-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="02b68-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image6.png))</span></span>


<span data-ttu-id="02b68-175">수정한 인덱스 뷰 목록 4에 Html.Label() 확장 메서드를 사용 하 여 모든 렌더링 하는 &lt;레이블&gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its &lt;label&gt; tags.</span></span>

<span data-ttu-id="02b68-176">**4 – 나열 `Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="02b68-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="02b68-177">요약</span><span class="sxs-lookup"><span data-stu-id="02b68-177">Summary</span></span>

<span data-ttu-id="02b68-178">이 자습서에서는 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="02b68-179">사용자 지정을 만드는 방법을 배웠습니다 먼저 `Label()` HTML 도우미 메서드를 만들어를 공유 하는 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-179">First, you learned how to create a custom `Label()` HTML Helper by creating a shared method that returns a string.</span></span> <span data-ttu-id="02b68-180">다음으로, 사용자 지정을 만드는 방법을 배웠습니다 `Label()` 에 확장 메서드를 만들어 HTML 도우미 메서드는 `HtmlHelper` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="02b68-181">이 자습서에서는 매우 간단한 HTML 도우미 메서드는 구축에 집중 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="02b68-182">참고로, 하는 HTML 도우미는 원하는 만큼 복잡 해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="02b68-183">트리 뷰, 메뉴 또는 데이터베이스 데이터 테이블 같은 풍부한 콘텐츠를 렌더링 하는 HTML 도우미를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b68-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="02b68-184">[이전](asp-net-mvc-views-overview-vb.md)
> [다음](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="02b68-184">[Previous](asp-net-mvc-views-overview-vb.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span></span>
