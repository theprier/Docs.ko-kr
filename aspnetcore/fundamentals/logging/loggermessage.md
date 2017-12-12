---
title: "LoggerMessage ASP.NET 코어에서 사용한 고성능 로깅"
author: guardrex
description: "성능 로깅 시나리오에 대 한로 거 확장 방법 보다 더 적은 개체 할당을 필요로 하는 캐시 가능한 대리자를 만드는 LoggerMessage 기능을 사용 하는 방법을 알아봅니다."
ms.author: riande
manager: wpickett
ms.date: 11/03/2017
ms.topic: article
ms.technology: aspnet
ms.prod: asp.net-core
uid: fundamentals/logging/loggermessage
ms.openlocfilehash: defba75c6c9ea13d24af4cd8515d82d9e7cf9853
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
# <a name="high-performance-logging-with-loggermessage-in-aspnet-core"></a>LoggerMessage ASP.NET 코어에서 사용한 고성능 로깅

[Luke Latham](https://github.com/guardrex)으로

[LoggerMessage](/dotnet/api/microsoft.extensions.logging.loggermessage) 기능 더 적은 수의 개체 할당을 요구 하 고 보다 계산 오버 헤드가 감소 하는 캐시 가능한 대리자를 만드는 [로 거 확장 메서드](/dotnet/api/Microsoft.Extensions.Logging.LoggerExtensions)와 같은 `LogInformation`, `LogDebug`, 및 `LogError`. 성능 우선 로깅 시나리오를 사용 하는 `LoggerMessage` 패턴입니다.

`LoggerMessage`로 거 확장 방법에 비해 다음과 같은 성능 이점을 제공합니다.

* 로 거 확장 메서드는 "boxing" (변환) 값 형식 같은 필요할 `int`에 `object`합니다. `LoggerMessage` static을 사용 하 여 boxing를 방지 하는 패턴 `Action` 필드 및 강력한 형식의 매개 변수가 있는 확장 메서드입니다.
* 로 거 확장 메서드는 로그 메시지가 기록 됩니다 될 때마다 메시지 서식 파일 (명명 된 형식 문자열) 구문 분석 해야 합니다. `LoggerMessage`메시지 정의 된 경우 서식 파일을 한 번 구문 분석만 필요 합니다.

[샘플 코드 보기 또는 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/logging/loggermessage/sample/)([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

샘플 응용 프로그램을 보여 줍니다. `LoggerMessage` 기능 추적 시스템 기본 견적 합니다. 추가 하 고 메모리 내 데이터베이스를 사용 하 여 따옴표를 삭제 하는 응용 프로그램입니다. 이러한 작업이 발생 하는 대로 로그 메시지를 사용 하 여 생성 되는 `LoggerMessage` 패턴입니다.

## <a name="loggermessagedefine"></a>LoggerMessage.Define

[(LogLevel, EventId, String) 정의](/dotnet/api/microsoft.extensions.logging.loggermessage.define) 만듭니다는 `Action` 메시지를 기록 하는 데 대 한 delegate입니다. `Define`명명 된 형식 문자열 (템플릿)에 최대 6 개의 형식 매개 변수가 전달 허용 하는 오버 로드 합니다.

## <a name="loggermessagedefinescope"></a>LoggerMessage.DefineScope

[DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) 만듭니다는 `Func` 정의 하기 위한 대리자는 [범위 로그](xref:fundamentals/logging/index#log-scopes)합니다. `DefineScope`오버 로드 명명 된 형식 문자열 (템플릿)을 최대 3 개의 형식 매개 변수를 전달할 수 있습니다.

## <a name="message-template-named-format-string"></a>메시지 서식 파일 (명명 된 형식 문자열)

에 제공 하는 문자열은 `Define` 및 `DefineScope` methods는 템플릿과 보간된 문자열입니다. 자리 표시자는 형식 지정 된 순서에 채워집니다. 서식 파일에서 자리 표시자 이름 템플릿 전체 알기 쉽고 일치 해야 합니다. 구조적된 로그 데이터 내에서 속성 이름으로 사용 합니다. 권장 [파스칼식 대/소문자](/dotnet/standard/design-guidelines/capitalization-conventions) 자리 표시자 이름에 대 한 합니다. 예를 들어 `{Count}`, `{FirstName}`합니다.

## <a name="implementing-loggermessagedefine"></a>LoggerMessage.Define 구현

각 로그 메시지는 한 `Action` 가 만든 정적 필드에 보관 `LoggerMessage.Define`합니다. 예를 들어 샘플 응용 프로그램은 인덱스 페이지에 대 한 GET 요청에 대 한 로그 메시지를 설명 하는 필드를 만듭니다 (*Internal/LoggerExtensions.cs*):

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet1)]

에 대 한는 `Action`를 지정 합니다.

* 로그 수준입니다.
* 고유한 이벤트 식별자 ([EventId](/dotnet/api/microsoft.extensions.logging.eventid))와 정적 확장 메서드의 이름입니다.
* 메시지를 서식 파일 (명명 된 형식 문자열)입니다. 

샘플 응용 프로그램 집합의 인덱스 페이지에 대 한 요청에서:

* 로그 수준에 `Information`합니다.
* 이벤트 id를 `1` 의 이름으로는 `IndexPageRequested` 메서드.
* 메시지 서식 파일 (명명 된 형식 문자열)를 문자열로 합니다.

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet5)]

구조적된 로그 저장소 로깅 보강 하는 이벤트 id에 제공 될 경우 이벤트 이름을 사용할 수 있습니다. 예를 들어 [Serilog](https://github.com/serilog/serilog-extensions-logging) 이벤트 이름을 사용 합니다.

`Action` 강력한 형식의 확장 메서드를 통해 호출 됩니다. `IndexPageRequested` 샘플 응용 프로그램에서에서 인덱스 페이지 GET 요청에 대 한 메시지를 기록 하는 메서드:

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet9)]

`IndexPageRequested`로 거에 호출 됩니다는 `OnGetAsync` 메서드에서 *Pages/Index.cshtml.cs*:

[!code-csharp[Main](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet2&highlight=3)]

응용 프로그램의 콘솔 출력을 검사 합니다.

```console
info: LoggerMessageSample.Pages.IndexModel[1]
      => RequestId:0HL90M6E7PHK4:00000001 RequestPath:/ => /Index
      GET request for Index page
```

매개 변수는 로그 메시지를 전달 하려면 정적 필드를 만들 때 최대 6 개의 형식을 정의 합니다. 샘플 응용 프로그램을 정의 하 여 따옴표를 추가 하는 경우 문자열을 기록는 `string` 에 대 한 입력은 `Action` 필드:

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet2)]

대리자의 로그 메시지 서식 파일에서 제공 되는 형식을 해당 자리 표시자 값을 받습니다. 여기서 따옴표 매개 변수는 따옴표를 추가 하기 위한 대리자를 정의 하는 샘플 응용 프로그램을 `string`:

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet6)]

정적 확장 메서드는 따옴표를 추가 하는 데 `QuoteAdded`견적 인수 값을 받고, 전달 하는 `Action` 위임 합니다.

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet10)]

인덱스 페이지의 코드 숨김 파일 (*Pages/Index.cshtml.cs*), `QuoteAdded` 메시지를 기록 하기 위해 호출 됩니다.

[!code-csharp[Main](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet3&highlight=6)]

응용 프로그램의 콘솔 출력을 검사 합니다.

```console
info: LoggerMessageSample.Pages.IndexModel[2]
      => RequestId:0HL90M6E7PHK5:0000000A RequestPath:/ => /Index
      Quote added (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand')
```

샘플 응용 프로그램 구현 하는 `try` &ndash; `catch` 견적 삭제에 대 한 패턴입니다. 성공적으로 삭제 작업에 대 한 정보 메시지가 기록 됩니다. 예외가 throw 될 때 삭제 작업에 대 한 오류 메시지가 기록 됩니다. 로그 메시지는 실패 한 삭제 작업에 대 한 예외 스택 추적 포함 됩니다 (*Internal/LoggerExtensions.cs*):

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet3)]

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet7)]

예외에는 대리자에 전달 되는 방법을 확인 `QuoteDeleteFailed`:

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet11)]

인덱스 페이지 코드 숨김에서 성공적으로 견적 삭제 호출 되는 `QuoteDeleted` 메서드로 거를 합니다. 견적 삭제를 찾을 수 없을 때는 `ArgumentNullException` throw 됩니다. 예외를 트래핑 하 여는 `try` &ndash; `catch` 문을 호출 하 여 기록의 `QuoteDeleteFailed` 에 거에 대 한 메서드는 `catch` 블록 (*Pages/Index.cshtml.cs*):

[!code-csharp[Main](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet5&highlight=14,18)]

견적 성공적으로 삭제 하는 경우, 응용 프로그램의 콘솔 출력을 검사 합니다.

```console
info: LoggerMessageSample.Pages.IndexModel[4]
      => RequestId:0HL90M6E7PHK5:00000016 RequestPath:/ => /Index
      Quote deleted (Quote = 'You can avoid reality, but you cannot avoid the consequences of avoiding reality. - Ayn Rand' Id = 1)
```

견적 삭제에 실패 하면 응용 프로그램의 콘솔 출력을 검사 합니다. 예외는 로그 메시지에 포함 되어 있는지 참고:

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

## <a name="implementing-loggermessagedefinescope"></a>LoggerMessage.DefineScope 구현

정의 [범위 로그](xref:fundamentals/logging/index#log-scopes) 로그 메시지를 사용 하 여 계열에 적용 하는 [DefineScope(String)](/dotnet/api/microsoft.extensions.logging.loggermessage.definescope) 메서드.

샘플 응용 프로그램에는 **모두 지우기** 모든 데이터베이스에서 따옴표의 삭제에 대 한 단추입니다. 따옴표 하나 제거 하 여 삭제 한 번에 있습니다. 견적을 삭제할 때마다는 `QuoteDeleted` 로 거에 대해 메서드를 호출 합니다. 로그 범위를 이러한 로그 메시지에 추가 됩니다.

사용 하도록 설정 `IncludeScopes` 콘솔으로 거 옵션에서:

[!code-csharp[Main](loggermessage/sample/Program.cs?name=snippet1&highlight=22)]

설정 `IncludeScopes` 로그 범위를 사용 하려면 ASP.NET 코어 2.0 응용 프로그램에서 필요 합니다. 설정 `IncludeScopes` 통해 *appsettings* 구성 파일에는 ASP.NET Core 2.1 릴리스에 계획에 있는 기능입니다.

샘플 응용 프로그램에는 다른 공급자 지우고 로깅 출력을 줄이려면 필터를 추가 합니다. 이렇게 하면 보여 주는 샘플의 로그 메시지를 쉽게 `LoggerMessage` 기능입니다.

로그 범위를 만들려면를 보유 하는 필드를 추가 하는 `Func` 범위에 대 한 위임 합니다. 샘플 응용 프로그램 라는 필드를 만듭니다. `_allQuotesDeletedScope` (*Internal/LoggerExtensions.cs*):

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet4)]

사용 하 여 `DefineScope` 대리자입니다. 까지 세 가지 종류 지정할 수 있습니다 사용할 템플릿 인수로 대리자를 호출 하는 경우. 삭제 된 따옴표의 개수를 포함 하는 메시지 서식 파일을 사용 하 여 샘플 응용 프로그램 (한 `int` 유형):

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet8)]

로그 메시지에 대 한 정적 확장 메서드를 제공 합니다. 메시지 서식 파일에 표시 되는 명명 된 속성에 대 한 모든 형식 매개 변수를 포함 합니다. 샘플 응용 프로그램에서 사용 된 `count` 삭제 하는 따옴표 및 반환 `_allQuotesDeletedScope`:

[!code-csharp[Main](loggermessage/sample/Internal/LoggerExtensions.cs?name=snippet12)]

로깅 확장 호출 범위 래핑하는 `using` 블록:

[!code-csharp[Main](loggermessage/sample/Pages/Index.cshtml.cs?name=snippet4&highlight=5-6,14)]

응용 프로그램의 콘솔 출력에 있는 로그 메시지를 검사 합니다. 다음과 같은 결과가 포함 된 로그 범위 메시지와 함께 삭제 되는 세 가지 따옴표를 보여 줍니다.

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

## <a name="see-also"></a>참고 항목

* [로깅](xref:fundamentals/logging/index)
