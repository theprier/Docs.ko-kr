---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: ASP.NET Web API 2의에서 단위 테스트 컨트롤러 | Microsoft Docs
author: MikeWasson
description: 이 항목에서는 Web API 2의 단위 테스트 컨트롤러에 대 한 몇 가지 특정 기술을 설명 합니다. 이 항목을 읽기 전에 자습서 단위를 읽기만 하는 것이 좋습니다는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/11/2014
ms.topic: article
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 1a3cfa1962a5f914fd2393088bec4424f6453d07
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389385"
---
<a name="unit-testing-controllers-in-aspnet-web-api-2"></a>ASP.NET Web API 2의에서 단위 테스트 컨트롤러
====================
[Mike Wasson](https://github.com/MikeWasson)

> 이 항목에서는 Web API 2의 단위 테스트 컨트롤러에 대 한 몇 가지 특정 기술을 설명 합니다. 이 항목을 읽기 전에 하려는 경우 자습서를 읽어 보세요 [단위 테스트 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), 단위 테스트 프로젝트를 솔루션에 추가 하는 방법을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> - [Visual Studio 2017](https://www.visualstudio.com/vs/)
> - Web API 2
> - [Moq](https://github.com/Moq) 4.5.30

> [!NOTE]
> Moq를 사용 하지만 동일한 개념 모든 모의 프레임 워크에 적용 됩니다. Moq 4.5.30 (이상) Visual Studio 2017, Roslyn 및.NET 4.5 이상 버전을 지원 합니다.

단위 테스트에서 일반적인 패턴은 &quot;정렬 act assert&quot;:

- 설정 테스트를 실행 하려면 모든 필수 구성 요소를 정렬 합니다.
- Act: 테스트를 수행 합니다.
- Assert: 테스트가 성공 했는지 확인 합니다.

정렬 단계에는 자주 mock를 사용 하거나 스텁 개체입니다. 한 가지 테스트에서 테스트 포커스가 하므로 종속성 수가 최소화 됩니다.

Web API 컨트롤러에서 단위 테스트를 해야 하는 몇 가지는 다음과 같습니다.

- 작업 응답의 올바른 형식을 반환합니다.
- 잘못 된 매개 변수가 올바른 오류 응답을 반환 합니다.
- 리포지토리 또는 서비스 계층에서 올바른 메서드를 호출 하는 작업입니다.
- 응답 도메인 모델에 포함 된 경우에 모델 형식을 확인 합니다.

다음은 몇 가지 일반 작업을 테스트 하려면 하지만 세부 정보 컨트롤러 구현에 따라 달라 집니다. 컨트롤러 작업 반환 하는지 여부를 크게 향상 될 수 하는 특히 **HttpResponseMessage** 하거나 **IHttpActionResult**합니다. 이러한 결과 형식에 대 한 자세한 내용은 참조 하세요. [Web Api 2에서 작업 결과](../getting-started-with-aspnet-web-api/action-results.md)합니다.

## <a name="testing-actions-that-return-httpresponsemessage"></a>HttpResponseMessage를 반환 하는 테스트 작업

한 예로 컨트롤러 작업 반환 **HttpResponseMessage**합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

컨트롤러 삽입에 종속성 주입 사용을 `IProductRepository`입니다. 사용 컨트롤러 더 테스트할 수 있으므로 모의 리포지토리를 삽입할 수 있습니다. 다음 단위 테스트를 확인 합니다 `Get` 메서드 쓰기를 `Product` 응답 본문에 있습니다. 가정 `repository` mock는 `IProductRepository`합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

설정 해야 **요청** 하 고 **구성** 컨트롤러입니다. 사용 하 여 테스트에 실패 하는 고, 그렇지는 **ArgumentNullException** 하거나 **InvalidOperationException**합니다.

## <a name="testing-link-generation"></a>테스트 링크 생성

합니다 `Post` 메서드 호출 **UrlHelper.Link** 응답에 링크를 만들려고 합니다. 이 단위 테스트에서 약간 더 많은 설치가 필요합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

합니다 **UrlHelper** 클래스 테스트에 대 한 값을 설정 해야 하므로 요청 URL 및 경로 데이터를 해야 합니다. 또 다른 옵션은 stub 또는 mock **UrlHelper**합니다. 이 방법의 기본 값을 바꿔야 [ApiController.Url](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) 고정된 값을 반환 하는 mock 또는 스텁 버전을 사용 하 여 합니다.

사용 하 여 테스트를 다시 작성해 보겠습니다 합니다 [Moq](https://github.com/Moq) 프레임 워크입니다. 설치는 `Moq` 테스트 프로젝트에서 NuGet 패키지.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

이 버전에서는 필요가 경로 데이터를 설정 하기 때문에 mock **UrlHelper** 상수 문자열을 반환 합니다.


## <a name="testing-actions-that-return-ihttpactionresult"></a>IHttpActionResult 반환 하는 테스트 작업

Web API 2 컨트롤러 작업을 반환할 수 있습니다 **IHttpActionResult**에 비슷합니다 **ActionResult** ASP.NET MVC에서. 합니다 **IHttpActionResult** 인터페이스는 HTTP 응답을 만들기 위한 명령 패턴을 정의 합니다. 컨트롤러 응답을 직접 만드는 대신 반환 된 **IHttpActionResult**합니다. 파이프라인을 호출 하는 나중에 **IHttpActionResult** 응답을 만들려고 합니다. 이 접근 방식을 쉽게 단위 테스트 작성에 필요한 설정의 많은 건너뛸 수 있으므로 **HttpResponseMessage**합니다.

같습니다.는 예제 컨트롤러 작업 반환 **IHttpActionResult**합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

이 예제를 사용 하 여 몇 가지 일반적인 패턴을 보여 줍니다 **IHttpActionResult**합니다. 살펴보겠습니다 어떻게 단위를 테스트 합니다.

### <a name="action-returns-200-ok-with-a-response-body"></a>작업 응답 본문이 포함 된 200 (정상)를 반환합니다.

합니다 `Get` 메서드 호출 `Ok(product)` 제품 있으면 됩니다. 단위 테스트에서 반환 형식 인지 확인 **OkNegotiatedContentResult** 및 반환 된 제품에는 올바른 ID가 있습니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

단위 테스트는 작업 결과 실행 하지 않습니다. 작업 결과 HTTP 응답을를 올바르게 만드는 가정할 수 있습니다. (이유는 Web API 프레임 워크에는 자체 단위 테스트가!)

### <a name="action-returns-404-not-found"></a>작업 404 (찾을 수 없음)를 반환합니다.

합니다 `Get` 메서드 호출 `NotFound()` 제품 없는 경우. 이 경우에 대 한 단위 테스트에 검사 반환 형식이 **NotFoundResult**합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a>작업 응답 본문 없이 200 (정상)를 반환합니다.

합니다 `Delete` 메서드 호출 `Ok()` 빈 HTTP 200 응답을 반환 합니다. 단위 테스트는 이전 예제와 같이 반환 형식으로이 경우 확인 **OkResult**합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a>작업 위치 헤더를 사용 하 여 201 (만들어짐)를 반환합니다.

합니다 `Post` 메서드 호출 `CreatedAtRoute` Location 헤더의 URI 사용 하 여 HTTP 201 응답을 반환 합니다. 단위 테스트를 작업에 올바른 라우팅 값 설정 함을 확인 합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a>작업 응답 본문이 포함 된 다른 2xx를 반환합니다.

합니다 `Put` 메서드 호출 `Content` 응답 본문과 함께 HTTP 202 (수락 됨) 응답을 반환 합니다. 이 경우 200 (정상)를 반환 하도록 유사 하지만 단위 테스트 상태 코드를 확인 해야 합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a>추가 리소스

- [Entity Framework 머킹 때 단위 테스트 ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- [ASP.NET 웹 API 서비스에 대 한 테스트를 작성](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx) (Youssef Moussaoui 블로그 게시물).
- [경로 디버거를 사용 하 여 ASP.NET Web API 디버깅](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)
