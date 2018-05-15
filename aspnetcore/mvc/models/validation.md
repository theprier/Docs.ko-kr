---
title: ASP.NET Core MVC의 모델 유효성 검사
author: rachelappel
description: ASP.NET Core MVC의 모델 유효성 검사에 대해 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 12/18/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/models/validation
ms.openlocfilehash: 1ab19fad90eab9f2da58b4d62615a85d71894218
ms.sourcegitcommit: 5130b3034165f5cf49d829fe7475a84aa33d2693
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="model-validation-in-aspnet-core-mvc"></a><span data-ttu-id="668dd-103">ASP.NET Core MVC의 모델 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="668dd-103">Model validation in ASP.NET Core MVC</span></span>

<span data-ttu-id="668dd-104">작성자: [Rachel Appel](https://github.com/rachelappel)</span><span class="sxs-lookup"><span data-stu-id="668dd-104">By [Rachel Appel](https://github.com/rachelappel)</span></span>

## <a name="introduction-to-model-validation"></a><span data-ttu-id="668dd-105">모델 유효성 검사 소개</span><span class="sxs-lookup"><span data-stu-id="668dd-105">Introduction to model validation</span></span>

<span data-ttu-id="668dd-106">앱은 데이터베이스에 데이터를 저장하기 전에 데이터를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-106">Before an app stores data in a database, the app must validate the data.</span></span> <span data-ttu-id="668dd-107">데이터는 잠재적 보안 위협을 확인하고, 형식 및 크기별로 적절하게 서식이 지정되었는지 확인하고, 규칙을 준수해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-107">Data must be checked for potential security threats, verified that it's appropriately formatted by type and size, and it must conform to your rules.</span></span> <span data-ttu-id="668dd-108">유효성 검사는 중복되고 구현되기 번거로울 수 있지만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-108">Validation is necessary although it can be redundant and tedious to implement.</span></span> <span data-ttu-id="668dd-109">MVC에서 유효성 검사는 클라이언트와 서버 모두에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-109">In MVC, validation happens on both the client and server.</span></span>

<span data-ttu-id="668dd-110">다행히 .NET는 유효성 검사를 유효성 검사 특성으로 추상화했습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-110">Fortunately, .NET has abstracted validation into validation attributes.</span></span> <span data-ttu-id="668dd-111">이러한 특성에는 유효성 검사 코드가 포함되어 작성해야 하는 코드의 양을 감소시킵니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-111">These attributes contain validation code, thereby reducing the amount of code you must write.</span></span>

<span data-ttu-id="668dd-112">[GitHub에서 샘플 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/models/validation/sample)</span><span class="sxs-lookup"><span data-stu-id="668dd-112">[View or download sample from GitHub](https://github.com/aspnet/Docs/tree/master/aspnetcore/mvc/models/validation/sample).</span></span>

## <a name="validation-attributes"></a><span data-ttu-id="668dd-113">유효성 검사 특성</span><span class="sxs-lookup"><span data-stu-id="668dd-113">Validation Attributes</span></span>

<span data-ttu-id="668dd-114">유효성 검사 특성은 모델 유효성 검사를 구성하는 방법이므로 데이터베이스 테이블의 필드에 대한 유효성 검사와 개념적으로 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-114">Validation attributes are a way to configure model validation so it's similar conceptually to validation on fields in database tables.</span></span> <span data-ttu-id="668dd-115">데이터 형식이나 필수 필드를 할당하는 등 제약 조건이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-115">This includes constraints such as assigning data types or required fields.</span></span> <span data-ttu-id="668dd-116">다른 종류의 유효성 검사에는 신용 카드, 전화 번호 또는 이메일 주소와 같은 비즈니스 규칙을 적용하기 위해 데이터에 대한 패턴을 적용하는 것이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-116">Other types of validation include applying patterns to data to enforce business rules, such as a credit card, phone number, or email address.</span></span> <span data-ttu-id="668dd-117">유효성 검사 특성을 통해 훨씬 간단하고 사용하기 쉽게 이러한 요구 사항을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-117">Validation attributes make enforcing these requirements much simpler and easier to use.</span></span>

<span data-ttu-id="668dd-118">영화 및 TV 프로그램에 대 한 정보를 저장하는 앱에서 주석이 추가된 `Movie` 모델은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-118">Below is an annotated `Movie` model from an app that stores information about movies and TV shows.</span></span> <span data-ttu-id="668dd-119">대부분의 속성은 필수이며 여러 문자열 속성에는 길이 요구 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-119">Most of the properties are required and several string properties have length requirements.</span></span> <span data-ttu-id="668dd-120">또한 사용자 지정 유효성 검사 특성과 함께 `Price` 속성 대신에 0~$999.99 사이라는 숫자 범위 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-120">Additionally, there's a numeric range restriction in place for the `Price` property from 0 to $999.99, along with a custom validation attribute.</span></span>

[!code-csharp[](validation/sample/Movie.cs?range=6-29)]

<span data-ttu-id="668dd-121">단순히 모델을 통해 읽으면 이 앱에서 데이터에 대한 규칙을 표시하여 코드를 쉽게 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-121">Simply reading through the model reveals the rules about data for this app, making it easier to maintain the code.</span></span> <span data-ttu-id="668dd-122">널리 사용되는 여러 기본 제공 유효성 검사 특성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-122">Below are several popular built-in validation attributes:</span></span>

* <span data-ttu-id="668dd-123">`[CreditCard]`: 속성에 신용 카드 형식이 있는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-123">`[CreditCard]`: Validates the property has a credit card format.</span></span>

* <span data-ttu-id="668dd-124">`[Compare]`: 모델의 두 속성이 일치하는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-124">`[Compare]`: Validates two properties in a model match.</span></span>

* <span data-ttu-id="668dd-125">`[EmailAddress]`: 속성에 이메일 형식이 있는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-125">`[EmailAddress]`: Validates the property has an email format.</span></span>

* <span data-ttu-id="668dd-126">`[Phone]`: 속성에 전화 번호 형식이 있는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-126">`[Phone]`: Validates the property has a telephone format.</span></span>

* <span data-ttu-id="668dd-127">`[Range]`: 지정된 범위 내에서 속성 값이 포함되는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-127">`[Range]`: Validates the property value falls within the given range.</span></span>

* <span data-ttu-id="668dd-128">`[RegularExpression]`: 데이터가 지정된 정규식과 일치하는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-128">`[RegularExpression]`: Validates that the data matches the specified regular expression.</span></span>

* <span data-ttu-id="668dd-129">`[Required]`: 필수 속성으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-129">`[Required]`: Makes a property required.</span></span>

* <span data-ttu-id="668dd-130">`[StringLength]`: 문자열 속성에 지정된 최대 길이가 있는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-130">`[StringLength]`: Validates that a string property has at most the given maximum length.</span></span>

* <span data-ttu-id="668dd-131">`[Url]`: 속성에 URL 형식이 있는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-131">`[Url]`: Validates the property has a URL format.</span></span>

<span data-ttu-id="668dd-132">MVC는 유효성 검사를 위해 `ValidationAttribute`에서 파생된 모든 특성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-132">MVC supports any attribute that derives from `ValidationAttribute` for validation purposes.</span></span> <span data-ttu-id="668dd-133">많은 유용한 유효성 검사 특성을 [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) 네임스페이스에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-133">Many useful validation attributes can be found in the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace.</span></span>

<span data-ttu-id="668dd-134">제공되는 기본 제공 특성보다 더 많은 기능이 필요한 인스턴스가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-134">There may be instances where you need more features than built-in attributes provide.</span></span> <span data-ttu-id="668dd-135">이 경우에 `ValidationAttribute`에서 파생하거나 `IValidatableObject`를 구현하도록 모델을 변경하여 사용자 지정 유효성 검사 특성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-135">For those times, you can create custom validation attributes by deriving from `ValidationAttribute` or changing your model to implement `IValidatableObject`.</span></span>

## <a name="notes-on-the-use-of-the-required-attribute"></a><span data-ttu-id="668dd-136">필수 특성 사용에 대한 참고</span><span class="sxs-lookup"><span data-stu-id="668dd-136">Notes on the use of the Required attribute</span></span>

<span data-ttu-id="668dd-137">nullable 형식이 아닌 [값 형식](/dotnet/csharp/language-reference/keywords/value-types)(`decimal`, `int`, `float`,`DateTime`)은 기본적으로 필요하며 `Required` 특성은 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-137">Non-nullable [value types](/dotnet/csharp/language-reference/keywords/value-types) (such as `decimal`, `int`, `float`, and `DateTime`) are inherently required and don't need the `Required` attribute.</span></span> <span data-ttu-id="668dd-138">앱은 `Required`으로 표시된 null이 아닌 형식에 서버 쪽 유효성 검사를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-138">The app performs no server-side validation checks for non-nullable types that are marked `Required`.</span></span>

<span data-ttu-id="668dd-139">유효성 검사 및 유효성 검사 특성과 관련되지 않는 MVC 모델 바인딩은 null이 아닌 형식에 누락 값 또는 공백을 포함하는 형식 필드 전송을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-139">MVC model binding, which isn't concerned with validation and validation attributes, rejects a form field submission containing a missing value or whitespace for a non-nullable type.</span></span> <span data-ttu-id="668dd-140">대상 속성에 `BindRequired` 특성이 없는 경우에 모델 바인딩은 null이 아닌 형식에 대한 누락 데이터를 무시합니다. 여기서 들어오는 형식 데이터에서 형식 필드는 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-140">In the absence of a `BindRequired` attribute on the target property, model binding ignores missing data for non-nullable types, where the form field is absent from the incoming form data.</span></span>

<span data-ttu-id="668dd-141">[BindRequired 특성](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.bindrequiredattribute)([특성을 포함한 모델 바인딩 동작 사용자 지정](xref:mvc/models/model-binding#customize-model-binding-behavior-with-attributes) 참조)은 형식 데이터를 완료하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-141">The [BindRequired attribute](/dotnet/api/microsoft.aspnetcore.mvc.modelbinding.bindrequiredattribute) (also see [Customize model binding behavior with attributes](xref:mvc/models/model-binding#customize-model-binding-behavior-with-attributes)) is useful to ensure form data is complete.</span></span> <span data-ttu-id="668dd-142">속성에 적용하는 경우 모델 바인딩 시스템에는 해당 속성에 대한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-142">When applied to a property, the model binding system requires a value for that property.</span></span> <span data-ttu-id="668dd-143">형식에 적용하는 경우 모델 바인딩 시스템에는 해당 형식의 모든 속성에 대한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-143">When applied to a type, the model binding system requires values for all of the properties of that type.</span></span>

<span data-ttu-id="668dd-144">[Nullable\<T > 형식](/dotnet/csharp/programming-guide/nullable-types/)(예: `decimal?` 또는 `System.Nullable<decimal>`)을 사용하고 `Required`으로 표시하는 경우 속성이 표준 null 형식인 것처럼 서버 쪽 유효성 검사가 수행됩니다(예: `string`).</span><span class="sxs-lookup"><span data-stu-id="668dd-144">When you use a [Nullable\<T> type](/dotnet/csharp/programming-guide/nullable-types/) (for example, `decimal?` or `System.Nullable<decimal>`) and mark it `Required`, a server-side validation check is performed as if the property were a standard nullable type (for example, a `string`).</span></span>

<span data-ttu-id="668dd-145">클라이언트 쪽 유효성 검사에는 `Required`로 표시한 모델 속성에 해당하는 형식 필드에 대한 값 및 `Required`로 표시하지 않은 null이 아닌 형식 속성에 대한 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-145">Client-side validation requires a value for a form field that corresponds to a model property that you've marked `Required` and for a non-nullable type property that you haven't marked `Required`.</span></span> <span data-ttu-id="668dd-146">`Required`는 클라이언트 쪽 유효성 검사 오류 메시지를 제어하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-146">`Required` can be used to control the client-side validation error message.</span></span>

## <a name="model-state"></a><span data-ttu-id="668dd-147">모델 상태</span><span class="sxs-lookup"><span data-stu-id="668dd-147">Model State</span></span>

<span data-ttu-id="668dd-148">모델 상태는 제출된 HTML 형식 값으로 유효성 검사 오류를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-148">Model state represents validation errors in submitted HTML form values.</span></span>

<span data-ttu-id="668dd-149">MVC는오류의 최대 수(기본적으로 200개)에 도달할 때까지 필드를 계속 유효성 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-149">MVC will continue validating fields until reaches the maximum number of errors (200 by default).</span></span> <span data-ttu-id="668dd-150">*Startup.cs* 파일의 `ConfigureServices` 메서드에 다음 코드를 삽입하여 이 번호를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-150">You can configure this number by inserting the following code into the `ConfigureServices` method in the *Startup.cs* file:</span></span>

[!code-csharp[](validation/sample/Startup.cs?range=27)]

## <a name="handling-model-state-errors"></a><span data-ttu-id="668dd-151">모델 상태 오류 처리</span><span class="sxs-lookup"><span data-stu-id="668dd-151">Handling Model State Errors</span></span>

<span data-ttu-id="668dd-152">모델 유효성 검사는 각 컨트롤러 작업을 호출하기 전에 발생하며, `ModelState.IsValid`를 검사하고 적절하게 반응하는 것은 작업 메서드의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-152">Model validation occurs prior to each controller action being invoked, and it's the action method's responsibility to inspect `ModelState.IsValid` and react appropriately.</span></span> <span data-ttu-id="668dd-153">대부분의 경우 적합한 반응은 이상적으로 모델 유효성 검사에 실패한 이유를 자세히 보여주는 오류 응답을 반환하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-153">In many cases, the appropriate reaction is to return an error response, ideally detailing the reason why model validation failed.</span></span>

<span data-ttu-id="668dd-154">필터가 이러한 정책을 구현하기에 적절한 경우에 일부 앱은 모델 유효성 검사 오류를 처리하는 표준 규칙을 따르도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-154">Some apps will choose to follow a standard convention for dealing with model validation errors, in which case a filter may be an appropriate place to implement such a policy.</span></span> <span data-ttu-id="668dd-155">유효한 모델 및 잘못된 모델 상태일 때 작업 동작 방식을 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-155">You should test how your actions behave with valid and invalid model states.</span></span>

## <a name="manual-validation"></a><span data-ttu-id="668dd-156">수동 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="668dd-156">Manual validation</span></span>

<span data-ttu-id="668dd-157">모델 바인딩 및 유효성 검사가 완료되면 일부를 반복하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-157">After model binding and validation are complete, you may want to repeat parts of it.</span></span> <span data-ttu-id="668dd-158">예를 들어 사용자는 정수가 필요한 필드에 텍스트를 입력하거나 모델의 속성에 대한 값을 계산해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-158">For example, a user may have entered text in a field expecting an integer, or you may need to compute a value for a model's property.</span></span>

<span data-ttu-id="668dd-159">유효성 검사를 수동으로 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-159">You may need to run validation manually.</span></span> <span data-ttu-id="668dd-160">이렇게 하려면 다음과 같이 `TryValidateModel` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-160">To do so, call the `TryValidateModel` method, as shown here:</span></span>

[!code-csharp[](validation/sample/MoviesController.cs?range=52)]

## <a name="custom-validation"></a><span data-ttu-id="668dd-161">사용자 지정 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="668dd-161">Custom validation</span></span>

<span data-ttu-id="668dd-162">유효성 검사 특성은 대부분의 유효성 검사 요구 사항에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-162">Validation attributes work for most validation needs.</span></span> <span data-ttu-id="668dd-163">그러나 일부 유효성 검사 규칙은 비즈니스에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-163">However, some validation rules are specific to your business.</span></span> <span data-ttu-id="668dd-164">규칙은 필드가 필요하거나 값의 범위를 준수하는지 확인하는 등 일반적인 데이터 유효성 검사 기술이 아닐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-164">Your rules might not be common data validation techniques such as ensuring a field is required or that it conforms to a range of values.</span></span> <span data-ttu-id="668dd-165">이러한 시나리오에서 사용자 지정 유효성 검사 특성을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-165">For these scenarios, custom validation attributes are a great solution.</span></span> <span data-ttu-id="668dd-166">MVC에서 고유한 사용자 지정 유효성 검사 특성을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-166">Creating your own custom validation attributes in MVC is easy.</span></span> <span data-ttu-id="668dd-167">`ValidationAttribute`에서 상속하고, `IsValid` 메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-167">Just inherit from the `ValidationAttribute`, and override the `IsValid` method.</span></span> <span data-ttu-id="668dd-168">`IsValid` 메서드는 *value*라는 개체 및 *validationContext*라는 `ValidationContext` 개체 등 두 개의 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-168">The `IsValid` method accepts two parameters, the first is an object named *value* and the second is a `ValidationContext` object named *validationContext*.</span></span> <span data-ttu-id="668dd-169">*값*은 사용자 지정 유효성 검사기의 유효성을 검사하는 필드의 실제 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-169">*Value* refers to the actual value from the field that your custom validator is validating.</span></span>

<span data-ttu-id="668dd-170">다음 샘플에서 비즈니스 규칙에 따르면 사용자가 1960년 이후에 출시된 영화에 대해 장르를 *클래식*으로 설정하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-170">In the following sample, a business rule states that users may not set the genre to *Classic* for a movie released after 1960.</span></span> <span data-ttu-id="668dd-171">`[ClassicMovie]` 특성은 장르를 먼저 확인하고, 클래식인 경우 출시 날짜를 확인하여 1960년보다 이후인지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-171">The `[ClassicMovie]` attribute checks the genre first, and if it's a classic, then it checks the release date to see that it's later than 1960.</span></span> <span data-ttu-id="668dd-172">1960년 이후에 출시되었다면 유효성 검사에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-172">If it's released after 1960, validation fails.</span></span> <span data-ttu-id="668dd-173">특성은 데이터 유효성을 검사하는 데 사용할 수 있는 연도를 나타내는 정수 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-173">The attribute accepts an integer parameter representing the year that you can use to validate data.</span></span> <span data-ttu-id="668dd-174">다음과 같이 특성의 생성자에서 매개 변수의 값을 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-174">You can capture the value of the parameter in the attribute's constructor, as shown here:</span></span>

[!code-csharp[](validation/sample/ClassicMovieAttribute.cs?range=9-29)]

<span data-ttu-id="668dd-175">위의 `movie` 변수는 유효성을 검사할 형식 전송의 데이터를 포함하는 `Movie` 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-175">The `movie` variable above represents a `Movie` object that contains the data from the form submission to validate.</span></span> <span data-ttu-id="668dd-176">이 경우에 유효성 검사 코드는 규칙에 따라 `ClassicMovieAttribute` 클래스의 `IsValid` 메서드에서 날짜 및 장르를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-176">In this case, the validation code checks the date and genre in the `IsValid` method of the `ClassicMovieAttribute` class as per the rules.</span></span> <span data-ttu-id="668dd-177">유효성 검사에 성공하면 `IsValid`는 `ValidationResult.Success` 코드를 반환하고, 유효성 검사에 실패하면 오류 메시지와 함께 `ValidationResult` 코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-177">Upon successful validation `IsValid` returns a `ValidationResult.Success` code, and when validation fails, a `ValidationResult` with an error message.</span></span> <span data-ttu-id="668dd-178">사용자가 `Genre` 필드를 수정하고 형식을 제출하는 경우 `ClassicMovieAttribute`의 `IsValid` 메서드는 영화가 클래식인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-178">When a user modifies the `Genre` field and submits the form, the `IsValid` method of the `ClassicMovieAttribute` will verify whether the movie is a classic.</span></span> <span data-ttu-id="668dd-179">기본 제공 특성과 마찬가지로 `ClassicMovieAttribute`을 `ReleaseDate`와 같은 속성에 적용하여 앞의 코드 샘플에 표시된 대로 유효성 검사를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-179">Like any built-in attribute, apply the `ClassicMovieAttribute` to a property such as `ReleaseDate` to ensure validation happens, as shown in the previous code sample.</span></span> <span data-ttu-id="668dd-180">이 예제가 `Movie` 형식에서만 작동하므로 더 나은 옵션은 다음 단락에 표시된 대로 `IValidatableObject`를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-180">Since the example works only with `Movie` types, a better option is to use `IValidatableObject` as shown in the following paragraph.</span></span>

<span data-ttu-id="668dd-181">또는 `IValidatableObject` 인터페이스에서 `Validate` 메서드를 구현하여 모델에서 이 동일한 코드를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-181">Alternatively, this same code could be placed in the model by implementing the `Validate` method on the `IValidatableObject` interface.</span></span> <span data-ttu-id="668dd-182">사용자 지정 유효성 검사 특성이 개별 속성 유효성 검사에서 잘 작동하는 반면 `IValidatableObject`를 구현하는 작업은 다음과 같이 클래스 수준 유효성 검사를 구현하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-182">While custom validation attributes work well for validating individual properties, implementing `IValidatableObject` can be used to implement class-level validation as seen here.</span></span>

[!code-csharp[](validation/sample/MovieIValidatable.cs?range=32-40)]

## <a name="client-side-validation"></a><span data-ttu-id="668dd-183">클라이언트 쪽 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="668dd-183">Client side validation</span></span>

<span data-ttu-id="668dd-184">클라이언트 쪽 유효성 검사는 사용자에게 매우 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-184">Client side validation is a great convenience for users.</span></span> <span data-ttu-id="668dd-185">그렇지 않은 경우 서버에 대한 왕복을 기다리는 데 드는 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-185">It saves time they would otherwise spend waiting for a round trip to the server.</span></span> <span data-ttu-id="668dd-186">비즈니스 용어로 몇 초를 매일 수백 번 반복하게 되면 많은 시간과 비용, 노력이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-186">In business terms, even a few fractions of seconds multiplied hundreds of times each day adds up to be a lot of time, expense, and frustration.</span></span> <span data-ttu-id="668dd-187">간단하고 즉각적인 유효성 검사를 사용하면 사용자는 보다 효율적으로 작업하고 더 좋은 품질의 입력 및 출력을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-187">Straightforward and immediate validation enables users to work more efficiently and produce better quality input and output.</span></span>

<span data-ttu-id="668dd-188">다음에 표시된 대로 사용할 클라이언트 쪽 유효성 검사 대신 적절한 JavaScript 스크립트 참조를 사용하는 보기가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-188">You must have a view with the proper JavaScript script references in place for client side validation to work as you see here.</span></span>

[!code-cshtml[](validation/sample/Views/Shared/_Layout.cshtml?range=37)]

[!code-cshtml[](validation/sample/Views/Shared/_ValidationScriptsPartial.cshtml)]

<span data-ttu-id="668dd-189">[jQuery 비간섭 유효성 검사](https://github.com/aspnet/jquery-validation-unobtrusive) 스크립트는 널리 사용되는 [jQuery 유효성 검사](https://jqueryvalidation.org/) 플러그 인에 기반한 사용자 지정 Microsoft 프런트 엔드 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-189">The [jQuery Unobtrusive Validation](https://github.com/aspnet/jquery-validation-unobtrusive) script is a custom Microsoft front-end library that builds on the popular [jQuery Validate](https://jqueryvalidation.org/) plugin.</span></span> <span data-ttu-id="668dd-190">jQuery 비간섭 유효성 검사를 사용하지 않고 두 위치(모델 속성에 대한 서버 쪽 유효성 검사 특성에서 한 번 및 클라이언트 쪽 스크립트에서 다시 한 번)에서 동일한 유효성 검사 논리를 코딩해야 합니다. (jQuery 유효성 검사의 [`validate()`](https://jqueryvalidation.org/validate/) 메서드에 대한 예제는 복잡함을 보여줍니다.)</span><span class="sxs-lookup"><span data-stu-id="668dd-190">Without jQuery Unobtrusive Validation, you would have to code the same validation logic in two places: once in the server side validation attributes on model properties, and then again in client side scripts (the examples for jQuery Validate's [`validate()`](https://jqueryvalidation.org/validate/) method shows how complex this could become).</span></span> <span data-ttu-id="668dd-191">대신 MVC의 [태그 도우미](xref:mvc/views/tag-helpers/intro) 및 [HTML 도우미](xref:mvc/views/overview)는 모델 속성의 유효성 검사 특성 및 형식 메타데이터를 사용하여 유효성 검사가 필요한 형식 요소에서 HTML 5 [데이터 특성](http://w3c.github.io/html/dom.html#embedding-custom-non-visible-data-with-the-data-attributes)을 렌더링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-191">Instead, MVC's [Tag Helpers](xref:mvc/views/tag-helpers/intro) and [HTML helpers](xref:mvc/views/overview) are able to use the validation attributes and type metadata from model properties to render HTML 5 [data- attributes](http://w3c.github.io/html/dom.html#embedding-custom-non-visible-data-with-the-data-attributes) in the form elements that need validation.</span></span> <span data-ttu-id="668dd-192">MVC에서는 기본 제공 및 사용자 지정 특성에 대한 `data-` 특성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-192">MVC generates the `data-` attributes for both built-in and custom attributes.</span></span> <span data-ttu-id="668dd-193">jQuery 비간섭 유효성 검사는 `data-` 특성을 구문 분석한 다음, jQuery 유효성 검사에 대한 논리를 전달하여 효과적으로 서버 쪽 유효성 검사 논리를 클라이언트에 "복사"합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-193">jQuery Unobtrusive Validation then parses thes `data-` attributes and passes the logic to jQuery Validate, effectively "copying" the server side validation logic to the client.</span></span> <span data-ttu-id="668dd-194">다음과 같이 관련 태그 도우미를 사용하여 클라이언트에서 유효성 검사 오류를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-194">You can display validation errors on the client using the relevant tag helpers as shown here:</span></span>

[!code-cshtml[](validation/sample/Views/Movies/Create.cshtml?highlight=4,5&range=19-25)]

<span data-ttu-id="668dd-195">위의 태그 도우미는 아래의 HTML을 렌더링합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-195">The tag helpers above render the HTML below.</span></span> <span data-ttu-id="668dd-196">HTML의 `data-` 특성 출력은 `ReleaseDate` 속성에 대한 유효성 검사 특성에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-196">Notice that the `data-` attributes in the HTML output correspond to the validation attributes for the `ReleaseDate` property.</span></span> <span data-ttu-id="668dd-197">아래의 `data-val-required` 특성은 사용자가 릴리스 날짜 필드를 입력하지 않았음을 표시하는 오류 메시지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-197">The `data-val-required` attribute below contains an error message to display if the user doesn't fill in the release date field.</span></span> <span data-ttu-id="668dd-198">jQuery 비간섭 유효성 검사는 jQuery 유효성 검사 [`required()`](https://jqueryvalidation.org/required-method/) 메서드에 이 값을 전달합니다. 그러면**\<span>** 요소와 함께 해당 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-198">jQuery Unobtrusive Validation passes this value to the jQuery Validate [`required()`](https://jqueryvalidation.org/required-method/) method, which then displays that message in the accompanying **\<span>** element.</span></span>

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

<span data-ttu-id="668dd-199">클라이언트 쪽 유효성 검사는 형식이 유효할 때까지 전송을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-199">Client-side validation prevents submission until the form is valid.</span></span> <span data-ttu-id="668dd-200">제출 단추는 형식을 전송하거나 오류 메시지를 표시하는 JavaScript를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-200">The Submit button runs JavaScript that either submits the form or displays error messages.</span></span>

<span data-ttu-id="668dd-201">MVC는 속성의 .NET 데이터 형식에 따라 형식 특성 값을 결정하고 `[DataType]` 특성을 사용하여 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-201">MVC determines type attribute values based on the .NET data type of a property, possibly overridden using `[DataType]` attributes.</span></span> <span data-ttu-id="668dd-202">기본 `[DataType]` 특성은 실제 서버 쪽 유효성 검사를 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-202">The base `[DataType]` attribute does no real server-side validation.</span></span> <span data-ttu-id="668dd-203">브라우저는 고유한 오류 메시지를 선택하고 원하는 대로 해당 오류를 표시하지만 jQuery 유효성 검사 비간섭 패키지는 이 메시지를 재정의하고 다른 메시지와 일관되게 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-203">Browsers choose their own error messages and display those errors as they wish, however the jQuery Validation Unobtrusive package can override the messages and display them consistently with others.</span></span> <span data-ttu-id="668dd-204">사용자가 `[EmailAddress]`와 같은 `[DataType]` 하위 클래스를 적용할 때 가장 분명하게 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-204">This happens most obviously when users apply `[DataType]` subclasses such as `[EmailAddress]`.</span></span>

### <a name="add-validation-to-dynamic-forms"></a><span data-ttu-id="668dd-205">동적 형식에 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="668dd-205">Add Validation to Dynamic Forms</span></span>

<span data-ttu-id="668dd-206">페이지가 처음 로드될 때 jQuery 비간섭 유효성 검사가 유효성 검사 논리 및 매개 변수를 jQuery 유효성 검사에 전달하기 때문에 동적으로 생성된 형식은 유효성 검사를 자동으로 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-206">Because jQuery Unobtrusive Validation passes validation logic and parameters to jQuery Validate when the page first loads, dynamically generated forms won't automatically exhibit validation.</span></span> <span data-ttu-id="668dd-207">대신 jQuery 비간섭 유효성 검사에서 동적 폼을 만든 후에 즉시 구문 분석하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-207">Instead, you must tell jQuery Unobtrusive Validation to parse the dynamic form immediately after creating it.</span></span> <span data-ttu-id="668dd-208">예를 들어 아래 코드에서는 AJAX를 통해 추가된 형식에서 클라이언트 쪽 유효성 검사를 설정할 수 있는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-208">For example, the code below shows how you might set up client side validation on a form added via AJAX.</span></span>

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

<span data-ttu-id="668dd-209">`$.validator.unobtrusive.parse()` 메서드는 하나의 인수에 대해 jQuery 선택기를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-209">The `$.validator.unobtrusive.parse()` method accepts a jQuery selector for its one argument.</span></span> <span data-ttu-id="668dd-210">이 메서드는 jQuery 비간섭 유효성 검사에서 해당 선택기 내에 있는 형식의 `data-` 특성을 구문 분석하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-210">This method tells jQuery Unobtrusive Validation to parse the `data-` attributes of forms within that selector.</span></span> <span data-ttu-id="668dd-211">이러한 특성의 값은 jQuery 유효성 검사 플러그 인에 전달되므로 형식은 원하는 클라이언트 쪽 유효성 검사 규칙을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-211">The values of those attributes are then passed to the jQuery Validate plugin so that the form exhibits the desired client side validation rules.</span></span>

### <a name="add-validation-to-dynamic-controls"></a><span data-ttu-id="668dd-212">동적 컨트롤에 유효성 검사 추가</span><span class="sxs-lookup"><span data-stu-id="668dd-212">Add Validation to Dynamic Controls</span></span>

<span data-ttu-id="668dd-213">`<input/>` 및 `<select/>` 등의 개별 컨트롤이 동적으로 생성될 경우 형식에 대한 유효성 검사 규칙을 업데이트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-213">You can also update the validation rules on a form when individual controls, such as `<input/>`s and `<select/>`s, are dynamically generated.</span></span> <span data-ttu-id="668dd-214">주변 형식이 이미 구문 분석되고 업데이트되지 않았기 때문에 이러한 요소에 대한 선택기를 `parse()` 메서드로 직접 전달할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-214">You cannot pass selectors for these elements to the `parse()` method directly because the surrounding form has already been parsed and won't update.</span></span> <span data-ttu-id="668dd-215">대신 먼저 기존 유효성 검사 데이터를 제거한 다음, 아래와 같이 전체 형식을 다시 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-215">Instead, you first remove the existing validation data, then reparse the entire form, as shown below:</span></span>

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

## <a name="iclientmodelvalidator"></a><span data-ttu-id="668dd-216">IClientModelValidator</span><span class="sxs-lookup"><span data-stu-id="668dd-216">IClientModelValidator</span></span>

<span data-ttu-id="668dd-217">사용자는 사용자 지정 특성에 대한 클라이언트 쪽 논리를 만들 수 있으며, [jquery 유효성 검사](http://jqueryvalidation.org/documentation/)에 어댑터를 만드는 [비간섭 유효성 검사](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)는 클라이언트에서 유효성 검사 중에 자동으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-217">You may create client side logic for your custom attribute, and [unobtrusive validation](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) which creates an adapter to [jquery validation](http://jqueryvalidation.org/documentation/) will execute it on the client for you automatically as part of validation.</span></span> <span data-ttu-id="668dd-218">첫 번째 단계는 다음과 같이 `IClientModelValidator` 인터페이스를 구현하여 추가할 데이터 특성을 제어하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-218">The first step is to control what data- attributes are added by implementing the `IClientModelValidator` interface as shown here:</span></span>

[!code-csharp[](validation/sample/ClassicMovieAttribute.cs?range=30-42)]

<span data-ttu-id="668dd-219">이 인터페이스를 구현하는 특성은 생성된 필드에 HTML 특성을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-219">Attributes that implement this interface can add HTML attributes to generated fields.</span></span> <span data-ttu-id="668dd-220">`ReleaseDate` 요소에 대한 출력을 검사하면 이전 예제와 비슷한 HTML을 표시합니다. 단지 이제는 `data-val-classicmovie` 특성이 `IClientModelValidator`라는 `AddValidation` 메서드에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-220">Examining the output for the `ReleaseDate` element reveals HTML that's similar to the previous example, except now there's a `data-val-classicmovie` attribute that was defined in the `AddValidation` method of `IClientModelValidator`.</span></span>

```html
<input class="form-control" type="datetime"
    data-val="true"
    data-val-classicmovie="Classic movies must have a release year earlier than 1960."
    data-val-classicmovie-year="1960"
    data-val-required="The ReleaseDate field is required."
    id="ReleaseDate" name="ReleaseDate" value="" />
```

<span data-ttu-id="668dd-221">비간섭 유효성 검사는 `data-` 특성에서 데이터를 사용하여 오류 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-221">Unobtrusive validation uses the data in the `data-` attributes to display error messages.</span></span> <span data-ttu-id="668dd-222">그러나 jQuery는 jQuery의 `validator` 개체에 추가될 때까지 규칙 또는 메시지를 인식하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-222">However, jQuery doesn't know about rules or messages until you add them to jQuery's `validator` object.</span></span> <span data-ttu-id="668dd-223">아래 예제에서 jQuery `validator` 개체에 대한 사용자 지정 클라이언트 유효성 검사 코드가 포함된 `classicmovie`라는 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-223">This is shown in the example below that adds a method named `classicmovie` containing custom client validation code to the jQuery `validator` object.</span></span> <span data-ttu-id="668dd-224">unobtrusive.adapters.add 메서드에 대한 설명은 [여기](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-224">An explanations of the unobtrusive.adapters.add method can be found [here](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)</span></span>

[!code-javascript[](validation/sample/Views/Movies/Create.cshtml?range=71-93)]

<span data-ttu-id="668dd-225">이제 jQuery에는 유효성 검사 코드가 false를 반환하는 경우 표시할 오류 메시지뿐만 아니라 사용자 지정 JavaScript 유효성 검사를 실행하는 정보도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-225">Now jQuery has the information to execute the custom JavaScript validation as well as the error message to display if that validation code returns false.</span></span>

## <a name="remote-validation"></a><span data-ttu-id="668dd-226">원격 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="668dd-226">Remote validation</span></span>

<span data-ttu-id="668dd-227">원격 유효성 검사는 서버의 데이터에 대한 클라이언트의 데이터 유효성을 검사해야 할 경우에 사용할 수 있는 유용한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-227">Remote validation is a great feature to use when you need to validate data on the client against data on the server.</span></span> <span data-ttu-id="668dd-228">예를 들어 앱은 이메일 또는 사용자 이름을 이미 사용 중인지 확인해야 하고, 이를 위해 많은 양의 데이터를 쿼리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-228">For example, your app may need to verify whether an email or user name is already in use, and it must query a large amount of data to do so.</span></span> <span data-ttu-id="668dd-229">하나 이상의 필드에 대한 유효성을 검사하는 대규모 데이터 집합을 다운로드하면 너무 많은 리소스를 소비하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-229">Downloading large sets of data for validating one or a few fields consumes too many resources.</span></span> <span data-ttu-id="668dd-230">또한 중요한 정보를 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-230">It may also expose sensitive information.</span></span> <span data-ttu-id="668dd-231">대안은 필드의 유효성을 검사하는 왕복 요청을 수행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-231">An alternative is to make a round-trip request to validate a field.</span></span>

<span data-ttu-id="668dd-232">2단계 프로세스에서 원격 유효성 검사를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-232">You can implement remote validation in a two step process.</span></span> <span data-ttu-id="668dd-233">먼저 `[Remote]` 특성을 사용하여 모델을 주석으로 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-233">First, you must annotate your model with the `[Remote]` attribute.</span></span> <span data-ttu-id="668dd-234">`[Remote]` 특성은 클라이언트 쪽 JavaScript를 적절한 코드를 호출하는 데 사용할 수 있는 여러 오버로드를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-234">The `[Remote]` attribute accepts multiple overloads you can use to direct client side JavaScript to the appropriate code to call.</span></span> <span data-ttu-id="668dd-235">다음 예제에서는 `Users` 컨트롤러의 `VerifyEmail` 작업 메서드를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-235">The example below points to the `VerifyEmail` action method of the `Users` controller.</span></span>

[!code-csharp[](validation/sample/User.cs?range=7-8)]

<span data-ttu-id="668dd-236">두 번째 단계는 `[Remote]` 특성에 정의된 대로 해당 작업 메서드에서 유효성 검사 코드를 지정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-236">The second step is putting the validation code in the corresponding action method as defined in the `[Remote]` attribute.</span></span> <span data-ttu-id="668dd-237">jQuery 유효성 검사 [`remote()`](https://jqueryvalidation.org/remote-method/) 메서드 설명서에 따라:</span><span class="sxs-lookup"><span data-stu-id="668dd-237">According to the jQuery Validate [`remote()`](https://jqueryvalidation.org/remote-method/) method documentation:</span></span>

> <span data-ttu-id="668dd-238">서버 쪽 응답은 기본 오류 메시지를 사용하며 유효한 요소에 대해 `"true"`인 JSON 문자열이며 잘못된 요소에 대해 `"false"`, `undefined` 또는 `null`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-238">The serverside response must be a JSON string that must be `"true"` for valid elements, and can be `"false"`, `undefined`, or `null` for invalid elements, using the default error message.</span></span> <span data-ttu-id="668dd-239">서버 쪽 응답이 문자열인 경우(예:</span><span class="sxs-lookup"><span data-stu-id="668dd-239">If the serverside response is a string, eg.</span></span> <span data-ttu-id="668dd-240">`"That name is already taken, try peter123 instead"`) 이 문자열은 기본값 대신 사용자 지정 오류 메시지로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-240">`"That name is already taken, try peter123 instead"`, this string will be displayed as a custom error message in place of the default.</span></span>

<span data-ttu-id="668dd-241">`VerifyEmail()` 메서드의 정의는 아래 표시된 대로 이러한 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-241">The definition of the `VerifyEmail()` method follows these rules, as shown below.</span></span> <span data-ttu-id="668dd-242">이메일을 사용한 경우 유효성 검사 오류 메시지가 반환됩니다. 또는 이메일이 무료인 경우 `true`이며 `JsonResult` 개체에서 결과를 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-242">It returns a validation error message if the email is taken, or `true` if the email is free, and wraps the result in a `JsonResult` object.</span></span> <span data-ttu-id="668dd-243">클라이언트 쪽은 반환 값을 계속 사용하거나 필요한 경우 오류를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-243">The client side can then use the returned value to proceed or display the error if needed.</span></span>

[!code-csharp[](validation/sample/UsersController.cs?range=19-28)]

<span data-ttu-id="668dd-244">이제 사용자가 이메일을 입력하면 보기의 JavaScript에서는 해당 이메일을 사용하는지 확인하기 위해 원격 호출을 수행하고, 해당하는 경우 오류 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-244">Now when users enter an email, JavaScript in the view makes a remote call to see if that email has been taken and, if so, displays the error message.</span></span> <span data-ttu-id="668dd-245">그렇지 않으면 사용자는 일반적으로 형식을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-245">Otherwise, the user can submit the form as usual.</span></span>

<span data-ttu-id="668dd-246">`[Remote]` 특성의 `AdditionalFields` 속성은 서버에서 데이터에 대한 필드 조합의 유효성을 검사하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-246">The `AdditionalFields` property of the `[Remote]` attribute is useful for validating combinations of fields against data on the server.</span></span> <span data-ttu-id="668dd-247">예를 들어 위의 `User` 모델에 `FirstName` 및 `LastName`라는 두 개의 추가 속성이 있는 경우 기존 사용자가 해당 쌍의 이름을 사용하지 않는지 확인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-247">For example, if the `User` model from above had two additional properties called `FirstName` and `LastName`, you might want to verify that no existing users already have that pair of names.</span></span> <span data-ttu-id="668dd-248">다음 코드와 같이 새로운 속성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-248">You define the new properties as shown in the following code:</span></span>

[!code-csharp[](validation/sample/User.cs?range=10-13)]

<span data-ttu-id="668dd-249">`AdditionalFields`는 명시적으로 `"FirstName"` 및 `"LastName"` 문자열로 설정될 수 있지만 다음과 같은 [`nameof`](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/nameof) 연산자를 사용하면 나중에 리팩터링을 간소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-249">`AdditionalFields` could've been set explicitly to the strings `"FirstName"` and `"LastName"`, but using the [`nameof`](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/nameof) operator like this simplifies later refactoring.</span></span> <span data-ttu-id="668dd-250">유효성 검사를 수행하는 작업 메서드는 `FirstName` 값 및 `LastName` 값에 대해 하나씩 두 개의 인수를 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-250">The action method to perform the validation must then accept two arguments, one for the value of `FirstName` and one for the value of `LastName`.</span></span>

[!code-csharp[](validation/sample/UsersController.cs?range=30-39)]

<span data-ttu-id="668dd-251">이제 사용자가 이름과 성을 입력할 때 JavaScript:</span><span class="sxs-lookup"><span data-stu-id="668dd-251">Now when users enter a first and last name, JavaScript:</span></span>

* <span data-ttu-id="668dd-252">해당 쌍의 이름을 사용 중인지 확인하기 위해 원격 호출을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-252">Makes a remote call to see if that pair of names has been taken.</span></span>
* <span data-ttu-id="668dd-253">쌍이 사용 중인 경우 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-253">If the pair has been taken, an error message is displayed.</span></span> 
* <span data-ttu-id="668dd-254">그렇지 않은 경우 사용자는 형식을 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-254">If not taken, the user can submit the form.</span></span>

<span data-ttu-id="668dd-255">`[Remote]` 특성을 포함하는 두 개 이상의 추가 필드 유효성을 검사해야 하는 경우 쉼표로 구분된 목록으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-255">If you need to validate two or more additional fields with the `[Remote]` attribute, you provide them as a comma-delimited list.</span></span> <span data-ttu-id="668dd-256">예를 들어 `MiddleName` 특성을 메서드에 추가하고, 다음 코드에 표시된 대로 `[Remote]` 특성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-256">For example, to add a `MiddleName` property to the model, set the `[Remote]` attribute as shown in the following code:</span></span>

```cs
[Remote(action: "VerifyName", controller: "Users", AdditionalFields = nameof(FirstName) + "," + nameof(LastName))]
public string MiddleName { get; set; }
```

<span data-ttu-id="668dd-257">모든 특성 인수와 같은 `AdditionalFields`은 상수 식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-257">`AdditionalFields`, like all attribute arguments, must be a constant expression.</span></span> <span data-ttu-id="668dd-258">따라서 [보간된 문자열](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/interpolated-strings)을 사용하거나 [`string.Join()`](https://msdn.microsoft.com/library/system.string.join(v=vs.110).aspx)를 호출하여 `AdditionalFields`을 초기화하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-258">Therefore, you must not use an [interpolated string](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/interpolated-strings) or call [`string.Join()`](https://msdn.microsoft.com/library/system.string.join(v=vs.110).aspx) to initialize `AdditionalFields`.</span></span> <span data-ttu-id="668dd-259">`[Remote]` 특성에 추가한 모든 추가 필드의 경우 해당하는 컨트롤러 작업 메서드에 다른 인수를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="668dd-259">For every additional field that you add to the `[Remote]` attribute, you must add another argument to the corresponding controller action method.</span></span>
