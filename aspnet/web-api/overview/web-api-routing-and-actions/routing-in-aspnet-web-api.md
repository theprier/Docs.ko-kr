---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API에서에서 라우팅 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/11/2012
ms.topic: article
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 5e3bba70993dafcdd93feed52813ee80697b1038
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37374207"
---
<a name="routing-in-aspnet-web-api"></a>ASP.NET Web API에서 라우팅
====================
[Mike Wasson](https://github.com/MikeWasson)

이 문서에서는 ASP.NET Web API 컨트롤러에 HTTP 요청을 라우팅합니다 하는 방법을 설명 합니다.

> [!NOTE]
> ASP.NET MVC에 익숙한 경우에 Web API 라우팅는 MVC 라우팅 매우 비슷합니다. 주요 차이점은 Web API URI 경로가 HTTP 메서드를 사용 하 여 작업을 선택 합니다. MVC 스타일 라우팅 Web API에서 사용할 수 있습니다. 이 문서는 ASP.NET MVC에 대 한 정보를 가정 하지 않습니다.


## <a name="routing-tables"></a>라우팅 테이블

ASP.NET Web API에는 *컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다. 컨트롤러의 공용 메서드 호출 됩니다 *작업 메서드에* 있거나 단순히 *작업*합니다. Web API 프레임 워크는 요청을 받으면 요청을 작업에 라우팅합니다.

호출 하는 작업을 확인 하려면 프레임 워크를 사용 하는 *라우팅 테이블*합니다. Visual Studio 프로젝트 템플릿을 웹 API에 대 한 기본 경로 만듭니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

이 경로 앱에 배치 되는 WebApiConfig.cs 파일에 정의 된\_시작 디렉터리:

![](routing-in-aspnet-web-api/_static/image1.png)

에 대 한 자세한 내용은 합니다 **WebApiConfig** 클래스를 참조 하십시오 [ASP.NET Web API 구성](../advanced/configuring-aspnet-web-api.md)합니다.

직접 라우팅 테이블 Web API를 자체 호스트 하는 경우 설정 해야 합니다 **HttpSelfHostConfiguration** 개체입니다. 자세한 내용은 [Web API를 자체 호스팅하는](../older-versions/self-host-a-web-api.md)합니다.

라우팅 테이블의 각 항목에 포함 된 *경로 템플릿을*합니다. 웹 API에 대 한 기본 경로 템플릿은 &quot;api / {컨트롤러} / {id}&quot;합니다. 이 템플릿에서 &quot;api&quot; 리터럴 경로 세그먼트 및 {컨트롤러}, {id}는 자리 표시자 변수입니다.

Web API 프레임 워크는 HTTP 요청을 받으면 라우팅 테이블에 경로 템플릿 중 하나에 대 한 URI를 일치 시 키 려 고 합니다. 경로가 일치 하는 경우 클라이언트는 404 오류를 받습니다. 예를 들어, 다음 Uri는 기본 경로 일치 합니다.

- api 연락처
- /api/contacts/1
- /api/products/gizmo1

그러나 다음 URI와 일치 하지 않으면 포함 하지 않으므로 합니다 &quot;api&quot; 세그먼트:

- / contacts/1

> [!NOTE]
> 경로에 "api"를 사용 하는 이유는 ASP.NET MVC 라우팅를 사용 하 여 충돌을 방지 하기 위해서입니다. 이렇게 할 수 있습니다 &quot;연결/&quot; MVC 컨트롤러로 이동 하 고 &quot;/api/contacts&quot; Web API 컨트롤러를 이동 합니다. 물론,이 규칙을 마음에 들지 않는 경우 기본 경로 테이블을 변경할 수 있습니다.

일치 하는 경로가 발견 되 면 Web API 컨트롤러 및 작업을 선택 합니다.

- Web API 컨트롤러를 찾으려면 추가 &quot;컨트롤러&quot; 의 값을 *{컨트롤러}* 변수입니다.
- 작업을 찾으려면 Web API HTTP 메서드를 찾은 이름이 해당 HTTP 메서드 이름으로 시작 하는 작업을 찾습니다. 예를 들어 GET 요청에서 Web API ()은 시작 액션에 대 한 &quot;가져오기... &quot;와 같은 &quot;GetContact&quot; 하거나 &quot;GetAllContacts&quot;합니다. 이 규칙 GET, POST, PUT, 및 삭제 메서드에만 적용 됩니다. 컨트롤러에서 특성을 사용 하 여 다른 HTTP 메서드를 사용할 수 있습니다. 뒷부분의 예제를 살펴보겠습니다.
- 경로 템플릿에서 다른 자리 표시자 변수가 같은 *{id}* 작업 매개 변수에 매핑됩니다.

예를 살펴보겠습니다. 다음 컨트롤러를 정의 하는 것을 가정 합니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

각각에 대해 호출 되는 동작과 함께 몇 가지 가능한 HTTP 요청을 다음과 같습니다.

| HTTP 메서드 | URI 경로 | 작업 | 매개 변수 |
| --- | --- | --- | --- |
| 가져오기 | api/제품 | GetAllProducts | *(없음)* |
| 가져오기 | api/제품/4 | GetProductById | 4 |
| Delete | api/제품/4 | DeleteProduct | 4 |
| 올리기 | api/제품 | *(일치)* |  |

있음을 합니다 *{id}* URI의 세그먼트가 있는 경우에 매핑되는 *id* 동작의 매개 변수입니다. 이 예제에서는 컨트롤러 정의 된 하나 두 개의 GET 메서드를 *id* 매개 변수 및 매개 변수 없이 합니다.

또한 컨트롤러에서 정의 하지 않으므로 POST 요청은 실패 하는 참고를 &quot;Post 하는 중... &quot; 메서드.

## <a name="routing-variations"></a>라우팅 변형

이전 섹션에서는 ASP.NET Web API에 대 한 기본 라우팅 메커니즘을 설명합니다. 이 섹션에서는 일부 변형을 설명합니다.

### <a name="http-methods"></a>HTTP 메서드

HTTP 메서드에 대 한 명명 규칙을 사용 하는 대신 명시적으로 방법을 지정할 수 있습니다는 HTTP 작업에 대 한 작업 메서드를 데코레이팅하여 합니다 **HttpGet**하십시오 **HttpPut**, **HttpPost** , 또는 **HttpDelete** 특성입니다.

다음 예에서 FindProduct 메서드는 GET 요청에 매핑됩니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

작업에 대 한 여러 HTTP 메서드를 허용 하거나 이외의 GET, PUT, POST 및 DELETE HTTP 메서드를 허용 하려면 사용 합니다 **AcceptVerbs** HTTP 메서드 목록을 사용 하는 특성입니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>작업 이름으로 라우팅

기본 라우팅 템플릿을 사용 하 여 Web API HTTP 메서드를 사용 하 여 작업을 선택 합니다. 그러나 작업 이름이 URI에 포함 되어 있는 경로 만들 수 있습니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

이 경로 템플릿에서 합니다 *{action}* 매개 변수는 컨트롤러에 대 한 작업 메서드 이름입니다. 라우팅의이 스타일을 사용 하 여 허용 된 HTTP 메서드를 지정할 특성을 사용 합니다. 예를 들어 컨트롤러에는 다음 메서드도 있습니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

이 경우 "api/제품/세부 정보/1"에 대 한 GET 요청은 Details 메서드 매핑됩니다. 라우팅의이 스타일은 ASP.NET MVC 유사 하며 RPC 스타일 API에 대 한 적절 한 수 있습니다.

작업 이름을 사용 하 여 재정의할 수 있습니다 합니다 **ActionName** 특성입니다. 다음 예에 매핑되는 두 가지 작업 &quot;미리 보기 제품/api / /*id*합니다. 도구가 지 원하는 GET 및 POST를 지원:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>비 작업

메서드를 작업으로 호출 되지 않도록 하려면 사용 합니다 **NonAction** 특성입니다. 이 신호를 프레임 워크 메서드가 작업을 그렇지 않으면 라우팅 규칙과 일치 하는 경우에 합니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>추가 정보

이 항목에서는 라우팅의 상위 수준 보기를 제공 합니다. 자세한 내용을 참조 하세요 [라우팅 및 작업 선택](routing-and-action-selection.md)는 정확 하 게 하는 방법을 설명 프레임 워크는 경로에 URI와 일치, 컨트롤러를 선택 합니다. 그런 다음 호출할 작업을 선택 합니다.
