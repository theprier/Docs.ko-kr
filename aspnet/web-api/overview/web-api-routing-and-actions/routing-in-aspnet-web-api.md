---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API의에서 라우팅 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/11/2012
ms.topic: article
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: aa0ecc96029051fef6a81ac08f7fcf52a24de59c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="routing-in-aspnet-web-api"></a>ASP.NET Web API의 라우팅
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

이 문서에서는 ASP.NET Web API 컨트롤러를 HTTP 요청을 라우팅하 하는 방법에 대해 설명 합니다.

> [!NOTE]
> ASP.NET MVC에 익숙한 경우 Web API 라우팅는 MVC 라우팅 매우 비슷합니다. 주요 차이점은 Web API HTTP 메서드를 URI 경로 사용 하 여 작업 선택 합니다. MVC 스타일 라우팅 Web API에서 사용할 수 있습니다. 이 문서는 ASP.NET MVC에 대 한 정보를 상속 되지 않습니다.


## <a name="routing-tables"></a>라우팅 테이블

ASP.NET Web API에는 *컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다. 컨트롤러의 공용 메서드를 라고 *작업 메서드* 또는 단순히 *동작*합니다. Web API 프레임 워크는 요청을 받으면 요청을 동작을 라우팅합니다.

프레임 워크에서 호출 하는 동작을 확인 하려면 다음을 사용 합니다.는 *라우팅 테이블*합니다. 웹 API에 대 한 Visual Studio 프로젝트 템플릿은 기본 경로를 만듭니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

이 경로 응용 프로그램에 있는 WebApiConfig.cs 파일에 정의 된\_시작 디렉터리:

![](routing-in-aspnet-web-api/_static/image1.png)

에 대 한 자세한 내용은 **경우 WebApiConfig** 클래스를 참조 하십시오. [ASP.NET Web API 구성](../advanced/configuring-aspnet-web-api.md)합니다.

라우팅 테이블에 직접 설정 해야 자체 웹 API를 호스트 하는 경우는 **HttpSelfHostConfiguration** 개체입니다. 자세한 내용은 참조 [자체 호스트 하는 Web API](../older-versions/self-host-a-web-api.md)합니다.

라우팅 테이블의 각 항목을 포함 한 *경로 템플릿을*합니다. 웹 API에 대 한 기본 경로 서식 파일은 &quot;api / {controller} / {id}&quot;합니다. 이 서식 파일에서 &quot;api&quot; 은 리터럴 경로 세그먼트 및 {컨트롤러} 및 {id}는 자리 표시자 변수입니다.

Web API 프레임 워크는 HTTP 요청을 받으면 라우팅 테이블에 경로 템플릿 중 하나에 대 한 URI와 일치 하도록 시도 합니다. 경로가 없는 일치 하는 경우 클라이언트가 404 오류를 받습니다. 예를 들어, 다음 Uri 기본 경로도 일치 합니다.

- / api/연락처
- /api/contacts/1
- /api/products/gizmo1

그러나 다음과 같은 URI와 일치 하지 않으면 없기 때문에 &quot;api&quot; 세그먼트:

- / 연락처/1

> [!NOTE]
> 경로에서 "api"를 사용 하기 위한 이유 ASP.NET mvc 라우팅 충돌을 방지 하기 위해서입니다. 할 수 있습니다 이런 방식으로 &quot;연결/&quot; 된 MVC 컨트롤러로 이동 하 고 &quot;/api/연락처&quot; Web API 컨트롤러로 이동 합니다. 물론,이 규칙을 마음에 들지 않는 경우 기본 경로 테이블을 변경할 수 있습니다.

일치 하는 경로가 발견 되 면 Web API 컨트롤러 및 작업을 선택 합니다.

- Web API 컨트롤러를 찾으려면 추가 &quot;컨트롤러&quot; 의 값에는 *{컨트롤러}* 변수입니다.
- 작업을 찾으려면 Web API HTTP 메서드를 찾은 해당 HTTP 메서드 이름으로 시작 하는 동작을 찾습니다. 예를 들어 GET 요청에서 Web API ()은로 시작 하는 동작에 대 한 &quot;가져오기... &quot;와 같은 &quot;GetContact&quot; 또는 &quot;GetAllContacts&quot;합니다. 이 규칙 가져오기, POST, PUT, 및 삭제 메서드에만 적용 됩니다. 컨트롤러에서 특성을 사용 하 여 다른 HTTP 메서드를 사용할 수 있습니다. 예를 들어 나중에 보겠습니다.
- 경로 템플릿의 다른 자리 표시자 변수와 같은 *{id}* 액션 매개 변수는 매핑됩니다.

예를 살펴 보겠습니다. 다음 컨트롤러를 정의 하는 가정 합니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

다음은 각각에 대해 호출 된 동작과 함께 몇 가지 가능한 HTTP 요청입니다.

| HTTP 메서드 | URI 경로 | 작업 | 매개 변수 |
| --- | --- | --- | --- |
| 가져오기 | api/제품 | GetAllProducts | *(없음)* |
| 가져오기 | api/제품/4 | GetProductById | 4 |
| Delete | api/제품/4 | DeleteProduct | 4 |
| 올리기 | api/제품 | *(일치)* |  |

다음에 유의 *{id}* URI의 세그먼트가 있는 경우 매핑되는 *id* 동작의 매개 변수입니다. 이 예제는 컨트롤러에 두 개의 GET 메서드를 정의 *id* 매개 변수 및 매개 변수 없이 합니다.

POST 요청이 실패 하는 컨트롤러에서 정의 하지 않으므로 참고 또한는 &quot;게시물 중... &quot; 메서드.

## <a name="routing-variations"></a>라우팅 변형

이전 섹션 ASP.NET Web API에 대 한 기본 라우팅 메커니즘을 설명합니다. 이 섹션에서는 몇 변형을 설명 합니다.

### <a name="http-methods"></a>HTTP 메서드

HTTP 메서드에 대 한 명명 규칙을 사용 하는 대신 명시적으로 방법을 지정할 수 있습니다는 HTTP 작업에 대 한 사용 하 여 동작 메서드를 데코레이팅하는 **HttpGet**, **HttpPut**, **HttpPost** , 또는 **HttpDelete** 특성입니다.

다음 예제에서는 FindProduct 메서드는 GET 요청에 매핑됩니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

사용 하 여 작업을 위한 여러 HTTP 메서드가 허용 하거나 이외의 GET, PUT, POST 및 DELETE HTTP 메서드를 허용 하려면는 **AcceptVerbs** 목록이 며 HTTP 메서드는 특성입니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>작업 이름으로 라우팅

기본 라우팅 템플릿을 사용 하 여 Web API HTTP 메서드를 사용 하 여 작업 선택 합니다. 그러나 URI에 작업 이름이 포함 되어 있는 경로 만들 수 있습니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

이 경로 템플릿에 *{action}* 컨트롤러 동작 메서드 매개 변수 이름을 지정 합니다. 라우팅의이 스타일으로 허용 된 HTTP 메서드를 지정할 특성을 사용 합니다. 예를 들어 컨트롤러에 다음 메서드가 있다고 가정 합니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

이 경우 "api/제품/세부 정보/1"에 대 한 GET 요청 Details 메서드를 매핑합니다. 이 스타일 라우팅의 ASP.NET MVC 유사 하며 RPC 스타일 API에 대 한 적합할 수 있습니다.

작업 이름을 사용 하 여 재정의할 수 있습니다는 **ActionName** 특성입니다. 다음 예제에서는 두 가지 동작에 매핑되는 &quot;api/제품/축소판 그림/*id*합니다. 도구가 지 원하는 GET 및 POST를 지원:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>비 작업

메서드는 동작 호출 되지 않도록 하려면 사용 된 **NonAction** 특성입니다. 이 신호 프레임 워크에 메서드가 작업을 하지 않으면 라우팅 규칙과 일치 하는 경우에 합니다.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>추가 정보

이 항목 라우팅의 상위 수준 보기를 제공합니다. 자세한 내용은 참조 [라우팅 및 작업 선택](routing-and-action-selection.md)를 정확히 어떻게 프레임 워크 경로 대 한 URI를 일치, 컨트롤러를 선택한 다음 선택 호출할 작업을 설명 하는 합니다.
