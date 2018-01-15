---
title: "ASP.NET Core의 오류 처리"
author: ardalis
description: "ASP.NET Core 응용 프로그램에서 오류를 처리 하는 방법을 알아봅니다."
keywords: "ASP.NET Core, 오류 처리, 예외 처리"
ms.author: tdykstra
manager: wpickett
ms.date: 11/30/2016
ms.topic: article
ms.assetid: 4db51023-c8a6-4119-bbbe-3917e272c260
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/error-handling
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: de2ba0ff9ad17c198c06b510ecfb49f808721bdf
ms.sourcegitcommit: 732cd2684246e49e796836596643a8d37e20c46d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2017
---
# <a name="introduction-to-error-handling-in-aspnet-core"></a>ASP.NET Core의 오류 처리

작성자: [Steve Smith](https://ardalis.com/) 및 [Tom Dykstra](https://github.com/tdykstra/)

본문에서는 ASP.NET Core 응용 프로그램에서 오류를 처리하는 일반적인 방법을 살펴봅니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/error-handling/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="the-developer-exception-page"></a>개발자 예외 페이지

자세한 예외 정보를 보여주는 오류 페이지를 표시하도록 응용 프로그램을 구성하려면, `Microsoft.AspNetCore.Diagnostics` NuGet 패키지를 설치하고 [Startup 클래스의 Configure 메서드](startup.md)에 다음과 같은 라인을 추가합니다.

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_DevExceptionPage&highlight=7)]

이때, `app.UseMvc` 같은 예외를 잡고자 하는 모든 미들웨어보다 `UseDeveloperExceptionPage`를 먼저 배치해야 합니다. 

>[!WARNING]
> 응용 프로그램이 **Development 환경에서 실행될 때만** 개발자 예외 페이지를 사용하도록 구성해야 합니다. 응용 프로그램이 프로덕션에서 실행될 때조차 공개적으로 상세한 예외 정보를 노출하고 싶지는 않을 것입니다. [다양한 환경에서 작업하는 방법](environments.md)에 관해서 더 자세히 알아보시기 바랍니다. 

개발자 예외 페이지를 확인해보려면, 예제 응용 프로그램의 환경을 `Development`로 설정하고 실행한 다음, 응용 프로그램의 기본 URL에 `?throw=true`를 추가합니다. 개발자 예외 페이지에서는 예외 및 요청에 대한 정보가 담긴 몇 가지 탭이 제공됩니다. 먼저 첫 번째 탭에는 스택 추적 정보가 제공됩니다. 

![스택 추적](error-handling/_static/developer-exception-page.png)

두 번째 탭에는 쿼리 문자열 매개 변수가 존재할 경우 모두 표시됩니다.

![쿼리 문자열 매개 변수](error-handling/_static/developer-exception-page-query.png)

이 요청에는 쿠키가 존재하지 않지만, 만약 존재하면 **Cookies** 탭에 표시됩니다. 그리고 마지막 탭에서는 전달된 헤더를 확인할 수 있습니다.

![헤더](error-handling/_static/developer-exception-page-headers.png)

## <a name="configuring-a-custom-exception-handling-page"></a>사용자 지정 예외 처리 페이지 구성하기

앱이 `Development` 환경에서 실행되지 않을 때는 예외 처리기 페이지를 구성해서 활용하는 것이 바람직합니다.

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_DevExceptionPage&highlight=11)]

이때 MVC 앱의 경우, 오류 처리기 액션 메서드에 명시적으로 `HttpGet` 같은 HTTP 메서드 어트리뷰트를 지정하면 안 됩니다. 명시적 동사를 지정하면 일부 요청이 메서드에 도달하지 못할 수도 있습니다.

```csharp
[Route("/Error")]
public IActionResult Index()
{
    // Handle error here
}
```

## <a name="configuring-status-code-pages"></a>상태 코드 페이지 구성하기

기본적으로 응용 프로그램에서는 500 (내부 서버 오류) 또는 404 (찾을 수 없음) 같은 HTTP 상태 코드에 대한 자세한 상태 코드 페이지를 제공하지 않습니다. 그러나 `Configure` 메서드에 다음과 같은 라인을 추가해서 `StatusCodePagesMiddleware`를 구성할 수 있습니다.

```csharp
app.UseStatusCodePages();
```

이 미들웨어는 기본적으로 404 같은 일반적인 상태 코드에 대한 단순한 텍스트 전용 처리기를 추가합니다.

![404 페이지](error-handling/_static/default-404-status-code.png)

이 미들웨어는 몇 가지 다른 확장 메서드도 지원합니다. 그중 한 버전은 람다 식을 전달받고, 또 다른 버전은 콘텐츠 형식 및 서식 문자열을 전달받습니다.  

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_StatusCodePages)]

```csharp
app.UseStatusCodePages("text/plain", "Status code page, status code: {0}");
```

리디렉션 확장 메서드도 제공됩니다. 한 메서드는 클라이언트에 302 상태 코드를 전송하고, 다른 메서드는 본래의 상태 코드를 클라이언트에 반환하지만 URL 리디렉션 처리기를 실행합니다.

[!code-csharp[Main](error-handling/sample/Startup.cs?name=snippet_StatusCodePagesWithRedirect)]

```csharp
app.UseStatusCodePagesWithReExecute("/error/{0}");
```

특정 요청에 대해 상태 코드 페이지를 비활성시키고 싶다면, 다음과 같이 처리할 수 있습니다.

```csharp
var statusCodePagesFeature = context.Features.Get<IStatusCodePagesFeature>();
if (statusCodePagesFeature != null)
{
    statusCodePagesFeature.Enabled = false;
}
```

## <a name="exception-handling-code"></a>예외 처리 코드

예외 처리 페이지의 코드에서도 예외는 발생할 수 있습니다. 따라서 프로덕션 오류 페이지는 순수한 정적 콘텐츠로 구성하는 것도 좋습니다. 

또한, 일단 응답 헤더를 전송하고 나면 응답의 상태 코드를 변경할 수 없으며, 어떠한 예외 페이지나 처리기도 실행될 수 없음에 유의하세요. 해당 응답은 완료되거나 연결 중단되어야 합니다.

## <a name="server-exception-handling"></a>서버 예외 처리

응용 프로그램의 예외 처리 로직뿐만 아니라, 응용 프로그램을 호스팅하는 [서버](servers/index.md)도 예외 처리를 일부 수행합니다. 서버는 헤더가 전송되기 전에 예외를 잡으면 본문 없이 500 내부 서버 오류 응답을 전송합니다. 반면 헤더가 전송된 이후에 예외를 잡으면 연결을 닫습니다. 앱에서 처리하지 않는 요청은 서버에 의해서 처리되며, 발생하는 모든 예외는 서버의 예외 처리 로직에 따라 처리됩니다. 응용 프로그램에 구성된 사용자 지정 오류 페이지나 예외 처리 미들웨어 또는 필터는 이 동작에 영향을 미치지 않습니다.

## <a name="startup-exception-handling"></a>시작 예외 처리

응용 프로그램을 시작하는 동안 발생하는 예외는 호스팅 계층에서만 처리가 가능합니다. `captureStartupErrors` 및 `detailedErrors` 키를 사용해서 [시작하는 동안 발생하는 오류에 대한 응답으로 호스트가 동작하는 방식](hosting.md#detailed-errors)을 구성할 수 있습니다.

호스팅은 호스트 주소/포트 바인딩 이후에 오류가 발생할 경우에만 캡처된 시작 오류에 대한 오류 페이지를 표시할 수 있습니다. 그러나 무슨 이유로든 모든 바인딩이 실패하면, 호스팅 계층이 심각한 예외를 로그에 기록하고, dotnet 프로세스가 중단되며, 아무런 오류 페이지도 표시되지 않습니다.

## <a name="aspnet-mvc-error-handling"></a>ASP.NET MVC 오류 처리

[MVC](../mvc/index.md) 응용 프로그램에서는 예외 필터 구성 및 모델 유효성 검사 같은 추가적인 오류 처리 옵션을 사용할 수 있습니다.

### <a name="exception-filters"></a>예외 필터

MVC 앱에서는 전역으로, 또는 컨트롤러 별이나 액션 별로 예외 필터를 구성할 수 있습니다. 이런 필터들은 컨트롤러 액션이나 다른 필터를 실행하는 동안 발생하는 처리되지 않은 예외를 처리하며, 그 외의 경우에는 호출되지 않습니다. 예외 필터에 관해서 [필터](../mvc/controllers/filters.md)에서 더 자세히 살펴보시기 바랍니다.

>[!TIP]
> 예외 필터는 MVC 액션에서 발생하는 예외를 처리하는 용도로는 적합하지만 오류 처리 미들웨어만큼 유연하지는 않습니다. 따라서 일반적인 상황에서는 미들웨어를 이용해서 예외를 처리하고, MVC 액션에 따라서 오류를 *다르게* 처리해야 하는 경우에만 필터를 사용하십시오.

### <a name="handling-model-state-errors"></a>모델 상태 오류 처리

[모델 유효성 검사](../mvc/models/validation.md)는 각 컨트롤러 액션이 호출되기 전에 발생하며, `ModelState.IsValid`를 검사해서 적절히 대응하는 것은 액션 메서드의 역할입니다. 

일부 앱은 표준 규칙에 따라 모델 유효성 검사 오류를 처리하는데, 이 경우 정책을 구현하기에 적절한 장소 중 하나가 바로 [필터](../mvc/controllers/filters.md)입니다. 이때 유효하지 않은 모델 상태에서 액션이 동작하는 방식을 테스트해야 합니다. 이에 관해서는 [컨트롤러 로직 테스트하기](../mvc/controllers/testing.md)를 참고하시기 바랍니다.
