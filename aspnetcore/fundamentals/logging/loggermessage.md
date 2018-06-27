---
title: ASP.NET Core에서 LoggerMessage를 사용한 고성능 로깅
author: guardrex
description: LoggerMessage를 사용하여 고성능 로깅 시나리오에 적은 개체 할당을 필요로 하는 캐시 가능한 대리자를 만드는 방법을 알아봅니다.
ms.author: riande
ms.date: 11/03/2017
uid: fundamentals/logging/loggermessage
ms.openlocfilehash: e952591bac29868d87d765820e88c74b50a1fe88
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36272437"
---
# <a name="high-performance-logging-with-loggermessage-in-aspnet-core"></a><span data-ttu-id="b3d50-103">ASP.NET Core에서 LoggerMessage를 사용한 고성능 로깅</span><span class="sxs-lookup"><span data-stu-id="b3d50-103">High-performance logging with LoggerMessage in ASP.NET Core</span></span>

<span data-ttu-id="b3d50-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="b3d50-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="b3d50-105">[LoggerMessage](/dotnet/api/microsoft.extensions.logging.loggermessage) 기능은 `LogInformation`, `LogDebug` 및 `LogError`와 같은 [로거 확장 메서드](/dotnet/api/Microsoft.Extensions.Logging.LoggerExtensions)에 비해 적은 개체 할당 및 감소된 계산 오버헤드를 필요로 하는 캐시 가능한 대리자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-105">[LoggerMessage](/dotnet/api/microsoft.extensions.logging.loggermessage) features create cacheable delegates that require fewer object allocations and reduced computational overhead compared to [logger extension methods](/dotnet/api/Microsoft.Extensions.Logging.LoggerExtensions), such as `LogInformation`, `LogDebug`, and `LogError`.</span></span> <span data-ttu-id="b3d50-106">고성능 로깅 시나리오의 경우 `LoggerMessage` 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-106">For high-performance logging scenarios, use the `LoggerMessage` pattern.</span></span>

<span data-ttu-id="b3d50-107">`LoggerMessage`는 로거 확장 메서드에 비해 다음과 같은 성능 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-107">`LoggerMessage` provides the following performance advantages over Logger extension methods:</span></span>

* <span data-ttu-id="b3d50-108">로거 확장 메서드는 `object`에 대한 `int`와 같은 "boxing"(변환) 값 형식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-108">Logger extension methods require "boxing" (converting) value types, such as `int`, into `object`.</span></span> <span data-ttu-id="b3d50-109">`LoggerMessage` 패턴은 정적 `Action` 필드 및 강력한 형식의 매개 변수가 있는 확장 메서드를 사용하여 boxing을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-109">The `LoggerMessage` pattern avoids boxing by using static `Action` fields and extension methods with strongly-typed parameters.</span></span>
* <span data-ttu-id="b3d50-110">로거 확장 메서드는 로그 메시지가 기록될 때마다 메시지 템플릿(명명된 형식 문자열)을 구문 분석해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-110">Logger extension methods must parse the message template (named format string) every time a log message is written.</span></span> <span data-ttu-id="b3d50-111">`LoggerMessage`는 메시지가 정의될 때 템플릿 구문 분석이 한번만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-111">`LoggerMessage` only requires parsing a template once when the message is defined.</span></span>

<span data-ttu-id="b3d50-112">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="b3d50-112">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/sample/) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

<span data-ttu-id="b3d50-113">샘플 앱은 기본 견적 추적 시스템으로 `LoggerMessage` 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-113">The sample app demonstrates `LoggerMessage` features with a basic quote tracking system.</span></span> <span data-ttu-id="b3d50-114">앱은 메모리 내 데이터베이스를 사용하여 견적을 추가하고 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-114">The app adds and deletes quotes using an in-memory database.</span></span> <span data-ttu-id="b3d50-115">이러한 작업이 발생하는 대로 로그 메시지는 `LoggerMessage` 패턴을 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-115">As these operations occur, log messages are generated using the `LoggerMessage` pattern.</span></span>

## <a name="loggermessagedefine"></a><span data-ttu-id="b3d50-116">LoggerMessage.Define</span><span class="sxs-lookup"><span data-stu-id="b3d50-116">LoggerMessage.Define</span></span>

<span data-ttu-id="b3d50-117">[Define(LogLevel, EventId, String)](/dotnet/api/microsoft.extensions.logging.loggermessage.define)은 메시지 로깅을 위한 `Action` 대리자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-117">[Define(LogLevel, EventId, String)](/dotnet/api/microsoft.extensions.logging.loggermessage.define) creates an `Action` delegate for logging a message.</span></span> <span data-ttu-id="b3d50-118">`Define` 오버로드는 명명된 형식 문자열(템플릿)로 최대 6개의 형식 매개 변수 전달을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-118">`Define` overloads permit passing up to six type parameters to a named format string (template).</span></span>

<span data-ttu-id="b3d50-119">`Define` 메서드에 제공된 문자열은 템플릿이며 보간된 문자열이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-119">The string provided to the `Define` method is a template and not an interpolated string.</span></span> <span data-ttu-id="b3d50-120">자리 표시자는 형식이 지정된 순서로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-120">Placeholders are filled in the order that the types are specified.</span></span> <span data-ttu-id="b3d50-121">템플릿의 자리 표시자 이름은 템플릿에서 알기 쉽고 일관되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-121">Placeholder names in the template should be descriptive and consistent across templates.</span></span> <span data-ttu-id="b3d50-122">구조적 로그 데이터 내에서 속성 이름으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-122">They serve as property names within structured log data.</span></span> <span data-ttu-id="b3d50-123">자리 표시자 이름으로 [파스칼식 대/소문자](/dotnet/standard/design-guidelines/capitalization-conventions)를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-123">We recommend [Pascal casing](/dotnet/standard/design-guidelines/capitalization-conventions) for placeholder names.</span></span> <span data-ttu-id="b3d50-124">예: `{Count}`, `{FirstName}`</span><span class="sxs-lookup"><span data-stu-id="b3d50-124">For example, `{Count}`, `{FirstName}`.</span></span>

<span data-ttu-id="b3d50-125">각 로그 메시지는 `LoggerMessage.Define`에서 만들어진 정적 필드에 보관된 `Action`입니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-125">Each log message is an `Action` held in a static field created by `LoggerMessage.Define`.</span></span> <span data-ttu-id="b3d50-126">예를 들어 샘플 앱은 인덱스 페이지의 GET 요청에 대한 로그 메시지를 설명하는 필드를 만듭니다(*Internal/LoggerExtensions.cs*).</span><span class="sxs-lookup"><span data-stu-id="b3d50-126">For example, the sample app creates a field to describe a log message for a GET request for the Index page (*Internal/LoggerExtensions.cs*):</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet1)]

<span data-ttu-id="b3d50-127">`Action`의 경우 다음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-127">For the `Action`, specify:</span></span>

* <span data-ttu-id="b3d50-128">로그 수준</span><span class="sxs-lookup"><span data-stu-id="b3d50-128">The log level.</span></span>
* <span data-ttu-id="b3d50-129">정적 확장 메서드의 이름이 있는 고유한 이벤트 식별자([EventId](/dotnet/api/microsoft.extensions.logging.eventid))</span><span class="sxs-lookup"><span data-stu-id="b3d50-129">A unique event identifier ([EventId](/dotnet/api/microsoft.extensions.logging.eventid)) with the name of the static extension method.</span></span>
* <span data-ttu-id="b3d50-130">메시지 템플릿(명명된 형식 문자열)</span><span class="sxs-lookup"><span data-stu-id="b3d50-130">The message template (named format string).</span></span> 

<span data-ttu-id="b3d50-131">샘플 앱의 인덱스 페이지에 대한 요청은 다음을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-131">A request for the Index page of the sample app sets the:</span></span>

* <span data-ttu-id="b3d50-132">로그 수준을 `Information`으로</span><span class="sxs-lookup"><span data-stu-id="b3d50-132">Log level to `Information`.</span></span>
* <span data-ttu-id="b3d50-133">이벤트 ID를 `IndexPageRequested` 메서드의 이름이 있는 `1`로</span><span class="sxs-lookup"><span data-stu-id="b3d50-133">Event id to `1` with the name of the `IndexPageRequested` method.</span></span>
* <span data-ttu-id="b3d50-134">메시지 템플릿(명명된 형식 문자열)을 문자열로</span><span class="sxs-lookup"><span data-stu-id="b3d50-134">Message template (named format string) to a string.</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet5)]

<span data-ttu-id="b3d50-135">구조적 로깅 저장소는 로깅을 보강하도록 이벤트 ID로 제공될 경우 이벤트 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-135">Structured logging stores may use the event name when it's supplied with the event id to enrich logging.</span></span> <span data-ttu-id="b3d50-136">예를 들어 [Serilog](https://github.com/serilog/serilog-extensions-logging)는 이벤트 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-136">For example, [Serilog](https://github.com/serilog/serilog-extensions-logging) uses the event name.</span></span>

<span data-ttu-id="b3d50-137">`Action`은 강력한 형식의 확장 메서드를 통해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-137">The `Action` is invoked through a strongly-typed extension method.</span></span> <span data-ttu-id="b3d50-138">`IndexPageRequested` 메서드는 샘플 앱에서 인덱스 페이지 GET 요청에 대한 메시지를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-138">The `IndexPageRequested` method logs a message for an Index page GET request in the sample app:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet9)]

<span data-ttu-id="b3d50-139">`IndexPageRequested`는 *Pages/Index.cshtml.cs*에서 `OnGetAsync` 메서드의 로거에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-139">`IndexPageRequested` is called on the logger in the `OnGetAsync` method in *Pages/Index.cshtml.cs*:</span></span>

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=3)]

<span data-ttu-id="b3d50-140">앱의 콘솔 출력을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-140">Inspect the app's console output:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[1]
      => RequestId:0HL90M6E7PHK4:00000001 RequestPath:/ => /Index
      GET request for Index page
```

<span data-ttu-id="b3d50-141">로그 메시지에 매개 변수를 전달하려면 정적 필드를 만들 때 최대 6개의 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-141">To pass parameters to a log message, define up to six types when creating the static field.</span></span> <span data-ttu-id="b3d50-142">샘플 앱은 `Action` 필드에 대한 `string` 형식을 정의하여 견적을 추가할 때 문자열을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-142">The sample app logs a string when adding a quote by defining a `string` type for the `Action` field:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet2)]

<span data-ttu-id="b3d50-143">대리자의 로그 메시지 템플릿은 제공되는 형식에서 해당 자리 표시자 값을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-143">The delegate's log message template receives its placeholder values from the types provided.</span></span> <span data-ttu-id="b3d50-144">샘플 앱은 견적 매개 변수가 `string`인 견적을 추가하기 위한 대리자를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-144">The sample app defines a delegate for adding a quote where the quote parameter is a `string`:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet6)]

<span data-ttu-id="b3d50-145">견적을 추가하기 위한 정적 확장 메서드, `QuoteAdded`는 견적 인수 값을 받고 `Action` 대리자에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-145">The static extension method for adding a quote, `QuoteAdded`, receives the quote argument value and passes it to the `Action` delegate:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet10)]

<span data-ttu-id="b3d50-146">인덱스 페이지의 페이지 모델(*Pages/Index.cshtml.cs*)에서 `QuoteAdded`는 메시지를 기록하기 위해 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-146">In the Index page's page model (*Pages/Index.cshtml.cs*), `QuoteAdded` is called to log the message:</span></span>

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet3&highlight=6)]

<span data-ttu-id="b3d50-147">앱의 콘솔 출력을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-147">Inspect the app's console output:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[2]
      => RequestId:0HL90M6E7PHK5:0000000A RequestPath:/ => /Index
      Quote added (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand')
```

<span data-ttu-id="b3d50-148">샘플 앱은 견적 삭제를 위한 `try`&ndash;`catch` 패턴을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-148">The sample app implements a `try`&ndash;`catch` pattern for quote deletion.</span></span> <span data-ttu-id="b3d50-149">성공적인 삭제 작업에 대한 정보 메시지가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-149">An informational message is logged for a successful delete operation.</span></span> <span data-ttu-id="b3d50-150">예외가 throw될 경우 삭제 작업에 대한 오류 메시지가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-150">An error message is logged for a delete operation when an exception is thrown.</span></span> <span data-ttu-id="b3d50-151">실패한 삭제 작업에 대한 로그 메시지는 예외 스택 추적(*Internal/LoggerExtensions.cs*)을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-151">The log message for the unsuccessful delete operation includes the exception stack trace (*Internal/LoggerExtensions.cs*):</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet3)]

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet7)]

<span data-ttu-id="b3d50-152">`QuoteDeleteFailed`에서 예외가 대리자에 전달되는 방식을 참고합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-152">Note how the exception is passed to the delegate in `QuoteDeleteFailed`:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet11)]

<span data-ttu-id="b3d50-153">인덱스 페이지에 대한 페이지 모델에서 성공적인 견적 삭제는 로거에서 `QuoteDeleted` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-153">In the page model for the Index page, a successful quote deletion calls the `QuoteDeleted` method on the logger.</span></span> <span data-ttu-id="b3d50-154">삭제에 대한 견적을 찾을 수 없는 경우 `ArgumentNullException`이 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-154">When a quote isn't found for deletion, an `ArgumentNullException` is thrown.</span></span> <span data-ttu-id="b3d50-155">예외는 `try`&ndash;`catch`문에 의해 트래핑되며 `catch` 블록에서 로거의 `QuoteDeleteFailed` 메서드를 호출하여 기록됩니다(*Pages/Index.cshtml.cs*).</span><span class="sxs-lookup"><span data-stu-id="b3d50-155">The exception is trapped by the `try`&ndash;`catch` statement and logged by calling the `QuoteDeleteFailed` method on the logger in the `catch` block (*Pages/Index.cshtml.cs*):</span></span>

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet5&highlight=14,18)]

<span data-ttu-id="b3d50-156">견적이 성공적으로 삭제되면 앱의 콘솔 출력을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-156">When a quote is successfully deleted, inspect the app's console output:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:00000016 RequestPath:/ => /Index
      Quote deleted (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand' Id = 1)
```

<span data-ttu-id="b3d50-157">견적 삭제가 실패하면 앱의 콘솔 출력을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-157">When quote deletion fails, inspect the app's console output.</span></span> <span data-ttu-id="b3d50-158">예외는 로그 메시지에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-158">Note that the exception is included in the log message:</span></span>

```console
fail: LoggerMessageSample.Pages.IndexModel[5]
      => RequestId:0HL90M6E7PHK5:00000010 RequestPath:/ => /Index
      Quote delete failed (Id = 999)
System.ArgumentNullException: Value cannot be null.
Parameter name: entity
   at Microsoft.EntityFrameworkCore.Utilities.Check.NotNull[T](T value, String parameterName)
   at Microsoft.EntityFrameworkCore.DbContext.Remove[TEntity](TEntity entity)
   at Microsoft.EntityFrameworkCore.Internal.InternalDbSet`1.Remove(TEntity entity)
   at LoggerMessageSample.Pages.IndexModel.<OnPostDeleteQuoteAsync>d__14.MoveNext() in 
      <PATH>\sample\Pages\Index.cshtml.cs:line 87
```

## <a name="loggermessagedefinescope"></a><span data-ttu-id="b3d50-159">LoggerMessage.DefineScope</span><span class="sxs-lookup"><span data-stu-id="b3d50-159">LoggerMessage.DefineScope</span></span>

<span data-ttu-id="b3d50-160">[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope)는 [로그 범위](xref:fundamentals/logging/index#log-scopes) 정의를 위한 `Func` 대리자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-160">[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) creates a `Func` delegate for defining a [log scope](xref:fundamentals/logging/index#log-scopes).</span></span> <span data-ttu-id="b3d50-161">`DefineScope` 오버로드는 명명된 형식 문자열(템플릿)로 최대 3개의 형식 매개 변수 전달을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-161">`DefineScope` overloads permit passing up to three type parameters to a named format string (template).</span></span>

<span data-ttu-id="b3d50-162">`Define` 메서드의 경우와 마찬가지로 `DefineScope` 메서드에 제공된 문자열은 템플릿이며 보간된 문자열이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-162">As is the case with the `Define` method, the string provided to the `DefineScope` method is a template and not an interpolated string.</span></span> <span data-ttu-id="b3d50-163">자리 표시자는 형식이 지정된 순서로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-163">Placeholders are filled in the order that the types are specified.</span></span> <span data-ttu-id="b3d50-164">템플릿의 자리 표시자 이름은 템플릿에서 알기 쉽고 일관되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-164">Placeholder names in the template should be descriptive and consistent across templates.</span></span> <span data-ttu-id="b3d50-165">구조적 로그 데이터 내에서 속성 이름으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-165">They serve as property names within structured log data.</span></span> <span data-ttu-id="b3d50-166">자리 표시자 이름으로 [파스칼식 대/소문자](/dotnet/standard/design-guidelines/capitalization-conventions)를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-166">We recommend [Pascal casing](/dotnet/standard/design-guidelines/capitalization-conventions) for placeholder names.</span></span> <span data-ttu-id="b3d50-167">예: `{Count}`, `{FirstName}`</span><span class="sxs-lookup"><span data-stu-id="b3d50-167">For example, `{Count}`, `{FirstName}`.</span></span>

<span data-ttu-id="b3d50-168">[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) 메서드를 사용하여 일련의 로그 메시지에 적용하도록 [로그 범위](xref:fundamentals/logging/index#log-scopes)를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-168">Define a [log scope](xref:fundamentals/logging/index#log-scopes) to apply to a series of log messages using the [DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) method.</span></span>

<span data-ttu-id="b3d50-169">샘플 앱에는 데이터베이스에서 모든 견적을 삭제하기 위한 **모두 지우기** 단추가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-169">The sample app has a **Clear All** button for deleting all of the quotes in the database.</span></span> <span data-ttu-id="b3d50-170">견적은 한 번에 하나를 제거하여 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-170">The quotes are deleted by removing them one at a time.</span></span> <span data-ttu-id="b3d50-171">견적이 삭제될 때마다 로거에서 `QuoteDeleted` 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-171">Each time a quote is deleted, the `QuoteDeleted` method is called on the logger.</span></span> <span data-ttu-id="b3d50-172">로그 범위가 이러한 로그 메시지에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-172">A log scope is added to these log messages.</span></span>

<span data-ttu-id="b3d50-173">*appsettings.json*의 콘솔 로거 섹션에서 `IncludeScopes`를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-173">Enable `IncludeScopes` in the console logger section of *appsettings.json*:</span></span>

[!code-csharp[](loggermessage/sample/appsettings.json?highlight=3-5)]

<span data-ttu-id="b3d50-174">로그 범위를 만들려면 범위에 대한 `Func` 대리자를 보유하는 필드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-174">To create a log scope, add a field to hold a `Func` delegate for the scope.</span></span> <span data-ttu-id="b3d50-175">샘플 앱은 `_allQuotesDeletedScope`라는 필드를 만듭니다(*Internal/LoggerExtensions.cs*).</span><span class="sxs-lookup"><span data-stu-id="b3d50-175">The sample app creates a field called `_allQuotesDeletedScope` (*Internal/LoggerExtensions.cs*):</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet4)]

<span data-ttu-id="b3d50-176">`DefineScope`를 사용하여 대리자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-176">Use `DefineScope` to create the delegate.</span></span> <span data-ttu-id="b3d50-177">대리자가 호출되는 경우 템플릿 인수로 사용하기 위해 최대 세 개의 형식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-177">Up to three types can be specified for use as template arguments when the delegate is invoked.</span></span> <span data-ttu-id="b3d50-178">샘플 앱은 삭제된 견적의 수를 포함하는 메시지 템플릿을 사용합니다(`int` 형식).</span><span class="sxs-lookup"><span data-stu-id="b3d50-178">The sample app uses a message template that includes the number of deleted quotes (an `int` type):</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet8)]

<span data-ttu-id="b3d50-179">로그 메시지에 대한 정적 확장 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-179">Provide a static extension method for the log message.</span></span> <span data-ttu-id="b3d50-180">메시지 템플릿에 표시되는 명명된 속성에 대한 모든 형식 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-180">Include any type parameters for named properties that appear in the message template.</span></span> <span data-ttu-id="b3d50-181">샘플 앱은 `_allQuotesDeletedScope`를 삭제하고 반환하는 데 `count`의 견적을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-181">The sample app takes in a `count` of quotes to delete and returns `_allQuotesDeletedScope`:</span></span>

[!code-csharp[](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet12)]

<span data-ttu-id="b3d50-182">범위는 `using` 블록에서 로깅 확장 호출을 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-182">The scope wraps the logging extension calls in a `using` block:</span></span>

[!code-csharp[](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet4&highlight=5-6,14)]

<span data-ttu-id="b3d50-183">앱의 콘솔 출력에서 로그 메시지를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-183">Inspect the log messages in the app's console output.</span></span> <span data-ttu-id="b3d50-184">다음 결과는 포함된 로그 범위 메시지와 함께 삭제된 세 가지 견적을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b3d50-184">The following result shows three quotes deleted with the log scope message included:</span></span>

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 1' Id = 2)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 2' Id = 3)
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:0000002E RequestPath:/ => /Index => All quotes deleted (Count = 3)
      Quote deleted (Quote = 'Quote 3' Id = 4)
```

## <a name="additional-resources"></a><span data-ttu-id="b3d50-185">추가 자료</span><span class="sxs-lookup"><span data-stu-id="b3d50-185">Additional resources</span></span>

* [<span data-ttu-id="b3d50-186">로깅</span><span class="sxs-lookup"><span data-stu-id="b3d50-186">Logging</span></span>](xref:fundamentals/logging/index)
