---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: ASP.NET Web API 2에서에서 전역 오류 처리 | Microsoft Docs
author: davidmatson
description: ''
ms.author: riande
ms.date: 02/03/2014
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 3e371760d2b34eb2be492e6ebbb33a5f9f7eff10
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48577173"
---
<a name="global-error-handling-in-aspnet-web-api-2"></a>ASP.NET Web API 2에서에서 전역 오류 처리
====================
하 여 [David Matson](https://github.com/davidmatson), [Rick Anderson]((https://twitter.com/RickAndMSFT))

지금 로그인 하거나 전역 오류 처리를 Web API에서 쉽지가 않습니다. 통해 일부 처리 되지 않은 예외를 처리할 수 있습니다 [예외 필터](exception-handling.md), 되지만 많은 예외 필터에서 처리할 수 없는 경우. 예를 들어:

1. 컨트롤러 생성자에서 throw 된 예외입니다.
2. 메시지 처리기에서 throw 된 예외입니다.
3. 라우팅 중에 throw 된 예외입니다.
4. 응답 콘텐츠를 직렬화 하는 동안 throw 된 예외입니다.

로그 (사용 가능한) 위치를 처리 하는 간단 하 고 일관 된 방법을 제공 하려고 합니다. 이러한 예외입니다. 

두 가지 주요 오류 응답을 보낼 수 있는 모든 수행할 수 있습니다 하는 경우는 예외를 로그 경우 예외를 처리 합니다. 후자의 경우에 대 한 예로 응답 콘텐츠를 스트리밍 도중 예외가 발생 하는 경우 에 경우에 너무 늦게 상태 코드, 헤더 및 부분 콘텐츠를 이미 완료를 통해 연결 중단 되므로 이후 새 응답 메시지를 보내려고 합니다. 예외를 처리 하 여 새 응답 메시지를 생성할 수 없습니다, 경우에 계속 지원 예외를 기록 합니다. 오류를 감지할 수 있는 경우에는 다음과 같이 적절 한 오류 응답을 반환할 수 있습니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>기존 옵션

외에 [예외 필터](exception-handling.md)하십시오 [메시지 처리기](../advanced/http-message-handlers.md) 모든 500 수준 응답을 관찰 하려면 지금 사용할 수 있지만 해당 응답에서 작업은 어렵고, 원래 오류에 대 한 컨텍스트 부족 하기. 메시지 처리기 수도 일부 처리할 수 있도록 하는 경우에 대 한 예외 필터와 동일한 제한 사항이 있습니다. Web API는 오류 상태를 캡처하는 추적 인프라는 추적 인프라는 진단 용도로 및 하지 설계 되었거나 프로덕션 환경에서 실행 하는 것에 대 한 적합 한. 전역 예외 처리 및 로깅 서비스를 프로덕션 하는 동안 실행할 수 있으며 기존 모니터링 솔루션에 연결할 수 있어야 합니다. (예를 들어 [ELMAH](https://code.google.com/p/elmah/) ).

### <a name="solution-overview"></a>솔루션 개요

 두 가지 새로운 사용자를 대체할 수 있는 서비스를 제공 하 고 [IExceptionLogger](../releases/whats-new-in-aspnet-web-api-21.md) 및 IExceptionHandler, 로그 및 처리 되지 않은 예외를 처리 합니다. 서비스는 매우 비슷하지만 두 가지 주요 차이점:

1. 여러 예외로 거 하지만 한 개의 예외 처리기 등록을 지원 합니다.
2. 예외로 거 항상 호출 연결을 중단 하려고 하는 경우에 합니다. 예외 처리기만 호출 보낼 응답 메시지를 선택할 수 있을 때.

예외가 발견 된 지점에서 관련 정보를 포함 하는 예외 컨텍스트에 대 한 액세스를 제공 하는 두 서비스 특히 [HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx)는 [HttpRequestContext](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx), 예외 및 예외 소스 (아래 세부 정보)를 발생 합니다.

### <a name="design-principles"></a>디자인 원칙

1. **주요 변경 내용이 없습니다** 하나 솔루션에 영향을 주는 중요 한 제약 조건이 있을 다음 주요 변경 내용이 없습니다, 계약 형식 중 하나는 릴리스 또는 동작에이 기능을 추가 중인 되기 때문에 있습니다. 이 제약 조건은 측면 500 응답으로 예외를 설정 하는 기존 catch 블록에서 완료 하고자 하는 몇 가지 정리를 제외 합니다. 이 추가 정리는 후속 버전에 대 한 것으로 간주 될 수 있습니다. 이 작업이 중요 한 경우에 대해 투표 하세요 [ASP.NET Web API 사용자 의견](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception)합니다.
2. **Web API를 사용 하 여 일관성을 유지 관리를 생성** Web API의 필터 파이프라인은 작업별, 컨트롤러 또는 전역 범위에서 논리를 적용 하는 유연 하 게 교차 편집 문제를 처리 하는 훌륭한 방법입니다. 예외 필터를 포함 하 여 필터를 전역 범위에 등록 하는 경우에 항상 작업 및 컨트롤러 컨텍스트를 가집니다. 계약에 적합 한 필터는 예외 필터도 전역 범위가 지정 된 된 작업 또는 컨트롤러 컨텍스트가 없는 경우 메시지 처리기에서 예외와 같은 경우를 처리 하는 몇 가지 예외에 대 한 적합 하지는 것이 있습니다. 예외 처리에 대 한 필터에서 제공 하 여 유연한 범위를 사용 하고자 하는 경우 예외 필터 여전히 필요 합니다. 하지만, 컨트롤러 컨텍스트 외부에서 예외를 처리 해야 하는 경우도 별도 구문 (것은 컨트롤러 컨텍스트 및 작업 상황에 맞는 제약 없이) 전역 오류 처리에 대 한 합니다.

### <a name="when-to-use"></a>사용 하는 경우

- 예외로 거는 Web API에서 발생 하는 모든 처리 되지 않은 예외를 보는 데 솔루션입니다.
- 예외 처리기는 Web API에서 발생 한 처리 되지 않은 예외에 대 한 모든 가능한 응답을 사용자 지정 하기 위한 솔루션입니다.
- 예외 필터는 특정 작업 또는 컨트롤러와 관련 된 하위 집합 처리 되지 않은 예외 처리를 위한 가장 간단한 해결책입니다.

### <a name="service-details"></a>서비스 세부 정보

 예외로 거 및 처리기 서비스 인터페이스를 해당 컨텍스트는 간단한 비동기 메서드의 같습니다. 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 이러한 인터페이스 둘 다에 대 한 기본 클래스도 제공 합니다. 코어 (동기 또는 비동기) 메서드를 재정의 로그 또는 처리 권장 하는 데 필요한 시간. 로깅에 대 한는 `ExceptionLogger` 는 core 로깅 메서드는 한 번만 호출 각 예외에 대 한 기본 클래스는 확인 (나중에 전파 하는 경우에 추가 호출 스택 및이 다시 발생). `ExceptionHandler` 중첩 레거시 무시 하 고, 호출 스택의 맨 위에 있는 예외 catch 블록에 대해서만 메서드를 처리 하는 코어를 호출 하는 기본 클래스입니다. (이러한 기본 클래스의 간소화 된 버전의에서 경우 아래 부록) 둘 다 `IExceptionLogger` 하 고 `IExceptionHandler` 를 통해 예외에 대 한 정보를 받을 `ExceptionContext`합니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

항상 제공 프레임 워크 예외로 거를 또는 예외 처리기를 호출 하는 경우는 `Exception` 및 `Request`합니다. 단위 테스트를 제외 하 고 항상 제공 된 `RequestContext`합니다. 거의 제공 된 `ControllerContext` 및 `ActionContext` (경우에 예외 필터에 대 한 catch 블록에서 호출). 거의 제공을 `Response`(에서만, 응답을 기록 하는 동안 중간 IIS 경우도). 이러한 속성 중 일부를 수 있으므로 유의 `null` 것이 소비자에 대 한 확인가 `null` 예외 클래스의 멤버에 액세스 하기 전에 합니다.`CatchBlock` catch 블록 확인 예외를 나타내는 문자열입니다. Catch 블록 문자열은 다음과 같습니다.

- HttpServer (SendAsync 메서드)
- HttpControllerDispatcher (SendAsync 메서드)
- HttpBatchHandler (SendAsync 메서드)
- IExceptionFilter (ExecuteAsync 예외 필터 파이프라인의 ApiController의 처리)
- OWIN 호스트:

    - HttpMessageHandlerAdapter.BufferResponseContentAsync (에 대 한 출력을 버퍼링)
    - HttpMessageHandlerAdapter.CopyResponseContentAsync (스트리밍에 대 한 출력)
- 웹 호스트:

    - HttpControllerHandler.WriteBufferedResponseContentAsync (에 대 한 출력을 버퍼링)
    - HttpControllerHandler.WriteStreamedResponseContentAsync (스트리밍에 대 한 출력)
    - HttpControllerHandler.WriteErrorResponseContentAsync (예: 버퍼링 된 출력 모드에서 오류 복구에 실패)

Catch 블록 문자열의 목록도 정적 읽기 전용 속성을 통해 제공 됩니다. (코어 catch 블록 문자열 정적 ExceptionCatchBlocks에는 하나의 정적 클래스에서 각 OWIN 및 웹 호스트에 대 한 나머지 표시) 합니다.`IsTopLevelCatchBlock` 호출 스택의 맨 위에 있는 예외를 처리 하는 패턴을 권장 하는 데 도움이 됩니다. 원하는 위치에 중첩 된 catch 블록이 발생 하는 500 응답으로 예외를 설정 하는 대신 예외 처리기는 예외 정보를 호스트에서 볼 수 있을 때까지 전파를 할 수 있습니다.

이외에 `ExceptionContext`로 거를 또 하나의 전체를 통해 정보를 가져옵니다 `ExceptionLoggerContext`:

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

두 번째 속성인 `CanBeHandled`를 처리할 수 없는 예외를 식별 하는 거를 허용 합니다. 경우 연결이 중단 되 및 없는 새 응답 메시지를 보낼 수로 거를 호출할 수 있지만 처리기는 ***되지*** 호출할 수 고로 거를이 속성에서이 시나리오를 파악할 수 있습니다.

에 추가 합니다 `ExceptionContext`, 처리기 전체에서 설정할 수 있습니다 하나 더 많은 속성을 가져옵니다 `ExceptionHandlerContext` 예외를 처리 하:

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

예외 처리기를 설정 하 여 예외 처리 했음을 나타냅니다 합니다 `Result` 작업 결과 속성 (예를 들어를 [ExceptionResult](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx)를 [InternalServerErrorResult](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx)를 [ StatusCodeResult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx), 또는 사용자 지정 결과). 경우는 `Result` 속성이 null 이므로, 예외 처리 되지 않습니다 및 원래의 예외가 다시 throw 됩니다.

호출 스택의 맨 위에 있는 예외에 대 한 API 호출자는 적절 한 응답을 확인 하도록 추가 단계를 적용 했습니다. 호스트에서 전파 하면 예외를 호출자에 게 퍼플 노란색 화면이 표시 됩니다 또는 다른 일부 호스트는 일반적으로 HTML 응답 및 하지 적절 한 API 오류 응답을 제공 합니다. 이러한 경우에 null이 아닌 경우 및 사용자 지정 예외 처리기를 명시적으로 설정 하는 경우에 결과 시작 다시 `null` (처리 되지 않은)는 예외 전파를 호스트 합니다. 설정 `Result` 에 `null` 이러한 경우에 유용할 수 있습니다 두 가지 시나리오에 대 한 합니다.

1. 사용자 지정 예외를 처리 하기 전에/외부 웹 API를 등록 하는 미들웨어를 사용 하 여 Web API를 호스트 하는 OWIN.
2. 여기서는 노란색 퍼플 스크린이 처리 되지 않은 예외에 대 한 유용한 응답 실제로 브라우저를 통해 로컬 디버깅

예외로 거와 예외 처리기에 대 한로 거 또는 처리기 자체가 예외를 throw 하는 경우 복구에 아무 것도 하지 것입니다. (예외 전파, 하는 경우이 페이지의 맨 아래에 피드백을 남길 수 있도록 이외의 경우 더 나은 방법은) 예외로 거 및 처리기에 대 한 계약 예외 전파;은 호출자가 최대 허용 하지 않아야는 이 고, 그렇지 예외 됩니다만, 종종까지 호스트에 전파 (예: ASP HTML 오류가 발생. NET의 노란색 화면)에 보낼 클라이언트 (대개 API 호출자는 JSON 또는 XML에 대 한 기본 옵션 되지 않음).

## <a name="examples"></a>예제

### <a name="tracing-exception-logger"></a>예외로 거를 추적합니다.

아래 예외로 거 구성 된 추적 원본 (Visual Studio의 디버그 출력 창 포함)에 예외 데이터를 보냅니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>사용자 지정 오류 메시지 예외 처리기

아래 다음 클라이언트 지원 팀에 연락 하는 것에 대 한 전자 메일 주소를 포함 하 여 사용자 지정 오류 응답을 생성 합니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>예외 필터를 등록합니다.

"ASP.NET MVC 4 웹 응용 프로그램" 프로젝트 템플릿을 사용 하 여 프로젝트를 만들 경우 내에서 Web API 구성 코드를 입력 합니다 `WebApiConfig` 클래스를 *앱/시작 (_s)* 폴더:

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>부록: 기본 클래스 세부 내용

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
