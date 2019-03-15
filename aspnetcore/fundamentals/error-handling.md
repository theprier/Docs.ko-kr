---
title: ASP.NET Core에서 오류 처리
author: tdykstra
description: ASP.NET Core 앱에서 오류를 처리하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: tdykstra
ms.custom: mvc
ms.date: 03/05/2019
uid: fundamentals/error-handling
ms.openlocfilehash: d809c70b3fae6b2d21d5ec0871298d905b873d5d
ms.sourcegitcommit: 191d21c1e37b56f0df0187e795d9a56388bbf4c7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2019
ms.locfileid: "57665365"
---
# <a name="handle-errors-in-aspnet-core"></a>ASP.NET Core에서 오류 처리

작성자: [Tom Dykstra](https://github.com/tdykstra/), [Luke Latham](https://github.com/guardrex) 및 [Steve Smith](https://ardalis.com/)

이 문서에서는 ASP.NET Core 앱에서 오류를 처리하기 위한 일반적인 접근법을 다룹니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/samples/2.x) ([다운로드 방법](xref:index#how-to-download-a-sample))

## <a name="developer-exception-page"></a>개발자 예외 페이지

요청 예외에 대한 자세한 정보를 보여주는 페이지를 표시하는 앱을 구성하려면 개발자 예외 페이지를 사용합니다. [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 패키지가 사용할 수 있게 된 페이지는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에서 사용할 수 있습니다. 앱이 개발 [환경](xref:fundamentals/environments)에서 실행 중이면 `Startup.Configure` 메서드에 줄을 추가합니다.

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_UseDeveloperExceptionPage)]

예외를 catch하려는 미들웨어 앞에 <xref:Microsoft.AspNetCore.Builder.DeveloperExceptionPageExtensions.UseDeveloperExceptionPage*> 호출을 둡니다.

> [!WARNING]
> **앱이 개발 환경에서 실행 중인 경우에만** 개발자 예외 페이지를 사용하도록 설정합니다. 프로덕션 환경에서 앱을 실행할 때 자세한 예외 정보를 공개적으로 공유하지 않을 수도 있습니다. 환경 구성 방법에 대한 자세한 내용은 <xref:fundamentals/environments>를 참조하세요.

개발자 예외 페이지를 보려면 샘플 앱을 `Development`로 설정된 환경으로 실행하고, `?throw=true`를 앱의 기본 URL에 추가합니다. 페이지에는 예외 및 요청에 대한 다음 정보가 포함되어 있습니다.

* 스택 추적
* 쿼리 문자열 매개 변수(있는 경우)
* 쿠키(있는 경우)
* 헤더

## <a name="configure-a-custom-exception-handling-page"></a>사용자 지정 예외 처리 페이지 구성

개발 환경에서 앱이 실행되지 않는 경우 <xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*> 확장 메서드를 호출하여 예외 처리 미들웨어를 추가합니다. 미들웨어는 다음을 수행합니다.

* 예외를 catch합니다.
* 예외를 기록합니다.
* 대체 파이프라인에서 표시된 페이지 또는 컨트롤러에 대한 요청을 다시 실행합니다. 응답이 시작된 경우에는 요청이 다시 실행되지 않습니다.

샘플 앱의 다음 예제에서 <xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*>는 비개발 환경에 예외 처리 미들웨어를 추가합니다. 확장 메서드는 예외가 catch되고 기록된 후에 다시 실행된 요청에 대한 오류 페이지 또는 컨트롤러를 `/Error` 엔드포인트에 지정합니다.

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_UseExceptionHandler1)]

Razor Pages 앱 템플릿은 Pages 폴더에 오류 페이지(*.cshtml*) 및 <xref:Microsoft.AspNetCore.Mvc.RazorPages.PageModel> 클래스(`ErrorModel`)를 제공합니다.

MVC 앱에서는 다음 오류 처리기 메서드가 MVC 앱 템플릿에 포함되고 홈 컨트롤러에 표시됩니다.

```csharp
[AllowAnonymous]
public IActionResult Error()
{
    return View(new ErrorViewModel 
        { RequestId = Activity.Current?.Id ?? HttpContext.TraceIdentifier });
}
```

`HttpGet` 등의 HTTP 메서드 특성을 사용하여 오류 처리기 작업 메서드를 데코레이트하지 않습니다. 명시적 동사는 일부 요청이 메서드에 도달하지 않도록 방해합니다. 인증되지 않은 사용자가 오류 보기를 수신할 수 있도록 메서드에 대한 익명 액세스를 허용합니다.

## <a name="access-the-exception"></a>예외에 액세스

<xref:Microsoft.AspNetCore.Diagnostics.IExceptionHandlerPathFeature>를 사용하여 컨트롤러 또는 페이지의 예외 또는 원래 요청 경로에 액세스합니다.

* 경로는 <xref:Microsoft.AspNetCore.Diagnostics.IExceptionHandlerPathFeature.Path> 속성에서 확인할 수 있습니다.
* 상속된 [IExceptionHandlerFeature.Error](xref:Microsoft.AspNetCore.Diagnostics.IExceptionHandlerFeature.Error) 속성에서 <xref:System.Exception?displayProperty=fullName>을 읽습니다.

```csharp
// using Microsoft.AspNetCore.Diagnostics;

var exceptionHandlerPathFeature = 
    HttpContext.Features.Get<IExceptionHandlerPathFeature>();
var path = exceptionHandlerPathFeature?.Path;
var error = exceptionHandlerPathFeature?.Error;
```

> [!WARNING]
> <xref:Microsoft.AspNetCore.Diagnostics.IExceptionHandlerFeature> 또는 <xref:Microsoft.AspNetCore.Diagnostics.IExceptionHandlerPathFeature>에서 클라이언트로 중요한 오류 정보를 **제공하지 마세요**. 오류 제공은 보안 위험입니다.

## <a name="configure-custom-exception-handling-code"></a>사용자 지정 예외 처리 코드 구성

[사용자 지정 예외 처리 페이지](#configure-a-custom-exception-handling-page)의 오류에 대해 엔드포인트를 제공하는 대신 <xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*>에 람다를 제공합니다. <xref:Microsoft.AspNetCore.Builder.ExceptionHandlerExtensions.UseExceptionHandler*>에 람다를 사용하면 응답을 반환하기 전에 오류에 액세스할 수 있습니다.

샘플 앱에서는 `Startup.Configure`에서 사용자 지정 예외 처리 코드를 보여 줍니다. 인덱스 페이지의 **예외 Throw** 링크를 사용하여 예외를 트리거하세요. 다음 람다가 실행됩니다.

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_UseExceptionHandler2)]

> [!WARNING]
> <xref:Microsoft.AspNetCore.Diagnostics.IExceptionHandlerFeature> 또는 <xref:Microsoft.AspNetCore.Diagnostics.IExceptionHandlerPathFeature>에서 클라이언트로 중요한 오류 정보를 **제공하지 마세요**. 오류 제공은 보안 위험입니다.

## <a name="configure-status-code-pages"></a>상태 코드 페이지 구성

기본적으로 ASP.NET Core 앱은 ‘404 - 찾을 수 없음’과 같은 HTTP 상태 코드에 대한 상태 코드 페이지를 제공하지 않습니다. 앱에서 상태 코드와 빈 응답 본문을 반환합니다. 상태 코드 페이지를 제공하려면 상태 코드 페이지 미들웨어를 사용합니다.

[Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 패키지가 사용할 수 있게 된 미들웨어는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에서 사용할 수 있습니다.

`Startup.Configure` 메서드에 줄을 추가합니다.

```csharp
app.UseStatusCodePages();
```

요청 처리 미들웨어(예: 정적 파일 미들웨어 및 MVC 미들웨어) 전에 <xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePages*> 메서드를 호출합니다.

기본적으로 상태 코드 페이지 미들웨어는 ‘404 - 찾을 수 없음’과 같은 일반적인 상태 코드에 대한 텍스트 전용 처리기를 추가합니다.

```
Status Code: 404; Not Found
```

미들웨어는 해당 동작의 사용자 지정을 허용하는 여러 확장 메서드를 지원합니다.

<xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePages*>의 오버로드는 사용자 지정 오류 처리 논리를 처리하고 응답을 수동으로 작성하는 데 사용할 수 있는 람다 식을 받습니다.

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_StatusCodePages)]

<xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePages*>의 오버로드는 콘텐츠 형식 및 응답 텍스트를 사용자 지정하는 데 사용할 수 있는 콘텐츠 형식 및 형식 문자열을 받습니다.

```csharp
app.UseStatusCodePages("text/plain", "Status code page, status code: {0}");
```

### <a name="redirect-and-re-execute-extension-methods"></a>확장 메서드 리디렉션 및 다시 실행

<xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithRedirects*>:

* ‘302 - 있음’ 상태 코드를 클라이언트에 보냅니다. 
* 클라이언트를 URL 템플릿에 제공된 위치로 리디렉션합니다.

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_StatusCodePagesWithRedirect)]

<xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithRedirects*>는 일반적으로 앱이 다음과 같아야 하는 경우에 사용됩니다.

* 대체로 다른 앱이 오류를 처리하는 상황에서 앱이 클라이언트를 다른 엔드포인트로 리디렉션해야 하는 경우. 웹앱의 경우 클라이언트의 브라우저 주소 표시줄에 리디렉션된 엔드포인트가 반영됩니다.
* 원래 상태 코드를 유지하고 초기 리디렉션 응답과 함께 반환하면 안 되는 경우

<xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithReExecute*>:

* 원래 상태 코드를 클라이언트로 반환합니다.
* 대체 경로에서 요청 파이프라인을 다시 실행하여 응답 본문을 생성합니다.

```csharp
app.UseStatusCodePagesWithReExecute("/Error/{0}");
```

<xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePagesWithReExecute*>는 일반적으로 앱이 다음과 같아야 하는 경우에 사용됩니다.

* 다른 엔드포인트로 리디렉션하지 않고 요청을 처리해야 하는 경우. 웹앱의 경우 클라이언트의 브라우저 주소 표시줄에 원래 요청된 엔드포인트가 반영됩니다.
* 원래 상태 코드를 유지하고 응답과 함께 반환해야 하는 경우

템플릿에는 상태 코드에 대한 자리 표시자(`{0}`)가 포함될 수 있습니다. 템플릿은 슬래시(`/`)로 시작해야 합니다. 자리 표시자를 사용하는 경우, 엔드포인트(페이지 또는 컨트롤러)가 경로 세그먼트를 처리할 수 있는지 확인합니다. 예를 들어 오류에 대한 Razor 페이지가 `@page` 지시문을 사용한 선택적 경로 세그먼트 값을 수락해야 합니다.

```cshtml
@page "{code?}"
```

Razor 페이지 처리기 메서드 또는 MVC 컨트롤러에서 특정 요청에 대한 상태 코드 페이지를 비활성화할 수 있습니다. 상태 코드 페이지를 사용하지 않으려면 요청의 [HttpContext.Features](xref:Microsoft.AspNetCore.Http.HttpContext.Features) 컬렉션에서 <xref:Microsoft.AspNetCore.Diagnostics.IStatusCodePagesFeature>를 검색하고, 사용 가능한 경우 기능을 비활성화합니다.

```csharp
var statusCodePagesFeature = HttpContext.Features.Get<IStatusCodePagesFeature>();

if (statusCodePagesFeature != null)
{
    statusCodePagesFeature.Enabled = false;
}
```

앱 내에서 엔드포인트를 가리키는 <xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePages*> 오버로드를 사용하려면 엔드포인트에 대해 MVC 뷰 또는 Razor 페이지를 만듭니다. 예를 들어 Razor Pages 앱 템플릿은 다음 페이지와 페이지 모델 클래스를 생성합니다.

*Error.cshtml*:

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

*Error.cshtml.cs*:

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

*Error.cshtml.cs*:

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

## <a name="exception-handling-code"></a>예외 처리 코드

예외 처리 페이지의 코드는 예외를 throw할 수 있습니다. 종종 프로덕션 오류 페이지에 대해 완전한 정적 콘텐츠를 구성하는 것이 좋습니다.

또한 응답의 헤더가 전송되고 나면 다음 제한이 적용되는 것에 유의하세요.

* 앱에서 응답의 상태 코드를 변경할 수 없습니다.
* 예외 페이지 또는 처리기를 실행할 수 없습니다. 응답을 완료하거나 연결이 중단되어야 합니다.

## <a name="server-exception-handling"></a>서버 예외 처리

앱의 예외 처리 논리 외에도 [서버 구현](xref:fundamentals/servers/index)에서 몇 가지 예외를 처리할 수 있습니다. 응답 헤더가 전송되기 전에 예외를 catch한 서버는 응답 본문 없이 ‘500 - 내부 서버 오류’ 응답을 보냅니다. 응답 헤더가 전송된 후에 예외를 catch한 서버는 연결을 닫습니다. 앱으로 처리되지 않는 요청은 서버에서 처리됩니다. 서버에서 요청을 처리할 때 발생하는 모든 예외는 서버의 예외 처리에 의해 처리됩니다. 앱의 사용자 지정 오류 페이지, 예외 처리 미들웨어 및 필터는 이 동작에 영향을 미치지 않습니다.

## <a name="startup-exception-handling"></a>시작 예외 처리

호스팅 계층만 앱 시작 시 발생하는 예외를 처리할 수 있습니다. [웹 호스트](xref:fundamentals/host/web-host)를 사용하면 `captureStartupErrors` 및 `detailedErrors` 키로 [시작 시 오류에 대해 호스트가 응답하는 방법을 구성](xref:fundamentals/host/web-host#detailed-errors)할 수 있습니다.

호스팅은 호스트 주소/포트 바인딩 후에 오류가 발생하는 경우 캡처된 시작 오류에 대한 오류 페이지만 표시할 수 있습니다. 어떤 이유로든 바인딩에 실패하는 경우

* 호스팅 계층에서 심각한 예외를 기록합니다.
* dotnet 프로세스의 작동이 중단됩니다.
* [Kestrel](xref:fundamentals/servers/kestrel) 서버에서 앱을 실행 중일 때는 오류 페이지가 표시되지 않습니다.

[IIS](/iis) 또는 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)에서 실행 중일 때, 프로세스를 시작할 수 없는 경우 [ASP.NET Core 모듈](xref:host-and-deploy/aspnet-core-module)에서 *502.5 - 프로세스 실패*를 반환합니다. 자세한 내용은 <xref:host-and-deploy/iis/troubleshoot>을 참조하세요. Azure App Service의 시작 문제 해결에 대한 내용은 <xref:host-and-deploy/azure-apps/troubleshoot>을 참조하세요.

## <a name="aspnet-core-mvc-error-handling"></a>ASP.NET Core MVC 오류 처리

[MVC](xref:mvc/overview) 앱에는 예외 필터 구성 및 모델 유효성 검사 수행과 같이 오류를 처리하기 위한 몇 가지 추가 옵션이 있습니다.

### <a name="exception-filters"></a>예외 필터

전역으로 또는 MVC 앱에서 컨트롤러당 또는 작업당 기준으로 예외 필터를 구성할 수 있습니다. 이러한 필터는 컨트롤러 작업 또는 다른 필터를 실행하는 동안 발생하는 처리되지 않은 예외를 처리합니다. 그렇지 않으면 이러한 필터는 호출되지 않습니다. 자세한 내용은 <xref:mvc/controllers/filters#exception-filters>을 참조하세요.

> [!TIP]
> 예외 필터는 MVC 작업 내에서 발생하는 예외를 트래핑하는 데 유용하지만 예외 처리 미들웨어만큼 유연하지는 않습니다. 미들웨어를 사용하는 것이 좋습니다. 선택한 MVC 작업에 따라 오류 처리를 ‘다르게 수행’해야 하는 경우에만 필터를 사용합니다.

### <a name="handle-model-state-errors"></a>모델 상태 오류 처리

[모델 유효성 검사](xref:mvc/models/validation)는 각 컨트롤러 작업을 호출하기 전에 발생하며, [ModelState.IsValid](xref:Microsoft.AspNetCore.Mvc.ModelBinding.ModelStateDictionary.IsValid)를 검사하고 적절하게 대응하는 것은 작업 메서드의 책임입니다.

일부 앱은 [모델 유효성 검사](xref:mvc/models/validation) 오류를 처리하는 표준 규칙을 따르며, 이 경우 [필터](xref:mvc/controllers/filters)가 해당 정책을 구현하기에 적합할 수 있습니다. 잘못된 모델 상태일 때 작업 동작 방식을 테스트해야 합니다. 자세한 내용은 <xref:mvc/controllers/testing>을 참조하세요.

## <a name="additional-resources"></a>추가 자료

* <xref:host-and-deploy/azure-iis-errors-reference>
* <xref:host-and-deploy/iis/troubleshoot>
* <xref:host-and-deploy/azure-apps/troubleshoot>
