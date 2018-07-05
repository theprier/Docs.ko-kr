---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2에에서 대 한 라우팅 특성 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 52164fde1a2277bb9ef07f2a5476ca78b71a8e52
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37802759"
---
<a name="attribute-routing-in-aspnet-web-api-2"></a>ASP.NET Web API 2에서에서 특성 라우팅
====================
[Mike Wasson](https://github.com/MikeWasson)

*라우팅* 는 Web API 작업에 대 한 URI를 일치 하는 방법입니다. Web API 2에는 새 형식을 지 원하는 라우팅의 호출 *특성 라우팅은*합니다. 이름에서 알 수 있듯이 특성 라우팅을 사용 하 여 특성 경로 정의. 특성 라우팅을 제어할 수 자세한 Uri 통해 web API에에서 있습니다. 예를 들어, 리소스의 계층 구조를 설명 하는 Uri를 쉽게 만들 수 있습니다.

호출 규칙 기반 라우팅의 이전 스타일 라우팅 완벽 하 게 지원 됩니다. 사실, 동일한 프로젝트에 두 가지 방법을 결합할 수 있습니다.

이 항목에서는 특성 라우팅을 사용 하도록 설정 하는 방법을 보여 줍니다 하 고 특성 라우팅에 대 한 다양 한 옵션을 설명 합니다. 특성 라우팅을 사용 하는 종단 간 자습서를 참조 하세요 [Web API 2에서 특성 라우팅을 사용 하 여 REST API를 만들고](create-a-rest-api-with-attribute-routing.md)합니다.


## <a name="prerequisites"></a>전제 조건

[Visual Studio 2017](https://www.visualstudio.com/vs/) Community, Professional 또는 Enterprise Edition

또는, NuGet 패키지 관리자를 사용 하 여 필요한 패키지를 설치 합니다. **도구** Visual Studio에서 메뉴 **라이브러리 패키지 관리자**을 선택한 후 **패키지 관리자 콘솔**합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>라우팅 특성 이유?

사용 되는 웹 API의 첫 번째 릴리스인 *규칙 기반* 라우팅입니다. 라우팅의 해당 형식에 하나를 정의 하거나 더 많은 경로 템플릿은 기본적으로 문자열을 매개 변수화 합니다. 프레임 워크는 요청을 받으면 경로 템플릿에 대 한 URI와 일치 합니다. (규칙 기반 라우팅에 대 한 자세한 내용은 참조 하십시오 [ASP.NET Web API에서 라우팅](routing-in-aspnet-web-api.md)합니다.

규칙 기반 라우팅의 장점 중 하나는 한 곳에 정의 된 템플릿 및 라우팅 규칙은 모든 컨트롤러에서 일관 되 게 적용 됩니다. 그러나 규칙 기반 라우팅 하기가 어렵습니다 RESTful Api에 공통 되는 특정 URI 패턴을 지원 하도록 합니다. 예를 들어 리소스 자식 리소스를 종종 포함: 고객이 주문을 갖고, 영화 행위자, 책 저자 있고 등입니다. 이러한 관계를 반영 하는 Uri를 만드는 자연 스러운 것:

`/customers/1/orders`

이러한 유형의 URI 규칙 기반 라우팅을 사용 하 여 만드는 어렵습니다. 수행 될 수 있지만 컨트롤러 많거나 리소스 형식이 있는 경우에 결과 확장 하지 않습니다.

특성 라우팅을 사용 하 여이 URI에 대 한 경로 정의 하는 것이 간단 합니다. 단순히 컨트롤러 작업에 특성을 추가 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

특성 라우팅는 쉽게 몇 가지 다른 패턴 다음과 같습니다.

**API 버전 관리**

이 예제에서는 "/ 제품/api/v1" 보다 다른 컨트롤러에 게 회람 "/ 제품/api/v2" 것입니다.

`/api/v1/products`  
`/api/v2/products`

**오버 로드 된 URI 세그먼트**

이 예제에서는 주문 번호를 "1"은 있지만 컬렉션에 "보류 중"으로 매핑합니다.

`/orders/1`  
`/orders/pending`

**여러 매개 변수 유형**

이 예제에서는 주문 번호를 "1"은 있지만 "2013/06/16" 날짜를 지정 합니다.

`/orders/1`  
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>특성 라우팅을 사용 하도록 설정

특성 라우팅을 사용, 호출 **MapHttpAttributeRoutes** 구성 중입니다. 에 정의 되어이 확장 메서드는 **System.Web.Http.HttpConfigurationExtensions** 클래스입니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

특성 라우팅을 결합할 수 있습니다 [규칙 기반](routing-in-aspnet-web-api.md) 라우팅입니다. 규칙 기반 경로 정의 하려면 호출을 **MapHttpRoute** 메서드.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

Web API를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [ASP.NET Web API 2 구성](../advanced/configuring-aspnet-web-api.md)합니다.

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>참고: Web API 1에서 마이그레이션

Web API 2, 이전에 Web API 프로젝트 템플릿이 다음과 같은 코드 생성:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

특성 라우팅을 사용 하는 경우이 코드는 예외가 throw 됩니다. 특성 라우팅을 사용 하도록 기존 Web API 프로젝트를 업그레이드 하는 경우이 구성 코드를 다음으로 업데이트 해야 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> 자세한 내용은 [ASP.NET 호스트를 사용한 Web API 구성](../advanced/configuring-aspnet-web-api.md#webhost)합니다.


<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>경로 특성 추가

특성을 사용 하 여 정의 하는 경로의 예는 다음과 같습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

문자열 &quot;고객 / {customerId} orders&quot; 경로 대 한 URI 템플릿입니다. Web API 템플릿 요청 URI를 일치 시 키 려 합니다. 이 예제에서는 "customers" 및 "orders"는 리터럴 세그먼트 및 "{customerId}"은 변수 매개 변수입니다. 다음 Uri이이 템플릿을 일치 합니다.

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

사용 하 여 일치 하는 것을 제한할 수 있습니다 [제약 조건](#constraints)이 항목의 뒷부분에 설명 합니다.

있음을 합니다 &quot;{customerId}&quot; 경로 템플릿에 매개 변수 이름과 일치 하는 *customerId* 메서드의 매개 변수입니다. Web API 컨트롤러 작업을 호출 하는 경우 경로 매개 변수를 바인딩합니다 하려고 합니다. 예를 들어, URI가 `http://example.com/customers/1/orders`, Web API 하려고 "1" 값을 바인딩하는 *customerId* 작업에서 매개 변수입니다.

URI 템플릿을 여러 매개 변수를 포함할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

경로 특성이 없는 컨트롤러 메서드 규칙 기반 라우팅을 사용 합니다. 이런 방식으로 두 가지 유형의 동일한 프로젝트에서 라우팅을 결합할 수 있습니다.

## <a name="http-methods"></a>HTTP 메서드

또한 웹 API는 HTTP 메서드 (GET, POST 등) 요청에 따라 작업을 선택 합니다. 기본적으로 Web API 컨트롤러 메서드 이름의 시작 부분을 사용 하 여 대/소문자 일치 항목을 찾습니다. 예를 들어 컨트롤러 메서드가 `PutCustomers` HTTP PUT 요청을 일치 합니다.

재정의할 수 있습니다이 규칙 하나를 사용 하 여 메서드를 데코레이팅하여 다음과 같은 특성.

- **[HttpDelete]**
- **[HttpGet]**
- **[HttpHead]**
- **[HttpOptions]**
- **[HttpPatch]**
- **[HttpPost]**
- **[HttpPut]**

다음 예제에서는 HTTP POST 요청으로 CreateBook 메서드를 매핑합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

다른 모든 HTTP 메서드를 비표준 메서드를 포함 하 여 사용 합니다 **AcceptVerbs** HTTP 메서드 목록을 사용 하는 특성입니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>경로 접두사

종종 동일한 접두사로 시작 하는 모든 컨트롤러의 경로입니다. 예를 들어:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

전체 컨트롤러에 대 한 공통 접두사를 사용 하 여 설정할 수 있습니다 합니다 **[RoutePrefix]** 특성:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

경로 접두사를 재정의 하려면 메서드 특성에 물결표 (~)를 사용 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

경로 접두사는 매개 변수를 포함할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>경로 제약 조건

경로 제약 조건은 경로 템플릿에 매개 변수를 일치 시키는 방법을 제한할 수 있습니다. 일반 구문은 &quot;{0} 매개 변수: 제약 조건}&quot;합니다. 예를 들어:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

여기에서 첫 번째 경로 경우에 선택할 합니다 &quot;id&quot; URI의 세그먼트는 정수입니다. 그렇지 않으면 두 번째 경로 선택 됩니다.

다음 표에서 지원 되는 제약 조건을 나열 합니다.

| 제약 조건 | 설명 | 예 |
| --- | --- | --- |
| 알파 | 일치 대문자 또는 소문자로 라틴어 알파벳 문자 (a-z A-z) | {x: 알파} |
| bool | 부울 값과 일치 합니다. | {x: bool} |
| datetime | 일치 하는 **날짜/시간** 값입니다. | {x:datetime} |
| decimal | 10 진수 값과 일치 합니다. | {x:decimal} |
| double | 64 비트 부동 소수점 값과 일치 합니다. | {x:double} |
| float | 32 비트 부동 소수점 값과 일치 합니다. | {x: float} |
| guid | GUID 값과 일치 합니다. | {x: guid} |
| int | 32 비트 정수 값과 일치 합니다. | {x: int} |
| 길이 | 지정된 된 길이 사용 하 여 또는 길이의 지정된 된 범위 내의 문자열과 일치합니다. | {x: length(6)} {x: length(1,20)} |
| long | 64 비트 정수 값과 일치 합니다. | {x: 장기} |
| max | 정수 최대값을 찾습니다. | {x:max(10)} |
| maxlength | 최대 길이 사용 하 여 문자열과 일치합니다. | {x:maxlength(10)} |
| 분 | 정수 최소값을 찾습니다. | {x:min(10)} |
| minlength | 최소 길이 사용 하 여 문자열과 일치합니다. | {x: minlength(10)} |
| range | 정수 값의 범위 내에서 일치합니다. | {x: range(10,50)} |
| 정규식 | 정규식과 일치 합니다. | {x: regex(^\d{3}-\d{3}-\d{4}$)} |

알림 제약 조건 중 일부는 같은 &quot;min&quot;, 괄호 안에 인수를 사용 합니다. 콜론으로 구분 된 매개 변수에 여러 제약 조건을 적용할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>사용자 지정 경로 제약 조건

구현 하 여 사용자 지정 경로 제약 조건을 만들 수 있습니다 합니다 **IHttpRouteConstraint** 인터페이스입니다. 예를 들어, 다음 제약 조건이 0이 아닌 정수 값으로 매개 변수를 제한합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

다음 코드에는 제약 조건을 등록 하는 방법을 보여 줍니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

이제 경로에서 제약 조건을 적용할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

전체를 바꿀 수도 있습니다 **DefaultInlineConstraintResolver** 구현 하 여 클래스를 **IInlineConstraintResolver** 인터페이스입니다. 이렇게 바뀝니다 모든 기본 제약 조건, 하지 않는 한 구현의 **IInlineConstraintResolver** 구체적으로 추가 합니다.

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>선택적 URI 매개 변수 및 기본 값

선택적 URI 매개 변수를 경로 매개 변수를 매개 변수를 추가 하 여 가능 합니다. 경로 매개 변수는 선택 사항, 메서드 매개 변수의 기본값을 정의 해야 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

이 예에서 `/api/books/locale/1033` 고 `/api/books/locale` 동일한 리소스를 반환 합니다.

또는 경로 템플릿 내에서 기본 값을 다음과 같이 지정할 수 있습니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

이전 예제와 거의 동일 하지만 기본값 적용 될 때 동작의 약간의 차이점이 있을 합니다.

- 첫 번째 예에서 ("{lcid?}") 매개 변수는 정확한 값이 있으므로 1033의 기본값은 메서드 매개 변수를 직접 할당 됩니다.
- 두 번째 예제에서 ("{lcid 1033 =}"), 기본값인 "1033" 모델 바인딩 프로세스를 진행 합니다. 기본 모델 바인더를 숫자 값 1033 "1033"로 변환 됩니다. 그러나 다른 작업을 수행할 수 있는 사용자 지정 모델 바인더에 연결할 수 있습니다.

(대부분의 경우에서 파이프라인에서 사용자 지정 모델 바인더 경우가 아니라면 두 형식의 해당 됩니다.)

<a id="route-names"></a>
## <a name="route-names"></a>경로 이름

Web API에서 모든 경로는 이름이 있습니다. 경로 이름은 HTTP 응답의 링크를 포함할 수 있도록 링크를 생성할 때 유용 합니다.

경로 이름을 지정 하려면 설정 합니다 **이름** 속성입니다. 다음 예제에서는 경로 이름을 설정 하는 방법 및 링크를 생성 하는 경우 경로 이름을 사용 하는 방법을 보여 줍니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>경로 순서

프레임 워크 경로 사용 하 여 URI를 찾으려고 하는 경우에 특정 순서 대로 경로 평가 합니다. 순서를 지정 하려면 설정 합니다 **RouteOrder** 속성 경로입니다. 값이 낮을수록 먼저 평가 됩니다. 기본 순서 값은 0입니다.

전체 순서를 결정 하는 방법을 다음과 같습니다.

1. 비교는 **RouteOrder** 경로 특성의 속성입니다.
2. 경로 템플릿에 각 URI 세그먼트를 살펴봅니다. 각 세그먼트에 대 한 다음과 같은 정렬 합니다. 

    1. 리터럴 세그먼트입니다.
    2. 제약 조건으로 경로 매개 변수입니다.
    3. 제약 조건 없이 경로 매개 변수입니다.
    4. 제약 조건 사용 하 여 와일드 카드 매개 변수 세그먼트입니다.
    5. 제약 조건 없이 와일드 카드 매개 변수 세그먼트입니다.
3. 동률의 경우 경로 대/소문자는 서 수 문자열 비교로 정렬 됩니다 ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx))의 경로 템플릿입니다.

예를 들면 다음과 같습니다. 다음 컨트롤러를 정의 한다고 가정 합니다.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

이러한 경로 다음과 같이 정렬 됩니다.

1. 주문/세부 정보
2. 주문 / {id}
3. orders/{customerName}
4. orders/{\*date}
5. orders/pending

"Details" 리터럴 세그먼트 "{id}" 앞에 나타나는 있지만 "pending" 마지막으로 때문에 표시 됩니다 하는 **RouteOrder** 속성은 1입니다. (이 예에서는 고객이 없는 "details" 라고 가정 있습니다 "보류 중" 또는 합니다. 일반적으로 모호한 경로가 것을 방지 하려고 합니다. 이 예에 대 한 더 나은 경로 템플릿 `GetByCustomer` 는 "customers / {customerName}")
