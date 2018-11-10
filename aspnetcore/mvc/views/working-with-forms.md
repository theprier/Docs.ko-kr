---
title: ASP.NET Core 형식의 태그 도우미
author: rick-anderson
description: 형식과 함께 사용되는 기본 제공 태그 도우미를 설명합니다.
ms.author: riande
ms.custom: mvc
ms.date: 10/24/2018
uid: mvc/views/working-with-forms
ms.openlocfilehash: 7319fbbfe3e78e61526f9042b2b6004a351c2186
ms.sourcegitcommit: 2ef32676c16f76282f7c23154d13affce8c8bf35
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50234620"
---
# <a name="tag-helpers-in-forms-in-aspnet-core"></a><span data-ttu-id="ca37f-103">ASP.NET Core 형식의 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="ca37f-103">Tag Helpers in forms in ASP.NET Core</span></span>

<span data-ttu-id="ca37f-104">작성자 [Rick Anderson](https://twitter.com/RickAndMSFT), [Dave Paquette](https://twitter.com/Dave_Paquette) 및 [Jerrie Pelser](https://github.com/jerriep)</span><span class="sxs-lookup"><span data-stu-id="ca37f-104">By [Rick Anderson](https://twitter.com/RickAndMSFT), [Dave Paquette](https://twitter.com/Dave_Paquette), and [Jerrie Pelser](https://github.com/jerriep)</span></span>

<span data-ttu-id="ca37f-105">이 문서에서는 형식 및 형식에서 일반적으로 사용되는 HTML 요소 작업을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-105">This document demonstrates working with Forms and the HTML elements commonly used on a Form.</span></span> <span data-ttu-id="ca37f-106">HTML [형식](https://www.w3.org/TR/html401/interact/forms.html) 요소는 서버에 데이터를 다시 게시하는 기본 메커니즘 웹앱을 사용하도록 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-106">The HTML [Form](https://www.w3.org/TR/html401/interact/forms.html) element provides the primary mechanism web apps use to post back data to the server.</span></span> <span data-ttu-id="ca37f-107">이 문서에서는 대부분 [태그 도우미](tag-helpers/intro.md) 및 강력한 HTML 형식을 생산적으로 만들 수 있는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-107">Most of this document describes [Tag Helpers](tag-helpers/intro.md) and how they can help you productively create robust HTML forms.</span></span> <span data-ttu-id="ca37f-108">이 문서를 읽기 전에 [태그 도우미 소개](tag-helpers/intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca37f-108">We recommend you read [Introduction to Tag Helpers](tag-helpers/intro.md) before you read this document.</span></span>

<span data-ttu-id="ca37f-109">많은 경우 HTML 도우미는 특정 태그 도우미에 대한 대체 방법을 제공하지만, 태그 도우미는 HTML 도우미를 대체하지 않으며 각 HTML 도우미에 대한 태그 도우미가 없다는 사실을 인지하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-109">In many cases, HTML Helpers provide an alternative approach to a specific Tag Helper, but it's important to recognize that Tag Helpers don't replace HTML Helpers and there's not a Tag Helper for each HTML Helper.</span></span> <span data-ttu-id="ca37f-110">HTML 도우미 대안이 있다면 그 내용도 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-110">When an HTML Helper alternative exists, it's mentioned.</span></span>

<a name="my-asp-route-param-ref-label"></a>

## <a name="the-form-tag-helper"></a><span data-ttu-id="ca37f-111">형식 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="ca37f-111">The Form Tag Helper</span></span>

<span data-ttu-id="ca37f-112">[형식](https://www.w3.org/TR/html401/interact/forms.html) 태그 도우미:</span><span class="sxs-lookup"><span data-stu-id="ca37f-112">The [Form](https://www.w3.org/TR/html401/interact/forms.html) Tag Helper:</span></span>

* <span data-ttu-id="ca37f-113">MVC 컨트롤러 동작 또는 명명된 경로에 대한 HTML [\<FORM>](https://www.w3.org/TR/html401/interact/forms.html) `action` 특성 값을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-113">Generates the HTML [\<FORM>](https://www.w3.org/TR/html401/interact/forms.html) `action` attribute value for a MVC controller action or named route</span></span>

* <span data-ttu-id="ca37f-114">사이트 간 요청 위조를 방지하기 위해 숨겨진 [요청 확인 토큰](/aspnet/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages)을 만듭니다(HTTP Post 작업 메서드에서 `[ValidateAntiForgeryToken]` 특성과 함께 사용할 경우).</span><span class="sxs-lookup"><span data-stu-id="ca37f-114">Generates a hidden [Request Verification Token](/aspnet/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) to prevent cross-site request forgery (when used with the `[ValidateAntiForgeryToken]` attribute in the HTTP Post action method)</span></span>

* <span data-ttu-id="ca37f-115">`asp-route-<Parameter Name>` 특성을 제공합니다. 여기서 `<Parameter Name>`을 경로 값에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-115">Provides the `asp-route-<Parameter Name>` attribute, where `<Parameter Name>` is added to the route values.</span></span> <span data-ttu-id="ca37f-116">`Html.BeginForm` 및 `Html.BeginRouteForm`에 대한 `routeValues` 매개 변수는 유사한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-116">The  `routeValues` parameters to `Html.BeginForm` and `Html.BeginRouteForm` provide similar functionality.</span></span>

* <span data-ttu-id="ca37f-117">HTML 도우미 대안 `Html.BeginForm` 및 `Html.BeginRouteForm`가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-117">Has an HTML Helper alternative `Html.BeginForm` and `Html.BeginRouteForm`</span></span>

<span data-ttu-id="ca37f-118">예제:</span><span class="sxs-lookup"><span data-stu-id="ca37f-118">Sample:</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Demo/RegisterFormOnly.cshtml)]

<span data-ttu-id="ca37f-119">위의 형식 태그 도우미에서는 다음 HTML을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-119">The Form Tag Helper above generates the following HTML:</span></span>

```HTML
<form method="post" action="/Demo/Register">
    <!-- Input and Submit elements -->
    <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
</form>
```

<span data-ttu-id="ca37f-120">MVC 런타임은 형식 태그 도우미 특성 `asp-controller` 및 `asp-action`에서 `action` 특성 값을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-120">The MVC runtime generates the `action` attribute value from the Form Tag Helper attributes `asp-controller` and `asp-action`.</span></span> <span data-ttu-id="ca37f-121">형식 태그 도우미도 사이트 간 요청 위조를 방지하기 위해 숨겨진 [요청 확인 토큰](/aspnet/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages)을 만듭니다(HTTP Post 작업 메서드에서 `[ValidateAntiForgeryToken]` 특성과 함께 사용할 경우).</span><span class="sxs-lookup"><span data-stu-id="ca37f-121">The Form Tag Helper also generates a hidden [Request Verification Token](/aspnet/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) to prevent cross-site request forgery (when used with the `[ValidateAntiForgeryToken]` attribute in the HTTP Post action method).</span></span> <span data-ttu-id="ca37f-122">사이트 간 요청 위조로부터 순수한 HTML 형식을 보호하기는 어렵습니다. 형식 태그 도우미는 이러한 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-122">Protecting a pure HTML Form from cross-site request forgery is difficult, the Form Tag Helper provides this service for you.</span></span>

### <a name="using-a-named-route"></a><span data-ttu-id="ca37f-123">명명된 경로 사용</span><span class="sxs-lookup"><span data-stu-id="ca37f-123">Using a named route</span></span>

<span data-ttu-id="ca37f-124">`asp-route` 태그 도우미 특성은 HTML `action` 특성에 대한 태그를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-124">The `asp-route` Tag Helper attribute can also generate markup for the HTML `action` attribute.</span></span> <span data-ttu-id="ca37f-125">`register`라는 [경로](../../fundamentals/routing.md)를 사용하는 앱은 등록 페이지에 다음 태그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-125">An app with a [route](../../fundamentals/routing.md)  named `register` could use the following markup for the registration page:</span></span>

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Demo/RegisterRoute.cshtml)]

<span data-ttu-id="ca37f-126">*보기/계정* 폴더의 보기 중 다수(*개별 사용자 계정*을 사용하여 새로운 웹앱을 만들 때 생성됨)에는 [asp-route-returnurl](xref:mvc/views/working-with-forms) 특성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-126">Many of the views in the *Views/Account* folder (generated when you create a new web app with *Individual User Accounts*) contain the [asp-route-returnurl](xref:mvc/views/working-with-forms) attribute:</span></span>

```cshtml
<form asp-controller="Account" asp-action="Login"
     asp-route-returnurl="@ViewData["ReturnUrl"]"
     method="post" class="form-horizontal" role="form">
```

>[!NOTE]
><span data-ttu-id="ca37f-127">기본 제공된 템플릿을 사용하면 권한이 부여된 리소스에 액세스하려고 하지만 인증되거나 권한이 없는 경우에만 `returnUrl`이 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-127">With the built in templates, `returnUrl` is only populated automatically when you try to access an authorized resource but are not authenticated or authorized.</span></span> <span data-ttu-id="ca37f-128">권한이 없는 액세스를 시도하는 경우 보안 미들웨어는 사용자를 `returnUrl` 설정이 포함된 로그인 페이지에 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-128">When you attempt an unauthorized access, the security middleware redirects you to the login page with the `returnUrl` set.</span></span>

## <a name="the-input-tag-helper"></a><span data-ttu-id="ca37f-129">입력 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="ca37f-129">The Input Tag Helper</span></span>

<span data-ttu-id="ca37f-130">입력 태그 도우미는 HTML [\<input>](https://www.w3.org/wiki/HTML/Elements/input) 요소를 Razor 보기의 모델 식에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-130">The Input Tag Helper binds an HTML [\<input>](https://www.w3.org/wiki/HTML/Elements/input) element to a model expression in your razor view.</span></span>

<span data-ttu-id="ca37f-131">구문:</span><span class="sxs-lookup"><span data-stu-id="ca37f-131">Syntax:</span></span>

```HTML
<input asp-for="<Expression Name>" />
```

<span data-ttu-id="ca37f-132">입력 태그 도우미:</span><span class="sxs-lookup"><span data-stu-id="ca37f-132">The Input Tag Helper:</span></span>

* <span data-ttu-id="ca37f-133">`asp-for` 특성에 지정된 식 이름에 대해 `id` 및 `name` HTML 특성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-133">Generates the `id` and `name` HTML attributes for the expression name specified in the `asp-for` attribute.</span></span> <span data-ttu-id="ca37f-134">`asp-for="Property1.Property2"`는 `m => m.Property1.Property2`와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-134">`asp-for="Property1.Property2"` is equivalent to `m => m.Property1.Property2`.</span></span> <span data-ttu-id="ca37f-135">식의 이름은 `asp-for` 특성 값에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-135">The name of the expression is what is used for the `asp-for` attribute value.</span></span> <span data-ttu-id="ca37f-136">추가 정보는 [식 이름](#expression-names) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca37f-136">See the [Expression names](#expression-names) section for additional information.</span></span>

* <span data-ttu-id="ca37f-137">모델 속성에 적용된 모델 형식 및 [데이터 주석](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.iattributeadapter) 특성에 따라 HTML `type` 특성 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-137">Sets the HTML `type` attribute value based on the model type and  [data annotation](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.iattributeadapter) attributes applied to the model property</span></span>

* <span data-ttu-id="ca37f-138">HTML `type` 특성 값이 지정 된 경우 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-138">Won't overwrite the HTML `type` attribute value when one is specified</span></span>

* <span data-ttu-id="ca37f-139">모델 속성에 적용되는 [데이터 주석](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.iattributeadapter) 특성에서 [HTML5](https://developer.mozilla.org/docs/Web/Guide/HTML/HTML5) 유효성 검사 특성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-139">Generates [HTML5](https://developer.mozilla.org/docs/Web/Guide/HTML/HTML5)  validation attributes from [data annotation](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.iattributeadapter) attributes applied to model properties</span></span>

* <span data-ttu-id="ca37f-140">`Html.TextBoxFor` 및 `Html.EditorFor`와 HTML 도우미 기능이 겹칩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-140">Has an HTML Helper feature overlap with `Html.TextBoxFor` and `Html.EditorFor`.</span></span> <span data-ttu-id="ca37f-141">자세한 내용은 **입력 태그 도우미에 대한 HTML 도우미 대안** 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca37f-141">See the **HTML Helper alternatives to Input Tag Helper** section for details.</span></span>

* <span data-ttu-id="ca37f-142">강력한 형식 지정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-142">Provides strong typing.</span></span> <span data-ttu-id="ca37f-143">속성의 이름이 변경되고 태그 도우미를 업데이트하지 않은 경우 다음과 비슷한 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-143">If the name of the property changes and you don't update the Tag Helper you'll get an error similar to the following:</span></span>

```HTML
An error occurred during the compilation of a resource required to process
this request. Please review the following specific error details and modify
your source code appropriately.

Type expected
 'RegisterViewModel' does not contain a definition for 'Email' and no
 extension method 'Email' accepting a first argument of type 'RegisterViewModel'
 could be found (are you missing a using directive or an assembly reference?)
```

<span data-ttu-id="ca37f-144">`Input` 태그 도우미는 .NET 형식을 기반으로 HTML `type` 특성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-144">The `Input` Tag Helper sets the HTML `type` attribute based on the .NET type.</span></span> <span data-ttu-id="ca37f-145">다음 표에서는 몇 가지 일반적인 .NET 형식 및 생성된 HTML 형식을 나열합니다(.NET 형식의 일부만 나열됨).</span><span class="sxs-lookup"><span data-stu-id="ca37f-145">The following table lists some common .NET types and generated HTML type (not every .NET type is listed).</span></span>

|<span data-ttu-id="ca37f-146">.NET 형식</span><span class="sxs-lookup"><span data-stu-id="ca37f-146">.NET type</span></span>|<span data-ttu-id="ca37f-147">입력 형식</span><span class="sxs-lookup"><span data-stu-id="ca37f-147">Input Type</span></span>|
|---|---|
|<span data-ttu-id="ca37f-148">Bool</span><span class="sxs-lookup"><span data-stu-id="ca37f-148">Bool</span></span>|<span data-ttu-id="ca37f-149">type="checkbox"</span><span class="sxs-lookup"><span data-stu-id="ca37f-149">type="checkbox"</span></span>|
|<span data-ttu-id="ca37f-150">문자열</span><span class="sxs-lookup"><span data-stu-id="ca37f-150">String</span></span>|<span data-ttu-id="ca37f-151">type="text"</span><span class="sxs-lookup"><span data-stu-id="ca37f-151">type="text"</span></span>|
|<span data-ttu-id="ca37f-152">DateTime</span><span class="sxs-lookup"><span data-stu-id="ca37f-152">DateTime</span></span>|<span data-ttu-id="ca37f-153">type="datetime"</span><span class="sxs-lookup"><span data-stu-id="ca37f-153">type="datetime"</span></span>|
|<span data-ttu-id="ca37f-154">Byte</span><span class="sxs-lookup"><span data-stu-id="ca37f-154">Byte</span></span>|<span data-ttu-id="ca37f-155">type="number"</span><span class="sxs-lookup"><span data-stu-id="ca37f-155">type="number"</span></span>|
|<span data-ttu-id="ca37f-156">Int</span><span class="sxs-lookup"><span data-stu-id="ca37f-156">Int</span></span>|<span data-ttu-id="ca37f-157">type="number"</span><span class="sxs-lookup"><span data-stu-id="ca37f-157">type="number"</span></span>|
|<span data-ttu-id="ca37f-158">Single, Double</span><span class="sxs-lookup"><span data-stu-id="ca37f-158">Single, Double</span></span>|<span data-ttu-id="ca37f-159">type="number"</span><span class="sxs-lookup"><span data-stu-id="ca37f-159">type="number"</span></span>|


<span data-ttu-id="ca37f-160">다음 표에서는 입력 태그 도우미가 특정 입력 형식에 매핑되는 몇 가지 일반적인 [데이터 주석](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.iattributeadapter) 특성을 보여줍니다(유효성 검사 특성의 일부만 나열됨).</span><span class="sxs-lookup"><span data-stu-id="ca37f-160">The following table shows some common [data annotations](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.iattributeadapter) attributes that the input tag helper will map to specific input types (not every validation attribute is listed):</span></span>


|<span data-ttu-id="ca37f-161">특성</span><span class="sxs-lookup"><span data-stu-id="ca37f-161">Attribute</span></span>|<span data-ttu-id="ca37f-162">입력 형식</span><span class="sxs-lookup"><span data-stu-id="ca37f-162">Input Type</span></span>|
|---|---|
|<span data-ttu-id="ca37f-163">[EmailAddress]</span><span class="sxs-lookup"><span data-stu-id="ca37f-163">[EmailAddress]</span></span>|<span data-ttu-id="ca37f-164">type="email"</span><span class="sxs-lookup"><span data-stu-id="ca37f-164">type="email"</span></span>|
|<span data-ttu-id="ca37f-165">[Url]</span><span class="sxs-lookup"><span data-stu-id="ca37f-165">[Url]</span></span>|<span data-ttu-id="ca37f-166">type="url"</span><span class="sxs-lookup"><span data-stu-id="ca37f-166">type="url"</span></span>|
|<span data-ttu-id="ca37f-167">[HiddenInput]</span><span class="sxs-lookup"><span data-stu-id="ca37f-167">[HiddenInput]</span></span>|<span data-ttu-id="ca37f-168">type="hidden"</span><span class="sxs-lookup"><span data-stu-id="ca37f-168">type="hidden"</span></span>|
|<span data-ttu-id="ca37f-169">[Phone]</span><span class="sxs-lookup"><span data-stu-id="ca37f-169">[Phone]</span></span>|<span data-ttu-id="ca37f-170">type="tel"</span><span class="sxs-lookup"><span data-stu-id="ca37f-170">type="tel"</span></span>|
|<span data-ttu-id="ca37f-171">[DataType(DataType.Password)]</span><span class="sxs-lookup"><span data-stu-id="ca37f-171">[DataType(DataType.Password)]</span></span>| <span data-ttu-id="ca37f-172">type="password"</span><span class="sxs-lookup"><span data-stu-id="ca37f-172">type="password"</span></span>|
|<span data-ttu-id="ca37f-173">[DataType(DataType.Date)]</span><span class="sxs-lookup"><span data-stu-id="ca37f-173">[DataType(DataType.Date)]</span></span>| <span data-ttu-id="ca37f-174">type="date"</span><span class="sxs-lookup"><span data-stu-id="ca37f-174">type="date"</span></span>|
|<span data-ttu-id="ca37f-175">[DataType(DataType.Time)]</span><span class="sxs-lookup"><span data-stu-id="ca37f-175">[DataType(DataType.Time)]</span></span>| <span data-ttu-id="ca37f-176">type="time"</span><span class="sxs-lookup"><span data-stu-id="ca37f-176">type="time"</span></span>|


<span data-ttu-id="ca37f-177">예제:</span><span class="sxs-lookup"><span data-stu-id="ca37f-177">Sample:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/RegisterViewModel.cs)]

[!code-HTML[](working-with-forms/sample/final/Views/Demo/RegisterInput.cshtml)]

<span data-ttu-id="ca37f-178">위의 코드는 다음과 같은 HTML을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-178">The code above generates the following HTML:</span></span>

```HTML
  <form method="post" action="/Demo/RegisterInput">
       Email:
       <input type="email" data-val="true"
              data-val-email="The Email Address field is not a valid email address."
              data-val-required="The Email Address field is required."
              id="Email" name="Email" value="" /> <br>
       Password:
       <input type="password" data-val="true"
              data-val-required="The Password field is required."
              id="Password" name="Password" /><br>
       <button type="submit">Register</button>
     <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
   </form>
```

<span data-ttu-id="ca37f-179">`Email` 및 `Password` 속성에 적용할 데이터 주석은 모델에서 메타데이터를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-179">The data annotations applied to the `Email` and `Password` properties generate metadata on the model.</span></span> <span data-ttu-id="ca37f-180">입력 태그 도우미는 모델 메타데이터를 사용하고 [HTML5](https://developer.mozilla.org/docs/Web/Guide/HTML/HTML5) `data-val-*` 특성을 생성합니다([모델 유효성 검사](../models/validation.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="ca37f-180">The Input Tag Helper consumes the model metadata and produces [HTML5](https://developer.mozilla.org/docs/Web/Guide/HTML/HTML5) `data-val-*` attributes (see [Model Validation](../models/validation.md)).</span></span> <span data-ttu-id="ca37f-181">이러한 특성에서는 입력 필드에 연결할 유효성 검사기를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-181">These attributes describe the validators to attach to the input fields.</span></span> <span data-ttu-id="ca37f-182">이 기능은 비간섭 HTML5 및 [jQuery](https://jquery.com/) 유효성 검사를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-182">This provides unobtrusive HTML5 and [jQuery](https://jquery.com/) validation.</span></span> <span data-ttu-id="ca37f-183">비간섭 특성은 `data-val-rule="Error Message"` 형식을 사용합니다. 여기서 규칙은 유효성 검사 규칙의 이름(예: `data-val-required`, `data-val-email`, `data-val-maxlength` 등)입니다. 오류 메시지가 특성에서 제공되는 경우 `data-val-rule` 특성에 대한 값으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-183">The unobtrusive attributes have the format `data-val-rule="Error Message"`, where rule is the name of the validation rule (such as `data-val-required`, `data-val-email`, `data-val-maxlength`, etc.) If an error message is provided in the attribute, it's displayed as the value for the `data-val-rule` attribute.</span></span> <span data-ttu-id="ca37f-184">또한 규칙에 대한 추가 세부 정보를 제공하는 `data-val-ruleName-argumentName="argumentValue"` 형식의 특성이 있습니다(예: `data-val-maxlength-max="1024"`).</span><span class="sxs-lookup"><span data-stu-id="ca37f-184">There are also attributes of the form `data-val-ruleName-argumentName="argumentValue"` that provide additional details about the rule, for example, `data-val-maxlength-max="1024"` .</span></span>

### <a name="html-helper-alternatives-to-input-tag-helper"></a><span data-ttu-id="ca37f-185">입력 태그 도우미에 대한 HTML 도우미 대안</span><span class="sxs-lookup"><span data-stu-id="ca37f-185">HTML Helper alternatives to Input Tag Helper</span></span>

<span data-ttu-id="ca37f-186">`Html.TextBox`, `Html.TextBoxFor`, `Html.Editor` 및 `Html.EditorFor`에는 입력 태그 도우미와 겹치는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-186">`Html.TextBox`, `Html.TextBoxFor`, `Html.Editor` and `Html.EditorFor` have overlapping features with the Input Tag Helper.</span></span> <span data-ttu-id="ca37f-187">입력 태그 도우미는 `type` 특성을 자동으로 설정하는 반면 `Html.TextBox` 및 `Html.TextBoxFor`는 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-187">The Input Tag Helper will automatically set the `type` attribute; `Html.TextBox` and `Html.TextBoxFor` won't.</span></span> <span data-ttu-id="ca37f-188">`Html.Editor` 및 `Html.EditorFor`는 컬렉션, 복잡한 개체 및 템플릿을 처리하는 반면 입력 태그 도우미는 처리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-188">`Html.Editor` and `Html.EditorFor` handle collections, complex objects and templates; the Input Tag Helper doesn't.</span></span> <span data-ttu-id="ca37f-189">입력 태그 도우미인 `Html.EditorFor` 및 `Html.TextBoxFor`은 강력한 형식이 지정(람다 식 사용)되는 반면 `Html.TextBox` 및 `Html.Editor`는 지정되지 않습니다(식 이름 사용).</span><span class="sxs-lookup"><span data-stu-id="ca37f-189">The Input Tag Helper, `Html.EditorFor`  and  `Html.TextBoxFor` are strongly typed (they use lambda expressions); `Html.TextBox` and `Html.Editor` are not (they use expression names).</span></span>

### <a name="htmlattributes"></a><span data-ttu-id="ca37f-190">HtmlAttributes</span><span class="sxs-lookup"><span data-stu-id="ca37f-190">HtmlAttributes</span></span>

<span data-ttu-id="ca37f-191">`@Html.Editor()` 및 `@Html.EditorFor()`는 해당 기본 템플릿을 실행할 때 `htmlAttributes`라는 특수한 `ViewDataDictionary` 항목을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-191">`@Html.Editor()` and `@Html.EditorFor()` use a special `ViewDataDictionary` entry named `htmlAttributes` when executing their default templates.</span></span> <span data-ttu-id="ca37f-192">이 동작은 필요에 따라 `additionalViewData` 매개 변수를 사용하여 확대됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-192">This behavior is optionally augmented using `additionalViewData` parameters.</span></span> <span data-ttu-id="ca37f-193">"htmlAttributes" 키는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-193">The key "htmlAttributes" is case-insensitive.</span></span> <span data-ttu-id="ca37f-194">"htmlAttributes" 키는 `@Html.TextBox()`와 같은 입력 도우미에 전달된 `htmlAttributes` 개체와 유사하게 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-194">The key "htmlAttributes" is handled similarly to the `htmlAttributes` object passed to input helpers like `@Html.TextBox()`.</span></span>

```HTML
@Html.EditorFor(model => model.YourProperty, 
  new { htmlAttributes = new { @class="myCssClass", style="Width:100px" } })
```

### <a name="expression-names"></a><span data-ttu-id="ca37f-195">식 이름</span><span class="sxs-lookup"><span data-stu-id="ca37f-195">Expression names</span></span>

<span data-ttu-id="ca37f-196">`asp-for` 특성 값은 `ModelExpression`이며 람다 식의 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-196">The `asp-for` attribute value is a `ModelExpression` and the right hand side of a lambda expression.</span></span> <span data-ttu-id="ca37f-197">따라서 `asp-for="Property1"`은 생성된 코드에서 `m => m.Property1`이 됩니다. 따라서 `Model`과 함께 접두사로 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-197">Therefore, `asp-for="Property1"` becomes `m => m.Property1` in the generated code which is why you don't need to prefix with `Model`.</span></span> <span data-ttu-id="ca37f-198">“\@” 문자를 사용하여 인라인 식을 시작하고 `m.` 앞으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-198">You can use the "\@" character to start an inline expression and move before the `m.`:</span></span>

```HTML
@{
       var joe = "Joe";
   }
   <input asp-for="@joe" />
```

<span data-ttu-id="ca37f-199">다음 항목을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-199">Generates the following:</span></span>

```HTML
<input type="text" id="joe" name="joe" value="Joe" />
```

<span data-ttu-id="ca37f-200">컬렉션 속성을 가진 `asp-for="CollectionProperty[23].Member"`은 `i`에 `23` 값이 포함될 경우 `asp-for="CollectionProperty[i].Member"`와 동일한 이름을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-200">With collection properties, `asp-for="CollectionProperty[23].Member"` generates the same name as `asp-for="CollectionProperty[i].Member"` when `i` has the value `23`.</span></span>

<span data-ttu-id="ca37f-201">ASP.NET Core MVC가 `ModelExpression`의 값을 계산하는 경우 `ModelState`를 비롯한 여러 원본을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-201">When ASP.NET Core MVC calculates the value of `ModelExpression`, it inspects several sources, including `ModelState`.</span></span> <span data-ttu-id="ca37f-202">`<input type="text" asp-for="@Name" />`을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-202">Consider `<input type="text" asp-for="@Name" />`.</span></span> <span data-ttu-id="ca37f-203">계산된 `value` 특성은 첫 번째 null이 아닌 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-203">The calculated `value` attribute is the first non-null value from:</span></span>

* <span data-ttu-id="ca37f-204">"Name" 키를 가진 `ModelState` 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-204">`ModelState` entry with key "Name".</span></span>
* <span data-ttu-id="ca37f-205">식 `Model.Name`의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-205">Result of the expression `Model.Name`.</span></span>

### <a name="navigating-child-properties"></a><span data-ttu-id="ca37f-206">자식 속성 탐색</span><span class="sxs-lookup"><span data-stu-id="ca37f-206">Navigating child properties</span></span>

<span data-ttu-id="ca37f-207">보기 모델의 속성 경로를 사용하여 자식 속성을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-207">You can also navigate to child properties using the property path of the view model.</span></span> <span data-ttu-id="ca37f-208">자식 `Address` 속성을 포함하는 보다 복잡한 모델 클래스를 사용해보세요.</span><span class="sxs-lookup"><span data-stu-id="ca37f-208">Consider a more complex model class that contains a child `Address` property.</span></span>

[!code-csharp[](../../mvc/views/working-with-forms/sample/final/ViewModels/AddressViewModel.cs?highlight=1,2,3,4&range=5-8)]

[!code-csharp[](../../mvc/views/working-with-forms/sample/final/ViewModels/RegisterAddressViewModel.cs?highlight=8&range=5-13)]

<span data-ttu-id="ca37f-209">보기에서 `Address.AddressLine1`에 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-209">In the view, we bind to `Address.AddressLine1`:</span></span>

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Demo/RegisterAddress.cshtml?highlight=6)]

<span data-ttu-id="ca37f-210">다음 HTML이 `Address.AddressLine1`에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-210">The following HTML is generated for `Address.AddressLine1`:</span></span>

```HTML
<input type="text" id="Address_AddressLine1" name="Address.AddressLine1" value="" />
```

### <a name="expression-names-and-collections"></a><span data-ttu-id="ca37f-211">식 이름 및 컬렉션</span><span class="sxs-lookup"><span data-stu-id="ca37f-211">Expression names and Collections</span></span>

<span data-ttu-id="ca37f-212">샘플, `Colors`의 배열을 포함하는 모델은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-212">Sample, a model containing an array of `Colors`:</span></span>

[!code-csharp[](../../mvc/views/working-with-forms/sample/final/ViewModels/Person.cs?highlight=3&range=5-10)]

<span data-ttu-id="ca37f-213">작업 방법:</span><span class="sxs-lookup"><span data-stu-id="ca37f-213">The action method:</span></span>

```csharp
public IActionResult Edit(int id, int colorIndex)
   {
       ViewData["Index"] = colorIndex;
       return View(GetPerson(id));
   }
```

<span data-ttu-id="ca37f-214">다음 Razor에서는 특정 `Color` 요소에 액세스하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-214">The following Razor shows how you access a specific `Color` element:</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Demo/EditColor.cshtml)]

<span data-ttu-id="ca37f-215">*Views/Shared/EditorTemplates/String.cshtml* 템플릿:</span><span class="sxs-lookup"><span data-stu-id="ca37f-215">The *Views/Shared/EditorTemplates/String.cshtml* template:</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Shared/EditorTemplates/String.cshtml)]

<span data-ttu-id="ca37f-216">`List<T>`를 사용하는 샘플:</span><span class="sxs-lookup"><span data-stu-id="ca37f-216">Sample using `List<T>`:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/ToDoItem.cs?range=3-8)]

<span data-ttu-id="ca37f-217">다음 Razor에서는 컬렉션을 반복하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-217">The following Razor shows how to iterate over a collection:</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Demo/Edit.cshtml)]

<span data-ttu-id="ca37f-218">*Views/Shared/EditorTemplates/ToDoItem.cshtml* 템플릿:</span><span class="sxs-lookup"><span data-stu-id="ca37f-218">The *Views/Shared/EditorTemplates/ToDoItem.cshtml* template:</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Shared/EditorTemplates/ToDoItem.cshtml)]

<span data-ttu-id="ca37f-219">값이 `asp-for` 또는 `Html.DisplayFor` 해당 컨텍스트에서 사용될 때 가능한 경우 `foreach`를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-219">`foreach` should be used if possible when the value is going to be used in an `asp-for` or `Html.DisplayFor` equivalent context.</span></span> <span data-ttu-id="ca37f-220">일반적으로, `for`는 열거자를 할당할 필요가 없으므로 `foreach`보다 좋습니다(시나리오에서 허용하는 경우). 그러나 LINQ 식에서 인덱서를 평가하는 작업은 비용이 많이 들기 때문에 최소화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-220">In general, `for` is better than `foreach` (if the scenario allows it) because it doesn't need to allocate an enumerator; however, evaluating an indexer in a LINQ expression can be expensive and should be minimized.</span></span>

&nbsp;

>[!NOTE]
><span data-ttu-id="ca37f-221">위의 주석 처리된 코드 샘플은 람다 식을 `@` 연산자와 바꿔서 목록에 있는 각 `ToDoItem`에 액세스하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-221">The commented sample code above shows how you would replace the lambda expression with the `@` operator to access each `ToDoItem` in the list.</span></span>

## <a name="the-textarea-tag-helper"></a><span data-ttu-id="ca37f-222">텍스트 영역 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="ca37f-222">The Textarea Tag Helper</span></span>

<span data-ttu-id="ca37f-223">`Textarea Tag Helper` 태그 도우미는 입력 태그 도우미와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-223">The `Textarea Tag Helper` tag helper is  similar to the Input Tag Helper.</span></span>

* <span data-ttu-id="ca37f-224">[\<textarea>](https://www.w3.org/wiki/HTML/Elements/textarea) 요소의 모델에서 `id` 및 `name` 특성과 데이터 유효성 검사 특성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-224">Generates the `id` and `name` attributes, and the data validation attributes from the model for a [\<textarea>](https://www.w3.org/wiki/HTML/Elements/textarea) element.</span></span>

* <span data-ttu-id="ca37f-225">강력한 형식 지정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-225">Provides strong typing.</span></span>

* <span data-ttu-id="ca37f-226">HTML 도우미 대안: `Html.TextAreaFor`</span><span class="sxs-lookup"><span data-stu-id="ca37f-226">HTML Helper alternative: `Html.TextAreaFor`</span></span>

<span data-ttu-id="ca37f-227">예제:</span><span class="sxs-lookup"><span data-stu-id="ca37f-227">Sample:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/DescriptionViewModel.cs)]

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Demo/RegisterTextArea.cshtml?highlight=4)]

<span data-ttu-id="ca37f-228">다음 HTML이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-228">The following HTML is generated:</span></span>

```HTML
<form method="post" action="/Demo/RegisterTextArea">
  <textarea data-val="true"
   data-val-maxlength="The field Description must be a string or array type with a maximum length of &#x27;1024&#x27;."
   data-val-maxlength-max="1024"
   data-val-minlength="The field Description must be a string or array type with a minimum length of &#x27;5&#x27;."
   data-val-minlength-min="5"
   id="Description" name="Description">
  </textarea>
  <button type="submit">Test</button>
  <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
</form>
```

## <a name="the-label-tag-helper"></a><span data-ttu-id="ca37f-229">레이블 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="ca37f-229">The Label Tag Helper</span></span>

* <span data-ttu-id="ca37f-230">식 이름의 [<label>](https://www.w3.org/wiki/HTML/Elements/label) 요소에서 레이블 캡션 및 `for` 특성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-230">Generates the label caption and `for` attribute on a [<label>](https://www.w3.org/wiki/HTML/Elements/label) element for an expression name</span></span>

* <span data-ttu-id="ca37f-231">HTML 도우미 대안: `Html.LabelFor`</span><span class="sxs-lookup"><span data-stu-id="ca37f-231">HTML Helper alternative: `Html.LabelFor`.</span></span>

<span data-ttu-id="ca37f-232">`Label Tag Helper`는 HTML 레이블 요소를 통해 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-232">The `Label Tag Helper`  provides the following benefits over a pure HTML label element:</span></span>

* <span data-ttu-id="ca37f-233">`Display` 특성에서 설명 레이블을 값을 자동으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-233">You automatically get the descriptive label value from the `Display` attribute.</span></span> <span data-ttu-id="ca37f-234">의도한 표시 이름은 시간에 따라 변경될 수 있고, `Display` 특성 및 레이블 태그 도우미의 조합은 사용되는 모든 곳에서 `Display`을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-234">The intended display name might change over time, and the combination of `Display` attribute and Label Tag Helper will apply the `Display` everywhere it's used.</span></span>

* <span data-ttu-id="ca37f-235">소스 코드의 간단한 태그</span><span class="sxs-lookup"><span data-stu-id="ca37f-235">Less markup in source code</span></span>

* <span data-ttu-id="ca37f-236">모델 속성을 사용하는 강력한 형식화입니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-236">Strong typing with the model property.</span></span>

<span data-ttu-id="ca37f-237">예제:</span><span class="sxs-lookup"><span data-stu-id="ca37f-237">Sample:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/SimpleViewModel.cs)]

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Demo/RegisterLabel.cshtml?highlight=4)]

<span data-ttu-id="ca37f-238">다음 HTML이 `<label>` 요소에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-238">The following HTML is generated for the `<label>` element:</span></span>

```HTML
<label for="Email">Email Address</label>
```

<span data-ttu-id="ca37f-239">레이블 태그 도우미는 "이메일"의 `for` 특성 값을 생성했습니다. 이 값은 `<input>` 요소와 연결된 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-239">The Label Tag Helper generated the `for` attribute value of "Email", which is the ID associated with the `<input>` element.</span></span> <span data-ttu-id="ca37f-240">태그 도우미는 일관된 `id` 및 `for` 요소를 제대로 연결할 수 있도록 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-240">The Tag Helpers generate consistent `id` and `for` elements so they can be correctly associated.</span></span> <span data-ttu-id="ca37f-241">이 샘플의 캡션은 `Display` 특성에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-241">The caption in this sample comes from the `Display` attribute.</span></span> <span data-ttu-id="ca37f-242">모델에 `Display` 특성이 포함되지 않는 경우 캡션은 식의 속성 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-242">If the model didn't contain a `Display` attribute, the caption would be the property name of the expression.</span></span>

## <a name="the-validation-tag-helpers"></a><span data-ttu-id="ca37f-243">유효성 검사 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="ca37f-243">The Validation Tag Helpers</span></span>

<span data-ttu-id="ca37f-244">두 개의 유효성 검사 태그 도우미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-244">There are two Validation Tag Helpers.</span></span> <span data-ttu-id="ca37f-245">`Validation Message Tag Helper`(모델의 단일 속성에 대한 유효성 검사 메시지 표시) 및 `Validation Summary Tag Helper`(유효성 검사 오류의 요약 표시)입니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-245">The `Validation Message Tag Helper` (which displays a validation message for a single property on your model), and the `Validation Summary Tag Helper` (which displays a summary of validation errors).</span></span> <span data-ttu-id="ca37f-246">`Input Tag Helper`는 모델 클래스의 데이터 주석 특성에 따라 입력 요소에 HTML5 클라이언트 쪽 유효성 검사 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-246">The `Input Tag Helper` adds HTML5 client side validation attributes to input elements based on data annotation attributes on your model classes.</span></span> <span data-ttu-id="ca37f-247">유효성 검사도 서버에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-247">Validation is also performed on the server.</span></span> <span data-ttu-id="ca37f-248">유효성 검사 태그 도우미는 유효성 검사 오류가 발생하는 경우 이러한 오류 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-248">The Validation Tag Helper displays these error messages when a validation error occurs.</span></span>

### <a name="the-validation-message-tag-helper"></a><span data-ttu-id="ca37f-249">유효성 검사 메시지 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="ca37f-249">The Validation Message Tag Helper</span></span>

* <span data-ttu-id="ca37f-250">[HTML5](https://developer.mozilla.org/docs/Web/Guide/HTML/HTML5) `data-valmsg-for="property"` 특성을 [범위](https://developer.mozilla.org/docs/Web/HTML/Element/span) 요소에 추가합니다. 그러면 지정된 모델 속성의 입력 필드에서 유효성 검사 오류 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-250">Adds the [HTML5](https://developer.mozilla.org/docs/Web/Guide/HTML/HTML5)  `data-valmsg-for="property"` attribute to the [span](https://developer.mozilla.org/docs/Web/HTML/Element/span) element, which attaches the validation error messages on the input field of the specified model property.</span></span> <span data-ttu-id="ca37f-251">클라이언트 쪽 유효성 검사 오류가 발생할 때 [jQuery](https://jquery.com/)는 `<span>` 요소에서 오류 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-251">When a client side validation error occurs, [jQuery](https://jquery.com/) displays the error message in the `<span>` element.</span></span>

* <span data-ttu-id="ca37f-252">유효성 검사도 서버에서 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-252">Validation also takes place on the server.</span></span> <span data-ttu-id="ca37f-253">클라이언트는 JavaScript를 사용하지 않도록 설정할 수 있고 일부 유효성 검사는 서버 쪽에서만 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-253">Clients may have JavaScript disabled and some validation can only be done on the server side.</span></span>

* <span data-ttu-id="ca37f-254">HTML 도우미 대안: `Html.ValidationMessageFor`</span><span class="sxs-lookup"><span data-stu-id="ca37f-254">HTML Helper alternative: `Html.ValidationMessageFor`</span></span>

<span data-ttu-id="ca37f-255">`Validation Message Tag Helper`는 HTML [범위](https://developer.mozilla.org/docs/Web/HTML/Element/span) 요소에서 `asp-validation-for` 특성과 함께 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-255">The `Validation Message Tag Helper`  is used with the `asp-validation-for` attribute on a HTML [span](https://developer.mozilla.org/docs/Web/HTML/Element/span) element.</span></span>

```HTML
<span asp-validation-for="Email"></span>
```

<span data-ttu-id="ca37f-256">유효성 검사 메시지 태그 도우미는 다음 HTML을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-256">The Validation Message Tag Helper will generate the following HTML:</span></span>

```HTML
<span class="field-validation-valid"
  data-valmsg-for="Email"
  data-valmsg-replace="true"></span>
```

<span data-ttu-id="ca37f-257">일반적으로 동일한 속성에서 `Input` 태그 도우미 이후에 `Validation Message Tag Helper`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-257">You generally use the `Validation Message Tag Helper`  after an `Input` Tag Helper for the same property.</span></span> <span data-ttu-id="ca37f-258">이렇게 하면 오류가 발생하는 입력 주변에서 유효성 검사 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-258">Doing so displays any validation error messages near the input that caused the error.</span></span>

> [!NOTE]
> <span data-ttu-id="ca37f-259">클라이언트 쪽 유효성 검사 대신 올바른 JavaScript 및 [jQuery](https://jquery.com/) 스크립트 참조를 사용하는 보기가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-259">You must have a view with the correct JavaScript and [jQuery](https://jquery.com/) script references in place for client side validation.</span></span> <span data-ttu-id="ca37f-260">자세한 내용은 [모델 유효성 검사](../models/validation.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ca37f-260">See [Model Validation](../models/validation.md) for more information.</span></span>

<span data-ttu-id="ca37f-261">서버 쪽 유효성 검사 오류가 발생하는 경우(예: 사용자 지정 서버 쪽 유효성 검사 또는 클라이언트 쪽 유효성 검사를 사용하지 않는 경우) MVC는 해당 오류 메시지를 `<span>` 요소의 본문으로 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-261">When a server side validation error occurs (for example when you have custom server side validation or client-side validation is disabled), MVC places that error message as the body of the `<span>` element.</span></span>

```HTML
<span class="field-validation-error" data-valmsg-for="Email"
            data-valmsg-replace="true">
   The Email Address field is required.
</span>
```

### <a name="the-validation-summary-tag-helper"></a><span data-ttu-id="ca37f-262">유효성 검사 요약 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="ca37f-262">The Validation Summary Tag Helper</span></span>

* <span data-ttu-id="ca37f-263">`asp-validation-summary` 특성이 있는 `<div>` 요소를 대상으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-263">Targets `<div>` elements with the `asp-validation-summary` attribute</span></span>

* <span data-ttu-id="ca37f-264">HTML 도우미 대안: `@Html.ValidationSummary`</span><span class="sxs-lookup"><span data-stu-id="ca37f-264">HTML Helper alternative: `@Html.ValidationSummary`</span></span>

<span data-ttu-id="ca37f-265">`Validation Summary Tag Helper`는 유효성 검사 메시지의 요약 정보를 표시하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-265">The `Validation Summary Tag Helper`  is used to display a summary of validation messages.</span></span> <span data-ttu-id="ca37f-266">`asp-validation-summary` 특성 값은 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-266">The `asp-validation-summary` attribute value can be any of the following:</span></span>

|<span data-ttu-id="ca37f-267">asp-validation-summary</span><span class="sxs-lookup"><span data-stu-id="ca37f-267">asp-validation-summary</span></span>|<span data-ttu-id="ca37f-268">표시되는 유효성 검사 메시지</span><span class="sxs-lookup"><span data-stu-id="ca37f-268">Validation messages displayed</span></span>|
|--- |--- |
|<span data-ttu-id="ca37f-269">ValidationSummary.All</span><span class="sxs-lookup"><span data-stu-id="ca37f-269">ValidationSummary.All</span></span>|<span data-ttu-id="ca37f-270">속성 및 모델 수준</span><span class="sxs-lookup"><span data-stu-id="ca37f-270">Property and model level</span></span>|
|<span data-ttu-id="ca37f-271">ValidationSummary.ModelOnly</span><span class="sxs-lookup"><span data-stu-id="ca37f-271">ValidationSummary.ModelOnly</span></span>|<span data-ttu-id="ca37f-272">모델</span><span class="sxs-lookup"><span data-stu-id="ca37f-272">Model</span></span>|
|<span data-ttu-id="ca37f-273">ValidationSummary.None</span><span class="sxs-lookup"><span data-stu-id="ca37f-273">ValidationSummary.None</span></span>|<span data-ttu-id="ca37f-274">없음</span><span class="sxs-lookup"><span data-stu-id="ca37f-274">None</span></span>|

### <a name="sample"></a><span data-ttu-id="ca37f-275">샘플</span><span class="sxs-lookup"><span data-stu-id="ca37f-275">Sample</span></span>

<span data-ttu-id="ca37f-276">다음 예제에서 데이터 모델은 `DataAnnotation` 특성으로 데코레이팅됩니다. 그러면 `<input>` 요소에 대한 유효성 검사 오류 메시지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-276">In the following example, the data model is decorated with `DataAnnotation` attributes, which generates validation error messages on the `<input>` element.</span></span>  <span data-ttu-id="ca37f-277">유효성 검사 오류가 발생하는 경우 유효성 검사 태그 도우미는 다음 오류 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-277">When a validation error occurs, the Validation Tag Helper displays the error message:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/RegisterViewModel.cs)]

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Demo/RegisterValidation.cshtml?highlight=4,6,8&range=1-10)]

<span data-ttu-id="ca37f-278">생성된 HTML(모델은 유효한 경우):</span><span class="sxs-lookup"><span data-stu-id="ca37f-278">The generated HTML (when the model is valid):</span></span>

```HTML
<form action="/DemoReg/Register" method="post">
  <div class="validation-summary-valid" data-valmsg-summary="true">
  <ul><li style="display:none"></li></ul></div>
  Email:  <input name="Email" id="Email" type="email" value=""
   data-val-required="The Email field is required."
   data-val-email="The Email field is not a valid email address."
   data-val="true"> <br>
  <span class="field-validation-valid" data-valmsg-replace="true"
   data-valmsg-for="Email"></span><br>
  Password: <input name="Password" id="Password" type="password"
   data-val-required="The Password field is required." data-val="true"><br>
  <span class="field-validation-valid" data-valmsg-replace="true"
   data-valmsg-for="Password"></span><br>
  <button type="submit">Register</button>
  <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
</form>
```

## <a name="the-select-tag-helper"></a><span data-ttu-id="ca37f-279">선택 태그 도우미</span><span class="sxs-lookup"><span data-stu-id="ca37f-279">The Select Tag Helper</span></span>

* <span data-ttu-id="ca37f-280">모델의 속성에 대한 [선택](https://www.w3.org/wiki/HTML/Elements/select) 및 관련된 [옵션](https://www.w3.org/wiki/HTML/Elements/option) 요소를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-280">Generates [select](https://www.w3.org/wiki/HTML/Elements/select) and associated [option](https://www.w3.org/wiki/HTML/Elements/option) elements for properties of your model.</span></span>

* <span data-ttu-id="ca37f-281">HTML 도우미 대안 `Html.DropDownListFor` 및 `Html.ListBoxFor`가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-281">Has an HTML Helper alternative `Html.DropDownListFor` and `Html.ListBoxFor`</span></span>

<span data-ttu-id="ca37f-282">`Select Tag Helper` `asp-for`는 [선택](https://www.w3.org/wiki/HTML/Elements/select) 요소에 대한 모델 속성 이름을 지정하고 `asp-items`는 [옵션](https://www.w3.org/wiki/HTML/Elements/option) 요소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-282">The `Select Tag Helper` `asp-for` specifies the model property  name for the [select](https://www.w3.org/wiki/HTML/Elements/select) element  and `asp-items` specifies the [option](https://www.w3.org/wiki/HTML/Elements/option) elements.</span></span>  <span data-ttu-id="ca37f-283">예:</span><span class="sxs-lookup"><span data-stu-id="ca37f-283">For example:</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Home/Index.cshtml?range=4)]

<span data-ttu-id="ca37f-284">예제:</span><span class="sxs-lookup"><span data-stu-id="ca37f-284">Sample:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/CountryViewModel.cs)]

<span data-ttu-id="ca37f-285">`Index` 메서드는 `CountryViewModel`를 초기화하고, 선택한 국가를 설정하고, `Index` 보기에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-285">The `Index` method initializes the `CountryViewModel`, sets the selected country and passes it to the `Index` view.</span></span>

[!code-csharp[](working-with-forms/sample/final/Controllers/HomeController.cs?range=8-13)]

<span data-ttu-id="ca37f-286">HTTP POST `Index` 메서드는 선택 항목을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-286">The HTTP POST `Index` method displays the selection:</span></span>

[!code-csharp[](working-with-forms/sample/final/Controllers/HomeController.cs?range=15-27)]

<span data-ttu-id="ca37f-287">`Index` 보기:</span><span class="sxs-lookup"><span data-stu-id="ca37f-287">The `Index` view:</span></span>

[!code-cshtml[](working-with-forms/sample/final/Views/Home/Index.cshtml?highlight=4)]

<span data-ttu-id="ca37f-288">다음 HTML을 생성합니다("CA"를 선택함).</span><span class="sxs-lookup"><span data-stu-id="ca37f-288">Which generates the following HTML (with "CA" selected):</span></span>

```html
<form method="post" action="/">
     <select id="Country" name="Country">
       <option value="MX">Mexico</option>
       <option selected="selected" value="CA">Canada</option>
       <option value="US">USA</option>
     </select>
       <br /><button type="submit">Register</button>
     <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
   </form>
```

> [!NOTE]
> <span data-ttu-id="ca37f-289">선택 태그 도우미와 함께 `ViewBag` 또는 `ViewData`를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-289">We don't recommend using `ViewBag` or `ViewData` with the Select Tag Helper.</span></span> <span data-ttu-id="ca37f-290">보기 모델은 일반적으로 더 강력하고 문제가 적은 방식으로 MVC 메타데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-290">A view model is more robust at providing MVC metadata and generally less problematic.</span></span>

<span data-ttu-id="ca37f-291">`asp-for` 특성 값은 특별한 경우이며 다른 태그 도우미 특성(예: `asp-items`)과 달리 `Model` 접두사를 필요로 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-291">The `asp-for` attribute value is a special case and doesn't require a `Model` prefix, the other Tag Helper attributes do (such as `asp-items`)</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Home/Index.cshtml?range=4)]

### <a name="enum-binding"></a><span data-ttu-id="ca37f-292">열거형 바인딩</span><span class="sxs-lookup"><span data-stu-id="ca37f-292">Enum binding</span></span>

<span data-ttu-id="ca37f-293">`enum` 속성과 함께 `<select>`를 사용하고 `enum` 값에서 `SelectListItem` 요소를 생성하는 것이 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-293">It's often convenient to use `<select>` with an `enum` property and generate the `SelectListItem` elements from the `enum` values.</span></span>

<span data-ttu-id="ca37f-294">예제:</span><span class="sxs-lookup"><span data-stu-id="ca37f-294">Sample:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/CountryEnumViewModel.cs?range=3-7)]

[!code-csharp[](working-with-forms/sample/final/ViewModels/CountryEnum.cs)]

<span data-ttu-id="ca37f-295">`GetEnumSelectList` 메서드는 열거형에 대해 `SelectList` 개체를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-295">The `GetEnumSelectList` method generates a `SelectList` object for an enum.</span></span>

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Home/IndexEnum.cshtml?highlight=5)]

<span data-ttu-id="ca37f-296">`Display` 특성으로 열거자 목록을 데코레이트하여 보다 풍부한 UI를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-296">You can decorate your enumerator list with the `Display` attribute to get a richer UI:</span></span>

[!code-csharp[](working-with-forms/sample/final/ViewModels/CountryEnum.cs?highlight=5,7)]

<span data-ttu-id="ca37f-297">다음 HTML이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-297">The following HTML is generated:</span></span>

```HTML
  <form method="post" action="/Home/IndexEnum">
         <select data-val="true" data-val-required="The EnumCountry field is required."
                 id="EnumCountry" name="EnumCountry">
             <option value="0">United Mexican States</option>
             <option value="1">United States of America</option>
             <option value="2">Canada</option>
             <option value="3">France</option>
             <option value="4">Germany</option>
             <option selected="selected" value="5">Spain</option>
         </select>
         <br /><button type="submit">Register</button>
         <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
    </form>
```

### <a name="option-group"></a><span data-ttu-id="ca37f-298">옵션 그룹</span><span class="sxs-lookup"><span data-stu-id="ca37f-298">Option Group</span></span>

<span data-ttu-id="ca37f-299">보기 모델에 하나 이상의 `SelectListGroup` 개체가 포함되는 경우 HTML [\<optgroup>](https://www.w3.org/wiki/HTML/Elements/optgroup) 요소가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-299">The HTML  [\<optgroup>](https://www.w3.org/wiki/HTML/Elements/optgroup) element is generated when the view model contains one or more `SelectListGroup` objects.</span></span>

<span data-ttu-id="ca37f-300">`CountryViewModelGroup`은 `SelectListItem` 요소를 "북아메리카" 및 "유럽" 그룹으로 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-300">The `CountryViewModelGroup` groups the `SelectListItem` elements into the "North America" and "Europe" groups:</span></span>

[!code-csharp[](../../mvc/views/working-with-forms/sample/final/ViewModels/CountryViewModelGroup.cs?highlight=5,6,14,20,26,32,38,44&range=6-56)]

<span data-ttu-id="ca37f-301">두 개의 그룹은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-301">The two groups are shown below:</span></span>

![옵션 그룹 예제](working-with-forms/_static/grp.png)

<span data-ttu-id="ca37f-303">생성된 코드:</span><span class="sxs-lookup"><span data-stu-id="ca37f-303">The generated HTML:</span></span>

```HTML
 <form method="post" action="/Home/IndexGroup">
      <select id="Country" name="Country">
          <optgroup label="North America">
              <option value="MEX">Mexico</option>
              <option value="CAN">Canada</option>
              <option value="US">USA</option>
          </optgroup>
          <optgroup label="Europe">
              <option value="FR">France</option>
              <option value="ES">Spain</option>
              <option value="DE">Germany</option>
          </optgroup>
      </select>
      <br /><button type="submit">Register</button>
      <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
 </form>
```

### <a name="multiple-select"></a><span data-ttu-id="ca37f-304">다중 선택</span><span class="sxs-lookup"><span data-stu-id="ca37f-304">Multiple select</span></span>

<span data-ttu-id="ca37f-305">`asp-for` 특성에 지정된 속성이 `IEnumerable`인 경우 태그 선택 도우미는 [multiple = "multiple"](http://w3c.github.io/html-reference/select.html) 특성을 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-305">The Select Tag Helper  will automatically generate the [multiple = "multiple"](http://w3c.github.io/html-reference/select.html)  attribute if the property specified in the `asp-for` attribute is an `IEnumerable`.</span></span> <span data-ttu-id="ca37f-306">예를 들어, 다음과 같은 모델을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-306">For example, given the following model:</span></span>

[!code-csharp[](../../mvc/views/working-with-forms/sample/final/ViewModels/CountryViewModelIEnumerable.cs?highlight=6)]

<span data-ttu-id="ca37f-307">다음 보기에서:</span><span class="sxs-lookup"><span data-stu-id="ca37f-307">With the following view:</span></span>

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Home/IndexMultiSelect.cshtml?highlight=4)]

<span data-ttu-id="ca37f-308">다음과 같은 HTML을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-308">Generates the following HTML:</span></span>

```HTML
<form method="post" action="/Home/IndexMultiSelect">
    <select id="CountryCodes"
    multiple="multiple"
    name="CountryCodes"><option value="MX">Mexico</option>
<option value="CA">Canada</option>
<option value="US">USA</option>
<option value="FR">France</option>
<option value="ES">Spain</option>
<option value="DE">Germany</option>
</select>
    <br /><button type="submit">Register</button>
  <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
</form>
```

### <a name="no-selection"></a><span data-ttu-id="ca37f-309">선택 영역 없음</span><span class="sxs-lookup"><span data-stu-id="ca37f-309">No selection</span></span>

<span data-ttu-id="ca37f-310">여러 페이지에서 "지정 안 됨" 옵션을 사용하는 경우 HTML의 반복을 제거하는 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-310">If you find yourself using the "not specified" option in multiple pages, you can create a template to eliminate repeating the HTML:</span></span>

[!code-HTML[](../../mvc/views/working-with-forms/sample/final/Views/Home/IndexEmptyTemplate.cshtml?highlight=5)]

<span data-ttu-id="ca37f-311">*Views/Shared/EditorTemplates/CountryViewModel.cshtml* 템플릿:</span><span class="sxs-lookup"><span data-stu-id="ca37f-311">The *Views/Shared/EditorTemplates/CountryViewModel.cshtml* template:</span></span>

[!code-HTML[](working-with-forms/sample/final/Views/Shared/EditorTemplates/CountryViewModel.cshtml)]

<span data-ttu-id="ca37f-312">HTML [\<option>](https://www.w3.org/wiki/HTML/Elements/option) 요소를 추가하는 작업은 *선택 영역 없음* 사례로 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-312">Adding HTML [\<option>](https://www.w3.org/wiki/HTML/Elements/option) elements isn't limited to the *No selection* case.</span></span> <span data-ttu-id="ca37f-313">예를 들어 다음과 같은 보기 및 작업 메서드는 위의 코드와 유사한 HTML을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ca37f-313">For example, the following view and action method will generate HTML similar to the code above:</span></span>

[!code-csharp[](working-with-forms/sample/final/Controllers/HomeController.cs?range=114-119)]

[!code-HTML[](working-with-forms/sample/final/Views/Home/IndexOption.cshtml)]

<span data-ttu-id="ca37f-314">현재 `Country` 값에 따라 올바른 `<option>` 요소가 선택됩니다(`selected="selected"` 특성 포함).</span><span class="sxs-lookup"><span data-stu-id="ca37f-314">The correct `<option>` element will be selected ( contain the `selected="selected"` attribute) depending on the current `Country` value.</span></span>

```HTML
 <form method="post" action="/Home/IndexEmpty">
      <select id="Country" name="Country">
          <option value="">&lt;none&gt;</option>
          <option value="MX">Mexico</option>
          <option value="CA" selected="selected">Canada</option>
          <option value="US">USA</option>
      </select>
      <br /><button type="submit">Register</button>
   <input name="__RequestVerificationToken" type="hidden" value="<removed for brevity>" />
 </form>
 ```

## <a name="additional-resources"></a><span data-ttu-id="ca37f-315">추가 자료</span><span class="sxs-lookup"><span data-stu-id="ca37f-315">Additional resources</span></span>

* <xref:mvc/views/tag-helpers/intro>
* [<span data-ttu-id="ca37f-316">HTML 형식 요소</span><span class="sxs-lookup"><span data-stu-id="ca37f-316">HTML Form element</span></span>](https://www.w3.org/TR/html401/interact/forms.html)
* [<span data-ttu-id="ca37f-317">요청 확인 토큰</span><span class="sxs-lookup"><span data-stu-id="ca37f-317">Request Verification Token</span></span>](/aspnet/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages)
* <xref:mvc/models/model-binding>
* <xref:mvc/models/validation>
* [<span data-ttu-id="ca37f-318">IAttributeAdapter 인터페이스</span><span class="sxs-lookup"><span data-stu-id="ca37f-318">IAttributeAdapter Interface</span></span>](/dotnet/api/Microsoft.AspNetCore.Mvc.DataAnnotations.IAttributeAdapter)
* [<span data-ttu-id="ca37f-319">이 문서의 코드 조각</span><span class="sxs-lookup"><span data-stu-id="ca37f-319">Code snippets for this document</span></span>](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/views/working-with-forms/sample/final)
