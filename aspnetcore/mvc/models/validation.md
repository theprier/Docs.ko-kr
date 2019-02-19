---
title: ASP.NET Core MVC의 모델 유효성 검사
author: tdykstra
description: ASP.NET Core MVC의 모델 유효성 검사에 대해 알아봅니다.
ms.author: riande
ms.custom: mvc
ms.date: 01/14/2019
uid: mvc/models/validation
ms.openlocfilehash: ca7ee54b8e6b6ae5091b0cb133e448ad9c04da8f
ms.sourcegitcommit: 6ba5fb1fd0b7f9a6a79085b0ef56206e462094b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56248521"
---
# <a name="model-validation-in-aspnet-core-mvc"></a><span data-ttu-id="db88f-103">ASP.NET Core MVC의 모델 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="db88f-103">Model validation in ASP.NET Core MVC</span></span>

<span data-ttu-id="db88f-104">작성자: [Rachel Appel](https://github.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="db88f-104">By [Rachel Appel](https://github.com/rachelappel)</span></span>

## <a name="introduction-to-model-validation"></a><span data-ttu-id="db88f-105">모델 유효성 검사 소개</span><span class="sxs-lookup"><span data-stu-id="db88f-105">Introduction to model validation</span></span>

<span data-ttu-id="db88f-106">앱은 데이터베이스에 데이터를 저장하기 전에 데이터를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-106">Before an app stores data in a database, the app must validate the data.</span></span> <span data-ttu-id="db88f-107">데이터는 잠재적 보안 위협을 확인하고, 형식 및 크기별로 적절하게 서식이 지정되었는지 확인하고, 규칙을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-107">Data must be checked for potential security threats, verified that it's appropriately formatted by type and size, and it must conform to your rules.</span></span> <span data-ttu-id="db88f-108">유효성 검사는 중복되고 구현되기 번거로울 수 있지만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-108">Validation is necessary although it can be redundant and tedious to implement.</span></span> <span data-ttu-id="db88f-109">MVC에서 유효성 검사는 클라이언트와 서버 모두에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-109">In MVC, validation happens on both the client and server.</span></span>

<span data-ttu-id="db88f-110">다행히 .NET는 유효성 검사를 유효성 검사 특성으로 추상화했습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-110">Fortunately, .NET has abstracted validation into validation attributes.</span></span> <span data-ttu-id="db88f-111">이러한 특성에는 유효성 검사 코드가 포함되어 작성해야 하는 코드의 양을 감소시킵니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-111">These attributes contain validation code, thereby reducing the amount of code you must write.</span></span>

<span data-ttu-id="db88f-112">ASP.NET Core 2.2 이상에서는 지정된 모델 그래프에 유효성 검사가 필요하지 않다고 판단되는 경우 ASP.NET Core 런타임이 유효성 검사를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-112">In ASP.NET Core 2.2 and later, the ASP.NET Core runtime short-circuits (skips) validation if it can determine that a given model graph doesn't require validation.</span></span> <span data-ttu-id="db88f-113">유효성 검사를 건너뛰는 것은 연결된 유효성 검사기를 가질 수 없거나 연결된 유효성 검사기가 없을 때 상당한 성능 향상을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-113">Skipping validation can provide significant performance improvements when validating models that cannot or do not have any associated validators.</span></span> <span data-ttu-id="db88f-114">건너뛴 유효성 검사에는 기본 형식(`byte[]`, `string[]`, `Dictionary<string, string>` 등)의 컬렉션 값은 개체 또는 유효성 검사기가 없는 복합 개체 그래프가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-114">The skipped validation includes objects such as collections of primitives (`byte[]`, `string[]`, `Dictionary<string, string>`, etc.), or complex object graphs without any validators.</span></span>

<span data-ttu-id="db88f-115">[GitHub에서 샘플 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/models/validation/sample)</span><span class="sxs-lookup"><span data-stu-id="db88f-115">[View or download sample from GitHub](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/models/validation/sample).</span></span>

## <a name="validation-attributes"></a><span data-ttu-id="db88f-116">유효성 검사 특성</span><span class="sxs-lookup"><span data-stu-id="db88f-116">Validation Attributes</span></span>

<span data-ttu-id="db88f-117">유효성 검사 특성은 모델 유효성 검사를 구성하는 방법이므로 데이터베이스 테이블의 필드에 대한 유효성 검사와 개념적으로 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-117">Validation attributes are a way to configure model validation so it's similar conceptually to validation on fields in database tables.</span></span> <span data-ttu-id="db88f-118">데이터 형식이나 필수 필드를 할당하는 등 제약 조건이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-118">This includes constraints such as assigning data types or required fields.</span></span> <span data-ttu-id="db88f-119">다른 종류의 유효성 검사에는 신용 카드, 전화 번호 또는 이메일 주소와 같은 비즈니스 규칙을 적용하기 위해 데이터에 대한 패턴을 적용하는 것이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-119">Other types of validation include applying patterns to data to enforce business rules, such as a credit card, phone number, or email address.</span></span> <span data-ttu-id="db88f-120">유효성 검사 특성을 통해 훨씬 간단하고 사용하기 쉽게 이러한 요구 사항을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-120">Validation attributes make enforcing these requirements much simpler and easier to use.</span></span>

<span data-ttu-id="db88f-121">유효성 검사 특성은 속성 수준에서 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-121">Validation attributes are specified at the property level:</span></span> 

```csharp
[Required]
public string MyProperty { get; set; }
```

<span data-ttu-id="db88f-122">영화 및 TV 프로그램에 대 한 정보를 저장하는 앱에서 주석이 추가된 `Movie` 모델은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-122">Below is an annotated `Movie` model from an app that stores information about movies and TV shows.</span></span> <span data-ttu-id="db88f-123">대부분의 속성은 필수이며 여러 문자열 속성에는 길이 요구 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-123">Most of the properties are required and several string properties have length requirements.</span></span> <span data-ttu-id="db88f-124">또한 사용자 지정 유효성 검사 특성과 함께 `Price` 속성 대신에 0~$999.99 사이라는 숫자 범위 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-124">Additionally, there's a numeric range restriction in place for the `Price` property from 0 to $999.99, along with a custom validation attribute.</span></span>

[!code-csharp[](validation/sample/Movie.cs?range=6-29)]

<span data-ttu-id="db88f-125">단순히 모델을 통해 읽으면 이 앱에서 데이터에 대한 규칙을 표시하여 코드를 쉽게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-125">Simply reading through the model reveals the rules about data for this app, making it easier to maintain the code.</span></span> <span data-ttu-id="db88f-126">널리 사용되는 여러 기본 제공 유효성 검사 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-126">Below are several popular built-in validation attributes:</span></span>

* <span data-ttu-id="db88f-127">`[CreditCard]`: 속성에 신용 카드 형식이 있는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-127">`[CreditCard]`: Validates the property has a credit card format.</span></span>

* <span data-ttu-id="db88f-128">`[Compare]`: 모델의 두 속성이 일치하는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-128">`[Compare]`: Validates two properties in a model match.</span></span>

* <span data-ttu-id="db88f-129">`[EmailAddress]`: 속성에 전자 메일 형식이 있는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-129">`[EmailAddress]`: Validates the property has an email format.</span></span>

* <span data-ttu-id="db88f-130">`[Phone]`: 속성에 전화 번호 형식이 있는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-130">`[Phone]`: Validates the property has a telephone format.</span></span>

* <span data-ttu-id="db88f-131">`[Range]`: 지정된 범위 내에서 속성 값이 포함되는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-131">`[Range]`: Validates the property value falls within the given range.</span></span>

* <span data-ttu-id="db88f-132">`[RegularExpression]`: 데이터가 지정된 정규식과 일치하는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-132">`[RegularExpression]`: Validates that the data matches the specified regular expression.</span></span>

* <span data-ttu-id="db88f-133">`[Required]`: 필수 속성으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-133">`[Required]`: Makes a property required.</span></span>

* <span data-ttu-id="db88f-134">`[StringLength]`: 문자열 속성에 지정된 최대 길이가 있는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-134">`[StringLength]`: Validates that a string property has at most the given maximum length.</span></span>

* <span data-ttu-id="db88f-135">`[Url]`: 속성에 URL 형식이 있는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-135">`[Url]`: Validates the property has a URL format.</span></span>

<span data-ttu-id="db88f-136">MVC는 유효성 검사를 위해 `ValidationAttribute`에서 파생된 모든 특성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-136">MVC supports any attribute that derives from `ValidationAttribute` for validation purposes.</span></span> <span data-ttu-id="db88f-137">많은 유용한 유효성 검사 특성을 [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) 네임스페이스에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-137">Many useful validation attributes can be found in the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace.</span></span>

<span data-ttu-id="db88f-138">제공되는 기본 제공 특성보다 더 많은 기능이 필요한 인스턴스가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-138">There may be instances where you need more features than built-in attributes provide.</span></span> <span data-ttu-id="db88f-139">이 경우에 `ValidationAttribute`에서 파생하거나 `IValidatableObject`를 구현하도록 모델을 변경하여 사용자 지정 유효성 검사 특성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-139">For those times, you can create custom validation attributes by deriving from `ValidationAttribute` or changing your model to implement `IValidatableObject`.</span></span>

## <a name="notes-on-the-use-of-the-required-attribute"></a><span data-ttu-id="db88f-140">필수 특성 사용에 대한 참고</span><span class="sxs-lookup"><span data-stu-id="db88f-140">Notes on the use of the Required attribute</span></span>

<span data-ttu-id="db88f-141">nullable 형식이 아닌 [값 형식](/dotnet/csharp/language-reference/keywords/value-types)(`decimal`, `int`, `float`,`DateTime`)은 기본적으로 필요하며 `Required` 특성은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-141">Non-nullable [value types](/dotnet/csharp/language-reference/keywords/value-types) (such as `decimal`, `int`, `float`, and `DateTime`) are inherently required and don't need the `Required` attribute.</span></span> <span data-ttu-id="db88f-142">앱은 `Required`으로 표시된 null이 아닌 형식에 서버 쪽 유효성 검사를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-142">The app performs no server-side validation checks for non-nullable types that are marked `Required`.</span></span>

<span data-ttu-id="db88f-143">유효성 검사 및 유효성 검사 특성과 관련되지 않는 MVC 모델 바인딩은 null이 아닌 형식에 누락 값 또는 공백을 포함하는 형식 필드 전송을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-143">MVC model binding, which isn't concerned with validation and validation attributes, rejects a form field submission containing a missing value or whitespace for a non-nullable type.</span></span> <span data-ttu-id="db88f-144">대상 속성에 `BindRequired` 특성이 없는 경우에 모델 바인딩은 null이 아닌 형식에 대한 누락 데이터를 무시합니다. 여기서 들어오는 형식 데이터에서 형식 필드는 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-144">In the absence of a `BindRequired` attribute on the target property, model binding ignores missing data for non-nullable types, where the form field is absent from the incoming form data.</span></span>

<span data-ttu-id="db88f-145">[BindRequired 특성](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.bindrequiredattribute)(<xref:mvc/models/model-binding#customize-model-binding-behavior-with-attributes>도 참조)은 양식 데이터가 완료되었는지 확인하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-145">The [BindRequired attribute](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.bindrequiredattribute) (also see <xref:mvc/models/model-binding#customize-model-binding-behavior-with-attributes>) is useful to ensure form data is complete.</span></span> <span data-ttu-id="db88f-146">속성에 적용하는 경우 모델 바인딩 시스템에는 해당 속성에 대한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-146">When applied to a property, the model binding system requires a value for that property.</span></span> <span data-ttu-id="db88f-147">형식에 적용하는 경우 모델 바인딩 시스템에는 해당 형식의 모든 속성에 대한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-147">When applied to a type, the model binding system requires values for all of the properties of that type.</span></span>

<span data-ttu-id="db88f-148">[Nullable\<T > 형식](/dotnet/csharp/programming-guide/nullable-types/)(예: `decimal?` 또는 `System.Nullable<decimal>`)을 사용하고 `Required`으로 표시하는 경우 속성이 표준 null 형식인 것처럼 서버 쪽 유효성 검사가 수행됩니다(예: `string`).</span><span class="sxs-lookup"><span data-stu-id="db88f-148">When you use a [Nullable\<T> type](/dotnet/csharp/programming-guide/nullable-types/) (for example, `decimal?` or `System.Nullable<decimal>`) and mark it `Required`, a server-side validation check is performed as if the property were a standard nullable type (for example, a `string`).</span></span>

<span data-ttu-id="db88f-149">클라이언트 쪽 유효성 검사에는 `Required`로 표시한 모델 속성에 해당하는 형식 필드에 대한 값 및 `Required`로 표시하지 않은 null이 아닌 형식 속성에 대한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-149">Client-side validation requires a value for a form field that corresponds to a model property that you've marked `Required` and for a non-nullable type property that you haven't marked `Required`.</span></span> <span data-ttu-id="db88f-150">`Required`는 클라이언트 쪽 유효성 검사 오류 메시지를 제어하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-150">`Required` can be used to control the client-side validation error message.</span></span>

::: moniker range=">= aspnetcore-2.1"

## <a name="top-level-node-validation"></a><span data-ttu-id="db88f-151">최상위 노드 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="db88f-151">Top-level node validation</span></span>

<span data-ttu-id="db88f-152">최상위 수준 노드에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-152">Top-level nodes include:</span></span>

* <span data-ttu-id="db88f-153">작업 매개 변수</span><span class="sxs-lookup"><span data-stu-id="db88f-153">Action parameters</span></span>
* <span data-ttu-id="db88f-154">컨트롤러 속성</span><span class="sxs-lookup"><span data-stu-id="db88f-154">Controller properties</span></span>
* <span data-ttu-id="db88f-155">페이지 처리기 매개 변수</span><span class="sxs-lookup"><span data-stu-id="db88f-155">Page handler parameters</span></span>
* <span data-ttu-id="db88f-156">페이지 모델 속성</span><span class="sxs-lookup"><span data-stu-id="db88f-156">Page model properties</span></span>

<span data-ttu-id="db88f-157">모델 바인딩 최상위 노드는 모델 속성의 유효성을 검사하는 것 외에도 유효성이 검사됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-157">Model-bound top-level nodes are validated in addition to validating model properties.</span></span> <span data-ttu-id="db88f-158">샘플 앱의 다음 예제에서 `VerifyPhone` 메서드는 <xref:System.ComponentModel.DataAnnotations.RegularExpressionAttribute>를 사용하여 양식의 폰 필드에서 사용자 데이터의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-158">In the following example from the sample app, the `VerifyPhone` method uses the <xref:System.ComponentModel.DataAnnotations.RegularExpressionAttribute> to validate the user data in the Phone field of a form:</span></span>

[!code-csharp[](validation/sample/UsersController.cs?name=snippet_VerifyPhone)]

<span data-ttu-id="db88f-159">최상위 노드는 유효성 검사 특성과 함께 <xref:Microsoft.AspNetCore.Mvc.ModelBinding.BindRequiredAttribute>를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-159">Top-level nodes can use <xref:Microsoft.AspNetCore.Mvc.ModelBinding.BindRequiredAttribute> with validation attributes.</span></span> <span data-ttu-id="db88f-160">샘플 앱의 다음 예제에서 `CheckAge` 메서드는 양식을 제출할 때 쿼리 문자열에서 `age` 매개 변수를 바인딩해야 함을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-160">In the following example from the sample app, the `CheckAge` method specifies that the `age` parameter must be bound from the query string when the form is submitted:</span></span>

[!code-csharp[](validation/sample/UsersController.cs?name=snippet_CheckAge)]

<span data-ttu-id="db88f-161">기간 확인 페이지(*CheckAge.cshtml*)에는 두 가지 양식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-161">In the Check Age page (*CheckAge.cshtml*), there are two forms.</span></span> <span data-ttu-id="db88f-162">첫 번째 양식은 `99`의 `Age` 값을 쿼리 문자열(`https://localhost:5001/Users/CheckAge?Age=99`)로 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-162">The first form submits an `Age` value of `99` as a query string: `https://localhost:5001/Users/CheckAge?Age=99`.</span></span>

<span data-ttu-id="db88f-163">쿼리 문자열에서 올바른 서식이 지정된 `age` 매개 변수를 제출하면 양식이 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-163">When a properly formatted `age` parameter from the query string is submitted, the form validates.</span></span>

<span data-ttu-id="db88f-164">기간 확인 페이지의 두 번째 양식은 요청 본문의 `Age` 값을 제출하고 유효성 검사가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-164">The second form on the Check Age page submits the `Age` value in the body of the request, and validation fails.</span></span> <span data-ttu-id="db88f-165">`age` 매개 변수는 쿼리 문자열에서 가져와야 하므로 바인딩이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-165">Binding fails because the `age` parameter must come from a query string.</span></span>

<span data-ttu-id="db88f-166">유효성 검사는 기본적으로 사용하도록 설정되고 <xref:Microsoft.AspNetCore.Mvc.MvcOptions>의 <xref:Microsoft.AspNetCore.Mvc.MvcOptions.AllowValidatingTopLevelNodes*> 속성에 의해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-166">Validation is enabled by default and controlled by the <xref:Microsoft.AspNetCore.Mvc.MvcOptions.AllowValidatingTopLevelNodes*> property of <xref:Microsoft.AspNetCore.Mvc.MvcOptions>.</span></span> <span data-ttu-id="db88f-167">최상위 노드 유효성 검사를 사용하지 않도록 설정하려면 MVC 옵션(`Startup.ConfigureServices`)에서 `AllowValidatingTopLevelNodes`를 `false`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-167">To disable top-level node validation, set `AllowValidatingTopLevelNodes` to `false` in MVC options (`Startup.ConfigureServices`):</span></span>

[!code-csharp[](validation/sample_snapshot/Startup.cs?name=snippet_AddMvc&highlight=4)]

::: moniker-end

## <a name="model-state"></a><span data-ttu-id="db88f-168">모델 상태</span><span class="sxs-lookup"><span data-stu-id="db88f-168">Model State</span></span>

<span data-ttu-id="db88f-169">모델 상태는 제출된 HTML 형식 값으로 유효성 검사 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-169">Model state represents validation errors in submitted HTML form values.</span></span>

<span data-ttu-id="db88f-170">MVC는 최대 오류 수(기본적으로 200개)에 도달할 때까지 필드의 유효성 검사를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-170">MVC will continue validating fields until it reaches the maximum number of errors (200 by default).</span></span> <span data-ttu-id="db88f-171">`Startup.ConfigureServices`에 다음 코드로 이 번호를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-171">You can configure this number with the following code in `Startup.ConfigureServices`:</span></span>

[!code-csharp[](validation/sample/Startup.cs?name=snippet_MaxModelValidationErrors)]

## <a name="handle-model-state-errors"></a><span data-ttu-id="db88f-172">모델 상태 오류 처리</span><span class="sxs-lookup"><span data-stu-id="db88f-172">Handle Model State errors</span></span>

<span data-ttu-id="db88f-173">모델 유효성 검사는 컨트롤러 작업을 실행하기 전에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-173">Model validation occurs before the execution of a controller action.</span></span> <span data-ttu-id="db88f-174">`ModelState.IsValid`를 검사하고 적절하게 반응하는 것은 작업의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-174">It's the action's responsibility to inspect `ModelState.IsValid` and react appropriately.</span></span> <span data-ttu-id="db88f-175">대부분의 경우 적합한 반응은 이상적으로 모델 유효성 검사에 실패한 이유를 자세히 보여주는 오류 응답을 반환하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-175">In many cases, the appropriate reaction is to return an error response, ideally detailing the reason why model validation failed.</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="db88f-176">`ModelState.IsValid`가 `[ApiController]` 특성을 사용하는 웹 API 컨트롤러에서 `false`로 평가되면, 문제 세부 정보가 포함된 자동 HTTP 400 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-176">When `ModelState.IsValid` evaluates to `false` in web API controllers using the `[ApiController]` attribute, an automatic HTTP 400 response containing issue details is returned.</span></span> <span data-ttu-id="db88f-177">자세한 정보는 [자동 HTTP 400 응답](xref:web-api/index#automatic-http-400-responses)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db88f-177">For more information, see [Automatic HTTP 400 responses](xref:web-api/index#automatic-http-400-responses).</span></span>

::: moniker-end

<span data-ttu-id="db88f-178">필터가 이러한 정책을 구현하기에 적절한 경우에 일부 앱은 모델 유효성 검사 오류를 처리하는 표준 규칙을 따르도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-178">Some apps will choose to follow a standard convention for dealing with model validation errors, in which case a filter may be an appropriate place to implement such a policy.</span></span> <span data-ttu-id="db88f-179">유효한 모델 및 잘못된 모델 상태일 때 작업 동작 방식을 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-179">You should test how your actions behave with valid and invalid model states.</span></span>

## <a name="manual-validation"></a><span data-ttu-id="db88f-180">수동 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="db88f-180">Manual validation</span></span>

<span data-ttu-id="db88f-181">모델 바인딩 및 유효성 검사가 완료되면 일부를 반복하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-181">After model binding and validation are complete, you may want to repeat parts of it.</span></span> <span data-ttu-id="db88f-182">예를 들어 사용자는 정수가 필요한 필드에 텍스트를 입력하거나 모델의 속성에 대한 값을 계산해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-182">For example, a user may have entered text in a field expecting an integer, or you may need to compute a value for a model's property.</span></span>

<span data-ttu-id="db88f-183">유효성 검사를 수동으로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-183">You may need to run validation manually.</span></span> <span data-ttu-id="db88f-184">이렇게 하려면 다음과 같이 `TryValidateModel` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-184">To do so, call the `TryValidateModel` method, as shown here:</span></span>

[!code-csharp[](validation/sample/MoviesController.cs?name=snippet_TryValidateModel)]

## <a name="custom-validation"></a><span data-ttu-id="db88f-185">사용자 지정 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="db88f-185">Custom validation</span></span>

<span data-ttu-id="db88f-186">유효성 검사 특성은 대부분의 유효성 검사 요구 사항에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-186">Validation attributes work for most validation needs.</span></span> <span data-ttu-id="db88f-187">그러나 일부 유효성 검사 규칙은 비즈니스에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-187">However, some validation rules are specific to your business.</span></span> <span data-ttu-id="db88f-188">규칙은 필드가 필요하거나 값의 범위를 준수하는지 확인하는 등 일반적인 데이터 유효성 검사 기술이 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-188">Your rules might not be common data validation techniques such as ensuring a field is required or that it conforms to a range of values.</span></span> <span data-ttu-id="db88f-189">이러한 시나리오에서 사용자 지정 유효성 검사 특성을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-189">For these scenarios, custom validation attributes are a great solution.</span></span> <span data-ttu-id="db88f-190">MVC에서 고유한 사용자 지정 유효성 검사 특성을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-190">Creating your own custom validation attributes in MVC is easy.</span></span> <span data-ttu-id="db88f-191">`ValidationAttribute`에서 상속하고, `IsValid` 메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-191">Just inherit from the `ValidationAttribute`, and override the `IsValid` method.</span></span> <span data-ttu-id="db88f-192">`IsValid` 메서드는 *value*라는 개체 및 *validationContext*라는 `ValidationContext` 개체 등 두 개의 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-192">The `IsValid` method accepts two parameters, the first is an object named *value* and the second is a `ValidationContext` object named *validationContext*.</span></span> <span data-ttu-id="db88f-193">*값*은 사용자 지정 유효성 검사기의 유효성을 검사하는 필드의 실제 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-193">*Value* refers to the actual value from the field that your custom validator is validating.</span></span>

<span data-ttu-id="db88f-194">다음 샘플에서 비즈니스 규칙에 따르면 사용자가 1960년 이후에 출시된 영화에 대해 장르를 *클래식*으로 설정하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-194">In the following sample, a business rule states that users may not set the genre to *Classic* for a movie released after 1960.</span></span> <span data-ttu-id="db88f-195">`[ClassicMovie]` 특성은 장르를 먼저 확인하고, 클래식인 경우 출시 날짜를 확인하여 1960년보다 이후인지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-195">The `[ClassicMovie]` attribute checks the genre first, and if it's a classic, then it checks the release date to see that it's later than 1960.</span></span> <span data-ttu-id="db88f-196">1960년 이후에 출시되었다면 유효성 검사에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-196">If it's released after 1960, validation fails.</span></span> <span data-ttu-id="db88f-197">특성은 데이터 유효성을 검사하는 데 사용할 수 있는 연도를 나타내는 정수 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-197">The attribute accepts an integer parameter representing the year that you can use to validate data.</span></span> <span data-ttu-id="db88f-198">다음과 같이 특성의 생성자에서 매개 변수의 값을 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-198">You can capture the value of the parameter in the attribute's constructor, as shown here:</span></span>

[!code-csharp[](validation/sample/ClassicMovieAttribute.cs?name=snippet_ClassicMovieAttribute)]

<span data-ttu-id="db88f-199">위의 `movie` 변수는 유효성을 검사할 형식 전송의 데이터를 포함하는 `Movie` 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-199">The `movie` variable above represents a `Movie` object that contains the data from the form submission to validate.</span></span> <span data-ttu-id="db88f-200">이 경우에 유효성 검사 코드는 규칙에 따라 `ClassicMovieAttribute` 클래스의 `IsValid` 메서드에서 날짜 및 장르를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-200">In this case, the validation code checks the date and genre in the `IsValid` method of the `ClassicMovieAttribute` class as per the rules.</span></span> <span data-ttu-id="db88f-201">유효성을 검사하여 `IsValid`가 `ValidationResult.Success` 코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-201">Upon successful validation ,`IsValid` returns a `ValidationResult.Success` code.</span></span> <span data-ttu-id="db88f-202">유효성 검사에 실패하면 오류 메시지가 발생하여 `ValidationResult`가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-202">When validation fails, a `ValidationResult` with an error message is returned:</span></span>

[!code-csharp[](validation/sample/ClassicMovieAttribute.cs?name=snippet_GetErrorMessage)]

<span data-ttu-id="db88f-203">사용자가 `Genre` 필드를 수정하고 형식을 제출하는 경우 `ClassicMovieAttribute`의 `IsValid` 메서드는 영화가 클래식인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-203">When a user modifies the `Genre` field and submits the form, the `IsValid` method of the `ClassicMovieAttribute` will verify whether the movie is a classic.</span></span> <span data-ttu-id="db88f-204">기본 제공 특성과 마찬가지로 `ClassicMovieAttribute`을 `ReleaseDate`와 같은 속성에 적용하여 앞의 코드 샘플에 표시된 대로 유효성 검사를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-204">Like any built-in attribute, apply the `ClassicMovieAttribute` to a property such as `ReleaseDate` to ensure validation happens, as shown in the previous code sample.</span></span> <span data-ttu-id="db88f-205">이 예제가 `Movie` 형식에서만 작동하므로 더 나은 옵션은 다음 단락에 표시된 대로 `IValidatableObject`를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-205">Since the example works only with `Movie` types, a better option is to use `IValidatableObject` as shown in the following paragraph.</span></span>

<span data-ttu-id="db88f-206">또는 `IValidatableObject` 인터페이스에서 `Validate` 메서드를 구현하여 모델에서 이 동일한 코드를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-206">Alternatively, this same code could be placed in the model by implementing the `Validate` method on the `IValidatableObject` interface.</span></span> <span data-ttu-id="db88f-207">사용자 지정 유효성 검사 특성이 개별 속성 유효성 검사에서 잘 작동하는 반면 `IValidatableObject`를 구현하는 작업은 클래스 수준 유효성 검사를 구현하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-207">While custom validation attributes work well for validating individual properties, implementing `IValidatableObject` can be used to implement class-level validation:</span></span>

[!code-csharp[](validation/sample/MovieIValidatable.cs?name=snippet&highlight=1,26-34)]

## <a name="client-side-validation"></a><span data-ttu-id="db88f-208">클라이언트 쪽 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="db88f-208">Client side validation</span></span>

<span data-ttu-id="db88f-209">클라이언트 쪽 유효성 검사는 사용자에게 매우 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-209">Client side validation is a great convenience for users.</span></span> <span data-ttu-id="db88f-210">그렇지 않은 경우 서버에 대한 왕복을 기다리는 데 드는 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-210">It saves time they would otherwise spend waiting for a round trip to the server.</span></span> <span data-ttu-id="db88f-211">비즈니스 용어로 몇 초를 매일 수백 번 반복하게 되면 많은 시간과 비용, 노력이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-211">In business terms, even a few fractions of seconds multiplied hundreds of times each day adds up to be a lot of time, expense, and frustration.</span></span> <span data-ttu-id="db88f-212">간단하고 즉각적인 유효성 검사를 사용하면 사용자가 보다 효율적으로 작업하고 더 좋은 품질의 입력 및 출력을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-212">Straightforward and immediate validation enables users to work more efficiently and produce better quality input and output.</span></span>

<span data-ttu-id="db88f-213">다음에 표시된 대로 사용할 클라이언트 쪽 유효성 검사 대신 적절한 JavaScript 스크립트 참조를 사용하는 보기가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-213">You must have a view with the proper JavaScript script references in place for client-side validation to work as you see here.</span></span>

[!code-cshtml[](validation/sample/Views/Shared/_Layout.cshtml?name=snippet_ScriptTag)]

[!code-cshtml[](validation/sample/Views/Shared/_ValidationScriptsPartial.cshtml)]

<span data-ttu-id="db88f-214">[jQuery 비간섭 유효성 검사](https://github.com/aspnet/jquery-validation-unobtrusive) 스크립트는 널리 사용되는 [jQuery 유효성 검사](https://jqueryvalidation.org/) 플러그 인에 기반한 사용자 지정 Microsoft 프런트 엔드 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-214">The [jQuery Unobtrusive Validation](https://github.com/aspnet/jquery-validation-unobtrusive) script is a custom Microsoft front-end library that builds on the popular [jQuery Validate](https://jqueryvalidation.org/) plugin.</span></span> <span data-ttu-id="db88f-215">jQuery 비간섭 유효성 검사를 사용하지 않고 두 위치(모델 속성에 대한 서버 쪽 유효성 검사 특성에서 한 번 및 클라이언트 쪽 스크립트에서 다시 한 번)에서 동일한 유효성 검사 논리를 코딩해야 합니다. (jQuery 유효성 검사의 [`validate()`](https://jqueryvalidation.org/validate/) 메서드에 대한 예제는 복잡함을 보여줍니다.)</span><span class="sxs-lookup"><span data-stu-id="db88f-215">Without jQuery Unobtrusive Validation, you would have to code the same validation logic in two places: once in the server side validation attributes on model properties, and then again in client side scripts (the examples for jQuery Validate's [`validate()`](https://jqueryvalidation.org/validate/) method shows how complex this could become).</span></span> <span data-ttu-id="db88f-216">대신 MVC의 [태그 도우미](xref:mvc/views/tag-helpers/intro) 및 [HTML 도우미](xref:mvc/views/overview)는 모델 속성의 유효성 검사 특성 및 형식 메타데이터를 사용하여 유효성 검사가 필요한 형식 요소에서 HTML 5 [데이터 특성](http://w3c.github.io/html/dom.html#embedding-custom-non-visible-data-with-the-data-attributes)을 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-216">Instead, MVC's [Tag Helpers](xref:mvc/views/tag-helpers/intro) and [HTML helpers](xref:mvc/views/overview) are able to use the validation attributes and type metadata from model properties to render HTML 5 [data- attributes](http://w3c.github.io/html/dom.html#embedding-custom-non-visible-data-with-the-data-attributes) in the form elements that need validation.</span></span> <span data-ttu-id="db88f-217">MVC에서는 기본 제공 및 사용자 지정 특성에 대한 `data-` 특성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-217">MVC generates the `data-` attributes for both built-in and custom attributes.</span></span> <span data-ttu-id="db88f-218">jQuery 비간섭 유효성 검사는 `data-` 특성을 구문 분석하고 jQuery 유효성 검사에 대한 논리를 전달하여 효과적으로 서버 쪽 유효성 검사 논리를 클라이언트에 “복사”합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-218">jQuery Unobtrusive Validation then parses the `data-` attributes and passes the logic to jQuery Validate, effectively "copying" the server side validation logic to the client.</span></span> <span data-ttu-id="db88f-219">다음과 같이 관련 태그 도우미를 사용하여 클라이언트에서 유효성 검사 오류를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-219">You can display validation errors on the client using the relevant tag helpers as shown here:</span></span>

[!code-cshtml[](validation/sample/Views/Movies/Create.cshtml?name=snippet_ReleaseDate&highlight=4-5)]

<span data-ttu-id="db88f-220">위의 태그 도우미는 아래의 HTML을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-220">The tag helpers above render the HTML below.</span></span> <span data-ttu-id="db88f-221">HTML의 `data-` 특성 출력은 `ReleaseDate` 속성에 대한 유효성 검사 특성에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-221">Notice that the `data-` attributes in the HTML output correspond to the validation attributes for the `ReleaseDate` property.</span></span> <span data-ttu-id="db88f-222">아래의 `data-val-required` 특성은 사용자가 릴리스 날짜 필드를 입력하지 않았음을 표시하는 오류 메시지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-222">The `data-val-required` attribute below contains an error message to display if the user doesn't fill in the release date field.</span></span> <span data-ttu-id="db88f-223">jQuery 비간섭 유효성 검사는 jQuery 유효성 검사 [`required()`](https://jqueryvalidation.org/required-method/) 메서드에 이 값을 전달합니다. 그러면 **\<span>** 요소와 함께 해당 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-223">jQuery Unobtrusive Validation passes this value to the jQuery Validate [`required()`](https://jqueryvalidation.org/required-method/) method, which then displays that message in the accompanying **\<span>** element.</span></span>

```html
<form action="/Movies/Create" method="post">
    <div class="form-horizontal">
        <h4>Movie</h4>
        <div class="text-danger"></div>
        <div class="form-group">
            <label class="col-md-2 control-label" for="ReleaseDate">ReleaseDate</label>
            <div class="col-md-10">
                <input class="form-control" type="datetime"
                data-val="true" data-val-required="The ReleaseDate field is required."
                id="ReleaseDate" name="ReleaseDate" value="" />
                <span class="text-danger field-validation-valid"
                data-valmsg-for="ReleaseDate" data-valmsg-replace="true"></span>
            </div>
        </div>
    </div>
</form>
```

<span data-ttu-id="db88f-224">클라이언트 쪽 유효성 검사는 형식이 유효할 때까지 전송을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-224">Client-side validation prevents submission until the form is valid.</span></span> <span data-ttu-id="db88f-225">제출 단추는 형식을 전송하거나 오류 메시지를 표시하는 JavaScript를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-225">The Submit button runs JavaScript that either submits the form or displays error messages.</span></span>

<span data-ttu-id="db88f-226">MVC는 속성의 .NET 데이터 형식에 따라 형식 특성 값을 결정하고 `[DataType]` 특성을 사용하여 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-226">MVC determines type attribute values based on the .NET data type of a property, possibly overridden using `[DataType]` attributes.</span></span> <span data-ttu-id="db88f-227">기본 `[DataType]` 특성은 실제 서버 쪽 유효성 검사를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-227">The base `[DataType]` attribute does no real server-side validation.</span></span> <span data-ttu-id="db88f-228">브라우저는 고유한 오류 메시지를 선택하고 원하는 대로 해당 오류를 표시하지만 jQuery 유효성 검사 비간섭 패키지는 이 메시지를 재정의하고 다른 메시지와 일관되게 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-228">Browsers choose their own error messages and display those errors as they wish, however the jQuery Validation Unobtrusive package can override the messages and display them consistently with others.</span></span> <span data-ttu-id="db88f-229">사용자가 `[EmailAddress]`와 같은 `[DataType]` 하위 클래스를 적용할 때 가장 분명하게 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-229">This happens most obviously when users apply `[DataType]` subclasses such as `[EmailAddress]`.</span></span>

### <a name="add-validation-to-dynamic-forms"></a><span data-ttu-id="db88f-230">동적 형식에 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="db88f-230">Add Validation to Dynamic Forms</span></span>

<span data-ttu-id="db88f-231">페이지가 처음 로드될 때 jQuery 비간섭 유효성 검사가 유효성 검사 논리 및 매개 변수를 jQuery 유효성 검사에 전달하기 때문에 동적으로 생성된 형식은 유효성 검사를 자동으로 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-231">Because jQuery Unobtrusive Validation passes validation logic and parameters to jQuery Validate when the page first loads, dynamically generated forms won't automatically exhibit validation.</span></span> <span data-ttu-id="db88f-232">대신 jQuery 비간섭 유효성 검사에서 동적 폼을 만든 후에 즉시 구문 분석하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-232">Instead, you must tell jQuery Unobtrusive Validation to parse the dynamic form immediately after creating it.</span></span> <span data-ttu-id="db88f-233">예를 들어 아래 코드에서는 AJAX를 통해 추가된 형식에서 클라이언트 쪽 유효성 검사를 설정할 수 있는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-233">For example, the code below shows how you might set up client side validation on a form added via AJAX.</span></span>

```js
$.get({
    url: "https://url/that/returns/a/form",
    dataType: "html",
    error: function(jqXHR, textStatus, errorThrown) {
        alert(textStatus + ": Couldn't add form. " + errorThrown);
    },
    success: function(newFormHTML) {
        var container = document.getElementById("form-container");
        container.insertAdjacentHTML("beforeend", newFormHTML);
        var forms = container.getElementsByTagName("form");
        var newForm = forms[forms.length - 1];
        $.validator.unobtrusive.parse(newForm);
    }
})
```

<span data-ttu-id="db88f-234">`$.validator.unobtrusive.parse()` 메서드는 하나의 인수에 대해 jQuery 선택기를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-234">The `$.validator.unobtrusive.parse()` method accepts a jQuery selector for its one argument.</span></span> <span data-ttu-id="db88f-235">이 메서드는 jQuery 비간섭 유효성 검사에서 해당 선택기 내에 있는 형식의 `data-` 특성을 구문 분석하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-235">This method tells jQuery Unobtrusive Validation to parse the `data-` attributes of forms within that selector.</span></span> <span data-ttu-id="db88f-236">이러한 특성의 값은 jQuery 유효성 검사 플러그 인에 전달되므로 형식은 원하는 클라이언트 쪽 유효성 검사 규칙을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-236">The values of those attributes are then passed to the jQuery Validate plugin so that the form exhibits the desired client side validation rules.</span></span>

### <a name="add-validation-to-dynamic-controls"></a><span data-ttu-id="db88f-237">동적 컨트롤에 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="db88f-237">Add Validation to Dynamic Controls</span></span>

<span data-ttu-id="db88f-238">`<input/>` 및 `<select/>` 등의 개별 컨트롤이 동적으로 생성될 경우 형식에 대한 유효성 검사 규칙을 업데이트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-238">You can also update the validation rules on a form when individual controls, such as `<input/>`s and `<select/>`s, are dynamically generated.</span></span> <span data-ttu-id="db88f-239">주변 형식이 이미 구문 분석되고 업데이트되지 않았기 때문에 이러한 요소에 대한 선택기를 `parse()` 메서드로 직접 전달할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-239">You cannot pass selectors for these elements to the `parse()` method directly because the surrounding form has already been parsed and won't update.</span></span> <span data-ttu-id="db88f-240">대신 먼저 기존 유효성 검사 데이터를 제거한 다음, 아래와 같이 전체 형식을 다시 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-240">Instead, you first remove the existing validation data, then reparse the entire form, as shown below:</span></span>

```js
$.get({
    url: "https://url/that/returns/a/control",
    dataType: "html",
    error: function(jqXHR, textStatus, errorThrown) {
        alert(textStatus + ": Couldn't add control. " + errorThrown);
    },
    success: function(newInputHTML) {
        var form = document.getElementById("my-form");
        form.insertAdjacentHTML("beforeend", newInputHTML);
        $(form).removeData("validator")    // Added by jQuery Validate
               .removeData("unobtrusiveValidation");   // Added by jQuery Unobtrusive Validation
        $.validator.unobtrusive.parse(form);
    }
})
```

## <a name="iclientmodelvalidator"></a><span data-ttu-id="db88f-241">IClientModelValidator</span><span class="sxs-lookup"><span data-stu-id="db88f-241">IClientModelValidator</span></span>

<span data-ttu-id="db88f-242">사용자는 사용자 지정 특성에 대한 클라이언트 쪽 논리를 만들 수 있으며, [jquery 유효성 검사](http://jqueryvalidation.org/documentation/)에 어댑터를 만드는 [비간섭 유효성 검사](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)는 클라이언트에서 유효성 검사 중에 자동으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-242">You may create client side logic for your custom attribute, and [unobtrusive validation](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) which creates an adapter to [jquery validation](http://jqueryvalidation.org/documentation/) will execute it on the client for you automatically as part of validation.</span></span> <span data-ttu-id="db88f-243">첫 번째 단계는 다음과 같이 `IClientModelValidator` 인터페이스를 구현하여 추가할 데이터 특성을 제어하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-243">The first step is to control what data- attributes are added by implementing the `IClientModelValidator` interface as shown here:</span></span>

[!code-csharp[](validation/sample/ClassicMovieAttribute.cs?name=snippet_AddValidation)]

<span data-ttu-id="db88f-244">이 인터페이스를 구현하는 특성은 생성된 필드에 HTML 특성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-244">Attributes that implement this interface can add HTML attributes to generated fields.</span></span> <span data-ttu-id="db88f-245">`ReleaseDate` 요소에 대한 출력을 검사하면 이전 예제와 비슷한 HTML을 표시합니다. 단지 이제는 `data-val-classicmovie` 특성이 `IClientModelValidator`라는 `AddValidation` 메서드에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-245">Examining the output for the `ReleaseDate` element reveals HTML that's similar to the previous example, except now there's a `data-val-classicmovie` attribute that was defined in the `AddValidation` method of `IClientModelValidator`.</span></span>

```html
<input class="form-control" type="datetime"
    data-val="true"
    data-val-classicmovie="Classic movies must have a release year earlier than 1960."
    data-val-classicmovie-year="1960"
    data-val-required="The ReleaseDate field is required."
    id="ReleaseDate" name="ReleaseDate" value="" />
```

<span data-ttu-id="db88f-246">비간섭 유효성 검사는 `data-` 특성에서 데이터를 사용하여 오류 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-246">Unobtrusive validation uses the data in the `data-` attributes to display error messages.</span></span> <span data-ttu-id="db88f-247">그러나 jQuery는 jQuery의 `validator` 개체에 추가될 때까지 규칙 또는 메시지를 인식하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-247">However, jQuery doesn't know about rules or messages until you add them to jQuery's `validator` object.</span></span> <span data-ttu-id="db88f-248">이는 사용자 지정 `classicmovie` 클라이언트 유효성 검사 메서드를 jQuery `validator` 개체에 추가하는 다음 예제에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-248">This is shown in the following example, which adds a custom `classicmovie` client validation method to the jQuery `validator` object.</span></span> <span data-ttu-id="db88f-249">`unobtrusive.adapters.add` 메서드에 대한 설명은 [Unobtrusive Client Validation in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)(ASP.NET MVC의 비간섭 클라이언트 유효성 검사)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db88f-249">For an explanation of the `unobtrusive.adapters.add` method, see [Unobtrusive Client Validation in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html).</span></span>

[!code-javascript[](validation/sample/Views/Movies/Create.cshtml?name=snippet_UnobtrusiveValidation)]

<span data-ttu-id="db88f-250">앞의 코드를 사용하면 `classicmovie` 메서드는 영화 개봉 날짜에 클라이언트 쪽 유효성 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-250">With the preceding code, the `classicmovie` method performs client-side validation on the movie release date.</span></span> <span data-ttu-id="db88f-251">메서드가 `false`를 반환하는 경우 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-251">The error message displays if the method returns `false`.</span></span>

## <a name="remote-validation"></a><span data-ttu-id="db88f-252">원격 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="db88f-252">Remote validation</span></span>

<span data-ttu-id="db88f-253">원격 유효성 검사는 서버의 데이터에 대한 클라이언트의 데이터 유효성을 검사해야 할 경우에 사용할 수 있는 유용한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-253">Remote validation is a great feature to use when you need to validate data on the client against data on the server.</span></span> <span data-ttu-id="db88f-254">예를 들어 앱은 이메일 또는 사용자 이름을 이미 사용 중인지 확인해야 하고, 이를 위해 많은 양의 데이터를 쿼리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-254">For example, your app may need to verify whether an email or user name is already in use, and it must query a large amount of data to do so.</span></span> <span data-ttu-id="db88f-255">하나 이상의 필드에 대한 유효성을 검사하는 대규모 데이터 집합을 다운로드하면 너무 많은 리소스를 소비하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-255">Downloading large sets of data for validating one or a few fields consumes too many resources.</span></span> <span data-ttu-id="db88f-256">또한 중요한 정보를 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-256">It may also expose sensitive information.</span></span> <span data-ttu-id="db88f-257">대안은 필드의 유효성을 검사하는 왕복 요청을 수행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-257">An alternative is to make a round-trip request to validate a field.</span></span>

<span data-ttu-id="db88f-258">2단계 프로세스에서 원격 유효성 검사를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-258">You can implement remote validation in a two step process.</span></span> <span data-ttu-id="db88f-259">먼저 `[Remote]` 특성을 사용하여 모델을 주석으로 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-259">First, you must annotate your model with the `[Remote]` attribute.</span></span> <span data-ttu-id="db88f-260">`[Remote]` 특성은 클라이언트 쪽 JavaScript를 적절한 코드를 호출하는 데 사용할 수 있는 여러 오버로드를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-260">The `[Remote]` attribute accepts multiple overloads you can use to direct client side JavaScript to the appropriate code to call.</span></span> <span data-ttu-id="db88f-261">다음 예제에서는 `Users` 컨트롤러의 `VerifyEmail` 작업 메서드를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-261">The example below points to the `VerifyEmail` action method of the `Users` controller.</span></span>

[!code-csharp[](validation/sample/User.cs?name=snippet_UserEmailProperty)]

<span data-ttu-id="db88f-262">두 번째 단계는 `[Remote]` 특성에 정의된 대로 해당 작업 메서드에서 유효성 검사 코드를 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-262">The second step is putting the validation code in the corresponding action method as defined in the `[Remote]` attribute.</span></span> <span data-ttu-id="db88f-263">jQuery 유효성 검사 [remote](https://jqueryvalidation.org/remote-method/) 메서드 설명서에 따라 서버 응답은 다음 중 하나인 JSON 문자열이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-263">According to the jQuery Validate [remote](https://jqueryvalidation.org/remote-method/) method documentation, the server response must be a JSON string that's either:</span></span>

* <span data-ttu-id="db88f-264">유효한 요소의 경우 `"true"`.</span><span class="sxs-lookup"><span data-stu-id="db88f-264">`"true"` for valid elements.</span></span>
* <span data-ttu-id="db88f-265">잘못된 요소의 경우 `"false"`, `undefined` 또는 `null`(기본 오류 메시지 사용).</span><span class="sxs-lookup"><span data-stu-id="db88f-265">`"false"`, `undefined`, or `null` for invalid elements, using the default error message.</span></span>

<span data-ttu-id="db88f-266">서버 응답이 문자열(예: `"That name is already taken, try peter123 instead"`)인 경우 문자열은 기본 문자열 대신 사용자 지정 오류 메시지로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-266">If the server response is a string (for example, `"That name is already taken, try peter123 instead"`), the string is displayed as a custom error message in place of the default string.</span></span>

<span data-ttu-id="db88f-267">`VerifyEmail` 메서드의 정의는 아래 표시된 대로 이러한 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-267">The definition of the `VerifyEmail` method follows these rules, as shown below.</span></span> <span data-ttu-id="db88f-268">이메일을 사용한 경우 유효성 검사 오류 메시지가 반환됩니다. 또는 이메일이 무료인 경우 `true`이며 `JsonResult` 개체에서 결과를 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-268">It returns a validation error message if the email is taken, or `true` if the email is free, and wraps the result in a `JsonResult` object.</span></span> <span data-ttu-id="db88f-269">클라이언트 쪽은 반환 값을 계속 사용하거나 필요한 경우 오류를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-269">The client side can then use the returned value to proceed or display the error if needed.</span></span>

[!code-csharp[](validation/sample/UsersController.cs?name=snippet_VerifyEmail)]

<span data-ttu-id="db88f-270">이제 사용자가 이메일을 입력하면 보기의 JavaScript에서는 해당 이메일을 사용하는지 확인하기 위해 원격 호출을 수행하고, 해당하는 경우 오류 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-270">Now when users enter an email, JavaScript in the view makes a remote call to see if that email has been taken and, if so, displays the error message.</span></span> <span data-ttu-id="db88f-271">그렇지 않으면 사용자는 일반적으로 형식을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-271">Otherwise, the user can submit the form as usual.</span></span>

<span data-ttu-id="db88f-272">`[Remote]` 특성의 `AdditionalFields` 속성은 서버에서 데이터에 대한 필드 조합의 유효성을 검사하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-272">The `AdditionalFields` property of the `[Remote]` attribute is useful for validating combinations of fields against data on the server.</span></span> <span data-ttu-id="db88f-273">예를 들어 위의 `User` 모델에 `FirstName` 및 `LastName`라는 두 개의 추가 속성이 있는 경우 기존 사용자가 해당 쌍의 이름을 사용하지 않는지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-273">For example, if the `User` model from above had two additional properties called `FirstName` and `LastName`, you might want to verify that no existing users already have that pair of names.</span></span> <span data-ttu-id="db88f-274">다음 코드와 같이 새로운 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-274">You define the new properties as shown in the following code:</span></span>

[!code-csharp[](validation/sample/User.cs?name=snippet_UserNameProperties)]

<span data-ttu-id="db88f-275">`AdditionalFields`는 명시적으로 `"FirstName"` 및 `"LastName"` 문자열로 설정될 수 있지만 다음과 같은 [`nameof`](/dotnet/csharp/language-reference/keywords/nameof) 연산자를 사용하면 나중에 리팩터링을 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-275">`AdditionalFields` could've been set explicitly to the strings `"FirstName"` and `"LastName"`, but using the [`nameof`](/dotnet/csharp/language-reference/keywords/nameof) operator like this simplifies later refactoring.</span></span> <span data-ttu-id="db88f-276">유효성 검사를 수행하는 작업 메서드는 `FirstName` 값 및 `LastName` 값에 대해 하나씩 두 개의 인수를 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-276">The action method to perform the validation must then accept two arguments, one for the value of `FirstName` and one for the value of `LastName`.</span></span>

[!code-csharp[](validation/sample/UsersController.cs?name=snippet_VerifyName)]

<span data-ttu-id="db88f-277">이제 사용자가 이름과 성을 입력할 때 JavaScript:</span><span class="sxs-lookup"><span data-stu-id="db88f-277">Now when users enter a first and last name, JavaScript:</span></span>

* <span data-ttu-id="db88f-278">해당 쌍의 이름을 사용 중인지 확인하기 위해 원격 호출을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-278">Makes a remote call to see if that pair of names has been taken.</span></span>
* <span data-ttu-id="db88f-279">쌍이 사용 중인 경우 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-279">If the pair has been taken, an error message is displayed.</span></span>
* <span data-ttu-id="db88f-280">그렇지 않은 경우 사용자는 형식을 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-280">If not taken, the user can submit the form.</span></span>

<span data-ttu-id="db88f-281">`[Remote]` 특성을 포함하는 두 개 이상의 추가 필드 유효성을 검사해야 하는 경우 쉼표로 구분된 목록으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-281">If you need to validate two or more additional fields with the `[Remote]` attribute, you provide them as a comma-delimited list.</span></span> <span data-ttu-id="db88f-282">예를 들어 `MiddleName` 특성을 메서드에 추가하고, 다음 코드에 표시된 대로 `[Remote]` 특성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-282">For example, to add a `MiddleName` property to the model, set the `[Remote]` attribute as shown in the following code:</span></span>

```cs
[Remote(action: "VerifyName", controller: "Users", AdditionalFields = nameof(FirstName) + "," + nameof(LastName))]
public string MiddleName { get; set; }
```

<span data-ttu-id="db88f-283">모든 특성 인수와 같은 `AdditionalFields`은 상수 식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-283">`AdditionalFields`, like all attribute arguments, must be a constant expression.</span></span> <span data-ttu-id="db88f-284">따라서 [보간된 문자열](/dotnet/csharp/language-reference/keywords/interpolated-strings)을 사용하거나 <xref:System.String.Join*>을 호출하여 `AdditionalFields`를 초기화하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-284">Therefore, you must not use an [interpolated string](/dotnet/csharp/language-reference/keywords/interpolated-strings) or call <xref:System.String.Join*> to initialize `AdditionalFields`.</span></span> <span data-ttu-id="db88f-285">`[Remote]` 특성에 추가한 모든 추가 필드의 경우 해당하는 컨트롤러 작업 메서드에 다른 인수를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db88f-285">For every additional field that you add to the `[Remote]` attribute, you must add another argument to the corresponding controller action method.</span></span>
