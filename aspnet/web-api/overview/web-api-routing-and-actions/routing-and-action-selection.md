---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: 라우팅 및 ASP.NET Web API의에서 작업 선택 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/27/2012
ms.topic: article
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 997582263bd48590b74434ee0ffc6be928fa1e08
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="routing-and-action-selection-in-aspnet-web-api"></a>라우팅 및 ASP.NET Web API의에서 작업 선택
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

이 문서에서는 ASP.NET Web API 컨트롤러에서 특정 동작에 HTTP 요청을 라우팅하 하는 방법에 대해 설명 합니다.

> [!NOTE]
> 라우팅의 대략적인 개요를 참조 하십시오. [ASP.NET Web API에서 라우팅](routing-in-aspnet-web-api.md)합니다.


이 문서 라우팅 프로세스의 세부 정보를 살펴봅니다. 웹 API 프로젝트를 만들고 일부 요청을 가져올 수 없음 찾기 예상 대로 라우팅 다행 스럽게도이 문서는 데 도움이 됩니다.

라우팅에 세 개의 주요 단계가 있습니다.

1. URI를 경로 템플릿에 일치 합니다.
2. 컨트롤러를 선택 하면 됩니다.
3. 작업을 선택 하면 됩니다.

사용자 고유의 사용자 지정 동작을 프로세스의 일부분을 바꿀 수 있습니다. 이 문서에서는 기본 동작에 설명합니다. 마지막으로 언급 동작을 사용자 지정할 수 있는 위치입니다.

## <a name="route-templates"></a>경로 템플릿

경로 템플릿을 URI 경로 유사 하지만 중괄호로 표시 되는 자리 표시자 값을 가질 수 있습니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

경로 만들 때에 자리 표시자의 일부 또는 전부에 대 한 기본값을 제공할 수 있습니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

제약 조건, 제한 URI 세그먼트 자리 표시자를 일치 수 정도 제공할 수 있습니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

프레임 워크를 템플릿에 URI 경로 세그먼트를 일치 시 키 려 합니다. 서식 파일에 있는 리터럴은 정확 하 게 일치 해야 합니다. 자리 표시자 제약 조건을 지정 하지 않는 한 모든 값을 일치 합니다. 프레임 워크에는 호스트 이름 또는 쿼리 매개 변수와 같은 URI의 다른 부분 일치 하지 않습니다. 프레임 워크는 URI와 일치 하면 경로 테이블의 첫 번째 경로 선택 합니다.

두 가지 특수 한 자리 표시 자가: "{컨트롤러}" 및 "{action}"입니다.

- "{컨트롤러}" 컨트롤러의 이름을 제공합니다.
- "{action}" 작업의 이름을 제공합니다. 웹 API 일반적인 규칙은 "{action}"를 생략 합니다.

### <a name="defaults"></a>기본값

기본값을 제공 하는 경우 경로 세그먼트를 누락 하는 URI를 일치 합니다. 예:

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

URI "`http://localhost/api/products`"이이 경로 일치 합니다. "{범주}" 세그먼트에는 "all" 기본값이 할당 됩니다.

### <a name="route-dictionary"></a>경로 사전

프레임 워크는 URI에 대 한 일치 하는 찾으면 하는 경우에 각 자리 표시자에 대 한 값이 포함 된 사전을 만듭니다. 키는 중괄호를 포함 하지 않고 자리 표시자 이름을입니다. 값 또는 기본값의 URI 경로에서 가져옵니다. 사전에 저장 되는 **IHttpRouteData** 개체입니다.

이 경로 일치 하는 단계는 특별 한 "{컨트롤러}" 및 "{action}" 자리 표시자 다른 자리 표시자와 동일 하 게 처리 됩니다. 다른 값을 사용 하 여 사전에 저장 하기만 하면 됩니다.

특수 값이 있을 수는 기본 **RouteParameter.Optional**합니다. 자리 표시자가이 값을 할당 하는 경우 값을 경로 사전에 추가 되지 않습니다. 예:

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

URI 경로 "api/products"에 대 한 경로 사전을 포함 됩니다.

- 컨트롤러: "products"
- 범주: "all"

그러나 "Api/제품/toys/123", 경로 사전을 포함 됩니다.

- 컨트롤러: "products"
- 범주: "toys"
- id: "123"

또한 기본값 경로 서식 파일에서 아무 곳 이나 표시 되지 않는 값을 포함할 수 있습니다. 경로가 일치 하는 경우 해당 값이 사전에 저장 됩니다. 예:

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

URI 경로 "8/api/루트" 이면 사전 두 값이 포함 됩니다.

- 컨트롤러: "customers"
- id: "8"

## <a name="selecting-a-controller"></a>컨트롤러를 선택 하면

컨트롤러 선택 하 여 처리 되는 **IHttpControllerSelector.SelectController** 메서드. 이 메서드는 **HttpRequestMessage** 인스턴스와 반환은 **HttpControllerDescriptor**합니다. 기본 구현에서 제공 되는 **DefaultHttpControllerSelector** 클래스입니다. 이 클래스는 간단한 알고리즘을 사용 합니다.

1. "컨트롤러" 키에 대 한 경로 사전을 확인 합니다.
2. 이 키에 대 한 값을 사용 하 고 컨트롤러 형식 이름을 가져오려면 "컨트롤러" 문자열을 추가 하세요.
3. 이 형식 이름 사용 하 여 Web API 컨트롤러를 찾습니다.

예를 들어 경로 사전을 키-값 쌍 "컨트롤러" = "products" 컨트롤러 형식 "ProductsController"입니다. 일치 하는 형식이 없습니다 또는 여러 명의 일치 항목이 있는 경우 프레임 워크 오류가 클라이언트에 반환 됩니다.

3 단계에 대 한 **DefaultHttpControllerSelector** 사용 하 여는 **IHttpControllerTypeResolver** 인터페이스 Web API 컨트롤러 형식의 목록을 가져올 수 있습니다. 기본 구현은 **IHttpControllerTypeResolver** (a) 구현 하는 모든 공용 클래스를 반환 합니다. **IHttpController**, (b)은 abstract, 및 (c) 이름이 "컨트롤러"로 끝나는 되지 않습니다.

## <a name="action-selection"></a>작업 선택

컨트롤러를 선택한 후 프레임 워크를 호출 하 여 작업을 선택 된 **IHttpActionSelector.SelectAction** 메서드. 이 메서드는 **HttpControllerContext** 반환는 **HttpActionDescriptor**합니다.

기본 구현에서 제공 되는 **ApiControllerActionSelector** 클래스입니다. 작업을 선택 하려면 다음에서 찾습니다.

- 요청의 HTTP 메서드입니다.
- 있는 경우 경로 템플릿에서 "{action}" 자리 표시자입니다.
- 컨트롤러 동작의 매개 변수입니다.

선택 알고리즘을 보고 하기 전에 컨트롤러 작업에 대 한 몇 가지 사항을 이해 해야 합니다.

**컨트롤러에서 메서드 "작업" 것으로 간주 됩니다?** 동작을 선택할 때 프레임 워크만 확인 공용 인스턴스 메서드를 컨트롤러에 있습니다. 또한이 메서드를 제외 ["특수 name"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) 메서드 (생성자, 이벤트, 연산자 오버 로드 등), 및에서 상속 된 메서드는 **ApiController** 클래스입니다.

**HTTP 메서드입니다.** 프레임 워크는만 다음과 같이 결정 요청의 HTTP 메서드를 일치 하는 작업을 선택 합니다.

1. 특성이 지정 된 HTTP 메서드를 지정할 수 있습니다: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**,  **HttpOptions**, **HttpPatch**, **HttpPost**, 또는 **HttpPut**합니다.
2. 그렇지 않은 경우와 컨트롤러 메서드의 이름을 "Get", "Post", "Put", "Delete", "h e a d", "옵션" 또는 "패치"으로 시작 하는 경우 다음 규칙에 따라 동작 해당 HTTP 메서드를 지원 합니다.
3. None 인 경우 메서드는 POST를 지원 합니다.

**매개 변수 바인딩입니다.** 매개 변수 바인딩은 Web API는 매개 변수의 값을 만드는 방법입니다. 다음은 매개 변수 바인딩에 대 한 기본 규칙이입니다.

- URI에서 단순 유형은 가져옵니다.
- 요청 본문에서 복합 형식은 가져옵니다.

단순 형식에 포함할 모든는 [.NET Framework 기본 형식](https://msdn.microsoft.com/library/system.type.isprimitive), 플러스 **DateTime**, **10 진수**, **Guid**, **문자열** , 및 **TimeSpan**합니다. 각 동작에 대해 최대 하나의 매개 변수는 요청 본문을 읽을 수 있습니다.

> [!NOTE]
> 기본 바인딩 규칙을 재정의 하는 것이 불가능 합니다. 참조 [내부적인 WebAPI 매개 변수 바인딩을](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)합니다.


해당 배경에 동작 선택 알고리즘이 같습니다.

1. HTTP 요청 메서드를 일치 하는 컨트롤러에 모든 동작의 목록을 만듭니다.
2. 경로 사전을 "작업" 항목이 있으면 이름이이 값과 일치 하지 않는 작업을 제거 합니다.
3. URI에 액션 매개 변수를 다음과 같이 일치 하려고 합니다. 

    1. 각 작업에 대 한 매개 변수는 단순 형식의 바인딩을 URI에서 매개 변수를 가져옵니다의 목록을 가져옵니다. 선택적 매개 변수를 제외 합니다.
    2. 이 목록에서 경로 사전을 또는 URI 쿼리 문자열에서 각 매개 변수 이름에 대 한 일치 하는 항목을 찾아 봅니다. 대/소문자 및 매개 변수 순서에 의존 하지 않는 항목 합니다.
    3. URI에서 모든 매개 변수 목록에서 일치 하는 항목에 있는 작업을 선택 합니다.
    4. 하나의 작업 보다 이러한 조건에 부합 하는 경우 대부분 매개 변수 일치 항목 하나를 선택 합니다.
4. 사용 하 여 동작을 무시 된 **[NonAction]** 특성입니다.

단계 # 3는 아마도 가장 복잡 합니다. 기본 개념 적용 되는 URI, 요청 본문에서 또는에서 사용자 지정 바인딩을 매개 변수 값을 가져올 수 있습니다. URI에서 제공 하는 매개 변수에 대 한 URI (경로 사전)를 통해 경로 또는 쿼리 문자열에 해당 매개 변수의 값을 실제로 포함 되어 있는지 확인 하려고 합니다.

예를 들어, 다음 작업을 살펴보겠습니다.

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

*id* uri 매개 변수를 바인딩합니다. 따라서이 작업에 "id", 경로 사전을 또는 쿼리 문자열에 대 한 값을 포함 하는 URI만 찾을 수 있습니다.

선택적 매개 변수는 선택 사항 이므로 한 예외. 선택적 매개 변수에 대 한 것이 확인 바인딩을 URI에서 값을 가져올 수 없습니다.

복합 형식은 다른 이유를 예외가 됩니다. 복합 형식은 사용자 지정 바인딩을 통해 URI에만 바인딩할 수 있습니다. 하지만 경우 프레임 워크를 알 수 없으므로 미리 매개 변수는 특정 URI에 바인딩하는 것 여부. 를 찾으려면 바인딩을 호출 해야 합니다. 선택 알고리즘의 목표 정적 설명에 있는 모든 바인딩에 호출 하기 전에 작업을 선택 하는 것입니다. 따라서 복합 형식 일치 알고리즘에서 제외 됩니다.

동작을 선택한 후에 모든 매개 변수 바인딩이 호출 됩니다.

요약:

- 작업 요청의 HTTP 메서드를 일치 해야 합니다.
- 작업 이름이 있는 경우 경로 사전에 있는 "action" 항목을 일치 해야 합니다.
- 동작의 모든 매개 변수에 대해 매개 변수는 URI에서 가져온 경우 다음 매개 변수 이름은 해야 찾을 수 경로 사전을 또는 URI 쿼리 문자열입니다. (선택적 매개 변수 및 복합 형식으로 매개 변수는 제외 됩니다.)
- 매개 변수 중 가장 많은 일치 하도록 시도 합니다. 가장 일치 하는 메서드 매개 변수 없이 수도 있습니다.

## <a name="extended-example"></a>확장 된 예제

경로:

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

컨트롤러:

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

HTTP 요청:

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a>경로 일치

URI "DefaultApi" 라는 경로 일치 합니다. 경로 사전을 다음 항목이 포함 되어 있습니다.

- 컨트롤러: "products"
- id: "1"

경로 사전을 쿼리 문자열 매개 변수, "version" 및 "details"는 하지만 작업 선택 중 여전히 고려 되 이러한 합니다.

### <a name="controller-selection"></a>컨트롤러 선택

컨트롤러 종류는 경로 사전의 "컨트롤러" 엔트리에서 `ProductsController`합니다.

### <a name="action-selection"></a>작업 선택

HTTP 요청에는 한 GET 요청이입니다. GET 지원 컨트롤러 작업에는 `GetAll`, `GetById`, 및 `FindProductsByName`합니다. 경로 사전에 "action"에 대 한 항목이 없습니다 작업 이름과 일치 필요가 없습니다.

다음으로, 하려고 작업에 대 한 매개 변수 이름과 일치 GET 작업에만 보고 합니다.

| 작업 | 일치 항목으로 매개 변수 |
| --- | --- |
| `GetAll` | 없음 |
| `GetById` | "id" |
| `FindProductsByName` | "name" |

에 *버전* 의 매개 변수 `GetById` 선택적 매개 변수 이기 때문에 간주 되지 않습니다.

`GetAll` 메서드가 다르거나 일반적으로 일치 합니다. `GetById` 도 일치 하는 메서드가, 경로 사전을 "id"를 포함 하기 때문에 있습니다. `FindProductsByName` 메서드가 일치 하지 않습니다.

`GetById` 메서드 wins에 대 한 매개 변수 없이 또는 하나의 매개 변수가 일치 하기 때문에, `GetAll`합니다. 메서드는 다음 매개 변수 값으로 호출 됩니다.

- *id* = 1
- *버전* = 1.5

경우에 확인 *버전* 사용 되지 않은 선택 알고리즘에서 URI 쿼리 문자열에서 발생 하는 매개 변수의 값입니다.

## <a name="extension-points"></a>확장점

Web API 라우팅 프로세스의 특정 부분에 대 한 확장 지점을 제공합니다.

| 인터페이스 | 설명 |
| --- | --- |
| **IHttpControllerSelector** | 컨트롤러를 선택 합니다. |
| **IHttpControllerTypeResolver** | 컨트롤러 종류의 목록을 가져옵니다. **DefaultHttpControllerSelector** 이 목록에서 컨트롤러 종류를 선택 합니다. |
| **IAssembliesResolver** | 프로젝트 어셈블리의 목록을 가져옵니다. **IHttpControllerTypeResolver** 인터페이스 컨트롤러 유형을 검색 하는이 목록을 사용 합니다. |
| **IHttpControllerActivator** | 새 컨트롤러 인스턴스를 만듭니다. |
| **IHttpActionSelector** | 작업을 선택 합니다. |
| **IHttpActionInvoker** | 작업을 호출 합니다. |

이러한 인터페이스에 대 한 사용자 지정 구현을 제공 하려면 사용 된 **서비스** 컬렉션에는 **HttpConfiguration** 개체:

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
