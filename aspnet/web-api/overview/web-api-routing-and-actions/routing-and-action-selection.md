---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: 라우팅 및 ASP.NET Web API에서에서 작업 선택 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 12/14/2018
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: ce54181996376cb5dde3b91c10c16f33b3c6a570
ms.sourcegitcommit: 6548c19f345850ee22b50f7ef9fca732895d9e08
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53425174"
---
<a name="routing-and-action-selection-in-aspnet-web-api"></a>라우팅 및 ASP.NET Web API에서에서 작업 선택
====================
[Mike Wasson](https://github.com/MikeWasson)

이 문서에서는 ASP.NET Web API 컨트롤러에 특정 작업에 HTTP 요청을 라우트하는 방법을 설명 합니다.

> [!NOTE]
> 라우팅의 개괄적인 개요를 참조 하세요 [ASP.NET Web API에서 라우팅](routing-in-aspnet-web-api.md)합니다.


이 문서에서는 라우팅 프로세스의 세부 정보를 살펴봅니다. Web API 프로젝트를 만들고 일부 요청이 가져올 없는 찾기 예상 대로 라우팅할 바랍니다이 기사의 데 도움이 됩니다.

라우팅에 세 가지 주요 단계가 있습니다.

1. 경로 템플릿에 URI를 비교 합니다.
2. 컨트롤러를 선택합니다.
3. 작업을 선택 합니다.

사용자 고유의 사용자 지정 동작을 사용 하 여 프로세스의 일부를 바꿀 수 있습니다. 이 문서에서는 기본 동작에 설명합니다. 끝으로 동작을 사용자 지정할 수 있는 위치 언급 합니다.

## <a name="route-templates"></a>경로 템플릿

경로 템플릿을 URI 경로 비슷한 보이지만 중괄호를 사용 하 여 표시 된 자리 표시자 값을 가질 수 있습니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

경로 만든 경우에 자리 표시자의 일부 또는 전부에 대 한 기본값을 제공할 수 있습니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

또한 URI 세그먼트를 자리 표시자 수 일치 하는 방법을 제한 하는 제약 조건을 제공할 수 있습니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

프레임 워크는 서식 파일의 URI 경로 세그먼트를 일치 시 키 려 합니다. 템플릿에서 리터럴은 정확 하 게 일치 해야 합니다. 자리 표시자 제약 조건을 지정 하지 않는 한 모든 값과 일치 합니다. 프레임 워크는 호스트 이름 또는 쿼리 매개 변수를 같은 URI의 다른 부분을 일치 하지 않습니다. 프레임 워크는 URI와 일치 하는 경로 테이블의 첫 번째 경로 선택 합니다.

두 가지 특수 한 자리 표시 자가: "{컨트롤러}" 및 "{action}".

- "{컨트롤러}"를 컨트롤러의 이름을 제공합니다.
- "{action}" 작업의 이름을 제공합니다. Web API "{action}"를 생략 하 일반적인 규칙이입니다.

### <a name="defaults"></a>기본값

기본값을 제공 하면 해당 세그먼트가 없는 URI 경로 일치 합니다. 예를 들면 다음과 같습니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

Uri `http://localhost/api/products/all` 고 `http://localhost/api/products` 이전 경로 일치 합니다. 누락 된 두 번째 URI에 `{category}` 세그먼트에는 기본값이 할당 됩니다 `all`합니다.

### <a name="route-dictionary"></a>경로 사전

프레임 워크는 URI와 일치 하는 찾으면 각 자리 표시자에 대 한 값이 들어 있는 사전을 만듭니다. 키는 중괄호를 포함 하지 않고, 자리 표시자 이름을입니다. 기본값 또는 URI 경로에서 값을 가져옵니다. 사전에 저장 되는 **IHttpRouteData** 개체입니다.

이 경로 일치 하는 단계 동안 특별 한 "{컨트롤러}" 및 "{action}" 자리 표시자를 다른 자리 표시자와 마찬가지로 처리 됩니다. 다른 값을 사용 하 여 사전에 저장 하기만 하면 됩니다.

기본값에는 특수 한 값을 가질 수 **RouteParameter.Optional**합니다. 자리 표시자 가져옵니다이 값을 할당 하는 경우 값 경로 사전에 추가 되지 않습니다. 예를 들면 다음과 같습니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

"Api/제품"의 URI 경로 대 한 경로 사전을 포함 됩니다.

- 컨트롤러: "제품"
- 범주: "all"

그러나 "Api/제품/toys/123", 경로 사전을 포함 됩니다.

- 컨트롤러: "제품"
- 범주: "toys"
- id: "123"

기본값은 경로 템플릿에서 아무 곳 이나 표시 되지 않는 값을 포함할 수도 있습니다. 경로 일치 하는 경우 해당 값이 사전에 저장 됩니다. 예를 들면 다음과 같습니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

URI 경로 "api/루트/8" 인 경우 사전 두 값이 포함 됩니다.

- 컨트롤러: "customers"
- id: "8"

## <a name="selecting-a-controller"></a>컨트롤러를 선택합니다.

컨트롤러 선택 하 여 처리 되는 **IHttpControllerSelector.SelectController** 메서드. 이 메서드는 **HttpRequestMessage** 인스턴스와 반환은 **HttpControllerDescriptor**합니다. 기본 구현에서 제공 되는 **DefaultHttpControllerSelector** 클래스입니다. 이 클래스는 간단한 알고리즘을 사용합니다.

1. "Controller" 키에 대 한 경로 사전을 확인 합니다.
2. 이 키에 대 한 값을 사용 하 고 컨트롤러 형식 이름을 가져오려면 "Controller" 문자열을 추가 합니다.
3. 이 형식 이름 사용 하 여 Web API 컨트롤러를 찾습니다.

예를 들어, 경로 사전 키-값 쌍 "controller"가 들어 있으면 = "제품", 컨트롤러 형식 "ProductsController"입니다. 일치 하는 형식이 없는 또는 여러 일치 항목이 있으면 클라이언트에 오류를 반환 하는 프레임 워크.

3 단계에 대 한 **DefaultHttpControllerSelector** 사용 하는 **IHttpControllerTypeResolver** 를 Web API 컨트롤러 유형 목록을 가져오는 인터페이스입니다. 기본 구현의 **IHttpControllerTypeResolver** (a) 구현 하는 모든 공용 클래스를 반환 **IHttpController**, (b)는 abstract (c) 이름이 "Controller"로 끝나는 없고 합니다.

## <a name="action-selection"></a>작업 선택

컨트롤러를 선택 하면 프레임 워크를 호출 하 여 작업을 선택 합니다 **IHttpActionSelector.SelectAction** 메서드. 이 메서드는 **HttpControllerContext** 반환 하 고는 **HttpActionDescriptor**합니다.

기본 구현에서 제공 되는 **ApiControllerActionSelector** 클래스입니다. 작업을 선택 하려면 다음에서 찾습니다.

- 요청의 HTTP 메서드입니다.
- 있는 경우 경로 템플릿에서 "{action}" 자리 표시자입니다.
- 컨트롤러에서 작업의 매개 변수입니다.

선택 알고리즘을 살펴보기 전에 컨트롤러 작업에 대 한 몇 가지 작업을 이해 해야 합니다.

**컨트롤러에서 메서드 "작업" 것으로 간주 됩니다.** 작업을 선택 하면 프레임 워크만 살펴봅니다 공용 인스턴스 메서드는 컨트롤러에서. 제외 뿐만 ["특수 한 이름이"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) 메서드 (생성자, 이벤트, 연산자 오버 로드 등), 및에서 상속 된 메서드는 **ApiController** 클래스입니다.

**HTTP 메서드입니다.** 프레임 워크는만 다음과 같이 결정 요청의 HTTP 메서드를 일치 하는 작업을 선택 합니다.

1. 특성을 사용 하 여 HTTP 메서드를 지정할 수 있습니다. **AcceptVerbs**, **HttpDelete**합니다 **HttpGet**를 **HttpHead**를 **HttpOptions**, **HttpPatch**하십시오 **HttpPost**, 또는 **HttpPut**합니다.
2. 이 고, 그렇지 컨트롤러 메서드의 이름을 "Get", "Post", "Put", "Delete", "Head", "옵션" 또는 "패치"를 사용 하 여 시작 되 면 다음 규칙에 따라 작업 해당 HTTP 메서드를 지원 합니다.
3. 위의 none 인 경우 메서드는 POST를 지원 합니다.

**매개 변수 바인딩입니다.** 매개 변수 바인딩의 경우 Web API는 매개 변수의 값을 만드는 방법 다음은 매개 변수 바인딩에 대 한 기본 규칙이입니다.

- 단순 형식 URI에서 가져옵니다.
- 요청 본문에서 복합 형식은 가져옵니다.

단순 형식에 포함할 모든는 [.NET Framework 기본 형식](https://msdn.microsoft.com/library/system.type.isprimitive), plus **DateTime**, **Decimal**, **Guid**, **문자열** , 및 **TimeSpan**합니다. 각 작업에 대해 최대 하나의 매개 변수는 요청 본문을 읽을 수 있습니다.

> [!NOTE]
> 기본 바인딩 규칙을 재정의 하는 것이 가능 합니다. 참조 [내부적 WebAPI 매개 변수 바인딩](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)합니다.


배경을 사용 하 여 작업 선택 알고리즘은 다음과 같습니다.

1. HTTP 요청 메서드 일치 하는 컨트롤러에서 모든 작업의 목록을 만듭니다.
2. 경로 사전을 "작업" 항목이 있으면 제거 작업 이름이이 값과 일치 하지 않습니다.
3. URI 작업 매개 변수를 다음과 같이 일치 하도록 시도 합니다. 

    1. 각 작업에 대 한 매개 변수는 단순 형식의 바인딩을 URI에서 매개 변수를 가져옵니다의 목록을 가져옵니다. 선택적 매개 변수를 제외 합니다.
    2. 이 목록에서를 URI 쿼리 문자열 또는 경로 사전을에서 각 매개 변수 이름에 대해 일치 하는 항목을 찾아 봅니다. 일치는 대/소문자 구분 및 매개 변수 순서에 종속 되지 않습니다.
    3. 모든 매개 변수 목록에 있는 일치 하는 URI에서 작업을 선택 합니다.
    4. 이러한 조건을 충족 하는 더 이상의 작업을 하는 경우 대부분의 매개 변수 일치를 사용 하 여 하나를 선택 합니다.
4. 사용 하 여 작업을 무시 합니다 **[NonAction]** 특성입니다.

3 단계 아마도 가장 혼동 됩니다. 기본 개념은 매개 변수는 URI, 요청 본문에서 또는 사용자 지정 바인딩에서 해당 값을 가져올 수 있습니다. URI에서 제공 되는 매개 변수에 대 한 URI (경로 사전)를 통해 경로 또는 쿼리 문자열 매개 변수 값을 실제로 포함 되어 있는지 확인 하려고 합니다.

예를 들어, 다음 작업을 고려 합니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

합니다 *id* uri 매개 변수를 바인딩합니다. 따라서이 작업에 "id", 경로 사전을 또는 쿼리 문자열에 대 한 값이 포함 된 URI 에서만 찾을 수 있습니다.

선택적 매개 변수는 선택 사항 이므로 예외. 선택적 매개 변수에 대 한 것 확인 바인딩을 URI에서 값을 가져올 수 없습니다.

복합 형식에는 다른 이유로 예외입니다. 복합 형식 사용자 지정 바인딩을 통해 URI에만 바인딩할 수 있습니다. 하지만 경우 프레임 워크를 알 수 없으므로 사전에 매개 변수는 특정 URI에 바인딩하는 것 여부를 합니다. 에 바인딩을 호출 해야 합니다. 선택 알고리즘의 목표 바인딩을 호출 하기 전에 정적 설명에서 작업을 선택 하는 것입니다. 따라서 복잡 한 형식 일치 알고리즘에서 제외 됩니다.

작업을 선택한 후에 모든 매개 변수 바인딩 호출 됩니다.

요약:

- 작업 요청의 HTTP 메서드를 일치 해야 합니다.
- 작업 이름이 있는 경우 경로 사전에 "작업" 항목이 일치 해야 합니다.
- 작업의 모든 매개 변수에 대해 매개 변수는 URI에서 가져온 경우 다음 매개 변수 이름 있어야 경로 사전을 또는 URI 쿼리 문자열에서. (선택적 매개 변수 및 복합 형식으로 매개 변수 제외 됩니다.)
- 가장 많은 매개 변수 일치 시 키 려 합니다. 가장 일치 하는 매개 변수 없이 메서드를 수 있습니다.

## <a name="extended-example"></a>확장 된 예제

경로:

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

컨트롤러:

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

HTTP 요청:

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a>경로 일치

URI "DefaultApi" 라는 경로 찾습니다. 경로 사전에는 다음 항목이 포함 됩니다.

- 컨트롤러: "제품"
- id: "1"

쿼리 문자열 매개 변수, "version" 및 "details" 경로 사전을 포함 하지 않지만 이러한 세대로 간주 됩니다 작업 선택 중입니다.

### <a name="controller-selection"></a>컨트롤러 선택

경로 사전에서 "controller" 엔트리에서 컨트롤러 형식이 `ProductsController`합니다.

### <a name="action-selection"></a>작업 선택

HTTP 요청은 GET 요청을 합니다. GET 지 컨트롤러 작업은 `GetAll`, `GetById`, 및 `FindProductsByName`합니다. 경로 사전이 되므로 작업 이름과 일치할 필요가 없습니다 "작업"에 대 한 진입점을 포함 하지 않습니다.

다음으로, 하려고 노력을 작업에 대 한 매개 변수 이름과 일치 GET 작업에만 확인 합니다.

| 작업 | 일치 하는 매개 변수 |
| --- | --- |
| `GetAll` | 없음 |
| `GetById` | "id" |
| `FindProductsByName` | "name" |

다음에 유의 합니다 *버전* 의 매개 변수 `GetById` 선택적 매개 변수 이므로 간주 되지 않습니다.

`GetAll` 메서드는 일반적으로 일치 합니다. `GetById` 메서드 일치, "id"를 포함 하는 경로 사전을 때문입니다. `FindProductsByName` 메서드 일치 하지 않습니다.

합니다 `GetById` 에 대 한 매개 변수 없이와 하나의 매개 변수를 일치 하기 때문에 메서드 wins `GetAll`합니다. 메서드는 다음 매개 변수 값을 사용 하 여 호출 됩니다.

- *id* = 1
- *버전* 1.5 =

도 있음을 *버전* 사용 되지 않는 선택 알고리즘에서 매개 변수의 URI 쿼리 문자열에서 발생 합니다.

## <a name="extension-points"></a>확장점

Web API 라우팅 프로세스의 일부에 대 한 확장 지점을 제공합니다.

| 인터페이스 | 설명 |
| --- | --- |
| **IHttpControllerSelector** | 컨트롤러를 선택합니다. |
| **IHttpControllerTypeResolver** | 컨트롤러 형식의 목록을 가져옵니다. 합니다 **DefaultHttpControllerSelector** 컨트롤러 형식을이 목록에서 선택 합니다. |
| **IAssembliesResolver** | 프로젝트 어셈블리의 목록을 가져옵니다. 합니다 **IHttpControllerTypeResolver** 인터페이스 컨트롤러 유형을 검색 하는이 목록을 사용 합니다. |
| **IHttpControllerActivator** | 새 컨트롤러 인스턴스를 만듭니다. |
| **IHttpActionSelector** | 작업을 선택합니다. |
| **IHttpActionInvoker** | 작업을 호출 합니다. |

사용 하 여 이러한 인터페이스에 대 한 고유한 구현을 제공 합니다는 **Services** 컬렉션에는 **HttpConfiguration** 개체:

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
