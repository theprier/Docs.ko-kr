---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: "에서 단위 테스트 컨트롤러 ASP.NET Web API 2 | Microsoft Docs"
author: MikeWasson
description: "이 항목의에서 단위 테스트 컨트롤러 Web API 2에 대 한 특정 기법을 설명 합니다. 이 항목을 읽기 전에 자습서 단위를 읽기만 할 수 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/11/2014
ms.topic: article
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: bda5148a4c1553d70f3173de66371fbb8576e83f
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="unit-testing-controllers-in-aspnet-web-api-2"></a>에서 단위 테스트 컨트롤러 ASP.NET Web API 2
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

> 이 항목의에서 단위 테스트 컨트롤러 Web API 2에 대 한 특정 기법을 설명 합니다. 이 항목을 읽기 전에 자습서 읽기를 수행할 수 있습니다 있습니다 [단위 테스트 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), 단위 테스트 프로젝트를 솔루션에 추가 하는 방법을 보여 주는 합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> - [Visual Studio 2017](https://www.visualstudio.com/vs/)
> - Web API 2
> - [Moq](https://github.com/Moq) 4.5.30

> [!NOTE]
> Moq를 사용 하지만 동일한 개념 모든 모의 프레임 워크에 적용 됩니다. Moq 4.5.30 (이상) Visual Studio 2017, Roslyn 및.NET 4.5 및 이후 버전을 지원 합니다.

단위 테스트의 일반적인 패턴은 &quot;정렬 act assert&quot;:

- 정렬: 테스트 실행에 대 한 모든 필수 구성 요소를 설정 합니다.
- Act: 테스트를 수행 합니다.
- 어설션 됩니다: 테스트가 성공 했는지 확인 합니다.

정렬 단계에는 자주 모의 사용 하 여 하거나 스텁 개체입니다. 한 가지 테스트는 테스트는 데 사용 되므로 종속 항목의 수를 최소화 하 합니다.

Web API 컨트롤러에 단위 테스트를 해야 하는 일부의 원인 다음과 같습니다.

- 작업이 올바른 유형의 응답을 반환합니다.
- 잘못 된 매개 변수가 올바른 오류 응답을 반환 합니다.
- 작업은 저장소 또는 서비스 계층에서 올바른 메서드를 호출합니다.
- 응답 도메인 모델을 포함 하는 경우 모델 유형을 확인 합니다.

를 테스트 하려면 일반 기능 중 일부은 이지만 구체적인 컨트롤러 구현에 따라 달라 집니다. 컨트롤러 작업을 반환 하는지 여부를 크게 향상 될 수 하는 특히 **HttpResponseMessage** 또는 **IHttpActionResult**합니다. 이러한 결과 형식에 대 한 자세한 내용은 참조 [Web Api 2에 대 한 작업 결과](../getting-started-with-aspnet-web-api/action-results.md)합니다.

## <a name="testing-actions-that-return-httpresponsemessage"></a>테스트 HttpResponseMessage를 반환 하는 작업

컨트롤러의 예를 들면 인 작업 반환 같습니다 **HttpResponseMessage**합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

공지 컨트롤러 사용 하는 종속성 주입을 삽입 하는 `IProductRepository`합니다. 이용 하면 컨트롤러 더 테스트 가능한 모의 리포지토리를 삽입할 수 있습니다. 다음 단위 테스트를 확인 하는 `Get` 메서드 쓰기는 `Product` 응답 본문에 있습니다. 가정 `repository` 는 모의 `IProductRepository`합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

설정 해야 **요청** 및 **구성** 컨트롤러에 있습니다. 테스트와 함께 실패 합니다는 그렇지 않은 경우는 **ArgumentNullException** 또는 **InvalidOperationException**합니다.

## <a name="testing-link-generation"></a>링크 생성 테스트

`Post` 메서드 호출 **UrlHelper.Link** 응답에서 링크를 합니다. 이 단위 테스트에서 약간 더 많은 설치를 필요합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

**UrlHelper** 클래스 이므로이 대 한 값을 설정 하는 테스트 요청 URL 및 경로 데이터를 필요 합니다. 또 다른 옵션은 모의 또는 스텁 **UrlHelper**합니다. 기본값을 바꾸는이 접근 방식 [ApiController.Url](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) 모의 또는 스텁 버전은 고정된 값을 반환 합니다.

사용 하 여 테스트를 다시 작성해 보겠습니다는 [Moq](https://github.com/Moq) 프레임 워크입니다. 설치는 `Moq` 테스트 프로젝트에서 NuGet 패키지 합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

이 버전에서는 하지 않아도 모든 경로 데이터를 설정 하기 때문에 모의 **UrlHelper** 상수 문자열을 반환 합니다.


## <a name="testing-actions-that-return-ihttpactionresult"></a>테스트 IHttpActionResult 반환 하는 작업

Web API 2 컨트롤러 작업이 반환할 수 **IHttpActionResult**는 **ActionResult** ASP.NET MVC에서 합니다. **IHttpActionResult** HTTP 응답을 만들기 위한 명령 패턴을 정의 하는 인터페이스입니다. 응답을 직접 만드는 대신 컨트롤러 반환는 **IHttpActionResult**합니다. 파이프라인 호출 나중는 **IHttpActionResult** 응답을 만들려고 합니다. 이러한 방식을 통해 단위 테스트를 작성 하는 보다 쉽게에 필요한 설치 프로그램의 많은 건너뛸 수 있으므로 **HttpResponseMessage**합니다.

여기 반환 되는 예제 컨트롤러 인 작업 **IHttpActionResult**합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

사용 하 여 몇 가지 일반적인 패턴을 보여 주는이 예제 **IHttpActionResult**합니다. 살펴보겠습니다 어떻게 단위를 테스트 합니다.

### <a name="action-returns-200-ok-with-a-response-body"></a>작업 응답 본문이 포함 200 (정상)를 반환합니다.

`Get` 메서드 호출 `Ok(product)` 발견 되는 제품입니다. 단위 테스트에서 반환 형식이 있는지 확인 **OkNegotiatedContentResult** 및 반환 된 제품에 올바른 id입니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

단위 테스트에 작업 결과 실행 하지 않습니다. 작업 결과 HTTP 응답을 올바르게 만듭니다 가정할 수 있습니다. (바로 이러한 이유로 Web API 프레임 워크에는 자체 단위 테스트가!)

### <a name="action-returns-404-not-found"></a>404 (찾을 수 없음)를 반환 하는 작업

`Get` 메서드 호출 `NotFound()` 제품을 찾을 수 없는 경우. 이 경우에 대 한 단위 테스트에 검사 반환 형식이 **NotFoundResult**합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a>작업 응답 본문이 없는 200 (정상)를 반환합니다.

`Delete` 메서드 호출 `Ok()` 빈 HTTP 200 응답 돌아갑니다. 단위 테스트는 이전 예제와 반환 형식이 고,이 경우 확인 **OkResult**합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a>위치 헤더와 201 (만들어짐)를 반환 하는 작업

`Post` 메서드 호출 `CreatedAtRoute` Location 헤더의 URI는 HTTP 201 응답과 돌아갑니다. 단위 테스트에서 동작 올바른 라우팅 값을 설정 함을 확인 합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a>작업 응답 본문이 포함 다른 2xx를 반환합니다.

`Put` 메서드 호출 `Content` 를 응답 본문이 포함 된 HTTP 202 (수락) 응답을 반환 합니다. 이 경우 200 (정상)를 반환 합니다. 유사 하지만 단위 테스트도 상태 코드를 확인 해야 합니다.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a>추가 리소스

- [Entity Framework를 모의 때 단위 테스트 ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- [ASP.NET Web API 서비스에 대 한 테스트를 작성](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx) (Youssef Moussaoui 하 여 블로그 게시물).
- [경로 디버거를 사용 하 여 ASP.NET Web API 디버깅](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)
