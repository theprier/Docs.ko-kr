---
uid: web-api/overview/error-handling/exception-handling
title: "ASP.NET Web API의에서 예외 처리 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/12/2012
ms.topic: article
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: c65ddcca012840d70ab5a33af92edb30041be971
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="exception-handling-in-aspnet-web-api"></a>ASP.NET Web API의에서 예외 처리
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

이 문서에서는 오류 및 ASP.NET Web API의 예외 처리를 설명 합니다.

- [HttpResponseException](#httpresponserexception)
- [예외 필터](#exception_filters)
- [예외 필터를 등록 하는 중](#registering_exception_filters)
- [HttpError](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a>HttpResponseException

Web API 컨트롤러 확인할 수 없는 예외를 throw 하는 경우 어떻게 됩니까? 기본적으로 대부분의 예외는 상태 코드 500 내부 서버 오류와 함께 HTTP 응답으로 변환 됩니다.

**HttpResponseException** 형식은 특수 한 경우. 이 예외는 예외 생성자에서 지정 하는 모든 HTTP 상태 코드를 반환 합니다. 경우 404 찾을 수 없는 다음 메서드 반환 하는 예를 들어는 *id* 매개 변수가 올바르지 않습니다.

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

응답 보다 자세히 제어 수도 전체 응답 메시지를 생성 하 고 사용 하 여 포함 된 **HttpResponseException:** 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a>예외 필터

웹 API를 작성 하 여 예외를 처리 하는 방법을 사용자 지정할 수는 *예외 필터*합니다. 예외 필터는 컨트롤러 메서드를 한 처리 되지 않은 예외를 throw 될 때 실행 되 *하지* 는 **HttpResponseException** 예외입니다. **HttpResponseException** 형식이 특별 한 경우 반환 된 HTTP 응답에 대 한 구체적으로 설계 되었습니다.

예외 필터를 구현에서 **System.Web.Http.Filters.IExceptionFilter** 인터페이스입니다. 파생 하는 예외 필터 작성 하는 가장 간단한 방법은 **System.Web.Http.Filters.ExceptionFilterAttribute** 클래스 및 재정의 **OnException** 메서드.

> [!NOTE]
> ASP.NET Web API의 예외 필터는 ASP.NET MVC의 경우와 비슷합니다. 그러나 선언 된 함수 및 별도 네임 스페이스에 개별적으로 합니다. 특히는 **HandleErrorAttribute** MVC에서 사용 되는 클래스는 Web API 컨트롤러에서 발생 한 예외를 처리 하지 않습니다.


다음으로 변환 하는 필터를은 **NotImplementedException** 예외가 HTTP 상태 코드 501 구현 되지 않음:

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

**응답** 의 속성은 **HttpActionExecutedContext** 클라이언트에 전송 될 HTTP 응답 메시지를 포함 하는 개체입니다.

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a>예외 필터를 등록 하는 중

웹 API 예외 필터를 등록 하는 방법은 여러 가지가 있습니다.

- 작업에 의해
- 컨트롤러에 의해
- 전역으로

특정 작업에 필터를 적용할 필터 특성으로 작업을 추가 합니다.

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

모든 컨트롤러에서 작업 하는 필터를 적용 하려면 필터 특성으로 컨트롤러 클래스에 추가 합니다.

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

필터를 적용 하려면 전역적으로 모든 Web API 컨트롤러에 추가 필터의 인스턴스는 **GlobalConfiguration.Configuration.Filters** 컬렉션입니다. 이 컬렉션의 예외 필터는 모든 Web API 컨트롤러 작업에 적용 됩니다.

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

"ASP.NET MVC 4 웹 응용 프로그램" 프로젝트 템플릿을 사용 하 여 프로젝트를 만드는 경우 내부 웹 API 구성 코드를 입력의 `WebApiConfig` 응용 프로그램에 있는 클래스\_시작 폴더:

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a>HttpError

**HttpError** 개체 응답 본문에 오류 정보를 반환 하는 일관 된 방법을 제공 합니다. 다음 예제와 HTTP 상태 코드 404 (찾을 수 없음)를 반환 하는 방법을 보여 줍니다.는 **HttpError** 응답 본문에 있습니다.

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

**CreateErrorResponse** 에 정의 된 확장 메서드는 **System.Net.Http.HttpRequestMessageExtensions** 클래스입니다. 내부적으로 **CreateErrorResponse** 만듭니다는 **HttpError** 인스턴스 한 다음 만듭니다는 **HttpResponseMessage** 를 포함 하는 **HttpError**.

메서드가 성공 하면이 예제에서는 제품 HTTP 응답에 반환 합니다. 요청 된 제품 없으면 HTTP 응답에 포함 되어 있지만 **HttpError** 요청 본문에 있습니다. 응답 다음과 같을 수 있습니다.

[!code-console[Main](exception-handling/samples/sample9.cmd)]

에 **HttpError** 이 예제 JSON으로 serialize 했습니다. 사용 하 여의 장점 중 하나 **HttpError** 동일한를 통해 이동 하는지는 [콘텐츠 협상](../formats-and-model-binding/content-negotiation.md) 다른 강력한 형식의 모델을 처리 하는 serialization 및 합니다.

### <a name="httperror-and-model-validation"></a>HttpError 및 모델 유효성 검사

모델 유효성 검사에 대 한 모델 상태를 전달할 수 있습니다 **CreateErrorResponse**응답의 유효성 검사 오류를 포함 합니다.

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

이 예에서는 다음 응답을 반환할 수 있습니다.

[!code-console[Main](exception-handling/samples/sample11.cmd)]

모델 유효성 검사에 대 한 자세한 내용은 참조 [ASP.NET Web API에서 모델 유효성 검사](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)합니다.

### <a name="using-httperror-with-httpresponseexception"></a>HttpResponseException HttpError 사용

앞의 예제에서는 반환는 **HttpResponseMessage** 컨트롤러 작업에서 메시지를 사용할 수도 **HttpResponseException** 반환 하는 **HttpError**합니다. 이렇게 하면 여전히 반환 하는 동안 일반 성공의 경우 강력한 형식의 모델이 반환 **HttpError** 오류가 발생 하는 경우:

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
