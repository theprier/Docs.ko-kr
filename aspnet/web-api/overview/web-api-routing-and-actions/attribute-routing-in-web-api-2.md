---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: "ASP.NET Web API 2에서에서의 라우팅 특성 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 01/20/2014
ms.topic: article
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: ad44ee525601f308498967159e964aa41a2ce00c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="attribute-routing-in-aspnet-web-api-2"></a>ASP.NET Web API 2에서에서 특성의 라우팅
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

*라우팅* 웹 API 작업에 대 한 URI를 일치 하는 방법이 됩니다. Web API 2는 새로운 형식을 지 원하는 라우팅 이라고 *특성 라우팅을*합니다. 이름에서 알 수 있듯이 특성을 사용 하 여 경로 정의 하 특성 라우팅을 합니다. 특성 라우팅을 제어할 수 더 많은 Uri 통해 웹 API에에서 있습니다. 예를 들어 계층의 리소스에 설명 하는 Uri를 쉽게 만들 수 있습니다.

이전 스타일의 라우팅 규칙 기반 라우팅, 프로파일러가 완전히 지원 됩니다. 실제로 같은 프로젝트의 두 가지 방법을 결합할 수 있습니다.

특성 라우팅을 위한 다양 한 옵션이이 항목와 특성 라우팅을 사용 하도록 설정 하는 방법을 보여 줍니다. 특성 라우팅을 사용 하는 종단 간 자습서를 참조 하십시오. [Web API 2에 특성 라우팅을 사용 하 여 REST API 만들기](create-a-rest-api-with-attribute-routing.md)합니다.


## <a name="prerequisites"></a>필수 구성 요소

[Visual Studio 2017](https://www.visualstudio.com/vs/) Community, Professional 또는 Enterprise Edition

또는, NuGet 패키지 관리자를 사용 하 여 필요한 패키지를 설치 합니다. **도구** 선택 Visual Studio에서 메뉴 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>라우팅 특성 이유?

사용 되는 Web API의 첫 번째 릴리스에서 *규칙 기반* 라우팅입니다. 라우팅의 해당 형식에 하나를 정의 하거나 기본적으로 더 많은 경로 템플릿 문자열을 매개 변수화 합니다. 프레임 워크는 요청을 받으면 경로 템플릿에 대 한 URI와 일치 합니다. (규칙 기반 라우팅에 대 한 자세한 내용은 참조 [ASP.NET Web API에서 라우팅](routing-in-aspnet-web-api.md)합니다.

규칙 기반 라우팅의 이점은 한 곳에 정의 된 템플릿 및 라우팅 규칙은 모든 컨트롤러 일관 되 게 적용 됩니다입니다. 안타깝게도, 라우팅 규칙 기반 하는 것 RESTful Api에 공통 되는 특정 URI 패턴을 지원 합니다. 예를 들어 리소스 자식 리소스를 주로 포함: 고객이 주문을 갖고, 영화 작업자에는, 책 저자 등과 합니다. 이러한 관계를 반영 하는 Uri를 만들 수입니다.

`/customers/1/orders`

이러한 유형의 URI 규칙 기반 라우팅을 사용 하 여 만드는 어렵습니다. 완료할 수 있지만 많은 컨트롤러 또는 리소스 종류를 설정한 경우에 결과 크기가 조정 하지 않습니다.

특성 라우팅을 사용 하 여이 URI에 대 한 경로 정의 하는 것이 쉽습니다. 컨트롤러 동작에는 특성을 추가 하기만 하면:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

다음은 라우팅 사용 하면 쉽게 특성 다른 몇 가지 패턴입니다.

**API 버전 관리**

이 예제에서는 "/ api/v 1/제품"과 다른 제어 라우트된 "/ api/v2/제품" 것입니다.

`/api/v1/products`  
`/api/v2/products`

**오버 로드 된 URI 세그먼트**

이 예제에서는 "1" 주문 번호 이지만 컬렉션에 "보류 중" 매핑됩니다.

`/orders/1`  
`/orders/pending`

**여러 매개 변수 형식**

이 예에서는 주문 번호를 "1"은 하지만 "16/06/2013" 날짜를 지정 합니다.

`/orders/1`  
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>특성 라우팅을 사용 하도록 설정

특성 라우팅을 사용 하려면 호출 **MapHttpAttributeRoutes** 구성 중입니다. 에 정의 되어이 확장 메서드는 **System.Web.Http.HttpConfigurationExtensions** 클래스입니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

특성 라우팅을와 결합할 수 있습니다 [규칙 기반](routing-in-aspnet-web-api.md) 라우팅입니다. 호출 규칙 기반 경로 정의 하려면는 **MapHttpRoute** 메서드.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

웹 API를 구성 하는 방법에 대 한 자세한 내용은 참조 [구성 ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md)합니다.

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>참고: Web API 1에서 마이그레이션

Web API 2 하기 전에 웹 API 프로젝트 템플릿은 다음과 같은 코드 생성:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

특성 라우팅을 사용 하는 경우이 코드는 예외가 throw 됩니다. 특성 라우팅을 사용 하려면 기존 웹 API 프로젝트를 업그레이드 하는 경우에 다음이 구성 코드를 업데이트 해야 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> 자세한 내용은 참조 [ASP.NET 호스팅와 Web API 구성](../advanced/configuring-aspnet-web-api.md#webhost)합니다.


<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>경로 특성 추가

특성을 사용 하 여 정의 하는 경로 예는 다음과 같습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

문자열 &quot;고객 / {customerId} orders&quot; 경로 대 한 URI 템플릿입니다. Web API 요청 URI를 템플릿에 일치 시 키 려 합니다. 이 예제에서는 "customers" 및 "orders"가 리터럴 세그먼트가 고 "{customerId}"는 가변 매개 변수입니다. 이 템플릿에 다음 Uri 일치:

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

사용 하 여 일치 프로세스를 제한할 수 있습니다 [제약 조건을](#constraints)이 항목의 뒷부분에 설명 된 대로 합니다.

다음에 유의 &quot;{customerId}&quot; 경로 템플릿에 매개 변수 이름과 일치는 *customerId* 메서드의 매개 변수입니다. Web API 컨트롤러 작업을 호출을 경로 매개 변수에 바인딩할 하려고 시도 합니다. 예를 들어, URI가 `http://example.com/customers/1/orders`, 웹 API 하려고 값 "1"에 바인딩하는 *customerId* 동작에 매개 변수입니다.

URI 템플릿에서 여러 매개 변수를 가질 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

경로 특성이 없는 모든 컨트롤러 메서드 규칙 기반 라우팅을 사용 합니다. 이런 방식으로 두 가지 유형의 라우팅 동일한 프로젝트에 결합할 수 있습니다.

## <a name="http-methods"></a>HTTP 메서드

또한 web API HTTP 메서드 (GET, POST 등)는 요청에 따라 작업을 선택 합니다. 기본적으로 웹 API 컨트롤러 메서드 이름의 시작 되 면 대/소문자 구분 일치 항목을 찾습니다. 예를 들어 라는 컨트롤러 메서드 `PutCustomers` HTTP PUT 요청을 일치 합니다.

재정의할 수 있습니다이 규칙이 준수 mathod 데코레이팅하여 다음과 같은 특성:

- **[HttpDelete]**
- **[HttpGet]**
- **[HttpHead]**
- **[HttpOptions]**
- **[HttpPatch]**
- **[HttpPost]**
- **[HttpPut]**

다음 예제에서는 HTTP POST 요청에 CreateBook 메서드를 매핑합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

사용 하 여 다른 모든 HTTP 메서드를 사용할 수 없는 메서드를 포함 하는 **AcceptVerbs** 목록이 며 HTTP 메서드는 특성입니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>경로 접두사

대개 동일한 접두사로 시작 하는 컨트롤러의 경로입니다. 예:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

사용 하 여 전체 컨트롤러에 대 한 공통 접두사를 설정할 수 있습니다는 **[RoutePrefix]** 특성:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

메서드 특성에 대해 물결표 (~)를 사용 하 여 경로 접두사를 재정의 하려면:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

경로 접두사 매개 변수를 포함할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>경로 제약 조건

경로 제약 조건이 경로 템플릿 매개 변수를 일치 시키는 방법을 제한할 수 있습니다. 일반 구문은 &quot;{매개 변수: 제약 조건}&quot;합니다. 예:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

여기서는 첫 번째 경로 경우에 선택할는 &quot;id&quot; URI의 세그먼트는 정수입니다. 그렇지 않으면 두 번째 경로 선택 됩니다.

다음 표에서 지원 되는 제약 조건을 나열 합니다.

| 제약 조건 | 설명 | 예제 |
| --- | --- | --- |
| 알파 | 일치 하는 항목 대문자 또는 소문자로 라틴어 알파벳 (a ~ z, A-Z) | {x: 알파} |
| bool | 부울 값을 찾습니다. | {x: bool} |
| datetime | 일치는 **DateTime** 값입니다. | {x: datetime을 (를) |
| decimal | 10 진수 값을 찾습니다. | {x: 소수} |
| double | 64 비트 부동 소수점 값을 찾습니다. | {x: double} |
| float | 32 비트 부동 소수점 값을 찾습니다. | {x: float} |
| guid | GUID 값과 일치 합니다. | {x: guid} |
| int | 32 비트 정수 값과 일치 합니다. | {x: int} |
| 길이 | 지정 된 길이로 또는 길이의 지정된 된 범위 내 문자열과 일치합니다. | {x: length(6)} {x: length(1,20)} |
| long | 64 비트 정수 값과 일치 합니다. | {x: long} |
| max | 최대 값을 가진 정수를 찾습니다. | {x: max(10)} |
| maxlength | 최대 길이가 문자열과 일치합니다. | {x: maxlength(10)} |
| 분 | 최소 값이 포함 된 정수를 찾습니다. | {x: min(10)} |
| minlength | 최소 길이가 문자열과 일치합니다. | {x: minlength(10)} |
| range | 정수 값의 범위 내에서 일치합니다. | {x: range(10,50)} |
| 정규식 | 정규식과 일치 합니다. | {x: regex(^\d{3}-\d{3}-\d{4}$)} |

공지 여 제약 조건 중 일부는 같은 &quot;min&quot;, 괄호 안에 인수를 사용 합니다. 콜론으로 구분 된 매개 변수에 여러 개의 제약 조건을 적용할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>사용자 지정 경로 제약 조건

구현 하 여 사용자 지정 경로 제약 조건을 만들 수 있습니다는 **IHttpRouteConstraint** 인터페이스입니다. 예를 들어 다음 제약 조건을 0이 아닌 정수 값을 매개 변수를 제한합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

다음 코드에는 제약 조건을 등록 하는 방법을 보여 줍니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

이제 사용자 경로에 제약 조건을 적용할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

전체를 바꿀 수도 있습니다 **DefaultInlineConstraintResolver** 클래스를 구현 하 여는 **IInlineConstraintResolver** 인터페이스입니다. 이렇게 바뀝니다 모든 기본 제공 제약 조건을 하지 않는 한 구현 **IInlineConstraintResolver** 구체적으로 추가 합니다.

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>선택적 URI 매개 변수 및 기본값

경로 매개 변수를 매개 변수를 추가 하 여 URI 매개 변수를 선택적 만들 수 있습니다. 경로 매개 변수는 선택 사항, 메서드 매개 변수에 대 한 기본값을 정의 해야 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

이 예제에서는 `/api/books/locale/1033` 및 `/api/books/locale` 동일한 리소스를 반환 합니다.

또는 다음과 같이 경로 템플릿 안에 기본값을 지정할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

앞의 예제와 거의 동일 하지만 기본값 적용 될 때 동작의 약간의 차이만 있습니다.

- 정확한 값이 매개 변수를 가집니다 ("{lcid?}") 첫 번째 예제에서 1033의 기본값 메서드 매개 변수에 직접 할당 됩니다.
- 두 번째 예제에서 ("{lcid 1033 =}"), "1033" 기본값인 모델 바인딩 프로세스를 진행 합니다. 기본 모델 바인더 숫자 값 1033 "1033"로 변환 됩니다. 그러나 다른 작업을 수행할 수 있는 사용자 지정 모델 바인더에 연결할 수 있습니다.

(대부분의 경우에서 파이프라인에서 사용자 지정 모델 바인더를 없는 경우 두 형식의 수는 동일 합니다.)

<a id="route-names"></a>
## <a name="route-names"></a>경로 이름

Web API에서 모든 경로는 이름이 있습니다. 경로 이름은 HTTP 응답의 링크를 포함할 수 있도록 링크를 생성 하는 데 유용 합니다.

경로 이름을 지정 하려면는 **이름** 특성에는 속성입니다. 다음 예제에서는 경로 이름을 설정 하는 방법 및 링크를 생성 하는 경우 경로 이름을 사용 하는 방법을 보여 줍니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>경로 순서

프레임 워크 경로 사용 하 여 URI를 일치 시 키 려, 경로 특정 순서로 평가 합니다. 순서를 지정 하려면 설정는 **RouteOrder** 경로 특성에는 속성입니다. 값이 낮을수록 먼저 계산 됩니다. 기본 순서 값은 0입니다.

총 순서를 결정 하는 방법을 다음과 같습니다.

1. 비교는 **RouteOrder** 경로 특성의 속성입니다.
2. 경로 템플릿에 각 URI 세그먼트를 살펴봅니다. 각 세그먼트에 대해 다음과 같이 정렬 합니다. 

    1. 리터럴 세그먼트입니다.
    2. 제약 조건으로 경로 매개 변수입니다.
    3. 제약 조건 없이 경로 매개 변수입니다.
    4. 제약 조건으로 와일드 카드 매개 변수 세그먼트입니다.
    5. 제약 조건 없이 와일드 카드 매개 변수 세그먼트입니다.
3. 동률의 경우 경로 대/소문자 비구분 서 수 문자열 비교로 정렬 됩니다 ([OrdinalIgnoreCase](https://msdn.microsoft.com/en-us/library/system.stringcomparer.ordinalignorecase.aspx))의 경로 템플릿입니다.

예를 들면 다음과 같습니다. 다음 컨트롤러 정의 있다고 가정 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

이러한 경로 다음과 같이 정렬 됩니다.

1. 주문/세부 정보
2. 주문 / {id}
3. 주문 / {customerName}
4. 주문 / {\*날짜}
5. 주문 / 보류 중

"Details"는 리터럴 세그먼트 및 "{id}" 앞에 표시 되 있지만 "보류 중" 표시 마지막는 **RouteOrder** 속성은 1입니다. (이 예에서는 고객이 없는 "details" 라고 가정 "보류 중" 또는 합니다. 일반적으로 모호한 경로 방지 하려고 합니다. 이 예제에 대 한 더 나은 경로 템플릿 `GetByCustomer` 는 "고객이 / {customerName}")
