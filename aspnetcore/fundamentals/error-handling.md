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
# <a name="introduction-to-error-handling-in-aspnet-core"></a>ASP.NET Core에서 오류 처리 소개

작성자: [Steve Smith](https://ardalis.com/) 및 [Tom Dykstra](https://github.com/tdykstra/)

이 문서에서는 ASP.NET Core 앱에서 오류를 처리하기 위한 일반적인 접근법을 다룹니다.

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/sample)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="the-developer-exception-page"></a>개발자 예외 페이지

예외에 대한 자세한 정보가 있는 페이지를 표시하도록 응용 프로그램을 구성하려면 `Microsoft.AspNetCore.Diagnostics` NuGet 패키지를 설치하고 줄을 [시작 클래스에서 메서드를 구성](startup.md)에 추가합니다.

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_DevExceptionPage&highlight=7)]

`app.UseMvc`와 같은 예외를 catch하려는 모든 미들웨어 앞에 `UseDeveloperExceptionPage`를 배치합니다.

>[!WARNING]
> **앱이 개발 환경에서 실행 중인 경우에만** 개발자 예외 페이지를 사용하도록 설정합니다. 프로덕션 환경에서 앱을 실행할 때 자세한 예외 정보를 공개적으로 공유하지 않을 수도 있습니다. [구성 환경에 대해 자세히 알아보세요](environments.md).

개발자 예외 페이지를 보려면 샘플 응용 프로그램을 `Development`로 설정된 환경으로 실행하고, `?throw=true`를 앱의 기본 URL에 추가합니다. 페이지에는 예외 및 요청에 대한 정보가 있는 여러 탭이 포함되어 있습니다. 첫 번째 탭에는 스택 추적이 포함됩니다. 

![스택 추적](error-handling/_static/developer-exception-page.png)

쿼리 문자열 매개 변수가 있는 경우 다음 탭에 표시됩니다.

![쿼리 문자열 매개 변수](error-handling/_static/developer-exception-page-query.png)

이 요청에는 쿠키가 없지만, 만약 있는 경우 **쿠키** 탭에 표시됩니다. 마지막 탭에서 전달된 헤더를 볼 수 있습니다.

![헤더](error-handling/_static/developer-exception-page-headers.png)

## <a name="configuring-a-custom-exception-handling-page"></a>사용자 지정 예외 처리 페이지 구성

앱이 `Development` 환경에서 실행되고 있지 않는 경우 사용할 예외 처리기 페이지를 구성하는 것이 좋습니다.

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_DevExceptionPage&highlight=11)]

MVC 앱에서는 `HttpGet`과 같은 HTTP 메서드 특성을 사용하여 오류 처리기 작업 메서드를 명시적으로 데코레이트하지 마십시오. 명시적 동사를 사용하면 일부 요청이 메서드에 도달하지 못할 수 있습니다.

```csharp
[Route("/Error")]
public IActionResult Index()
{
    // Handle error here
}
```

## <a name="configuring-status-code-pages"></a>상태 코드 페이지 구성

기본적으로 앱은 500(내부 서버 오류) 또는 404(찾을 수 없음)와 같은 HTTP 상태 코드에 대한 다양한 상태 코드 페이지를 제공하지 않습니다. `Configure` 메서드에 줄을 추가하여 `StatusCodePagesMiddleware`를 구성할 수 있습니다.

```csharp
app.UseStatusCodePages();
```

기본적으로 이 미들웨어는 404와 같이 일반적인 상태 코드에 대한 간단한 텍스트 전용 처리기를 추가합니다.

![404 페이지](error-handling/_static/default-404-status-code.png)

미들웨어는 몇 가지 다양한 확장 메서드를 지원합니다. 람다 식에서 사용하기도 하고, 콘텐츠 형식 및 형식 문자열을 사용하기도 합니다.

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_StatusCodePages)]

```csharp
app.UseStatusCodePages("text/plain", "Status code page, status code: {0}");
```

리디렉션 확장 메서드도 있습니다. 302 상태 코드를 클라이언트에 보내기도 하고, 클라이언트에 원래 상태 코드를 반환하면서 리디렉션 URL에 대한 처리기를 실행하기도 합니다.

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_StatusCodePagesWithRedirect)]

```csharp
app.UseStatusCodePagesWithReExecute("/error/{0}");
```

특정 요청에 대한 상태 코드 페이지를 사용하지 않도록 설정해야 하는 경우 그렇게 할 수 있습니다.

```csharp
var statusCodePagesFeature = context.Features.Get<IStatusCodePagesFeature>();
if (statusCodePagesFeature != null)
{
  statusCodePagesFeature.Enabled = false;
}
```

## <a name="exception-handling-code"></a>예외 처리 코드

예외 처리 페이지의 코드는 예외를 throw할 수 있습니다. 종종 프로덕션 오류 페이지에 대해 완전한 정적 콘텐츠를 구성하는 것이 좋습니다.

또한 일단 응답에 대한 헤더를 보내고 나면 응답의 상태 코드, 예외 페이지 또는 처리기 실행을 변경할 수 없다는 점에 유의하세요. 응답을 완료하거나 연결이 중단되어야 합니다.

## <a name="server-exception-handling"></a>서버 예외 처리

앱에서 논리를 처리하는 예외뿐 아니라 앱을 호스팅하는 [서버](servers/index.md)는 몇 가지 예외 처리를 수행합니다. 헤더를 보내기 전에 서버가 예외를 catch하는 경우 서버는 본문이 없는 500 내부 서버 오류 응답을 보냅니다. 헤더를 보낸 후에 서버가 예외를 catch하는 경우 서버는 연결을 닫습니다. 앱으로 처리되지 않는 요청은 서버에서 처리됩니다. 발생하는 모든 예외는 서버의 예외 처리에 의해 처리됩니다. 구성된 모든 사용자 지정 오류 페이지 또는 예외 처리 미들웨어 또는 필터는 이 동작에 영향을 미치지 않습니다.

## <a name="startup-exception-handling"></a>시작 예외 처리

호스팅 계층만 앱 시작 시 발생하는 예외를 처리할 수 있습니다. `captureStartupErrors` 및 `detailedErrors` 키를 사용하여 [시작 시 오류에 대해 응답의 호스트가 동작하는 방법을 구성](hosting.md#detailed-errors)할 수 있습니다.

호스팅은 호스트 주소/포트 바인딩 후에 오류가 발생하는 경우 캡처된 시작 오류에 대한 오류 페이지만 표시할 수 있습니다. 어떤 이유로 바인딩이 실패한 경우 호스팅 계층은 중요한 예외를 로그하고, dotnet 프로세스가 충돌하며, 오류 페이지가 표시되지 않습니다.

## <a name="aspnet-mvc-error-handling"></a>ASP.NET MVC 오류 처리

[MVC](xref:mvc/overview) 앱에는 예외 필터 구성 및 모델 유효성 검사 수행과 같이 오류를 처리하기 위한 몇 가지 추가 옵션이 있습니다.

### <a name="exception-filters"></a>예외 필터

전역으로 또는 MVC 앱에서 컨트롤러당 또는 작업당 기준으로 예외 필터를 구성할 수 있습니다. 이러한 필터는 컨트롤러 작업 또는 다른 필터를 실행하는 동안 발생하는 처리되지 않은 예외를 처리하며, 그 외에는 호출되지 않습니다. [필터](../mvc/controllers/filters.md)에서 예외 필터에 대해 자세히 알아보세요.

>[!TIP]
> 예외 필터는 MVC 작업 내에서 발생하는 예외를 트래핑하는 데 유용하지만 오류 처리 미들웨어만큼 유연하지는 않습니다. 일반적인 경우에는 미들웨어를 선호하고, 선택한 MVC 작업에 따라 오류 처리를 *다르게* 수행해야 하는 경우에만 필터를 사용합니다.

### <a name="handling-model-state-errors"></a>모델 상태 오류 처리

[모델 유효성 검사](../mvc/models/validation.md)는 각 컨트롤러 작업을 호출하기 전에 발생하며, `ModelState.IsValid`를 검사하고 적절하게 반응하는 것은 작업 메서드의 책임입니다.

[필터](../mvc/controllers/filters.md)가 그러한 정책을 구현하기에 적절한 경우에 일부 앱은 모델 유효성 검사 오류를 처리하는 데 표준 규칙을 따르도록 선택합니다. 잘못된 모델 상태일 때 작업 동작 방식을 테스트해야 합니다. [컨트롤러 논리 테스트](../mvc/controllers/testing.md)에서 자세히 알아보세요.



