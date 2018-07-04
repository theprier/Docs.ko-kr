---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Web API 2에서에서 작업의 결과 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/03/2014
ms.topic: article
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: 7726829ac9eba339ff3ac1c94c86132cb1090783
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37395531"
---
<a name="action-results-in-web-api-2"></a>Web API 2에서에서 작업 결과
====================
[Mike Wasson](https://github.com/MikeWasson)

이 항목에서는 ASP.NET Web API HTTP 응답 메시지에 컨트롤러 작업에서 반환 값을 변환 하는 방법을 설명 합니다.

Web API 컨트롤러 작업에는 다음 중 하나를 반환할 수 있습니다.

1. void
2. **HttpResponseMessage**
3. **IHttpActionResult**
4. 다른 형식

이 따라 반환 되 면 Web API 다른 메커니즘을 사용 하 여 HTTP 응답을 만듭니다.

| 반환 형식 | Web API에서 응답을 만드는 방법 |
| --- | --- |
| void | 빈 204 (내용 없음)를 반환 합니다. |
| **HttpResponseMessage** | HTTP 응답 메시지에 직접 변환 합니다. |
| **IHttpActionResult** | 호출 **ExecuteAsync** 만들려는 **HttpResponseMessage**, 다음 HTTP 응답 메시지를 변환 합니다. |
| 다른 형식 | Serialize 된 반환 값을 응답 본문;에 쓰기 200 (정상)를 반환 합니다. |

이 항목의 나머지 각 옵션을 자세히 설명합니다.

## <a name="void"></a>void

반환 형식이 `void`, Web API에는 단순히 빈 HTTP 응답 상태 코드 204 (내용 없음)를 사용 하 여 반환 합니다.

예제에서는 컨트롤러:

[!code-csharp[Main](action-results/samples/sample1.cs)]

HTTP 응답:

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a>HttpResponseMessage

작업을 반환 하는 경우는 [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API 반환 값으로 변환 합니다 직접 HTTP 응답 메시지의 속성을 사용 하는 **HttpResponseMessage** 채울 개체입니다는 응답입니다.

이 옵션은 많은 응답 메시지에 대 한 제어를 제공 합니다. 예를 들어 다음 컨트롤러 작업을 캐시 제어 헤더를 설정합니다.

[!code-csharp[Main](action-results/samples/sample3.cs)]

응답:

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

도메인 모델을 전달 하는 경우는 **CreateResponse** 메서드를 사용 하 여 Web API는 [미디어 포맷터](../formats-and-model-binding/media-formatters.md) 응답 본문에 직렬화 된 모델을 작성 합니다.

[!code-csharp[Main](action-results/samples/sample5.cs)]

Web API 요청에 Accept 헤더를 사용 하 여 포맷터 선택. 자세한 내용은 [콘텐츠 협상](../formats-and-model-binding/content-negotiation.md)합니다.

## <a name="ihttpactionresult"></a>IHttpActionResult

합니다 **IHttpActionResult** 인터페이스는 Web API 2에서 도입 되었습니다. 기본적으로 정의 하는 **HttpResponseMessage** 팩터리입니다. 사용 하는 몇 가지 이점은 다음과 같습니다 합니다 **IHttpActionResult** 인터페이스:

- 간소화 [단위 테스트](../testing-and-debugging/unit-testing-controllers-in-web-api.md) 컨트롤러입니다.
- 별도 클래스로 HTTP 응답을 만들기 위한 일반적인 논리를 이동 합니다.
- 응답 생성의 하위 수준 세부 정보를 숨겨 명확 하 게, 컨트롤러 작업의 의도를 만듭니다.

**IHttpActionResult** 단일 메서드를 포함 **ExecuteAsync**를 비동기적으로 만듭니다는 **HttpResponseMessage** 인스턴스.

[!code-csharp[Main](action-results/samples/sample6.cs)]

컨트롤러 작업을 반환 하는 경우는 **IHttpActionResult**, Web API를 호출 합니다 **ExecuteAsync** 메서드를를 **HttpResponseMessage**합니다. 변환 후 합니다 **HttpResponseMessage** HTTP 응답 메시지에 있습니다.

한 간단한 않아도 됨 다음과 같습니다 **IHttpActionResult** 를 만드는 일반 텍스트 응답:

[!code-csharp[Main](action-results/samples/sample7.cs)]

예제에서는 컨트롤러 작업:

[!code-csharp[Main](action-results/samples/sample8.cs)]

응답:

[!code-console[Main](action-results/samples/sample9.cmd)]

더 자주 사용 하 여 합니다 **IHttpActionResult** 구현에서 정의 합니다 **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** 네임 스페이스입니다. 합니다 **ApiController** 클래스는 이러한 기본 제공 작업 결과 반환 하는 도우미 메서드를 정의 합니다.

다음 예제에서는 요청에 기존 제품 ID가 일치 하지 않는 경우 컨트롤러 호출 [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) 404 (찾을 수 없음) 응답을 만들려고 합니다. 컨트롤러를 호출 하는 고, 그렇지 [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), 제품을 포함 하는 200 (정상) 응답을 만듭니다.

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a>다른 반환 형식

반환 다른 모든 형식에 대 한 웹 API에 사용 된 [미디어 포맷터](../formats-and-model-binding/media-formatters.md) 반환 값을 serialize 하 합니다. 웹 API는 응답 본문에 serialize 된 값을 씁니다. 응답 상태 코드는 200 (정상).

[!code-csharp[Main](action-results/samples/sample11.cs)]

이 방식의 단점은 404와 같이 오류 코드를 직접 반환할 수입니다. 그러나 throw 할 수 있습니다는 **HttpResponseException** 오류 코드에 대 한 합니다. 자세한 내용은 [ASP.NET Web API의 예외 처리](../error-handling/exception-handling.md)합니다.

Web API 요청에 Accept 헤더를 사용 하 여 포맷터 선택. 자세한 내용은 [콘텐츠 협상](../formats-and-model-binding/content-negotiation.md)합니다.

요청 예제

[!code-console[Main](action-results/samples/sample12.cmd)]

예제 응답:

[!code-console[Main](action-results/samples/sample13.cmd)]
