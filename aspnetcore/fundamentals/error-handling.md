---
title: ASP.NET Core에서 오류 처리
author: tdykstra
description: ASP.NET Core 앱에서 오류를 처리하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 03/01/2019
uid: fundamentals/error-handling
ms.openlocfilehash: a2ae2cb25c8cc5048b189b4035abbfc32a29aaff
ms.sourcegitcommit: 036d4b03fd86ca5bb378198e29ecf2704257f7b2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57345498"
---
# <a name="handle-errors-in-aspnet-core"></a><span data-ttu-id="3c88a-103">ASP.NET Core에서 오류 처리</span><span class="sxs-lookup"><span data-stu-id="3c88a-103">Handle errors in ASP.NET Core</span></span>

<span data-ttu-id="3c88a-104">작성자: [Tom Dykstra](https://github.com/tdykstra/), [Luke Latham](https://github.com/guardrex) 및 [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="3c88a-104">By [Tom Dykstra](https://github.com/tdykstra/), [Luke Latham](https://github.com/guardrex), and [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="3c88a-105">이 문서에서는 ASP.NET Core 앱에서 오류를 처리하기 위한 일반적인 접근법을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-105">This article covers common approaches to handling errors in ASP.NET Core apps.</span></span>

<span data-ttu-id="3c88a-106">[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/samples/2.x) ([다운로드 방법](xref:index#how-to-download-a-sample))</span><span class="sxs-lookup"><span data-stu-id="3c88a-106">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/samples/2.x) ([how to download](xref:index#how-to-download-a-sample))</span></span>

## <a name="developer-exception-page"></a><span data-ttu-id="3c88a-107">개발자 예외 페이지</span><span class="sxs-lookup"><span data-stu-id="3c88a-107">Developer Exception Page</span></span>

<span data-ttu-id="3c88a-108">예외에 대한 자세한 정보를 보여주는 페이지를 표시하는 앱을 구성하려면 *개발자 예외 페이지*를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-108">To configure an app to display a page that shows detailed information about exceptions, use the *Developer Exception Page*.</span></span> <span data-ttu-id="3c88a-109">[Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 패키지가 사용할 수 있게 된 페이지는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-109">The page is made available by the [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) package, which is available in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span> <span data-ttu-id="3c88a-110">`Startup.Configure` 메서드에 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-110">Add a line to the `Startup.Configure` method:</span></span>

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_DevExceptionPage&highlight=5)]

<span data-ttu-id="3c88a-111">예외를 catch하려는 미들웨어 앞에 <xref:Microsoft.AspNetCore.Builder.DeveloperExceptionPageExtensions.UseDeveloperExceptionPage*> 호출을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-111">Place the call to <xref:Microsoft.AspNetCore.Builder.DeveloperExceptionPageExtensions.UseDeveloperExceptionPage*> in front of any middleware where you want to catch exceptions.</span></span>

> [!WARNING]
> <span data-ttu-id="3c88a-112">**앱이 개발 환경에서 실행 중인 경우에만** 개발자 예외 페이지를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-112">Enable the Developer Exception Page **only when the app is running in the Development environment**.</span></span> <span data-ttu-id="3c88a-113">프로덕션 환경에서 앱을 실행할 때 자세한 예외 정보를 공개적으로 공유하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-113">You don't want to share detailed exception information publicly when the app runs in production.</span></span> <span data-ttu-id="3c88a-114">환경 구성 방법에 대한 자세한 내용은 <xref:fundamentals/environments>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c88a-114">For more information on configuring environments, see <xref:fundamentals/environments>.</span></span>

<span data-ttu-id="3c88a-115">개발자 예외 페이지를 보려면 샘플 앱을 `Development`로 설정된 환경으로 실행하고, `?throw=true`를 앱의 기본 URL에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-115">To see the Developer Exception Page, run the sample app with the environment set to `Development` and add `?throw=true` to the base URL of the app.</span></span> <span data-ttu-id="3c88a-116">페이지에는 예외 및 요청에 대한 다음 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-116">The page includes the following information about the exception and the request:</span></span>

* <span data-ttu-id="3c88a-117">스택 추적</span><span class="sxs-lookup"><span data-stu-id="3c88a-117">Stack trace</span></span>
* <span data-ttu-id="3c88a-118">쿼리 문자열 매개 변수(있는 경우)</span><span class="sxs-lookup"><span data-stu-id="3c88a-118">Query string parameters (if any)</span></span>
* <span data-ttu-id="3c88a-119">쿠키(있는 경우)</span><span class="sxs-lookup"><span data-stu-id="3c88a-119">Cookies (if any)</span></span>
* <span data-ttu-id="3c88a-120">헤더</span><span class="sxs-lookup"><span data-stu-id="3c88a-120">Headers</span></span>

## <a name="configure-a-custom-exception-handling-page"></a><span data-ttu-id="3c88a-121">사용자 지정 예외 처리 페이지 구성</span><span class="sxs-lookup"><span data-stu-id="3c88a-121">Configure a custom exception handling page</span></span>

<span data-ttu-id="3c88a-122">개발 환경에서 앱이 실행되지 않는 경우 <xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*> 확장 메서드를 호출하여 예외 처리 미들웨어를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-122">When the app isn't running in the Development environment, call the <xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*> extension method to add Exception Handling Middleware.</span></span> <span data-ttu-id="3c88a-123">미들웨어는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-123">The middleware:</span></span>

* <span data-ttu-id="3c88a-124">예외를 catch합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-124">Catches exceptions.</span></span>
* <span data-ttu-id="3c88a-125">예외를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-125">Logs exceptions.</span></span>
* <span data-ttu-id="3c88a-126">대체 파이프라인에서 표시된 페이지 또는 컨트롤러에 대한 요청을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-126">Re-executes the request in an alternate pipeline for the page or controller indicated.</span></span> <span data-ttu-id="3c88a-127">응답이 시작된 경우에는 요청이 다시 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-127">The request isn't re-executed if the response has started.</span></span>

<span data-ttu-id="3c88a-128">샘플 앱의 다음 예제에서 <xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*>는 비개발 환경에 예외 처리 미들웨어를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-128">In the following example from the sample app, <xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*> adds the Exception Handling Middleware in non-Development environments.</span></span> <span data-ttu-id="3c88a-129">확장 메서드는 예외가 catch되고 기록된 후에 다시 실행된 요청에 대한 오류 페이지 또는 컨트롤러를 `/Error` 엔드포인트에 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-129">The extension method specifies an error page or controller at the `/Error` endpoint for re-executed requests after exceptions are caught and logged:</span></span>

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_DevExceptionPage&highlight=9)]

<span data-ttu-id="3c88a-130">Razor Pages 앱 템플릿은 Pages 폴더에 오류 페이지(*.cshtml*) 및 <xref:Microsoft.AspNetCore.Mvc.RazorPages.PageModel> 클래스(`ErrorModel`)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-130">The Razor Pages app template provides an Error page (*.cshtml*) and <xref:Microsoft.AspNetCore.Mvc.RazorPages.PageModel> class (`ErrorModel`) in the Pages folder.</span></span>

<span data-ttu-id="3c88a-131">MVC 앱에서는 다음 오류 처리기 메서드가 MVC 앱 템플릿에 포함되고 홈 컨트롤러에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-131">In an MVC app, the following error handler method is included in the MVC app template and appears in the Home controller:</span></span>

```csharp
[AllowAnonymous]
public IActionResult Error()
{
    return View(new ErrorViewModel 
        { RequestId = Activity.Current?.Id ?? HttpContext.TraceIdentifier });
}
```

<span data-ttu-id="3c88a-132">`HttpGet` 등의 HTTP 메서드 특성을 사용하여 오류 처리기 작업 메서드를 데코레이트하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-132">Don't decorate the error handler action method with HTTP method attributes, such as `HttpGet`.</span></span> <span data-ttu-id="3c88a-133">명시적 동사는 일부 요청이 메서드에 도달하지 않도록 방해합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-133">Explicit verbs prevent some requests from reaching the method.</span></span> <span data-ttu-id="3c88a-134">인증되지 않은 사용자가 오류 보기를 수신할 수 있도록 메서드에 대한 익명 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-134">Allow anonymous access to the method so that unauthenticated users are able to receive the error view.</span></span>

## <a name="configure-status-code-pages"></a><span data-ttu-id="3c88a-135">상태 코드 페이지 구성</span><span class="sxs-lookup"><span data-stu-id="3c88a-135">Configure status code pages</span></span>

<span data-ttu-id="3c88a-136">기본적으로 ASP.NET Core 앱은 ‘404 - 찾을 수 없음’과 같은 HTTP 상태 코드에 대한 상태 코드 페이지를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-136">By default, an ASP.NET Core app doesn't provide a status code page for HTTP status codes, such as *404 - Not Found*.</span></span> <span data-ttu-id="3c88a-137">앱에서 상태 코드와 빈 응답 본문을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-137">The app returns a status code and an empty response body.</span></span> <span data-ttu-id="3c88a-138">상태 코드 페이지를 제공하려면 상태 코드 페이지 미들웨어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-138">To provide status code pages, use Status Code Pages Middleware.</span></span>

<span data-ttu-id="3c88a-139">[Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 패키지가 사용할 수 있게 된 미들웨어는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-139">The middleware is made available by the [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) package, which is available in the [Microsoft.AspNetCore.App metapackage](xref:fundamentals/metapackage-app).</span></span>

<span data-ttu-id="3c88a-140">`Startup.Configure` 메서드에 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-140">Add a line to the `Startup.Configure` method:</span></span>

```csharp
app.UseStatusCodePages();
```

<span data-ttu-id="3c88a-141">요청 처리 미들웨어(예: 정적 파일 미들웨어 및 MVC 미들웨어) 전에 <xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePages*> 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-141">Call the <xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePages*> method before request handling middleware (for example, Static File Middleware and MVC Middleware).</span></span>

<span data-ttu-id="3c88a-142">기본적으로 상태 코드 페이지 미들웨어는 ‘404 - 찾을 수 없음’과 같은 일반적인 상태 코드에 대한 텍스트 전용 처리기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-142">By default, Status Code Pages Middleware adds text-only handlers for common status codes, such as *404 - Not Found*:</span></span>

```
Status Code: 404; Not Found
```

<span data-ttu-id="3c88a-143">미들웨어는 해당 동작의 사용자 지정을 허용하는 여러 확장 메서드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-143">The middleware supports several extension methods that allow you to customize its behavior.</span></span>

<span data-ttu-id="3c88a-144"><xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePages*>의 오버로드는 사용자 지정 오류 처리 논리를 처리하고 응답을 수동으로 작성하는 데 사용할 수 있는 람다 식을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-144">An overload of <xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePages*> takes a lambda expression, which you can use to process custom error-handling logic and manually write the response:</span></span>

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_StatusCodePages)]

<span data-ttu-id="3c88a-145"><xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePages*>의 오버로드는 콘텐츠 형식 및 응답 텍스트를 사용자 지정하는 데 사용할 수 있는 콘텐츠 형식 및 형식 문자열을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-145">An overload of <xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePages*> takes a content type and format string, which you can use to customize the content type and response text:</span></span>

```csharp
app.UseStatusCodePages("text/plain", "Status code page, status code: {0}");
```

### <a name="redirect-and-re-execute-extension-methods"></a><span data-ttu-id="3c88a-146">확장 메서드 리디렉션 및 다시 실행</span><span class="sxs-lookup"><span data-stu-id="3c88a-146">Redirect and re-execute extension methods</span></span>

<span data-ttu-id="3c88a-147"><xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithRedirects*>:</span><span class="sxs-lookup"><span data-stu-id="3c88a-147"><xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithRedirects*>:</span></span>

* <span data-ttu-id="3c88a-148">‘302 - 있음’ 상태 코드를 클라이언트에 보냅니다. </span><span class="sxs-lookup"><span data-stu-id="3c88a-148">Sends a *302 - Found* status code to the client.</span></span>
* <span data-ttu-id="3c88a-149">클라이언트를 URL 템플릿에 제공된 위치로 리디렉션합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-149">Redirects the client to the location provided in the URL template.</span></span>

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_StatusCodePagesWithRedirect)]

<span data-ttu-id="3c88a-150"><xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithRedirects*>는 일반적으로 앱이 다음과 같아야 하는 경우에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-150"><xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithRedirects*> is commonly used when the app:</span></span>

* <span data-ttu-id="3c88a-151">대체로 다른 앱이 오류를 처리하는 상황에서 앱이 클라이언트를 다른 엔드포인트로 리디렉션해야 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3c88a-151">Should redirect the client to a different endpoint, usually in cases where a different app processes the error.</span></span> <span data-ttu-id="3c88a-152">웹앱의 경우 클라이언트의 브라우저 주소 표시줄에 리디렉션된 엔드포인트가 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-152">For web apps, the client's browser address bar reflects the redirected endpoint.</span></span>
* <span data-ttu-id="3c88a-153">원래 상태 코드를 유지하고 초기 리디렉션 응답과 함께 반환하면 안 되는 경우</span><span class="sxs-lookup"><span data-stu-id="3c88a-153">Shouldn't preserve and return the original status code with the initial redirect response.</span></span>

<span data-ttu-id="3c88a-154"><xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithReExecute*>:</span><span class="sxs-lookup"><span data-stu-id="3c88a-154"><xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithReExecute*>:</span></span>

* <span data-ttu-id="3c88a-155">원래 상태 코드를 클라이언트로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-155">Returns the original status code to the client.</span></span>
* <span data-ttu-id="3c88a-156">대체 경로에서 요청 파이프라인을 다시 실행하여 응답 본문을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-156">Generates the response body by re-executing the request pipeline using an alternate path.</span></span>

```csharp
app.UseStatusCodePagesWithReExecute("/Error/{0}");
```

<span data-ttu-id="3c88a-157"><xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithReExecute*>는 일반적으로 앱이 다음과 같아야 하는 경우에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-157"><xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithReExecute*> is commonly used when the app should:</span></span>

* <span data-ttu-id="3c88a-158">다른 엔드포인트로 리디렉션하지 않고 요청을 처리해야 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3c88a-158">Process the request without redirecting to a different endpoint.</span></span> <span data-ttu-id="3c88a-159">웹앱의 경우 클라이언트의 브라우저 주소 표시줄에 원래 요청된 엔드포인트가 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-159">For web apps, the client's browser address bar reflects the originally requested endpoint.</span></span>
* <span data-ttu-id="3c88a-160">원래 상태 코드를 유지하고 응답과 함께 반환해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="3c88a-160">Preserve and return the original status code with the response.</span></span>

<span data-ttu-id="3c88a-161">템플릿에는 상태 코드에 대한 자리 표시자(`{0}`)가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-161">Templates may include a placeholder (`{0}`) for the status code.</span></span> <span data-ttu-id="3c88a-162">템플릿은 슬래시(`/`)로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-162">The template must start with a forward slash (`/`).</span></span> <span data-ttu-id="3c88a-163">자리 표시자를 사용하는 경우, 엔드포인트(페이지 또는 컨트롤러)가 경로 세그먼트를 처리할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-163">When using a placeholder, confirm that the endpoint (page or controller) can process the path segment.</span></span> <span data-ttu-id="3c88a-164">예를 들어 오류에 대한 Razor 페이지가 `@page` 지시문을 사용한 선택적 경로 세그먼트 값을 수락해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-164">For example, a Razor Page for errors should accept the optional path segment value with the `@page` directive:</span></span>

```cshtml
@page "{code?}"
```

<span data-ttu-id="3c88a-165">Razor 페이지 처리기 메서드 또는 MVC 컨트롤러에서 특정 요청에 대한 상태 코드 페이지를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-165">Status code pages can be disabled for specific requests in a Razor Pages handler method or in an MVC controller.</span></span> <span data-ttu-id="3c88a-166">상태 코드 페이지를 사용하지 않으려면 요청의 [HttpContext.Features](xref:Microsoft.AspNetCore.Http.HttpContext.Features) 컬렉션에서 <xref:Microsoft.AspNetCore.Diagnostics.IStatusCodePagesFeature>를 검색하고, 사용 가능한 경우 기능을 비활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-166">To disable status code pages, attempt to retrieve the <xref:Microsoft.AspNetCore.Diagnostics.IStatusCodePagesFeature> from the request's [HttpContext.Features](xref:Microsoft.AspNetCore.Http.HttpContext.Features) collection and disable the feature if it's available:</span></span>

```csharp
var statusCodePagesFeature = HttpContext.Features.Get<IStatusCodePagesFeature>();

if (statusCodePagesFeature != null)
{
    statusCodePagesFeature.Enabled = false;
}
```

<span data-ttu-id="3c88a-167">앱 내에서 엔드포인트를 가리키는 <xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePages*> 오버로드를 사용하려면 엔드포인트에 대해 MVC 뷰 또는 Razor 페이지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-167">To use a <xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePages*> overload that points to an endpoint within the app, create an MVC view or Razor Page for the endpoint.</span></span> <span data-ttu-id="3c88a-168">예를 들어 Razor Pages 앱 템플릿은 다음 페이지와 페이지 모델 클래스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-168">For example, the Razor Pages app template produces the following page and page model class:</span></span>

<span data-ttu-id="3c88a-169">*Error.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="3c88a-169">*Error.cshtml*:</span></span>

::: moniker range=">= aspnetcore-2.2"

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
    Swapping to the <strong>Development</strong> environment displays 
    detailed information about the error that occurred.
</p>
<p>
    <strong>The Development environment shouldn't be enabled for deployed 
    applications.</strong> It can result in displaying sensitive information 
    from exceptions to end users. For local debugging, enable the 
    <strong>Development</strong> environment by setting the 
    <strong>ASPNETCORE_ENVIRONMENT</strong> environment variable to 
    <strong>Development</strong> and restarting the app.
</p>
```

<span data-ttu-id="3c88a-170">*Error.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="3c88a-170">*Error.cshtml.cs*:</span></span>

```csharp
[ResponseCache(Duration = 0, Location = ResponseCacheLocation.None, NoStore = true)]
public class ErrorModel : PageModel
{
    public string RequestId { get; set; }

    public bool ShowRequestId => !string.IsNullOrEmpty(RequestId);

    public void OnGet()
    {
        RequestId = Activity.Current?.Id ?? HttpContext.TraceIdentifier;
    }
}
```

::: moniker-end

::: moniker range="< aspnetcore-2.2"

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

<span data-ttu-id="3c88a-171">*Error.cshtml.cs*:</span><span class="sxs-lookup"><span data-stu-id="3c88a-171">*Error.cshtml.cs*:</span></span>

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

::: moniker-end

## <a name="exception-handling-code"></a><span data-ttu-id="3c88a-172">예외 처리 코드</span><span class="sxs-lookup"><span data-stu-id="3c88a-172">Exception-handling code</span></span>

<span data-ttu-id="3c88a-173">예외 처리 페이지의 코드는 예외를 throw할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-173">Code in exception handling pages can throw exceptions.</span></span> <span data-ttu-id="3c88a-174">종종 프로덕션 오류 페이지에 대해 완전한 정적 콘텐츠를 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-174">It's often a good idea for production error pages to consist of purely static content.</span></span>

<span data-ttu-id="3c88a-175">또한 응답의 헤더가 전송되고 나면 다음 제한이 적용되는 것에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="3c88a-175">Also, be aware that once the headers for a response are sent:</span></span>

* <span data-ttu-id="3c88a-176">앱에서 응답의 상태 코드를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-176">The app can't change the response's status code.</span></span>
* <span data-ttu-id="3c88a-177">예외 페이지 또는 처리기를 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-177">Any exception pages or handlers can't run.</span></span> <span data-ttu-id="3c88a-178">응답을 완료하거나 연결이 중단되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-178">The response must be completed or the connection aborted.</span></span>

## <a name="server-exception-handling"></a><span data-ttu-id="3c88a-179">서버 예외 처리</span><span class="sxs-lookup"><span data-stu-id="3c88a-179">Server exception handling</span></span>

<span data-ttu-id="3c88a-180">앱의 예외 처리 논리 외에도 [서버 구현](xref:fundamentals/servers/index)에서 몇 가지 예외를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-180">In addition to the exception handling logic in your app, the [server implementation](xref:fundamentals/servers/index) can handle some exceptions.</span></span> <span data-ttu-id="3c88a-181">응답 헤더가 전송되기 전에 예외를 catch한 서버는 응답 본문 없이 ‘500 - 내부 서버 오류’ 응답을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-181">If the server catches an exception before response headers are sent, the server sends a *500 - Internal Server Error* response without a response body.</span></span> <span data-ttu-id="3c88a-182">응답 헤더가 전송된 후에 예외를 catch한 서버는 연결을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-182">If the server catches an exception after response headers are sent, the server closes the connection.</span></span> <span data-ttu-id="3c88a-183">앱으로 처리되지 않는 요청은 서버에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-183">Requests that aren't handled by your app are handled by the server.</span></span> <span data-ttu-id="3c88a-184">발생하는 모든 예외는 서버의 예외 처리에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-184">Any exception that occurs is handled by the server's exception handling.</span></span> <span data-ttu-id="3c88a-185">구성된 모든 사용자 지정 오류 페이지 또는 예외 처리 미들웨어 또는 필터는 이 동작에 영향을 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-185">Any configured custom error pages or exception handling middleware or filters don't affect this behavior.</span></span>

## <a name="startup-exception-handling"></a><span data-ttu-id="3c88a-186">시작 예외 처리</span><span class="sxs-lookup"><span data-stu-id="3c88a-186">Startup exception handling</span></span>

<span data-ttu-id="3c88a-187">호스팅 계층만 앱 시작 시 발생하는 예외를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-187">Only the hosting layer can handle exceptions that take place during app startup.</span></span> <span data-ttu-id="3c88a-188">[웹 호스트](xref:fundamentals/host/web-host)를 사용하면 `captureStartupErrors` 및 `detailedErrors` 키로 [시작 시 오류에 대해 호스트가 응답하는 방법을 구성](xref:fundamentals/host/web-host#detailed-errors)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-188">Using [Web Host](xref:fundamentals/host/web-host), you can [configure how the host behaves in response to errors during startup](xref:fundamentals/host/web-host#detailed-errors) with the `captureStartupErrors` and `detailedErrors` keys.</span></span>

<span data-ttu-id="3c88a-189">호스팅은 호스트 주소/포트 바인딩 후에 오류가 발생하는 경우 캡처된 시작 오류에 대한 오류 페이지만 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-189">Hosting can only show an error page for a captured startup error if the error occurs after host address/port binding.</span></span> <span data-ttu-id="3c88a-190">어떤 이유로든 바인딩에 실패하는 경우</span><span class="sxs-lookup"><span data-stu-id="3c88a-190">If any binding fails for any reason:</span></span>

* <span data-ttu-id="3c88a-191">호스팅 계층에서 심각한 예외를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-191">The hosting layer logs a critical exception.</span></span>
* <span data-ttu-id="3c88a-192">dotnet 프로세스의 작동이 중단됩니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-192">The dotnet process crashes.</span></span>
* <span data-ttu-id="3c88a-193">[Kestrel](xref:fundamentals/servers/kestrel) 서버에서 앱을 실행 중일 때는 오류 페이지가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-193">No error page is displayed when the app is running on the [Kestrel](xref:fundamentals/servers/kestrel) server.</span></span>

<span data-ttu-id="3c88a-194">[IIS](/iis) 또는 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)에서 실행 중일 때, 프로세스를 시작할 수 없는 경우 [ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module)에서 *502.5 - 프로세스 실패*를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-194">When running on [IIS](/iis) or [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview), a *502.5 - Process Failure* is returned by the [ASP.NET Core Module](xref:host-and-deploy/aspnet-core-module) if the process can't start.</span></span> <span data-ttu-id="3c88a-195">자세한 내용은 <xref:host-and-deploy/iis/troubleshoot>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c88a-195">For more information, see <xref:host-and-deploy/iis/troubleshoot>.</span></span> <span data-ttu-id="3c88a-196">Azure App Service의 시작 문제 해결에 대한 내용은 <xref:host-and-deploy/azure-apps/troubleshoot>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c88a-196">For information on troubleshooting startup issues with Azure App Service, see <xref:host-and-deploy/azure-apps/troubleshoot>.</span></span>

## <a name="aspnet-core-mvc-error-handling"></a><span data-ttu-id="3c88a-197">ASP.NET Core MVC 오류 처리</span><span class="sxs-lookup"><span data-stu-id="3c88a-197">ASP.NET Core MVC error handling</span></span>

<span data-ttu-id="3c88a-198">[MVC](xref:mvc/overview) 앱에는 예외 필터 구성 및 모델 유효성 검사 수행과 같이 오류를 처리하기 위한 몇 가지 추가 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-198">[MVC](xref:mvc/overview) apps have some additional options for handling errors, such as configuring exception filters and performing model validation.</span></span>

### <a name="exception-filters"></a><span data-ttu-id="3c88a-199">예외 필터</span><span class="sxs-lookup"><span data-stu-id="3c88a-199">Exception filters</span></span>

<span data-ttu-id="3c88a-200">전역으로 또는 MVC 앱에서 컨트롤러당 또는 작업당 기준으로 예외 필터를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-200">Exception filters can be configured globally or on a per-controller or per-action basis in an MVC app.</span></span> <span data-ttu-id="3c88a-201">이러한 필터는 컨트롤러 작업 또는 다른 필터를 실행하는 동안 발생하는 처리되지 않은 예외를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-201">These filters handle any unhandled exception that occurs during the execution of a controller action or another filter.</span></span> <span data-ttu-id="3c88a-202">그렇지 않으면 이러한 필터는 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-202">These filters aren't called otherwise.</span></span> <span data-ttu-id="3c88a-203">자세한 내용은 <xref:mvc/controllers/filters>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c88a-203">To learn more, see <xref:mvc/controllers/filters>.</span></span>

> [!TIP]
> <span data-ttu-id="3c88a-204">예외 필터는 MVC 작업 내에서 발생하는 예외를 트래핑하는 데 유용하지만 오류 처리 미들웨어만큼 유연하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-204">Exception filters are useful for trapping exceptions that occur within MVC actions, but they're not as flexible as error handling middleware.</span></span> <span data-ttu-id="3c88a-205">미들웨어를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-205">We recommend the use of middleware.</span></span> <span data-ttu-id="3c88a-206">선택한 MVC 작업에 따라 오류 처리를 ‘다르게 수행’해야 하는 경우에만 필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-206">Use filters only where you need to perform error handling *differently* based on which MVC action is chosen.</span></span>

### <a name="handle-model-state-errors"></a><span data-ttu-id="3c88a-207">모델 상태 오류 처리</span><span class="sxs-lookup"><span data-stu-id="3c88a-207">Handle model state errors</span></span>

<span data-ttu-id="3c88a-208">[모델 유효성 검사](xref:mvc/models/validation)는 각 컨트롤러 작업을 호출하기 전에 발생하며, [ModelState.IsValid](xref:Microsoft.AspNetCore.Mvc.ModelBinding.ModelStateDictionary.IsValid)를 검사하고 적절하게 대응하는 것은 작업 메서드의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-208">[Model validation](xref:mvc/models/validation) occurs prior to invoking each controller action, and it's the action method's responsibility to inspect [ModelState.IsValid](xref:Microsoft.AspNetCore.Mvc.ModelBinding.ModelStateDictionary.IsValid) and react appropriately.</span></span>

<span data-ttu-id="3c88a-209">일부 앱은 [모델 유효성 검사](xref:mvc/models/validation) 오류를 처리하는 표준 규칙을 따르며, 이 경우 [필터](xref:mvc/controllers/filters)가 해당 정책을 구현하기에 적합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-209">Some apps choose to follow a standard convention for dealing with [model validation](xref:mvc/models/validation) errors, in which case a [filter](xref:mvc/controllers/filters) may be an appropriate place to implement such a policy.</span></span> <span data-ttu-id="3c88a-210">잘못된 모델 상태일 때 작업 동작 방식을 테스트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3c88a-210">You should test how your actions behave with invalid model states.</span></span> <span data-ttu-id="3c88a-211">자세한 내용은 <xref:mvc/controllers/testing>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3c88a-211">For more information, see <xref:mvc/controllers/testing>.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3c88a-212">추가 자료</span><span class="sxs-lookup"><span data-stu-id="3c88a-212">Additional resources</span></span>

* <xref:host-and-deploy/azure-iis-errors-reference>
* <xref:host-and-deploy/iis/troubleshoot>
* <xref:host-and-deploy/azure-apps/troubleshoot>
