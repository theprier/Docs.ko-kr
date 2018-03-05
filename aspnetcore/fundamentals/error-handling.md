---
title: "ASP.NET Core의 오류 처리"
author: ardalis
description: "ASP.NET Core 응용 프로그램에서 오류를 처리하는 방법을 알아봅니다."
manager: wpickett
ms.author: tdykstra
ms.custom: H1Hack27Feb2017
ms.date: 11/30/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: fundamentals/error-handling
ms.openlocfilehash: 5b0cda7b79b8a9523d1ba6a9b321d22d3ccc753a
ms.sourcegitcommit: 18d1dc86770f2e272d93c7e1cddfc095c5995d9e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="introduction-to-error-handling-in-aspnet-core"></a><span data-ttu-id="65a32-103">ASP.NET Core에서 오류 처리 소개</span><span class="sxs-lookup"><span data-stu-id="65a32-103">Introduction to Error Handling in ASP.NET Core</span></span>

<span data-ttu-id="65a32-104">작성자: [Steve Smith](https://ardalis.com/) 및 [Tom Dykstra](https://github.com/tdykstra/)</span><span class="sxs-lookup"><span data-stu-id="65a32-104">By [Steve Smith](https://ardalis.com/) and [Tom Dykstra](https://github.com/tdykstra/)</span></span>

<span data-ttu-id="65a32-105">이 문서에서는 ASP.NET Core 앱에서 오류를 처리하기 위한 일반적인 접근법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-105">This article covers common appoaches to handling errors in ASP.NET Core apps.</span></span>

<span data-ttu-id="65a32-106">[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="65a32-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/sample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="the-developer-exception-page"></a><span data-ttu-id="65a32-107">개발자 예외 페이지</span><span class="sxs-lookup"><span data-stu-id="65a32-107">The developer exception page</span></span>

<span data-ttu-id="65a32-108">예외에 대한 자세한 정보가 있는 페이지를 표시하도록 응용 프로그램을 구성하려면 `Microsoft.AspNetCore.Diagnostics` NuGet 패키지를 설치하고 줄을 [시작 클래스에서 메서드를 구성](startup.md)에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-108">To configure an app to display a page that shows detailed information about exceptions, install the `Microsoft.AspNetCore.Diagnostics` NuGet package and add a line to the [Configure method in the Startup class](startup.md):</span></span>

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_DevExceptionPage&highlight=7)]

<span data-ttu-id="65a32-109">`app.UseMvc`와 같은 예외를 catch하려는 모든 미들웨어 앞에 `UseDeveloperExceptionPage`를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-109">Put `UseDeveloperExceptionPage` before any middleware you want to catch exceptions in, such as `app.UseMvc`.</span></span>

>[!WARNING]
> <span data-ttu-id="65a32-110">**앱이 개발 환경에서 실행 중인 경우에만** 개발자 예외 페이지를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-110">Enable the developer exception page **only when the app is running in the Development environment**.</span></span> <span data-ttu-id="65a32-111">프로덕션 환경에서 앱을 실행할 때 자세한 예외 정보를 공개적으로 공유하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-111">You don't want to share detailed exception information publicly when the app runs in production.</span></span> <span data-ttu-id="65a32-112">[구성 환경에 대해 자세히 알아보세요](environments.md).</span><span class="sxs-lookup"><span data-stu-id="65a32-112">[Learn more about configuring environments](environments.md).</span></span>

<span data-ttu-id="65a32-113">개발자 예외 페이지를 보려면 샘플 응용 프로그램을 `Development`로 설정된 환경으로 실행하고, `?throw=true`를 앱의 기본 URL에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-113">To see the developer exception page, run the sample application with the environment set to `Development`, and add `?throw=true` to the base URL of the app.</span></span> <span data-ttu-id="65a32-114">페이지에는 예외 및 요청에 대한 정보가 있는 여러 탭이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-114">The page includes several tabs with information about the exception and the request.</span></span> <span data-ttu-id="65a32-115">첫 번째 탭에는 스택 추적이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-115">The first tab includes a stack trace.</span></span> 

![스택 추적](error-handling/_static/developer-exception-page.png)

<span data-ttu-id="65a32-117">쿼리 문자열 매개 변수가 있는 경우 다음 탭에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-117">The next tab shows the query string parameters, if any.</span></span>

![쿼리 문자열 매개 변수](error-handling/_static/developer-exception-page-query.png)

<span data-ttu-id="65a32-119">이 요청에는 쿠키가 없지만, 만약 있는 경우 **쿠키** 탭에 표시됩니다. 마지막 탭에서 전달된 헤더를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-119">This request didn't have any cookies, but if it did, they would appear on the **Cookies** tab. You can see the headers that were passed in the last tab.</span></span>

![헤더](error-handling/_static/developer-exception-page-headers.png)

## <a name="configuring-a-custom-exception-handling-page"></a><span data-ttu-id="65a32-121">사용자 지정 예외 처리 페이지 구성</span><span class="sxs-lookup"><span data-stu-id="65a32-121">Configuring a custom exception handling page</span></span>

<span data-ttu-id="65a32-122">앱이 `Development` 환경에서 실행되고 있지 않는 경우 사용할 예외 처리기 페이지를 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-122">It's a good idea to configure an exception handler page to use when the app isn't running in the `Development` environment.</span></span>

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_DevExceptionPage&highlight=11)]

<span data-ttu-id="65a32-123">MVC 앱에서는 `HttpGet`과 같은 HTTP 메서드 특성을 사용하여 오류 처리기 작업 메서드를 명시적으로 데코레이트하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="65a32-123">In an MVC app, don't explicitly decorate the error handler action method with HTTP method attributes, such as `HttpGet`.</span></span> <span data-ttu-id="65a32-124">명시적 동사를 사용하면 일부 요청이 메서드에 도달하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-124">Using explicit verbs could prevent some requests from reaching the method.</span></span>

```csharp
[Route("/Error")]
public IActionResult Index()
{
    // Handle error here
}
```

## <a name="configuring-status-code-pages"></a><span data-ttu-id="65a32-125">상태 코드 페이지 구성</span><span class="sxs-lookup"><span data-stu-id="65a32-125">Configuring status code pages</span></span>

<span data-ttu-id="65a32-126">기본적으로 앱은 500(내부 서버 오류) 또는 404(찾을 수 없음)와 같은 HTTP 상태 코드에 대한 다양한 상태 코드 페이지를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-126">By default, your app won't provide a rich status code page for HTTP status codes such as 500 (Internal Server Error) or 404 (Not Found).</span></span> <span data-ttu-id="65a32-127">`Configure` 메서드에 줄을 추가하여 `StatusCodePagesMiddleware`를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-127">You can configure the `StatusCodePagesMiddleware` by adding a line to the `Configure` method:</span></span>

```csharp
app.UseStatusCodePages();
```

<span data-ttu-id="65a32-128">기본적으로 이 미들웨어는 404와 같이 일반적인 상태 코드에 대한 간단한 텍스트 전용 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-128">By default, this middleware adds simple, text-only handlers for common status codes, such as 404:</span></span>

![404 페이지](error-handling/_static/default-404-status-code.png)

<span data-ttu-id="65a32-130">미들웨어는 몇 가지 다양한 확장 메서드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-130">The middleware supports several different extension methods.</span></span> <span data-ttu-id="65a32-131">람다 식에서 사용하기도 하고, 콘텐츠 형식 및 형식 문자열을 사용하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-131">One takes a lambda expression, another takes a content type and format string.</span></span>

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_StatusCodePages)]

```csharp
app.UseStatusCodePages("text/plain", "Status code page, status code: {0}");
```

<span data-ttu-id="65a32-132">리디렉션 확장 메서드도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-132">There are also redirect extension methods.</span></span> <span data-ttu-id="65a32-133">302 상태 코드를 클라이언트에 보내기도 하고, 클라이언트에 원래 상태 코드를 반환하면서 리디렉션 URL에 대한 처리기를 실행하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-133">One sends a 302 status code to the client, and one returns the original status code to the client but also executes the handler for the redirect URL.</span></span>

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_StatusCodePagesWithRedirect)]

```csharp
app.UseStatusCodePagesWithReExecute("/error/{0}");
```

<span data-ttu-id="65a32-134">특정 요청에 대한 상태 코드 페이지를 사용하지 않도록 설정해야 하는 경우 그렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-134">If you need to disable status code pages for certain requests, you can do so:</span></span>

```csharp
var statusCodePagesFeature = context.Features.Get<IStatusCodePagesFeature>();
if (statusCodePagesFeature != null)
{
  statusCodePagesFeature.Enabled = false;
}
```

## <a name="exception-handling-code"></a><span data-ttu-id="65a32-135">예외 처리 코드</span><span class="sxs-lookup"><span data-stu-id="65a32-135">Exception-handling code</span></span>

<span data-ttu-id="65a32-136">예외 처리 페이지의 코드는 예외를 throw할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-136">Code in exception handling pages can throw exceptions.</span></span> <span data-ttu-id="65a32-137">종종 프로덕션 오류 페이지에 대해 완전한 정적 콘텐츠를 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-137">It's often a good idea for production error pages to consist of purely static content.</span></span>

<span data-ttu-id="65a32-138">또한 일단 응답에 대한 헤더를 보내고 나면 응답의 상태 코드, 예외 페이지 또는 처리기 실행을 변경할 수 없다는 점에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="65a32-138">Also, be aware that once the headers for a response have been sent, you can't change the response's status code, nor can any exception pages or handlers run.</span></span> <span data-ttu-id="65a32-139">응답을 완료하거나 연결이 중단되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-139">The response must be completed or the connection aborted.</span></span>

## <a name="server-exception-handling"></a><span data-ttu-id="65a32-140">서버 예외 처리</span><span class="sxs-lookup"><span data-stu-id="65a32-140">Server exception handling</span></span>

<span data-ttu-id="65a32-141">앱에서 논리를 처리하는 예외뿐 아니라 앱을 호스팅하는 [서버](servers/index.md)는 몇 가지 예외 처리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-141">In addition to the exception handling logic in your app, the [server](servers/index.md) hosting your app performs some exception handling.</span></span> <span data-ttu-id="65a32-142">헤더를 보내기 전에 서버가 예외를 catch하는 경우 서버는 본문이 없는 500 내부 서버 오류 응답을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-142">If the server catches an exception before the headers are sent, the server sends a 500 Internal Server Error response with no body.</span></span> <span data-ttu-id="65a32-143">헤더를 보낸 후에 서버가 예외를 catch하는 경우 서버는 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-143">If the server catches an exception after the headers have been sent, the server closes the connection.</span></span> <span data-ttu-id="65a32-144">앱으로 처리되지 않는 요청은 서버에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-144">Requests that aren't handled by your app are handled by the server.</span></span> <span data-ttu-id="65a32-145">발생하는 모든 예외는 서버의 예외 처리에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-145">Any exception that occurs is handled by the server's exception handling.</span></span> <span data-ttu-id="65a32-146">구성된 모든 사용자 지정 오류 페이지 또는 예외 처리 미들웨어 또는 필터는 이 동작에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-146">Any configured custom error pages or exception handling middleware or filters don't affect this behavior.</span></span>

## <a name="startup-exception-handling"></a><span data-ttu-id="65a32-147">시작 예외 처리</span><span class="sxs-lookup"><span data-stu-id="65a32-147">Startup exception handling</span></span>

<span data-ttu-id="65a32-148">호스팅 계층만 앱 시작 시 발생하는 예외를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-148">Only the hosting layer can handle exceptions that take place during app startup.</span></span> <span data-ttu-id="65a32-149">`captureStartupErrors` 및 `detailedErrors` 키를 사용하여 [시작 시 오류에 대해 응답의 호스트가 동작하는 방법을 구성](hosting.md#detailed-errors)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-149">You can [configure how the host behaves in response to errors during startup](hosting.md#detailed-errors) using `captureStartupErrors` and the `detailedErrors` key.</span></span>

<span data-ttu-id="65a32-150">호스팅은 호스트 주소/포트 바인딩 후에 오류가 발생하는 경우 캡처된 시작 오류에 대한 오류 페이지만 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-150">Hosting can only show an error page for a captured startup error if the error occurs after host address/port binding.</span></span> <span data-ttu-id="65a32-151">어떤 이유로 바인딩이 실패한 경우 호스팅 계층은 중요한 예외를 로그하고, dotnet 프로세스가 충돌하며, 오류 페이지가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-151">If any binding fails for any reason, the hosting layer logs a critical exception, the dotnet process crashes, and no error page is displayed.</span></span>

## <a name="aspnet-mvc-error-handling"></a><span data-ttu-id="65a32-152">ASP.NET MVC 오류 처리</span><span class="sxs-lookup"><span data-stu-id="65a32-152">ASP.NET MVC error handling</span></span>

<span data-ttu-id="65a32-153">[MVC](xref:mvc/overview) 앱에는 예외 필터 구성 및 모델 유효성 검사 수행과 같이 오류를 처리하기 위한 몇 가지 추가 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-153">[MVC](xref:mvc/overview) apps have some additional options for handling errors, such as configuring exception filters and performing model validation.</span></span>

### <a name="exception-filters"></a><span data-ttu-id="65a32-154">예외 필터</span><span class="sxs-lookup"><span data-stu-id="65a32-154">Exception Filters</span></span>

<span data-ttu-id="65a32-155">전역으로 또는 MVC 앱에서 컨트롤러당 또는 작업당 기준으로 예외 필터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-155">Exception filters can be configured globally or on a per-controller or per-action basis in an MVC app.</span></span> <span data-ttu-id="65a32-156">이러한 필터는 컨트롤러 작업 또는 다른 필터를 실행하는 동안 발생하는 처리되지 않은 예외를 처리하며, 그 외에는 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-156">These filters handle any unhandled exception that occurs during the execution of a controller action or another filter, and are not called otherwise.</span></span> <span data-ttu-id="65a32-157">[필터](../mvc/controllers/filters.md)에서 예외 필터에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="65a32-157">Learn more about exception filters in [Filters](../mvc/controllers/filters.md).</span></span>

>[!TIP]
> <span data-ttu-id="65a32-158">예외 필터는 MVC 작업 내에서 발생하는 예외를 트래핑하는 데 유용하지만 오류 처리 미들웨어만큼 유연하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-158">Exception filters are good for trapping exceptions that occur within MVC actions, but they're not as flexible as error handling middleware.</span></span> <span data-ttu-id="65a32-159">일반적인 경우에는 미들웨어를 선호하고, 선택한 MVC 작업에 따라 오류 처리를 *다르게* 수행해야 하는 경우에만 필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-159">Prefer middleware for the general case, and use filters only where you need to do error handling *differently* based on which MVC action was chosen.</span></span>

### <a name="handling-model-state-errors"></a><span data-ttu-id="65a32-160">처리 모델 상태 오류</span><span class="sxs-lookup"><span data-stu-id="65a32-160">Handling Model State Errors</span></span>

<span data-ttu-id="65a32-161">[모델 유효성 검사](../mvc/models/validation.md)는 각 컨트롤러 작업을 호출하기 전에 발생하며, `ModelState.IsValid`를 검사하고 적절하게 반응하는 것은 작업 메서드의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-161">[Model validation](../mvc/models/validation.md) occurs prior to invoking each controller action, and it's the action method's responsibility to inspect `ModelState.IsValid` and react appropriately.</span></span>

<span data-ttu-id="65a32-162">[필터](../mvc/controllers/filters.md)가 그러한 정책을 구현하기에 적절한 경우에 일부 앱은 모델 유효성 검사 오류를 처리하는 데 표준 규칙을 따르도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-162">Some apps will choose to follow a standard convention for dealing with model validation errors, in which case a [filter](../mvc/controllers/filters.md) may be an appropriate place to implement such a policy.</span></span> <span data-ttu-id="65a32-163">잘못된 모델 상태일 때 작업 동작 방식을 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65a32-163">You should test how your actions behave with invalid model states.</span></span> <span data-ttu-id="65a32-164">[컨트롤러 논리 테스트](../mvc/controllers/testing.md)에서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="65a32-164">Learn more in [Testing controller logic](../mvc/controllers/testing.md).</span></span>



