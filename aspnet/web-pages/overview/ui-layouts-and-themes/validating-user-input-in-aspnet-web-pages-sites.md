---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: 페이지 (Razor) 사이트를 Asp.net에서 사용자 입력 유효성 검사 | Microsoft Docs
author: tfitzmac
description: 이 문서에서는 사용자 로부터 얻은 정보를 확인 하는 방법을 설명 &mdash; , 있는지는 사용자가 입력 유효한 html에서 정보에서에서 forms AS...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
ms.technology: dotnet-webpages
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 2a35e9895c5b711d5c6c5544987f99fe7e2e0085
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37368229"
---
<a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="1b06b-103">ASP.NET 웹 페이지 (Razor) 사이트에서 사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="1b06b-103">Validating User Input in ASP.NET Web Pages (Razor) Sites</span></span>
====================
<span data-ttu-id="1b06b-104">[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="1b06b-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="1b06b-105">이 문서에서는 사용자 로부터 얻은 정보를 확인 하는 방법을 설명 &mdash; , 있는지는 사용자가 입력 유효한 html에서 정보 forms ASP.NET Web Pages (Razor) 사이트에서.</span><span class="sxs-lookup"><span data-stu-id="1b06b-105">This article discusses how to validate information you get from users &mdash; that is, to make sure that users enter valid information in HTML forms in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> <span data-ttu-id="1b06b-106">학습할 내용:</span><span class="sxs-lookup"><span data-stu-id="1b06b-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="1b06b-107">사용자의 입력을 확인 하는 방법을 정의 하는 유효성 검사 조건에 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-107">How to check that a user's input matches validation criteria that you define.</span></span>
> - <span data-ttu-id="1b06b-108">모든 유효성 검사 테스트를 통과 하는지 여부를 결정 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-108">How to determine whether all validation tests have passed.</span></span>
> - <span data-ttu-id="1b06b-109">유효성 검사 오류를 표시 하는 방법 (및 서식을 지정 하는 방법).</span><span class="sxs-lookup"><span data-stu-id="1b06b-109">How to display validation errors (and how to format them).</span></span>
> - <span data-ttu-id="1b06b-110">사용자 로부터 직접 존재 하지 않는 데이터의 유효성을 검사 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="1b06b-110">How to validate data that doesn't come directly from users.</span></span>
> 
> <span data-ttu-id="1b06b-111">프로그래밍 개념 문서에 도입 된 ASP.NET은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-111">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="1b06b-112">`Validation` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-112">The `Validation` helper.</span></span>
> - <span data-ttu-id="1b06b-113">합니다 `Html.ValidationSummary` 고 `Html.ValidationMessage` 메서드.</span><span class="sxs-lookup"><span data-stu-id="1b06b-113">The `Html.ValidationSummary` and `Html.ValidationMessage` methods.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="1b06b-114">이 자습서에 사용 되는 소프트웨어 버전</span><span class="sxs-lookup"><span data-stu-id="1b06b-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="1b06b-115">ASP.NET Web Pages (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="1b06b-115">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="1b06b-116">이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-116">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="1b06b-117">이 자료에는 다음과 같은 섹션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-117">This article contains the following sections:</span></span>

- [<span data-ttu-id="1b06b-118">사용자 입력된 유효성 검사 개요</span><span class="sxs-lookup"><span data-stu-id="1b06b-118">Overview of User Input Validation</span></span>](#Overview_of_User_Input_Validation)
- [<span data-ttu-id="1b06b-119">사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="1b06b-119">Validating User Input</span></span>](#Validating_User_Input)
- [<span data-ttu-id="1b06b-120">클라이언트 쪽 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="1b06b-120">Adding Client-Side Validation</span></span>](#Adding_Client-Side_Validation)
- [<span data-ttu-id="1b06b-121">유효성 검사 오류를 서식 지정</span><span class="sxs-lookup"><span data-stu-id="1b06b-121">Formatting Validation Errors</span></span>](#Formatting_Validation_Errors)
- [<span data-ttu-id="1b06b-122">사용자 로부터 직접 존재 하지 않는 데이터 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="1b06b-122">Validating Data That Doesn't Come Directly from Users</span></span>](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a><span data-ttu-id="1b06b-123">사용자 입력된 유효성 검사 개요</span><span class="sxs-lookup"><span data-stu-id="1b06b-123">Overview of User Input Validation</span></span>

<span data-ttu-id="1b06b-124">페이지에서 정보를 입력 하도록 요청 하는 경우-형태로 예를 들어, 입력 값이 유효한 지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-124">If you ask users to enter information in a page — for example, into a form — it's important to make sure that the values that they enter are valid.</span></span> <span data-ttu-id="1b06b-125">예를 들어, 중요 한 정보를 누락 된 폼을 처리 하지 않으려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-125">For example, you don't want to process a form that's missing critical information.</span></span>

<span data-ttu-id="1b06b-126">사용자가 HTML 형식으로 값을 입력 하면 값을 입력 하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-126">When users enter values into an HTML form, the values that they enter are strings.</span></span> <span data-ttu-id="1b06b-127">대부분의 경우 필요한 값에는 정수 또는 날짜와 같은 몇 가지 다른 데이터 형식.</span><span class="sxs-lookup"><span data-stu-id="1b06b-127">In many cases, the values you need are some other data types, like integers or dates.</span></span> <span data-ttu-id="1b06b-128">따라서 해야 사용자가 입력 한 값을 적절 한 데이터 형식으로 올바르게 변환 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-128">Therefore, you also have to make sure that the values that users enter can be correctly converted to the appropriate data types.</span></span>

<span data-ttu-id="1b06b-129">값에 특정 제한 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-129">You might also have certain restrictions on the values.</span></span> <span data-ttu-id="1b06b-130">사용자가 정수를 올바르게 입력 하면 경우에 값을 특정 범위에 속하는지 확인 해야 예를 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-130">Even if users correctly enter an integer, for example, you might need to make sure that the value falls within a certain range.</span></span>

![CSS 스타일 클래스를 사용 하는 유효성 검사 오류](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> <span data-ttu-id="1b06b-132">**중요 한** 사용자 입력 유효성 검사는 보안을 위해 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-132">**Important** Validating user input is also important for security.</span></span> <span data-ttu-id="1b06b-133">폼에 입력할 수 있는 값을 제한 하는 사이트의 보안을 손상 시킬 수 있는 값을 입력할 수 누군가가 가능성이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-133">When you restrict the values that users can enter in forms, you reduce the chance that someone can enter a value that can compromise the security of your site.</span></span>


<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a><span data-ttu-id="1b06b-134">사용자 입력 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="1b06b-134">Validating User Input</span></span>

<span data-ttu-id="1b06b-135">ASP.NET 웹 페이지 2에서 사용할 수 있습니다는 `Validator` 사용자 입력을 테스트 하는 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-135">In ASP.NET Web Pages 2, you can use the `Validator` helper to test user input.</span></span> <span data-ttu-id="1b06b-136">다음을 수행 하는 기본 방법이입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-136">The basic approach is to do the following:</span></span>

1. <span data-ttu-id="1b06b-137">입력의 유효성을 검사 하려는 요소 (필드)를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-137">Determine which input elements (fields) you want to validate.</span></span>

    <span data-ttu-id="1b06b-138">일반적으로 값을 확인할 `<input>` 요소 형식에서입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-138">You typically validate values in `<input>` elements in a form.</span></span> <span data-ttu-id="1b06b-139">그러나 같은 제약 조건이 지정 된 요소에서 제공 되는 모든 입력의 유효성을 검사 하려면 입력도 좋습니다 것을 `<select>` 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-139">However, it's a good practice to validate all input, even input that comes from a constrained element like a `<select>` list.</span></span> <span data-ttu-id="1b06b-140">이렇게 하면 사용자 페이지의 제어를 우회 하 고 양식을 제출 하지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-140">This helps to make sure that users don't bypass the controls on a page and submit a form.</span></span>
2. <span data-ttu-id="1b06b-141">메서드를 사용 하 여 각 입력 요소에 대 한 페이지 코드에서 각 유효성 검사를 추가 합니다 `Validation` 도우미입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-141">In the page code, add individual validation checks for each input element by using methods of the `Validation` helper.</span></span>

    <span data-ttu-id="1b06b-142">필수 필드를 확인 하려면 사용 하 여 `Validation.RequireField(field, [error message])` (개별 필드)에 대 한 또는 `Validation.RequireFields(field1, field2, ...))` (목록은 필드).</span><span class="sxs-lookup"><span data-stu-id="1b06b-142">To check for required fields, use `Validation.RequireField(field, [error message])` (for an individual field) or `Validation.RequireFields(field1, field2, ...))` (for a list of fields).</span></span> <span data-ttu-id="1b06b-143">다른 유형의 유효성 검사를 사용 하 여 `Validation.Add(field, ValidationType)`입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-143">For other types of validation, use `Validation.Add(field, ValidationType)`.</span></span> <span data-ttu-id="1b06b-144">에 대 한 `ValidationType`, 이러한 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-144">For `ValidationType`, you can use these options:</span></span>

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. <span data-ttu-id="1b06b-145">페이지가 제출 되 면 확인 하 여 유효성 검사를 통과 하는지 여부를 확인 `Validation.IsValid`:</span><span class="sxs-lookup"><span data-stu-id="1b06b-145">When the page is submitted, check whether validation has passed by checking `Validation.IsValid`:</span></span>

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    <span data-ttu-id="1b06b-146">모든 유효성 검사 오류가 있는 경우 일반적인 페이지 처리를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-146">If there are any validation errors, you skip normal page processing.</span></span> <span data-ttu-id="1b06b-147">예를 들어 페이지의 목적은 데이터베이스를 업데이트 하는 경우 그럴 필요가 모든 유효성 검사 오류가 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-147">For example, if the purpose of the page is to update a database, you don't do that until all validation errors have been fixed.</span></span>
4. <span data-ttu-id="1b06b-148">유효성 검사 오류가 있으면 오류 메시지를 표시 페이지의 태그를 사용 하 여 `Html.ValidationSummary` 또는 `Html.ValidationMessage`, 또는 둘 다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-148">If there are validation errors, display error messages in the page's markup by using `Html.ValidationSummary` or `Html.ValidationMessage`, or both.</span></span>

<span data-ttu-id="1b06b-149">다음 예제에서는 다음이 단계를 보여 주는 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-149">The following example shows a page that illustrates these steps.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

<span data-ttu-id="1b06b-150">유효성 검사의 작동 원리를 보려면이 페이지를 실행 하 고 의도적으로 실수입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-150">To see how validation works, run this page and deliberately make mistakes.</span></span> <span data-ttu-id="1b06b-151">예를 들어, 다음은 페이지 모습 잊어버렸을 때 과정 이름을 입력을 입력 하는 경우는, 잘못 된 날짜를 입력 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="1b06b-151">For example, here's what the page looks like if you forget to enter a course name, if you enter an, and if you enter an invalid date:</span></span>

![렌더링된 된 페이지에 유효성 검사 오류](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a><span data-ttu-id="1b06b-153">클라이언트 쪽 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="1b06b-153">Adding Client-Side Validation</span></span>

<span data-ttu-id="1b06b-154">기본적으로 사용자 입력 유효성을 검사할지 사용자 제출 페이지-유효성 검사 서버 코드에서 수행 되는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-154">By default, user input is validated after users submit the page — that is, the validation is performed in server code.</span></span> <span data-ttu-id="1b06b-155">이 방식의 단점은 사용자 오류까지 후 페이지를 전송할 설정한 값을 알지는입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-155">A disadvantage of this approach is that users don't know that they've made an error until after they submit the page.</span></span> <span data-ttu-id="1b06b-156">폼 길거나 복잡 한 경우 페이지 제출 된 후에 오류를 보고 불편할 수 있습니다 사용자에 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-156">If a form is long or complex, reporting errors only after the page is submitted can be inconvenient to the user.</span></span>

<span data-ttu-id="1b06b-157">클라이언트 스크립트에서 유효성 검사를 수행 하는 지원을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-157">You can add support to perform validation in client script.</span></span> <span data-ttu-id="1b06b-158">이 경우 사용자 브라우저에서 작업 하면서 유효성 검사가 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-158">In that case, the validation is performed as users work in the browser.</span></span> <span data-ttu-id="1b06b-159">예를 들어, 값은 정수 여야 있는지를 지정 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-159">For example, suppose you specify that a value should be an integer.</span></span> <span data-ttu-id="1b06b-160">사용자가 정수가 아닌 값을 입력 하면 사용자가 입력 필드는 즉시 오류가 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-160">If a user enters a non-integer value, the error is reported as soon as the user leaves the entry field.</span></span> <span data-ttu-id="1b06b-161">사용자가 편리 하 게 되는 즉시 피드백을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-161">Users get immediate feedback, which is convenient for them.</span></span> <span data-ttu-id="1b06b-162">클라이언트 기반 유효성 검사는 사용자가 여러 오류를 해결 하려면 양식을 제출 해야 하는 횟수를 줄일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-162">Client-based validation can also reduce the number of times that the user has to submit the form to correct multiple errors.</span></span>

> [!NOTE]
> <span data-ttu-id="1b06b-163">클라이언트 쪽 유효성 검사를 사용 하는 경우에 유효성 검사 서버 코드에도 항상 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-163">Even if you use client-side validation, validation is always also performed in server code.</span></span> <span data-ttu-id="1b06b-164">사용자는 클라이언트 기반 유효성 검사를 무시 하는 경우 보안을 위해는 서버 코드에서 유효성 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-164">Performing validation in server code is a security measure, in case users bypass client-based validation.</span></span>


1. <span data-ttu-id="1b06b-165">페이지에는 다음과 같은 JavaScript 라이브러리를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-165">Register the following JavaScript libraries in the page:</span></span>  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   <span data-ttu-id="1b06b-166">라이브러리의 두 가지 하므로 컴퓨터나 서버에 반드시 필요가 content delivery network (CDN)에서 로드할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-166">Two of the libraries are loadable from a content delivery network (CDN), so you don't necessarily have to have them on your computer or server.</span></span> <span data-ttu-id="1b06b-167">그러나의 로컬 복사본이 있어야 *jquery.validate.unobtrusive.js*합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-167">However, you must have a local copy of *jquery.validate.unobtrusive.js*.</span></span> <span data-ttu-id="1b06b-168">경우 하지 이미 작업 중인 WebMatrix 템플릿을 사용 하 여 (같은 **시작 사이트** ) 라이브러리를 포함 하는의 기반이 되는 웹 페이지 사이트를 만들 **시작 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-168">If you are not already working with a WebMatrix template (like **Starter Site** ) that includes the library, create a Web Pages site that's based on **Starter Site**.</span></span> <span data-ttu-id="1b06b-169">복사 합니다 *.js* 현재 사이트에는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-169">Then copy the *.js* file to your current site.</span></span>
2. <span data-ttu-id="1b06b-170">유효성을 검사 하는 각 요소에 대 한 태그에 대 한 호출 추가 `Validation.For(field)`합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-170">In markup, for each element that you're validating, add a call to `Validation.For(field)`.</span></span> <span data-ttu-id="1b06b-171">이 메서드는 클라이언트 쪽 유효성 검사에 사용 되는 특성을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-171">This method emits attributes that are used by client-side validation.</span></span> <span data-ttu-id="1b06b-172">(실제 JavaScript 코드 대신 메서드 같은 특성을 내보내는 `data-val-...`합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-172">(Rather than emitting actual JavaScript code, the method emits attributes like `data-val-...`.</span></span> <span data-ttu-id="1b06b-173">이러한 특성 지원 jQuery를 사용 하 여 작업을 수행 하는 비 가시적인 클라이언트 유효성 검사 합니다.)</span><span class="sxs-lookup"><span data-stu-id="1b06b-173">These attributes support unobtrusive client validation that uses jQuery to do the work.)</span></span>

<span data-ttu-id="1b06b-174">페이지에는 앞서 살펴본 예제 클라이언트 유효성 검사 기능을 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-174">The following page shows how to add client validation features to the example shown earlier.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

<span data-ttu-id="1b06b-175">일부 유효성 검사는 클라이언트에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-175">Not all validation checks run on the client.</span></span> <span data-ttu-id="1b06b-176">특히, 데이터 형식 유효성 검사 (정수, 날짜 및 등)는 클라이언트에서 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-176">In particular, data-type validation (integer, date, and so on) don't run on the client.</span></span> <span data-ttu-id="1b06b-177">다음 검사는 클라이언트와 서버 모두에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-177">The following checks work on both the client and server:</span></span>

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

<span data-ttu-id="1b06b-178">이 예제에서는 유효한 날짜에 대 한 테스트는 클라이언트 코드에서 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-178">In this example, the test for a valid date won't work in client code.</span></span> <span data-ttu-id="1b06b-179">그러나 테스트 서버 코드에서 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-179">However, the test will be performed in server code.</span></span>

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a><span data-ttu-id="1b06b-180">유효성 검사 오류를 서식 지정</span><span class="sxs-lookup"><span data-stu-id="1b06b-180">Formatting Validation Errors</span></span>

<span data-ttu-id="1b06b-181">다음 예약 된 이름을 포함 하는 CSS 클래스를 정의 하 여 유효성 검사 오류가 표시 되는 방식을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-181">You can control how validation errors are displayed by defining CSS classes that have the following reserved names:</span></span>

- <span data-ttu-id="1b06b-182">`field-validation-error`.</span><span class="sxs-lookup"><span data-stu-id="1b06b-182">`field-validation-error`.</span></span> <span data-ttu-id="1b06b-183">출력을 정의 합니다 `Html.ValidationMessage` 메서드는 오류를 표시 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="1b06b-183">Defines the output of the `Html.ValidationMessage` method when it's displaying an error.</span></span>
- <span data-ttu-id="1b06b-184">`field-validation-valid`.</span><span class="sxs-lookup"><span data-stu-id="1b06b-184">`field-validation-valid`.</span></span> <span data-ttu-id="1b06b-185">출력을 정의 합니다 `Html.ValidationMessage` 메서드 오류가 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="1b06b-185">Defines the output of the `Html.ValidationMessage` method when there is no error.</span></span>
- <span data-ttu-id="1b06b-186">`input-validation-error`.</span><span class="sxs-lookup"><span data-stu-id="1b06b-186">`input-validation-error`.</span></span> <span data-ttu-id="1b06b-187">정의 하는 방법을 `<input>` 요소 오류가 있을 때 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-187">Defines how `<input>` elements are rendered when there's an error.</span></span> <span data-ttu-id="1b06b-188">(예를 들어의 배경색을 설정 하려면이 클래스를 사용할 수 있습니다는 &lt;입력&gt; 요소 값에 유효 하지 않은 경우 다른 색입니다.) 이 CSS 클래스 (ASP.NET 웹 페이지 2)의 클라이언트 유효성 검사 중에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-188">(For example, you can use this class to set the background color of an &lt;input&gt; element to a different color if its value is invalid.) This CSS class is used only during client validation (in ASP.NET Web Pages 2).</span></span>
- <span data-ttu-id="1b06b-189">`input-validation-valid`.</span><span class="sxs-lookup"><span data-stu-id="1b06b-189">`input-validation-valid`.</span></span> <span data-ttu-id="1b06b-190">모양을 정의 `<input>` 오류가 없는 경우 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-190">Defines the appearance of `<input>` elements when there is no error.</span></span>
- <span data-ttu-id="1b06b-191">`validation-summary-errors`.</span><span class="sxs-lookup"><span data-stu-id="1b06b-191">`validation-summary-errors`.</span></span> <span data-ttu-id="1b06b-192">출력을 정의 합니다 `Html.ValidationSummary` 메서드 오류 목록을 표시 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-192">Defines the output of the `Html.ValidationSummary` method it's displaying a list of errors.</span></span>
- <span data-ttu-id="1b06b-193">`validation-summary-valid`.</span><span class="sxs-lookup"><span data-stu-id="1b06b-193">`validation-summary-valid`.</span></span> <span data-ttu-id="1b06b-194">출력을 정의 합니다 `Html.ValidationSummary` 메서드 오류가 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="1b06b-194">Defines the output of the `Html.ValidationSummary` method when there is no error.</span></span>

<span data-ttu-id="1b06b-195">다음 `<style>` 블록 오류 조건에 대 한 규칙을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-195">The following `<style>` block shows rules for error conditions.</span></span>

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

<span data-ttu-id="1b06b-196">이 문서 앞부분에 나오는 예제 페이지에서이 style 블록을 포함 하는 경우 오류 표시는 다음 그림과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-196">If you include this style block in the example pages from earlier in the article, the error display will look like the following illustration:</span></span>

![CSS 스타일 클래스를 사용 하는 유효성 검사 오류](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="1b06b-198">CSS 클래스에 대 한 ASP.NET 웹 페이지 2의 클라이언트 유효성 검사를 사용 하지 않는 경우는 `<input>` 요소 (`input-validation-error` 고 `input-validation-valid` 아무런 효과가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-198">If you're not using client validation in ASP.NET Web Pages 2, the CSS classes for the `<input>` elements (`input-validation-error` and `input-validation-valid` don't have any effect.</span></span>


### <a name="static-and-dynamic-error-display"></a><span data-ttu-id="1b06b-199">정적 및 동적 오류 표시</span><span class="sxs-lookup"><span data-stu-id="1b06b-199">Static and Dynamic Error Display</span></span>

<span data-ttu-id="1b06b-200">CSS 규칙 등 쌍으로 제공 `validation-summary-errors` 고 `validation-summary-valid`입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-200">The CSS rules come in pairs, such as `validation-summary-errors` and `validation-summary-valid`.</span></span> <span data-ttu-id="1b06b-201">이러한 쌍 모두 조건에 대 한 규칙을 정의할 수: 오류 조건 및 "normal" (오류가 아닌) 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-201">These pairs let you define rules for both conditions: an error condition and a "normal" (non-error) condition.</span></span> <span data-ttu-id="1b06b-202">오류가 없는 경우에 오류 표시에 대 한 태그가 항상 렌더링 됨을 이해 하는 것이 반드시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-202">It's important to understand that the markup for the error display is always rendered, even if there are no errors.</span></span> <span data-ttu-id="1b06b-203">예를 들어 페이지에는 `Html.ValidationSummary` 태그에서 메서드를 페이지가 처음 요청 될 경우에 페이지 소스 다음 태그를 포함할 수는:</span><span class="sxs-lookup"><span data-stu-id="1b06b-203">For example, if a page has an `Html.ValidationSummary` method in the markup, the page source will contain the following markup even when the page is requested for the first time:</span></span>

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

<span data-ttu-id="1b06b-204">즉, 합니다 `Html.ValidationSummary` 메서드를 항상 렌더링을 `<div>` 요소 및 오류 목록이 비어 있는 경우에 목록.</span><span class="sxs-lookup"><span data-stu-id="1b06b-204">In other words, the `Html.ValidationSummary` method always renders a `<div>` element and a list, even if the error list is empty.</span></span> <span data-ttu-id="1b06b-205">마찬가지로, 합니다 `Html.ValidationMessage` 메서드를 항상 렌더링을 `<span>` 개별 필드, 오류가 발생 한 오류가 없는 경우에 자리 표시자로 요소.</span><span class="sxs-lookup"><span data-stu-id="1b06b-205">Similarly, the `Html.ValidationMessage` method always renders a `<span>` element as a placeholder for an individual field error, even if there is no error.</span></span>

<span data-ttu-id="1b06b-206">상황에 따라 오류 메시지를 표시 페이지 흐름이 발생할 수 있습니다 하 고 이동할 페이지의 요소를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-206">In some situations, displaying an error message can cause the page to reflow and can cause elements on the page to move around.</span></span> <span data-ttu-id="1b06b-207">CSS 규칙 끝나는 `-valid` 이 문제를 방지 하는 데 도움이 되는 레이아웃을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-207">The CSS rules that end in `-valid` let you define a layout that can help prevent this problem.</span></span> <span data-ttu-id="1b06b-208">예를 들어 정의할 수 있습니다 `field-validation-error` 및 `field-validation-valid` 둘 다에 있는 동일한 고정 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-208">For example, you can define `field-validation-error` and `field-validation-valid` to both have the same fixed size.</span></span> <span data-ttu-id="1b06b-209">이런 방식으로 필드의 표시 영역은 정적 이며 오류 메시지가 표시 되 면 페이지 흐름을 변경 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-209">That way, the display area for the field is static and won't change the page flow if an error message is displayed.</span></span>

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a><span data-ttu-id="1b06b-210">사용자 로부터 직접 존재 하지 않는 데이터 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="1b06b-210">Validating Data That Doesn't Come Directly from Users</span></span>

<span data-ttu-id="1b06b-211">때로는 HTML 양식에서 직접 존재 하지 않는 정보의 유효성을 검사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-211">Sometimes you have to validate information that doesn't come directly from an HTML form.</span></span> <span data-ttu-id="1b06b-212">일반적인 예는 다음 예제와 같이 쿼리 문자열에서 값이 전달 하는 위치 페이지:</span><span class="sxs-lookup"><span data-stu-id="1b06b-212">A typical example is a page where a value is passed in a query string, as in the following example:</span></span>

`http://server/myapp/EditClassInformation?classid=1022`

<span data-ttu-id="1b06b-213">확인 하려는 경우 페이지에 전달 되는 값 (여기의 값에 대 한 1022 `classid`) 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-213">In this case, you want to make sure that the value that's passed to the page (here, 1022 for the value of `classid`) is valid.</span></span> <span data-ttu-id="1b06b-214">직접 사용할 수 없습니다는 `Validation` 도우미가 유효성이 검사를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-214">You can't directly use the `Validation` helper to perform this validation.</span></span> <span data-ttu-id="1b06b-215">그러나 유효성 검사 시스템 유효성 검사 오류 메시지를 표시 하는 기능 등의 다른 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-215">However, you can use other features of the validation system, like the ability to display validation error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="1b06b-216">**중요** 항상에서 얻을 수 있는 값의 유효성 검사 *모든* 원본, 폼 필드 값, 쿼리 문자열 값 및 쿠키 값을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-216">**Important** Always validate values that you get from *any* source, including form-field values, query-string values, and cookie values.</span></span> <span data-ttu-id="1b06b-217">(아마도 악의적인 목적) 이러한 값을 변경 하는 데는 것이 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-217">It's easy for people to change these values (perhaps for malicious purposes).</span></span> <span data-ttu-id="1b06b-218">따라서 응용 프로그램을 보호 하기 위해 이러한 값을 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-218">So you must check these values in order to protect your application.</span></span>


<span data-ttu-id="1b06b-219">다음 예제 쿼리 문자열에 전달 되는 값을 어떻게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-219">The following example shows how you might validate a value that's passed in a query string.</span></span> <span data-ttu-id="1b06b-220">코드 값을 비어 있지 않고 정수 인지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-220">The code tests that the value is not empty and that it's an integer.</span></span>

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

<span data-ttu-id="1b06b-221">테스트 요청 양식을 제출 하 여 없을 때 수행 됩니다 (`if(!IsPost)`).</span><span class="sxs-lookup"><span data-stu-id="1b06b-221">Notice that the test is performed when the request is not a form submission (`if(!IsPost)`).</span></span> <span data-ttu-id="1b06b-222">이 테스트는 페이지가 요청 되 면 처음 전달 하지만 요청 양식을 제출 하 여를 하는 경우에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-222">This test would pass the first time that the page is requested, but not when the request is a form submission.</span></span>

<span data-ttu-id="1b06b-223">이 오류를 표시할 수 오류 유효성 검사 오류의 목록에 호출 하 여 추가 `Validation.AddFormError("message")`합니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-223">To display this error, you can add the error to the list of validation errors by calling `Validation.AddFormError("message")`.</span></span> <span data-ttu-id="1b06b-224">페이지에 대 한 호출을 포함 하는 경우는 `Html.ValidationSummary` 메서드를 오류는 사용자 입력 유효성 검사 오류와 마찬가지로 여기에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1b06b-224">If the page contains a call to the `Html.ValidationSummary` method, the error is displayed there, just like a user-input validation error.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="1b06b-225">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="1b06b-225">Additional Resources</span></span>

[<span data-ttu-id="1b06b-226">ASP.NET 웹 페이지 사이트에서 HTML 양식 사용</span><span class="sxs-lookup"><span data-stu-id="1b06b-226">Working with HTML Forms in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkID=202892)
