---
title: ASP.NET Core에서 오류 처리
author: ardalis
description: ASP.NET Core 앱에서 오류를 처리하는 방법을 알아봅니다.
ms.author: tdykstra
ms.custom: mvc
ms.date: 07/05/2018
uid: fundamentals/error-handling
ms.openlocfilehash: d1e94fdc89fbebc264dc001bbf35666af16f4799
ms.sourcegitcommit: 375e9a67f5e1f7b0faaa056b4b46294cc70f55b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50208033"
---
# <a name="handle-errors-in-aspnet-core"></a>ASP.NET Core에서 오류 처리

작성자: [Steve Smith](https://ardalis.com/) 및 [Tom Dykstra](https://github.com/tdykstra/)

이 문서에서는 ASP.NET Core 앱에서 오류를 처리하기 위한 일반적인 접근법을 다룹니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/samples/2.x/ErrorHandlingSample)([다운로드 방법](xref:index#how-to-download-a-sample))

## <a name="the-developer-exception-page"></a>개발자 예외 페이지

::: moniker range=">= aspnetcore-2.1"

예외에 대한 자세한 정보를 보여주는 페이지를 표시하는 앱을 구성하려면 *개발자 예외 페이지*를 사용합니다. [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 패키지가 사용할 수 있게 된 페이지는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에서 사용할 수 있습니다. `Startup.Configure` 메서드에 줄을 추가합니다.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

예외에 대한 자세한 정보를 보여주는 페이지를 표시하는 앱을 구성하려면 *개발자 예외 페이지*를 사용합니다. [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 패키지가 사용할 수 있게 된 페이지는 [Microsoft.AspNetCore.All 메타 패키지](xref:fundamentals/metapackage)에서 사용할 수 있습니다. `Startup.Configure` 메서드에 줄을 추가합니다.

::: moniker-end

::: moniker range="< aspnetcore-2.0"

예외에 대한 자세한 정보를 보여주는 페이지를 표시하는 앱을 구성하려면 *개발자 예외 페이지*를 사용합니다. 프로젝트 파일 내 [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 패키지에 대한 패키지 참조를 추가하여 해당 페이지를 사용할 수 있습니다. `Startup.Configure` 메서드에 줄을 추가합니다.

::: moniker-end

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_DevExceptionPage&highlight=7)]

`app.UseMvc`과 같은 예외를 캐치하려는 미들웨어 앞에 [UseDeveloperExceptionPage](/dotnet/api/microsoft.aspnetcore.builder.developerexceptionpageextensions.usedeveloperexceptionpage) 호출을 둡니다.

> [!WARNING]
> **앱이 개발 환경에서 실행 중인 경우에만** 개발자 예외 페이지를 사용하도록 설정합니다. 프로덕션 환경에서 앱을 실행할 때 자세한 예외 정보를 공개적으로 공유하지 않을 수도 있습니다. [구성 환경에 대해 자세히 알아보세요](xref:fundamentals/environments).

개발자 예외 페이지를 보려면 샘플 앱을 `Development`로 설정된 환경으로 실행하고, `?throw=true`를 앱의 기본 URL에 추가합니다. 페이지에는 예외 및 요청에 대한 정보가 있는 여러 탭이 포함되어 있습니다. 첫 번째 탭에는 스택 추적이 포함됩니다.

![스택 추적](error-handling/_static/developer-exception-page.png)

쿼리 문자열 매개 변수가 있는 경우 다음 탭에 표시됩니다.

![쿼리 문자열 매개 변수](error-handling/_static/developer-exception-page-query.png)

요청에 쿠키가 있는 경우 **쿠키** 탭에 표시됩니다. 헤더는 마지막 탭에 표시됩니다.

![헤더](error-handling/_static/developer-exception-page-headers.png)

## <a name="configure-a-custom-exception-handling-page"></a>사용자 지정 예외 처리 페이지 구성

앱이 `Development` 환경에서 실행되고 있지 않는 경우 사용할 예외 처리기 페이지를 구성합니다.

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_DevExceptionPage&highlight=11)]

Razor Pages 앱에서 [dotnet new](/dotnet/core/tools/dotnet-new) Razor Pages 템플릿은 *Pages* 폴더의 오류 페이지 및 오류 `PageModel` 클래스를 제공합니다.

MVC 앱에서는 `HttpGet`과 같은 HTTP 메서드 특성을 사용하여 오류 처리기 작업 메서드를 데코레이트하지 않습니다. 명시적 동사는 일부 요청이 메서드에 도달하지 않도록 방해합니다. 인증되지 않은 사용자가 오류 보기를 수신할 수 있도록 메서드에 대한 익명 액세스를 허용합니다.

예를 들어 다음 오류 처리기 메서드는 [dotnet new](/dotnet/core/tools/dotnet-new) MVC 템플릿에서 제공하고 홈 컨트롤러에 표시됩니다.

```csharp
[AllowAnonymous]
public IActionResult Error()
{
    return View(new ErrorViewModel 
        { RequestId = Activity.Current?.Id ?? HttpContext.TraceIdentifier });
}
```

## <a name="configure-status-code-pages"></a>상태 코드 페이지 구성

기본적으로 앱은 *404 찾을 수 없음*과 같은 HTTP 상태 코드에 대한 다양한 상태 코드 페이지를 제공하지 않습니다. 상태 코드 페이지를 제공하려면 상태 코드 페이지 미들웨어를 사용합니다.

::: moniker range=">= aspnetcore-2.1"

[Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 패키지가 사용할 수 있게 된 미들웨어는 [Microsoft.AspNetCore.App 메타패키지](xref:fundamentals/metapackage-app)에서 사용할 수 있습니다.

::: moniker-end

::: moniker range="= aspnetcore-2.0"

[Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 패키지가 사용할 수 있게 된 미들웨어는 [Microsoft.AspNetCore.AII 메타패키지](xref:fundamentals/metapackage)에서 사용할 수 있습니다.

::: moniker-end

::: moniker range="< aspnetcore-2.0"

프로젝트 파일 내 [Microsoft.AspNetCore.Diagnostics](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics/) 패키지에 대한 패키지 참조를 추가하여 미들웨어를 사용할 수 있습니다.

::: moniker-end

`Startup.Configure` 메서드에 줄을 추가합니다.

```csharp
app.UseStatusCodePages();
```

<xref:Microsoft.AspNetCore.Builder.StatusCodePagesExtensions.UseStatusCodePages*>는 파이프라인에서 요청 처리 미들웨어(예: 정적 파일 미들웨어 및 MVC 미들웨어) 전에 호출해야 합니다.

기본적으로 상태 코드 페이지 미들웨어는 404와 같은 일반적인 상태 코드에 대한 텍스트 전용 처리기를 추가합니다.

![404 페이지](error-handling/_static/default-404-status-code.png)

미들웨어는 몇 가지 확장 메서드를 지원합니다. 한 가지 메서드는 람다 식을 사용합니다.

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_StatusCodePages)]

또 다른 메서드는 콘텐츠 형식 및 형식 문자열을 사용합니다.

```csharp
app.UseStatusCodePages("text/plain", "Status code page, status code: {0}");
```

또한 리디렉션 및 다시 실행 확장 메서드도 있습니다. 리디렉션 메서드는 *302 있음* 상태 코드를 클라이언트에 보내서 클라이언트를 제공된 위치 URL 템플릿으로 리디렉션합니다. 템플릿에는 상태 코드에 대한 `{0}` 자리 표시자가 포함될 수 있습니다. `~`로 시작되는 URL 앞에는 기본 경로가 추가됩니다. `~`로 시작하지 않는 URL은 그대로 사용됩니다.

[!code-csharp[](error-handling/samples/2.x/ErrorHandlingSample/Startup.cs?name=snippet_StatusCodePagesWithRedirect)]

다시 실행 메서드는 원래 상태 코드를 클라이언트에 반환하고 대체 경로를 사용하여 요청 파이프 라인을 다시 실행하여 응답 본문이 생성되도록 지정합니다. 이 경로에는 상태 코드에 대한 `{0}` 자리 표시자가 포함될 수 있습니다.

```csharp
app.UseStatusCodePagesWithReExecute("/error/{0}");
```

Razor 페이지 처리기 메서드 또는 MVC 컨트롤러에서 특정 요청에 대한 상태 코드 페이지를 비활성화할 수 있습니다. 상태 코드 페이지를 비활성화하려면 요청의 [HttpContext.Features](/dotnet/api/microsoft.aspnetcore.http.httpcontext.features) 컬렉션에서 [IStatusCodePagesFeature](/dotnet/api/microsoft.aspnetcore.diagnostics.istatuscodepagesfeature)를 검색하고 사용 가능한 경우 기능을 비활성합니다.

```csharp
var statusCodePagesFeature = HttpContext.Features.Get<IStatusCodePagesFeature>();

if (statusCodePagesFeature != null)
{
    statusCodePagesFeature.Enabled = false;
}
```

앱 내에서 엔드포인트를 가리키는 `UseStatusCodePages*`를 사용하는 경우 엔드포인트에 대해 MVC 보기 또는 Razor Page를 만듭니다. 예를 들어 Razor Pages 앱의 [dotnet new](/dotnet/core/tools/dotnet-new) 템플릿은 다음 페이지와 페이지 모델 클래스를 생성합니다.

*Error.cshtml*:

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

## <a name="exception-handling-code"></a>예외 처리 코드

예외 처리 페이지의 코드는 예외를 throw할 수 있습니다. 종종 프로덕션 오류 페이지에 대해 완전한 정적 콘텐츠를 구성하는 것이 좋습니다.

또한 일단 응답에 대한 헤더를 보내고 나면 응답의 상태 코드, 예외 페이지 또는 처리기 실행을 변경할 수 없다는 점에 유의하세요. 응답을 완료하거나 연결이 중단되어야 합니다.

## <a name="server-exception-handling"></a>서버 예외 처리

앱에서 논리를 처리하는 예외뿐 아니라 앱을 호스팅하는 [서버](xref:fundamentals/servers/index)는 몇 가지 예외 처리를 수행합니다. 헤더를 보내기 전에 서버가 예외를 catch하는 경우 서버는 본문이 없는 *500 내부 서버 오류* 응답을 보냅니다. 헤더를 보낸 후에 서버가 예외를 catch하는 경우 서버는 연결을 닫습니다. 앱으로 처리되지 않는 요청은 서버에서 처리됩니다. 발생하는 모든 예외는 서버의 예외 처리에 의해 처리됩니다. 구성된 모든 사용자 지정 오류 페이지 또는 예외 처리 미들웨어 또는 필터는 이 동작에 영향을 미치지 않습니다.

## <a name="startup-exception-handling"></a>시작 예외 처리

호스팅 계층만 앱 시작 시 발생하는 예외를 처리할 수 있습니다. [웹 호스트](xref:fundamentals/host/web-host)를 사용하면 `captureStartupErrors` 및 `detailedErrors` 키로 [시작 시 오류에 대해 호스트가 응답하는 방법을 구성](xref:fundamentals/host/web-host#detailed-errors)할 수 있습니다.

호스팅은 호스트 주소/포트 바인딩 후에 오류가 발생하는 경우 캡처된 시작 오류에 대한 오류 페이지만 표시할 수 있습니다. 어떤 이유로 바인딩이 실패한 경우 호스팅 계층이 심각한 예외를 기록하고, dotnet 프로세스가 충돌하며, 앱이 [Kestrel](xref:fundamentals/servers/kestrel) 서버에서 실행 중일 때 오류 페이지가 표시되지 않습니다.

[IIS](/iis) 또는 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)에서 실행 중일 때, 프로세스를 시작할 수 없는 경우 [ASP.NET Core 모듈](xref:fundamentals/servers/aspnet-core-module)에서 *502.5 프로세스 실패*를 반환합니다. IIS를 사용하여 호스팅할 때 시작 문제 해결에 대한 내용은 <xref:host-and-deploy/iis/troubleshoot>을 참조하세요. Azure App Service의 시작 문제 해결에 대한 내용은 <xref:host-and-deploy/azure-apps/troubleshoot>을 참조하세요.

## <a name="aspnet-core-mvc-error-handling"></a>ASP.NET Core MVC 오류 처리

[MVC](xref:mvc/overview) 앱에는 예외 필터 구성 및 모델 유효성 검사 수행과 같이 오류를 처리하기 위한 몇 가지 추가 옵션이 있습니다.

### <a name="exception-filters"></a>예외 필터

전역으로 또는 MVC 앱에서 컨트롤러당 또는 작업당 기준으로 예외 필터를 구성할 수 있습니다. 이러한 필터는 컨트롤러 작업 또는 다른 필터를 실행하는 동안 발생하는 처리되지 않은 예외를 처리합니다. 그렇지 않으면 이러한 필터는 호출되지 않습니다. 자세한 내용은 [필터](xref:mvc/controllers/filters)를 참조하세요.

> [!TIP]
> 예외 필터는 MVC 작업 내에서 발생하는 예외를 트래핑하는 데 유용하지만 오류 처리 미들웨어만큼 유연하지는 않습니다. 일반적인 경우에는 미들웨어를 선호하고, 선택한 MVC 작업에 따라 오류 처리를 *다르게* 해야 하는 경우에만 필터를 사용합니다.

### <a name="handling-model-state-errors"></a>모델 상태 오류 처리

[모델 유효성 검사](xref:mvc/models/validation)는 각 컨트롤러 작업을 호출하기 전에 발생하며, `ModelState.IsValid`를 검사하고 적절하게 반응하는 것은 작업 메서드의 책임입니다.

[필터](xref:mvc/controllers/filters)가 이러한 정책을 구현하기에 적절한 경우에 일부 앱은 모델 유효성 검사 오류를 처리하는 표준 규칙을 따르도록 선택합니다. 잘못된 모델 상태일 때 작업 동작 방식을 테스트해야 합니다. [컨트롤러 논리 테스트](xref:mvc/controllers/testing)에서 자세히 알아보세요.

## <a name="additional-resources"></a>추가 자료

* <xref:host-and-deploy/azure-iis-errors-reference>
* <xref:host-and-deploy/iis/troubleshoot>
* <xref:host-and-deploy/azure-apps/troubleshoot>
