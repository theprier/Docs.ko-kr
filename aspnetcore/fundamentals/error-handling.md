---
title: ASP.NET Core에서 오류 처리
author: ardalis
description: ASP.NET Core 앱에서 오류를 처리하는 방법을 알아봅니다.
ms.author: tdykstra
ms.custom: mvc
ms.date: 07/05/2018
uid: fundamentals/error-handling
ms.openlocfilehash: 6aded9525a0abd31dec8441c7fba60d8845c7d93
ms.sourcegitcommit: 661d30492d5ef7bbca4f7e709f40d8f3309d2dac
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2018
ms.locfileid: "37938243"
---
# <a name="handle-errors-in-aspnet-core"></a><span data-ttu-id="b6cdb-103">ASP.NET Core에서 오류 처리</span><span class="sxs-lookup"><span data-stu-id="b6cdb-103">Handle errors in ASP.NET Core</span></span>

<span data-ttu-id="b6cdb-104">작성자: [Steve Smith](https://ardalis.com/) 및 [Tom Dykstra](https://github.com/tdykstra/)</span><span class="sxs-lookup"><span data-stu-id="b6cdb-104">By [Steve Smith](https://ardalis.com/) and [Tom Dykstra](https://github.com/tdykstra/)</span></span>

<span data-ttu-id="b6cdb-105">이 문서에서는 ASP.NET Core 앱에서 오류를 처리하기 위한 일반적인 접근법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-105">This article covers common approaches to handling errors in ASP.NET Core apps.</span></span>

<span data-ttu-id="b6cdb-106">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/samples/2.x/ErrorHandlingSample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="b6cdb-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/samples/2.x/ErrorHandlingSample) ([how to download](xref:tutorials/index#how-to-download-a-sample))</span></span>

## <a name="the-developer-exception-page"></a><span data-ttu-id="b6cdb-107">개발자 예외 페이지</span><span class="sxs-lookup"><span data-stu-id="b6cdb-107">The developer exception page</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="b6cdb-108">예외에 대한 자세한 정보를 표시하는 페이지를 표시하는 앱을 구성하려면 *개발자 예외 페이지*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-108">To configure an app to display a page that shows detailed information about exceptions, use the *developer exception page*.</span></span> <span data-ttu-id="b6cdb-109">[Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 패키지가 사용할 수 있게 된 페이지는 [Microsoft.AspNetCore.App 메타 패키지](xref:fundamentals/metapackage-app)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-109">The page made available by the [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) package, which is available in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="b6cdb-110">`Startup.Configure` 메서드에 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-110">Add a line to the `Startup.Configure` method:</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="b6cdb-111">예외에 대한 자세한 정보를 표시하는 페이지를 표시하는 앱을 구성하려면 *개발자 예외 페이지*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-111">To configure an app to display a page that shows detailed information about exceptions, use the *developer exception page*.</span></span> <span data-ttu-id="b6cdb-112">[Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 패키지가 사용할 수 있게 된 페이지는 [Microsoft.AspNetCore.All 메타 패키지](xref:fundamentals/metapackage)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-112">The page is made available by the [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) package, which is available in the [Microsoft.AspNetCore.All metapackage](xref:fundamentals/metapackage).</span></span> <span data-ttu-id="b6cdb-113">`Startup.Configure` 메서드에 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-113">Add a line to the `Startup.Configure` method:</span></span>

::: moniker-end

::: moniker range="< aspnetcore-2.0"

<span data-ttu-id="b6cdb-114">예외에 대한 자세한 정보를 표시하는 페이지를 표시하는 앱을 구성하려면 *개발자 예외 페이지*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-114">To configure an app to display a page that shows detailed information about exceptions, use the *developer exception page*.</span></span> <span data-ttu-id="b6cdb-115">프로젝트 파일 내 [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 패키지에 대한 패키지 참조를 추가하여 해당 페이지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-115">The page is made available by adding a package reference for the [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) package in the project file.</span></span> <span data-ttu-id="b6cdb-116">`Startup.Configure` 메서드에 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-116">Add a line to the `Startup.Configure` method:</span></span>

::: moniker-end

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_DevExceptionPage&highlight=7)]

<span data-ttu-id="b6cdb-117">`app.UseMvc`과 같은 예외를 캐치하려는 미들웨어 앞에 [UseDeveloperExceptionPage](/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage) 호출을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-117">Place the call to [UseDeveloperExceptionPage](/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage) in front of any middleware where you want to catch exceptions, such as `app.UseMvc`.</span></span>

>[!WARNING]
> <span data-ttu-id="b6cdb-118">**앱이 개발 환경에서 실행 중인 경우에만** 개발자 예외 페이지를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-118">Enable the developer exception page **only when the app is running in the Development environment**.</span></span> <span data-ttu-id="b6cdb-119">프로덕션 환경에서 앱을 실행할 때 자세한 예외 정보를 공개적으로 공유하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-119">You don't want to share detailed exception information publicly when the app runs in production.</span></span> <span data-ttu-id="b6cdb-120">[구성 환경에 대해 자세히 알아보세요](xref:fundamentals/environments).</span><span class="sxs-lookup"><span data-stu-id="b6cdb-120">[Learn more about configuring environments](xref:fundamentals/environments).</span></span>

<span data-ttu-id="b6cdb-121">개발자 예외 페이지를 보려면 샘플 앱을 `Development`로 설정된 환경으로 실행하고, `?throw=true`를 앱의 기본 URL에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-121">To see the developer exception page, run the sample app with the environment set to `Development`, and add `?throw=true` to the base URL of the app.</span></span> <span data-ttu-id="b6cdb-122">페이지에는 예외 및 요청에 대한 정보가 있는 여러 탭이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-122">The page includes several tabs with information about the exception and the request.</span></span> <span data-ttu-id="b6cdb-123">첫 번째 탭에는 스택 추적이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-123">The first tab includes a stack trace:</span></span>

![스택 추적](error-handling/_static/developer-exception-page.png)

<span data-ttu-id="b6cdb-125">쿼리 문자열 매개 변수가 있는 경우 다음 탭에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-125">The next tab shows the query string parameters, if any:</span></span>

![쿼리 문자열 매개 변수](error-handling/_static/developer-exception-page-query.png)

<span data-ttu-id="b6cdb-127">요청에 쿠키가 있는 경우 **쿠키** 탭에 표시됩니다. 헤더는 마지막 탭에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-127">If the request has cookies, they appear on the **Cookies** tab. Headers are seen in the last tab:</span></span>

![헤더](error-handling/_static/developer-exception-page-headers.png)

## <a name="configuring-a-custom-exception-handling-page"></a><span data-ttu-id="b6cdb-129">사용자 지정 예외 처리 페이지 구성</span><span class="sxs-lookup"><span data-stu-id="b6cdb-129">Configuring a custom exception handling page</span></span>

<span data-ttu-id="b6cdb-130">앱이 `Development` 환경에서 실행되고 있지 않는 경우 사용할 예외 처리기 페이지를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-130">Configure an exception handler page to use when the app isn't running in the `Development` environment:</span></span>

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_DevExceptionPage&highlight=11)]

<span data-ttu-id="b6cdb-131">Razor Pages 앱에서 [dotnet new](/dotnet/core/tools/dotnet-new) Razor Pages 템플릿은 *Pages* 폴터의 오류 페이지 및 `ErrorModel` 페이지 모델 클래스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-131">In a Razor Pages app, the [dotnet new](/dotnet/core/tools/dotnet-new) Razor Pages template provides an Error page and `ErrorModel` page model class in the *Pages* folder.</span></span>

<span data-ttu-id="b6cdb-132">MVC 앱에서는 `HttpGet`과 같은 HTTP 메서드 특성을 사용하여 오류 처리기 작업 메서드를 데코레이트하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-132">In an MVC app, don't decorate the error handler action method with HTTP method attributes, such as `HttpGet`.</span></span> <span data-ttu-id="b6cdb-133">명시적 동사는 일부 요청이 메서드에 도달하지 않도록 방해합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-133">Explicit verbs prevent some requests from reaching the method.</span></span> <span data-ttu-id="b6cdb-134">인증되지 않은 사용자가 오류 보기를 수신할 수 있도록 메서드에 대한 익명 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-134">Allow anonymous access to the method so that unauthenticated users are able to receive the error view.</span></span>

<span data-ttu-id="b6cdb-135">예를 들어 다음 오류 처리기 메서드는 [dotnet new](/dotnet/core/tools/dotnet-new) MVC 템플릿에서 제공하고 홈 컨트롤러에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-135">For example, the following error handler method is provided by the [dotnet new](/dotnet/core/tools/dotnet-new) MVC template and appears in the Home controller:</span></span>

```csharp
[AllowAnonymous]
public IActionResult Error()
{
    return View(new ErrorViewModel 
        { RequestId = Activity.Current?.Id ?? HttpContext.TraceIdentifier });
}
```

## <a name="configuring-status-code-pages"></a><span data-ttu-id="b6cdb-136">상태 코드 페이지 구성</span><span class="sxs-lookup"><span data-stu-id="b6cdb-136">Configuring status code pages</span></span>

<span data-ttu-id="b6cdb-137">기본적으로 앱은 *404 찾을 수 없음*과 같은 HTTP 상태 코드에 대한 다양한 상태 코드 페이지를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-137">By default, an app doesn't provide a rich status code page for HTTP status codes, such as *404 Not Found*.</span></span> <span data-ttu-id="b6cdb-138">상태 코드 페이지를 제공하려면 `Startup.Configure` 메서드에 줄을 추가하여 상태 코드 페이지 미들웨어를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-138">To provide status code pages, configure the Status Code Pages Middleware by adding a line to the `Startup.Configure` method:</span></span>

```csharp
app.UseStatusCodePages();
```

<span data-ttu-id="b6cdb-139">기본적으로 상태 코드 페이지 미들웨어는 404와 같은 일반적인 상태 코드에 대한 텍스트 전용 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-139">By default, Status Code Pages Middleware adds text-only handlers for common status codes, such as 404:</span></span>

![404 페이지](error-handling/_static/default-404-status-code.png)

<span data-ttu-id="b6cdb-141">미들웨어는 몇 가지 확장 메서드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-141">The middleware supports several extension methods.</span></span> <span data-ttu-id="b6cdb-142">한 가지 메서드는 람다 식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-142">One method takes a lambda expression:</span></span>

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_StatusCodePages)]

<span data-ttu-id="b6cdb-143">또 다른 메서드는 콘텐츠 형식 및 형식 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-143">Another method takes a content type and format string:</span></span>

```csharp
app.UseStatusCodePages("text/plain", "Status code page, status code: {0}");
```

<span data-ttu-id="b6cdb-144">또한 리디렉션 및 다시 실행 확장 메서드도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-144">There's also redirect and re-execute extension methods.</span></span> <span data-ttu-id="b6cdb-145">리디렉션 메서드는 *302 있음* 상태 코드를 클라이언트에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-145">The redirect method sends a *302 Found* status code to the client:</span></span>

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_StatusCodePagesWithRedirect)]

<span data-ttu-id="b6cdb-146">다시 실행 메서드는 원래 상태 코드를 클라이언트에 반환할 뿐만 아니라 리디렉션 URL에 대한 처리기도 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-146">The re-execute method returns the original status code to the client but also executes the handler for the redirect URL:</span></span>

```csharp
app.UseStatusCodePagesWithReExecute("/error/{0}");
```

<span data-ttu-id="b6cdb-147">Razor 페이지 처리기 메서드 또는 MVC 컨트롤러에서 특정 요청에 대한 상태 코드 페이지를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-147">Status code pages can be disabled for specific requests in a Razor Pages handler method or in an MVC controller.</span></span> <span data-ttu-id="b6cdb-148">상태 코드 페이지를 비활성화하려면 요청의 [HttpContext.Features](/dotnet/api/microsoft.aspnetcore.http.httpcontext.features) 컬렉션에서 [IStatusCodePagesFeature](/dotnet/api/microsoft.aspnetcore.diagnostics.istatuscodepagesfeature)를 검색하고 사용 가능한 경우 기능을 비활성합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-148">To disable status code pages, attempt to retrieve the [IStatusCodePagesFeature](/dotnet/api/microsoft.aspnetcore.diagnostics.istatuscodepagesfeature) from the request's [HttpContext.Features](/dotnet/api/microsoft.aspnetcore.http.httpcontext.features) collection and disable the feature if it's available:</span></span>

```csharp
var statusCodePagesFeature = HttpContext.Features.Get<IStatusCodePagesFeature>();

if (statusCodePagesFeature != null)
{
    statusCodePagesFeature.Enabled = false;
}
```

<span data-ttu-id="b6cdb-149">앱 내에서 엔드포인트를 가리키는 `UseStatusCodePages*`를 사용하는 경우 엔드포인트에 대해 MVC 보기 또는 Razor Page를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-149">If using a `UseStatusCodePages*` overload that points to an endpoint within the app, create an MVC view or Razor Page for the endpoint.</span></span> <span data-ttu-id="b6cdb-150">예를 들어 Razor Pages 앱의 [dotnet new](/dotnet/core/tools/dotnet-new) 템플릿은 다음 페이지와 페이지 모델 클래스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-150">For example, the [dotnet new](/dotnet/core/tools/dotnet-new) template for a Razor Pages app produces the following page and page model class:</span></span>

<span data-ttu-id="b6cdb-151">*Error.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="b6cdb-151">*Error.cshtml*:</span></span>

```cshtml
@page
@model ErrorModel
@{
    ViewData["Title"] = "Error";
}

<h1 class="text-danger">Error.</h1>
<h2 class="text-danger">An error occurred while processing your request.</h2>

@if (Model.ShowRequestId)
{
    <p>
        <strong>Request ID:</strong> <code>@Model.RequestId</code>
    </p>
}

<h3>Development Mode</h3>
<p>
    Swapping to <strong>Development</strong> environment will display more detailed 
    information about the error that occurred.
</p>
<p>
    <strong>Development environment should not be enabled in deployed applications
    </strong>, as it can result in sensitive information from exceptions being 
    displayed to end users. For local debugging, development environment can be 
    enabled by setting the <strong>ASPNETCORE_ENVIRONMENT</strong> environment 
    variable to <strong>Development</strong>, and restarting the application.
</p>
```

<span data-ttu-id="b6cdb-152">*Error.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="b6cdb-152">*Error.cshtml.cs*:</span></span>

```csharp
public class ErrorModel : PageModel
{
    public string RequestId { get; set; }

    public bool ShowRequestId => !string.IsNullOrEmpty(RequestId);

    [ResponseCache(Duration = 0, Location = ResponseCacheLocation.None, 
        NoStore = true)]
    public void OnGet()
    {
        RequestId = Activity.Current?.Id ?? HttpContext.TraceIdentifier;
    }
}
```

## <a name="exception-handling-code"></a><span data-ttu-id="b6cdb-153">예외 처리 코드</span><span class="sxs-lookup"><span data-stu-id="b6cdb-153">Exception-handling code</span></span>

<span data-ttu-id="b6cdb-154">예외 처리 페이지의 코드는 예외를 throw할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-154">Code in exception handling pages can throw exceptions.</span></span> <span data-ttu-id="b6cdb-155">종종 프로덕션 오류 페이지에 대해 완전한 정적 콘텐츠를 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-155">It's often a good idea for production error pages to consist of purely static content.</span></span>

<span data-ttu-id="b6cdb-156">또한 일단 응답에 대한 헤더를 보내고 나면 응답의 상태 코드, 예외 페이지 또는 처리기 실행을 변경할 수 없다는 점에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-156">Also, be aware that once the headers for a response have been sent, you can't change the response's status code, nor can any exception pages or handlers run.</span></span> <span data-ttu-id="b6cdb-157">응답을 완료하거나 연결이 중단되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-157">The response must be completed or the connection aborted.</span></span>

## <a name="server-exception-handling"></a><span data-ttu-id="b6cdb-158">서버 예외 처리</span><span class="sxs-lookup"><span data-stu-id="b6cdb-158">Server exception handling</span></span>

<span data-ttu-id="b6cdb-159">앱에서 논리를 처리하는 예외뿐 아니라 앱을 호스팅하는 [서버](xref:fundamentals/servers/index)는 몇 가지 예외 처리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-159">In addition to the exception handling logic in your app, the [server](xref:fundamentals/servers/index) hosting your app performs some exception handling.</span></span> <span data-ttu-id="b6cdb-160">헤더를 보내기 전에 서버가 예외를 catch하는 경우 서버는 본문이 없는 *500 내부 서버 오류* 응답을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-160">If the server catches an exception before the headers are sent, the server sends a *500 Internal Server Error* response with no body.</span></span> <span data-ttu-id="b6cdb-161">헤더를 보낸 후에 서버가 예외를 catch하는 경우 서버는 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-161">If the server catches an exception after the headers have been sent, the server closes the connection.</span></span> <span data-ttu-id="b6cdb-162">앱으로 처리되지 않는 요청은 서버에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-162">Requests that aren't handled by your app are handled by the server.</span></span> <span data-ttu-id="b6cdb-163">발생하는 모든 예외는 서버의 예외 처리에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-163">Any exception that occurs is handled by the server's exception handling.</span></span> <span data-ttu-id="b6cdb-164">구성된 모든 사용자 지정 오류 페이지 또는 예외 처리 미들웨어 또는 필터는 이 동작에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-164">Any configured custom error pages or exception handling middleware or filters don't affect this behavior.</span></span>

## <a name="startup-exception-handling"></a><span data-ttu-id="b6cdb-165">시작 예외 처리</span><span class="sxs-lookup"><span data-stu-id="b6cdb-165">Startup exception handling</span></span>

<span data-ttu-id="b6cdb-166">호스팅 계층만 앱 시작 시 발생하는 예외를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-166">Only the hosting layer can handle exceptions that take place during app startup.</span></span> <span data-ttu-id="b6cdb-167">[웹 호스트](xref:fundamentals/host/web-host)를 사용하면 `captureStartupErrors` 및 `detailedErrors` 키로 [시작 시 오류에 대해 호스트가 응답하는 방법을 구성](xref:fundamentals/host/web-host#detailed-errors)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-167">Using the [Web Host](xref:fundamentals/host/web-host), you can [configure how the host behaves in response to errors during startup](xref:fundamentals/host/web-host#detailed-errors) with the `captureStartupErrors` and `detailedErrors` keys.</span></span>

<span data-ttu-id="b6cdb-168">호스팅은 호스트 주소/포트 바인딩 후에 오류가 발생하는 경우 캡처된 시작 오류에 대한 오류 페이지만 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-168">Hosting can only show an error page for a captured startup error if the error occurs after host address/port binding.</span></span> <span data-ttu-id="b6cdb-169">어떤 이유로 바인딩이 실패한 경우 호스팅 계층이 심각한 예외를 기록하고, dotnet 프로세스가 충돌하며, 앱이 [Kestrel](xref:fundamentals/servers/kestrel) 서버에서 실행 중일 때 오류 페이지가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-169">If any binding fails for any reason, the hosting layer logs a critical exception, the dotnet process crashes, and no error page is displayed when the app is running on the [Kestrel](xref:fundamentals/servers/kestrel) server.</span></span>

<span data-ttu-id="b6cdb-170">[IIS](/iis) 또는 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)에서 실행 중일 때, 프로세스를 시작할 수 없는 경우 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)에서 *502.5 프로세스 실패*를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-170">When running on [IIS](/iis) or [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview), a *502.5 Process Failure* is returned by the [ASP.NET Core Module](xref:fundamentals/servers/aspnet-core-module) if the process can't be started.</span></span> <span data-ttu-id="b6cdb-171">IIS를 사용하여 호스팅할 때 시작 문제 해결에 대한 내용은 <xref:host-and-deploy/iis/troubleshoot>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-171">For information on troubleshooting startup issues when hosting with IIS, see <xref:host-and-deploy/iis/troubleshoot>.</span></span> <span data-ttu-id="b6cdb-172">Azure App Service의 시작 문제 해결에 대한 내용은 <xref:host-and-deploy/azure-apps/troubleshoot>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-172">For information on troubleshooting startup issues with Azure App Service, see <xref:host-and-deploy/azure-apps/troubleshoot>.</span></span>

## <a name="aspnet-mvc-error-handling"></a><span data-ttu-id="b6cdb-173">ASP.NET MVC 오류 처리</span><span class="sxs-lookup"><span data-stu-id="b6cdb-173">ASP.NET MVC error handling</span></span>

<span data-ttu-id="b6cdb-174">[MVC](xref:mvc/overview) 앱에는 예외 필터 구성 및 모델 유효성 검사 수행과 같이 오류를 처리하기 위한 몇 가지 추가 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-174">[MVC](xref:mvc/overview) apps have some additional options for handling errors, such as configuring exception filters and performing model validation.</span></span>

### <a name="exception-filters"></a><span data-ttu-id="b6cdb-175">예외 필터</span><span class="sxs-lookup"><span data-stu-id="b6cdb-175">Exception filters</span></span>

<span data-ttu-id="b6cdb-176">전역으로 또는 MVC 앱에서 컨트롤러당 또는 작업당 기준으로 예외 필터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-176">Exception filters can be configured globally or on a per-controller or per-action basis in an MVC app.</span></span> <span data-ttu-id="b6cdb-177">이러한 필터는 컨트롤러 작업 또는 다른 필터를 실행하는 동안 발생하는 처리되지 않은 예외를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-177">These filters handle any unhandled exception that occurs during the execution of a controller action or another filter.</span></span> <span data-ttu-id="b6cdb-178">그렇지 않으면 이러한 필터는 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-178">These filters aren't called otherwise.</span></span> <span data-ttu-id="b6cdb-179">자세한 내용은 [필터](xref:mvc/controllers/filters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-179">To learn more, see [Filters](xref:mvc/controllers/filters).</span></span>

> [!TIP]
> <span data-ttu-id="b6cdb-180">예외 필터는 MVC 작업 내에서 발생하는 예외를 트래핑하는 데 유용하지만 오류 처리 미들웨어만큼 유연하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-180">Exception filters are good for trapping exceptions that occur within MVC actions, but they're not as flexible as error handling middleware.</span></span> <span data-ttu-id="b6cdb-181">일반적인 경우에는 미들웨어를 선호하고, 선택한 MVC 작업에 따라 오류 처리를 *다르게* 해야 하는 경우에만 필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-181">Generally prefer the use of middleware, and use filters only where you need to perform error handling *differently* based on which MVC action is chosen.</span></span>

### <a name="handling-model-state-errors"></a><span data-ttu-id="b6cdb-182">모델 상태 오류 처리</span><span class="sxs-lookup"><span data-stu-id="b6cdb-182">Handling model state errors</span></span>

<span data-ttu-id="b6cdb-183">[모델 유효성 검사](xref:mvc/models/validation)는 각 컨트롤러 작업을 호출하기 전에 발생하며, `ModelState.IsValid`를 검사하고 적절하게 반응하는 것은 작업 메서드의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-183">[Model validation](xref:mvc/models/validation) occurs prior to invoking each controller action, and it's the action method's responsibility to inspect `ModelState.IsValid` and react appropriately.</span></span>

<span data-ttu-id="b6cdb-184">[필터](xref:mvc/controllers/filters)가 이러한 정책을 구현하기에 적절한 경우에 일부 앱은 모델 유효성 검사 오류를 처리하는 표준 규칙을 따르도록 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-184">Some apps choose to follow a standard convention for dealing with model validation errors, in which case a [filter](xref:mvc/controllers/filters) may be an appropriate place to implement such a policy.</span></span> <span data-ttu-id="b6cdb-185">잘못된 모델 상태일 때 작업 동작 방식을 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-185">You should test how your actions behave with invalid model states.</span></span> <span data-ttu-id="b6cdb-186">[컨트롤러 논리 테스트](xref:mvc/controllers/testing)에서 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-186">Learn more in [Test controller logic](xref:mvc/controllers/testing).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b6cdb-187">추가 자료</span><span class="sxs-lookup"><span data-stu-id="b6cdb-187">Additional resources</span></span>

* <xref:host-and-deploy/azure-iis-errors-reference>
* <xref:host-and-deploy/iis/troubleshoot>
* <xref:host-and-deploy/azure-apps/troubleshoot>
