---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: ASP.NET Web API 2 처리 하는 전역 오류 | Microsoft Docs
author: davidmatson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/03/2014
ms.topic: article
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: c593c56ba3d0ee8ebf6dc425408d2c3b91c83f93
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
ms.locfileid: "28042588"
---
<a name="global-error-handling-in-aspnet-web-api-2"></a>ASP.NET Web API 2 처리 하는 전역 오류
====================
여 [David Matson](https://github.com/davidmatson), [Rick Anderson](https://github.com/Rick-Anderson)

오늘날에 없는 경우 쉽게 웹 API를 로그 또는 오류를 전체적으로 처리 일부 처리 되지 않은 예외를 통해 처리할 수 [예외 필터](exception-handling.md), 하지만 예외 필터를 처리할 수 없는 사례의 수는 있습니다. 예:

1. 컨트롤러 생성자에서 throw 된 예외입니다.
2. 메시지 처리기에서 throw 된 예외입니다.
3. 라우팅 중 발생 한 예외입니다.
4. 응답 콘텐츠 직렬화 하는 동안 발생 한 예외입니다.

로그 (사용 가능한) 위치를 처리 하는 간단 하 고 일관 된 방법을 제공 하고자 합니다. 이러한 예외입니다. 

예외 처리, 오류 응답을 보낼 수 있는 모든 할 수 있는 하는 경우에는 로그의 예외는 경우 두 가지 주요 사례가 있습니다. 후자의 경우에 대 한 예로 응답 콘텐츠; 스트리밍 도중에 예외가 발생 한 경우 이 경우에 너무 늦었습니다 상태 코드, 헤더 및 부분 콘텐츠 이미 인스턴스용으로 통해 연결 중단 되므로 이후 새 응답 메시지를 보내려고 합니다. 예외를 새 응답 메시지를 생성 하기 위해 처리할 수 없는 경우에 여전히 지원에서 예외 기록입니다. 오류가 탐지 수의 경우에서 다음에 표시 된 대로 적절 한 오류 응답을 반환할 수 있습니다 했습니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>기존 옵션

외에 [예외 필터](exception-handling.md), [메시지 처리기](../advanced/http-message-handlers.md) 모든 500 수준 응답을 관찰 하려면 현재 사용할 수 있지만 해당 응답에서 작업 어렵습니다 원래 오류에 대 한 컨텍스트를 부족으로 합니다. 메시지 처리기 갖게 몇몇 처리할 수 있도록 하는 경우와 관련 된 예외 필터와 동일한 제한 사항이 적용 됩니다. 웹 API에는 오류 상태를 캡처하는 추적 인프라는 동안 추적 인프라는 진단 하기 위한 것 및은 not 설계 또는 프로덕션 환경에서 실행 하는 데 적합 합니다. 전역 예외 처리 및 로깅 서비스를 프로덕션에 실행할 수 있으며 기존 모니터링 솔루션에 연결할 수 있어야 합니다. (예를 들어 [ELMAH](https://code.google.com/p/elmah/) ).

### <a name="solution-overview"></a>솔루션 개요

 두 가지 새 사용자를 바꿀 수 있는 서비스 제공 [IExceptionLogger](../releases/whats-new-in-aspnet-web-api-21.md) IExceptionHandler 로그 처리 되지 않은 예외를 처리 하 고 있습니다. 서비스는 두 가지 주요 차이점은 있지만 매우 유사 합니다.

1. 예외로 거를 여러 개 있지만 한 개의 예외 처리기 등록을 지원 합니다.
2. 예외로 거 항상 호출 연결을 중단 하려고 하는 경우에 합니다. 예외 처리기만 호출 여전히 보낼 응답 메시지를 선택할 수 있을 때.

두 서비스 모두 예외 감지 되었으며 지점에서 관련 정보를 포함 하는 예외 컨텍스트에 대 한 액세스를 제공 특히 [HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx), [HttpRequestContext](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx), 예외 및 예외 원본 (아래의 세부 정보)를 발생 합니다.

### <a name="design-principles"></a>디자인 원칙

1. **주요 변경 내용이 없습니다** 이 기능은 중요 한 한 솔루션에 영향을 주지는 중요 한 제약 조건이 있을 다음 주요 변경 내용이 없습니다, 계약을 입력 하도록 하는 릴리스 또는 동작에 추가 되 고 않기 때문입니다. 이 제약 조건은 500 응답에 예외를 설정 하는 기존 catch 블록의 관점에서 수행 하려는 일부 정리를 제외 합니다. 이 추가 정리는 후속 버전에 대 한 것으로 간주 될 수 있습니다. 이를 중요 한 경우 하십시오 투표에 [ASP.NET Web API 사용자 음성](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception)합니다.
2. **웹 API와의 일관성을 유지 관리 생성** 웹 API 필터 파이프라인은 특정 작업, 컨트롤러 관련 또는 전역 범위에서 논리를 적용 하는 유연성과 일반적인 문제를 처리할 수 있는 좋은 방법입니다. 예외 필터를 포함 하 여 필터를 전역 범위에서 등록 하는 경우에 작업 및 컨트롤러 컨텍스트를 항상 포함 됩니다. 계약에 적합 한 필터를 있지만 예외 필터도 전역 범위가 지정 된 것과 되지 적합 한 경우 작업이 나 컨트롤러 컨텍스트가 없는 경우와 같은 메시지 처리기에서 예외를 처리 하는 일부 예외에 대 한 해당 의미 존재 합니다. 예외 처리에 대 한 필터에 의해 제공 유연한 범위 지정을 사용 하고자 하는 경우 예외 필터 여전히 필요 합니다. 하지만 (항목 합계의 컨트롤러 컨텍스트와 작업 컨텍스트 제약 조건) 없이 전체 전역 오류 처리에는 별도 구문, 컨트롤러 컨텍스트 외부의 예외를 처리 해야 하는 경우도 필요 합니다.

### <a name="when-to-use"></a>사용 하는 경우

- 예외로 거는 Web API에서 발생 하는 모든 처리 되지 않은 예외를 표시할 때 솔루션입니다.
- 예외 처리기는 Web API에서 발생 하는 처리 되지 않은 예외에 대 한 모든 가능한 응답을 사용자 지정 하기 위한 솔루션입니다.
- 예외 필터는 특정 작업이 나 컨트롤러에 관련 된 하위 집합 처리 되지 않은 예외 처리를 위한 것이 간편한 해결책입니다.

### <a name="service-details"></a>서비스 세부 정보

 예외로 거 및 처리기 서비스 인터페이스에는 각 컨텍스트에 라인으로 전환 하는 간단한 비동기 메서드는 같습니다. 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 두이 인터페이스에 대 한 기본 클래스도 제공 합니다. 코어 (동기화 또는 비동기) 메서드를 재정의 뿐 로깅하거나에 권장 되는 처리 하는 데 걸리는 시간입니다. 로깅을 위한는 `ExceptionLogger` 기본 클래스는 핵심 로깅 방법 각 예외에 대해 한 번씩 호출 됩니다만 확인 (나중에 전파 하는 경우에 추가로 호출 스택을 하 고 다시 발생 함). `ExceptionHandler` 기본 클래스 핵심 처리 중첩 레거시 무시 하 고는 호출 스택의 맨 위에 있는 예외 catch 블록에 대해서만 메서드를 호출 합니다. (이러한 기본 클래스의 단순화 된 버전은 아래 부록.) 둘 다 `IExceptionLogger` 및 `IExceptionHandler` 통해 예외에 대 한 정보를 받을 `ExceptionContext`합니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

항상 제공 프레임 워크는 예외로 거 또는 예외 처리기를 호출 하면 프로그램 `Exception` 및 `Request`합니다. 단위 테스트의 경우를 제외 하 고 제공 항상 합니다는 `RequestContext`합니다. 거의 제공는 `ControllerContext` 및 `ActionContext` (경우에 예외 필터에 대 한 catch 블록에서 호출). 매우 드물게 제공는 `Response`(응답을 기록 하는 동안 중간 특정 IIS 경우)에 해당 합니다. 이러한 속성 중 일부를 수 있기 때문에 사용자에 게 유의 `null` 를 확인 하려면 소비자가 `null` 예외 클래스의 멤버에 액세스 하기 전에.`CatchBlock` 예외는 catch 블록 보여 준다는 나타내는 문자열입니다. Catch 블록 문자열은 다음과 같습니다.

- HttpServer (SendAsync 메서드)
- HttpControllerDispatcher (SendAsync 메서드)
- HttpBatchHandler (SendAsync 메서드)
- IExceptionFilter (ExecuteAsync의 예외 필터 파이프라인 ApiController의 처리)
- OWIN 호스트:

    - HttpMessageHandlerAdapter.BufferResponseContentAsync (에 대 한 출력을 버퍼링)
    - HttpMessageHandlerAdapter.CopyResponseContentAsync (for streaming output)
- 웹 호스트:

    - HttpControllerHandler.WriteBufferedResponseContentAsync (에 대 한 출력을 버퍼링)
    - HttpControllerHandler.WriteStreamedResponseContentAsync (스트리밍에 대 한 출력)
    - HttpControllerHandler.WriteErrorResponseContentAsync (실패에 대 한 오류 복구 버퍼링 된 출력 모드에서)

Catch 블록 문자열 목록에도 정적 읽기 전용 속성을 통해 제공 됩니다. (코어 catch 블록 문자열 정적 ExceptionCatchBlocks에 있습니다; 하나의 정적 클래스에 각 OWIN 및 웹 호스트에 대 한 나머지 표시) 됩니다.`IsTopLevelCatchBlock` 호출 스택의 위쪽에만 예외 처리의 패턴을 권장 하는 데 도움이 됩니다. 원하는 위치에 중첩 된 catch 블록에서 발생 500 응답에 예외를 설정 하는 대신 예외 처리기에서 예외 전파를 호스트에서 볼 수는 때까지 설정할 수 있습니다.

이외에 `ExceptionContext`로 거를 통해 전체 정보의 한 더 많은 요소를 가져옵니다 `ExceptionLoggerContext`:

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

두 번째 속성 `CanBeHandled`를 처리할 수 없는 예외를 식별 하는 거를 허용 합니다. 때 연결이 중단 되 고 없는 새 응답 메시지를 보낼 수, 호출 되는 거 하지 않지만 처리기 ***하지*** 호출할 수는 거는이 시나리오에서이 속성을 식별할 수 있습니다.

변수에 대 한 추가 `ExceptionContext`, 처리기 전체에 설정할 수는 한 더 많은 속성을 가져옵니다 `ExceptionHandlerContext` 예외를 처리:

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

예외 처리기를 설정 하 여 예외가 처리 했음을 나타냅니다는 `Result` 작업 결과를 속성 (예를 들어 한 [ExceptionResult](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx), [InternalServerErrorResult](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx), [ StatusCodeResult](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx), 또는 사용자 지정 결과). 경우는 `Result` 속성이 null 이므로, 예외 처리 되지 않은 및 원래의 예외가 다시 throw 됩니다.

호출 스택의 맨 위에 있는 예외에 대 한 별도 단계 API 호출자에 대 한 적절 한 응답 되는지 했습니다. 호스트에서 예외 전파를 호출자에 게 사망의 노란색 화면 표시 되는 것 또는 HTML는 일반적으로 응답 하 고 적절 한 API 오류 응답 하지 않는 다른 호스트에서 제공 합니다. 이러한 경우에 null이 아닌 및 사용자 지정 예외 처리기가 명시적으로 설정 하는 경우에 결과 시작 다시 `null` (처리 되지 않은)은 예외 전파는 호스트입니다. 설정 `Result` 를 `null` 이러한 경우에 유용할 수 두 가지 시나리오:

1. 사용자 지정 예외 처리 하기 전에/외부 웹 API를 등록 하는 미들웨어로 Web API를 호스트 하는 OWIN 합니다.
2. 로컬 브라우저를 통해 디버깅, 여기서 사망의 노란색 화면은 처리 되지 않은 예외에 대 한 유용한 응답 실제로입니다.

예외로 거와 예외 처리기에 대 한로 거 또는 자체 처리기 예외를 throw 한 경우 복구할 수 아무 작업도 수행 하지 마십시오 했습니다. (전파 하는 경우이 페이지의 맨 아래에 피드백을 두고, 예외로 이외의 있어야 더 나은 방법은.) 예외로 거 및 처리기에 대 한 계약 예외 호출자;까지 전파 하지 통과 시킬 것은 그렇지 않으면 예외 방금에 전파 됩니다, 종종 모든 과정 (예: ASP HTML 오류가 발생 하는 호스트. NET의 노란색 화면)는 클라이언트 (JSON 또는 XML을 예상 하는 API 호출자는 기본적된으로 옵션을 대개 되지 않음)으로 다시 전송 됩니다.

## <a name="examples"></a>예제

### <a name="tracing-exception-logger"></a>예외로 거를 추적합니다.

아래 예외로 거 (Visual Studio에서 디버그 출력 창 포함)으로 구성 된 추적 소스를 예외 데이터를 보냅니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>사용자 지정 오류 메시지 예외 처리기

아래에서 다음을 지원 팀에 연락 하는 것에 대 한 전자 메일 주소를 포함 한 클라이언트에 대 한 사용자 지정 오류 응답을 생성 합니다.

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>예외 필터를 등록 하는 중

"ASP.NET MVC 4 웹 응용 프로그램" 프로젝트 템플릿을 사용 하 여 프로젝트를 만드는 경우 내부 웹 API 구성 코드를 입력의 `WebApiConfig` 클래스에 *앱/시작 (_s)* 폴더:

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>부록: 기본 클래스 세부 내용

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
