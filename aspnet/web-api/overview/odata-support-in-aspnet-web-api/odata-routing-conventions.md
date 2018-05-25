---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
title: 라우팅 규칙에 ASP.NET Web API 2 Odata | Microsoft Docs
author: MikeWasson
description: 이 문서에서는 OData 끝점에 대 한 Web API를 사용 하는 라우팅 규칙을 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/31/2013
ms.topic: article
ms.assetid: adbc175a-14eb-4ab2-a441-d056ffa8266f
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
msc.type: authoredcontent
ms.openlocfilehash: 0ab99dd443040b90ffefd2f5b9261a63b91e9463
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="routing-conventions-in-aspnet-web-api-2-odata"></a>라우팅 규칙에 ASP.NET Web API 2 Odata
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

> 이 문서에서는 OData 끝점에 대 한 Web API를 사용 하는 라우팅 규칙을 설명 합니다.


Web API OData 요청을 받으면 요청을 컨트롤러 이름과 작업 이름에 매핑합니다. 매핑을은 HTTP 메서드와 URI 기반으로 합니다. 예를 들어 `GET /odata/Products(1)` 매핑됩니다 `ProductsController.GetProduct`합니다.

이 문서의 1 부 기본 OData 라우팅 규칙에 설명합니다. 이러한 규칙에는 OData 끝점에 대 한 특히 되며 기본 Web API 라우팅 시스템으로 대체 됩니다. (호출할 때 발생 하는 대신 **MapODataRoute**.)

2 부, 사용자 지정 라우팅 규칙을 추가 하는 방법을 보여 줍니다. 현재 기본 제공 규칙은 전체 범위의 OData Uri를 포함 하지 않습니다 하지만 추가 하는 상황을 처리 하도록 확장할 수 있습니다.

- [기본 제공 라우팅 규칙](#conventions)
- [사용자 지정 라우팅 규칙](#custom)

<a id="conventions"></a>
## <a name="built-in-routing-conventions"></a>기본 제공 라우팅 규칙

Web API에서 OData 라우팅 규칙을 설명 하기 전에 OData Uri를 이해 하는 것이 좋습니다. [OData URI](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/) 이루어져 있습니다.

- 서비스 루트
- 리소스 경로
- 쿼리 옵션

![](odata-routing-conventions/_static/image1.png)

라우팅에 대 한 중요 한 부분은 리소스 경로입니다. 리소스 경로 세그먼트로 구분 됩니다. 예를 들어 `/Products(1)/Supplier` 세 세그먼트가:

- `Products`이름이 "제품" 엔터티 집합을 가리킵니다.
- `1`집합에서 단일 엔터티를 선택 하는 엔터티 키입니다.
- `Supplier`관련된 엔터티를 선택 하는 탐색 속성이입니다.

따라서이 경로 공급 업체에 1 제품을 선택 합니다.

> [!NOTE]
> OData 경로 세그먼트 URI 세그먼트에 항상 일치 하지 않습니다. 예를 들어, "1" 경로 세그먼트를 간주 됩니다.


**컨트롤러 이름입니다.** 엔터티 집합 리소스 경로 루트에서 컨트롤러 이름을 파생 항상 됩니다. 예를 들어, 리소스 경로 `/Products(1)/Supplier`, 명명 된 컨트롤러에 대 한 웹 API가 `ProductsController`합니다.

**작업 이름입니다.** 작업 이름은 다음 표에 나열 된 경로 세그먼트 및 엔터티 데이터 모델 (EDM)에서 파생 됩니다. 경우에 따라 작업 이름에 대 한 두 가지 옵션이 있습니다. 예를 들어, "Get" 또는 &quot;GetProducts&quot;합니다.

**엔터티 쿼리**

| 요청 | 예제 URI | 작업 이름 | 작업 예제 |
| --- | --- | --- | --- |
| /Entityset 가져오기 | / 제품 | GetEntitySet 또는 Get | GetProducts |
| /Entityset(key) 가져오기 | /Products(1) | GetEntityType 또는 Get | GetProduct |
| GET /entityset(key)/cast | /Products(1)/Models.Book | GetEntityType 또는 Get | GetBook |

자세한 내용은 참조 [읽기 전용 OData 끝점을 만드는](odata-v3/creating-an-odata-endpoint.md)합니다.

**만들기, 업데이트 및 엔터티 삭제**

| 요청 | 예제 URI | 작업 이름 | 작업 예제 |
| --- | --- | --- | --- |
| /Entityset 게시 | / 제품 | PostEntityType 또는 Post | PostProduct |
| PUT /entityset(key) | /Products(1) | PutEntityType 또는 Put | PutProduct |
| PUT /entityset(key)/cast | /Products(1)/Models.Book | PutEntityType 또는 Put | PutBook |
| /Entityset(key) 패치 | /Products(1) | PatchEntityType 또는 패치 | PatchProduct |
| PATCH /entityset(key)/cast | /Products(1)/Models.Book | PatchEntityType 또는 패치 | PatchBook |
| /Entityset(key) 삭제 | /Products(1) | DeleteEntityType 또는 삭제 | DeleteProduct |
| 캐스팅//entityset (키)를 삭제 합니다. | /Products(1)/Models.Book | DeleteEntityType 또는 삭제 | DeleteBook |

**탐색 속성 쿼리**

| 요청 | 예제 URI | 작업 이름 | 작업 예제 |
| --- | --- | --- | --- |
| GET /entityset (키) / 탐색 | / 제품 (1) / 공급자 | GetNavigationFromEntityType 또는 GetNavigation | GetSupplierFromProduct |
| GET /entityset(key)/cast/navigation | /Products(1)/Models.Book/Author | GetNavigationFromEntityType 또는 GetNavigation | GetAuthorFromBook |

자세한 내용은 참조 [엔터티 관계 작업](odata-v3/working-with-entity-relations.md)합니다.

**만들기 및 링크 삭제**

| 요청 | 예제 URI | 작업 이름 |
| --- | --- | --- |
| POST /entityset(key)/$links/navigation | /Products(1)/$links/Supplier | CreateLink |
| PUT /entityset(key)/$links/navigation | /Products(1)/$links/Supplier | CreateLink |
| DELETE /entityset(key)/$links/navigation | /Products(1)/$links/Supplier | DeleteLink |
| DELETE /entityset(key)/$links/navigation(relatedKey) | /Products/(1)/$links/Suppliers(1) | DeleteLink |

자세한 내용은 참조 [엔터티 관계 작업](odata-v3/working-with-entity-relations.md)합니다.

**속성**

*Web API 2 필요*

| 요청 | 예제 URI | 작업 이름 | 작업 예제 |
| --- | --- | --- | --- |
| GET /entityset(key)/property | /Products(1)/Name | GetPropertyFromEntityType 또는 GetProperty | GetNameFromProduct |
| GET /entityset(key)/cast/property | /Products(1)/Models.Book/Author | GetPropertyFromEntityType 또는 GetProperty | GetTitleFromBook |

**작업**

| 요청 | 예제 URI | 작업 이름 | 작업 예제 |
| --- | --- | --- | --- |
| POST /entityset(key)/action | /Products(1)/Rate | ActionNameOnEntityType 또는 ActionName | RateOnProduct |
| POST /entityset(key)/cast/action | /Products(1)/Models.Book/CheckOut | ActionNameOnEntityType 또는 ActionName | CheckOutOnBook |

자세한 내용은 참조 [OData 작업](odata-v3/odata-actions.md)합니다.

**메서드 시그니처**

다음은 메서드 서명에 대 한 몇 가지 규칙입니다.

- 경로 키를 포함 하는 경우 동작 라는 매개 변수 있어야 *키*합니다.
- 탐색 속성에는 키를 포함 하는 경로에 동작에 매개 변수 이름 있어야 *relatedKey*합니다.
- 데코 레이트 *키* 및 *relatedKey* 와 매개 변수는 **[FromODataUri]** 매개 변수입니다.
- POST 및 PUT 요청은 엔터티 형식의 매개 변수를 사용 합니다.
- 형식의 매개 변수를 사용 하는 PATCH 요청 **델타&lt;T&gt;** 여기서 *T* 엔터티 형식입니다.

참조용으로 모든 기본 OData 라우팅 규칙에 대 한 메서드 서명을 보여 주는 예제는 다음과 같습니다.

[!code-csharp[Main](odata-routing-conventions/samples/sample1.cs)]

<a id="custom"></a>
## <a name="custom-routing-conventions"></a>사용자 지정 라우팅 규칙

현재 기본 제공 규칙은 모든 가능한 OData Uri를 포함 하지 않습니다. 구현 하 여 새 규칙을 추가할 수는 **IODataRoutingConvention** 인터페이스입니다. 이 인터페이스에는 두 가지 방법이 있습니다.

[!code-csharp[Main](odata-routing-conventions/samples/sample2.cs)]

- **SelectController** 컨트롤러의 이름을 반환 합니다.
- **SelectAction** 동작의 이름을 반환 합니다.

두 방법에 대 한 규칙에 따라 해당 요청에 적용 되지 않는 경우 메서드가 해야 null을 반환 합니다.

**ODataPath** 매개 변수 구문 분석 된 OData 리소스 경로 나타냅니다. 목록이 **[ODataPathSegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** 리소스 경로의 각 세그먼트에 대 한 인스턴스. **ODataPathSegment** ; 추상 클래스에서 파생 된 클래스에 의해 표시 되는 각 세그먼트 형식 **ODataPathSegment**합니다.

**ODataPath.TemplatePath** 속성은 연결을 나타내는 문자열 경로 세그먼트의 모든 합니다. 예를 들어, URI가 `/Products(1)/Supplier`, 경로 서식 파일은 &quot;~/entityset/key/navigation&quot;합니다. 공지 세그먼트 URI 세그먼트에 직접 해당 하지 않습니다. 엔터티 키 (1)는 자체로 표시 됩니다는 예를 들어 **ODataPathSegment**합니다.

일반적으로 구현을 **IODataRoutingConvention** 다음 작업을 수행 합니다.

1. 이 규칙은 현재 요청에 적용 되는 경우 참조 하는 경로 템플릿을 비교 합니다. 적용 되지 않는 경우 null을 반환 합니다.
2. 속성을 사용 하는 규칙 적용 되는 경우는 **ODataPathSegment** 인스턴스를 컨트롤러 및 작업 이름을 파생 합니다.
3. 작업에 대 한 작업 매개 변수 (일반적으로 엔터티 키)에 바인딩해야 하는 경로 사전에 값을 추가 합니다.

구체적인 예를 살펴 보겠습니다. 기본 제공 라우팅 규칙이 고 탐색 컬렉션에 대 한 인덱싱을 지원 하지 않습니다. 즉, 규칙은 없습니다 Uri에 대 한 다음과 같은:

[!code-javascript[Main](odata-routing-conventions/samples/sample3.js)]

다음은 이러한 유형의 쿼리를 처리 하는 사용자 지정 라우팅 규칙입니다.

[!code-csharp[Main](odata-routing-conventions/samples/sample4.cs)]

메모:

1. 파생 되는 I **EntitySetRoutingConvention**때문에 **SelectController** 해당 클래스의 메서드는이 새 라우팅 규칙에 적합 합니다. 즉, 다시 구현 하지 않아도 **SelectController**합니다.
2. 규칙에 따라 GET 요청에만 적용 되 고 적용 된 경로 템플릿을 경우에 &quot;~/entityset/key/navigation/key&quot;합니다.
3. 작업 이름이 &quot;{EntityType을 (를) 가져올&quot;여기서 *{EntityType}* 탐색 컬렉션의 형식입니다. 예를 들어 &quot;GetSupplier&quot;합니다. 원하는 모든 명명 규칙 & #8212; 사용할 수 있습니다. 해야 사용자가 컨트롤러 작업이 일치 합니다.
4. 두 매개 변수를 수행 하는 동작 *키* 및 *relatedKey*합니다. (목록이 몇 가지 미리 정의 된 매개 변수 이름에 대 한 참조 [ODataRouteConstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx).)

다음 단계를 라우팅 규칙의 목록에 새 규칙을 추가 합니다. 이 상황이 다음 코드에 나와 있는 것 처럼 구성 하는 동안 발생 합니다.

[!code-csharp[Main](odata-routing-conventions/samples/sample5.cs)]

다음은 몇 가지 다른 샘플 라우팅 규칙을 연구할 유용할 수 있는입니다.

- [CompositeKeyRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataCompositeKeySample/ODataCompositeKeySample/Extensions/CompositeKeyRoutingConvention.cs)
- [CustomNavigationRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataServiceSample/ODataService/Extensions/CustomNavigationRoutingConvention.cs)
- [NonBindableActionRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataActionsSample/ODataActionsSample/NonBindableActionRoutingConvention.cs)
- [ODataVersionRouteConstraint](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataVersioningSample/ODataVersioningSample/Extensions/ODataVersionRouteConstraint.cs)

확인할 수 있도록 오픈 소스는 웹 API 자체는 물론는 [소스 코드](http://aspnetwebstack.codeplex.com/) 기본 제공 라우팅 규칙에 대 한 합니다. 이러한 작업에 정의 되는 **System.Web.Http.OData.Routing.Conventions** 네임 스페이스입니다.
