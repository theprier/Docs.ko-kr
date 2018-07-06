---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
title: ASP.NET Web API 2에서에서 라우팅 규칙 Odata | Microsoft Docs
author: MikeWasson
description: 이 문서에서는 Web API OData 끝점을 사용 하는 라우팅 규칙을 설명 합니다.
ms.author: aspnetcontent
ms.date: 07/31/2013
ms.assetid: adbc175a-14eb-4ab2-a441-d056ffa8266f
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-routing-conventions
msc.type: authoredcontent
ms.openlocfilehash: 645e820d3b03d1e3d2ac088973f6296efa5c2f40
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818267"
---
<a name="routing-conventions-in-aspnet-web-api-2-odata"></a>ASP.NET Web API 2에서에서 라우팅 규칙 Odata
====================
[Mike Wasson](https://github.com/MikeWasson)

> 이 문서에서는 Web API OData 끝점을 사용 하는 라우팅 규칙을 설명 합니다.


Web API OData 요청을 받으면 요청을 작업 이름과 컨트롤러 이름의을 매핑합니다. 매핑을은 HTTP 메서드와 URI 기반으로 합니다. 예를 들어 `GET /odata/Products(1)` 매핑됩니다 `ProductsController.GetProduct`합니다.

이 기사의 1 부 기본 OData 라우팅 규칙에 설명합니다. OData 끝점을 위해 특별히 설계 된 이러한 규칙 및 기본 Web API 라우팅 시스템으로 대체 됩니다. (호출할 때 발생 하는 교체 **MapODataRoute**.)

2 부의 사용자 지정 라우팅 규칙을 추가 하는 방법을 보여 줍니다. 현재 기본 제공 규칙을 전체 범위의 OData Uri를 다루지 않습니다 하지만 추가 사례를 처리 하도록 확장할 수 있습니다.

- [기본 제공 라우팅 규칙](#conventions)
- [사용자 지정 라우팅 규칙](#custom)

<a id="conventions"></a>
## <a name="built-in-routing-conventions"></a>기본 제공 라우팅 규칙

Web API에서 OData 라우팅 규칙을 설명 하기 전에는 OData Uri를 이해 하면 도움이 됩니다. [OData URI](http://www.odata.org/documentation/odata-v3-documentation/url-conventions/) 이루어져 있습니다.

- 서비스 루트
- 리소스 경로
- 쿼리 옵션

![](odata-routing-conventions/_static/image1.png)

라우팅에 대 한 중요 한 부분은 리소스 경로입니다. 리소스 경로 세그먼트로 구분 됩니다. 예를 들어 `/Products(1)/Supplier` 3 개의 세그먼트를 포함 합니다.

- `Products` "제품" 명명 된 엔터티 집합을 가리킵니다.
- `1` 집합에서 단일 엔터티를 선택 하는 엔터티 키입니다.
- `Supplier` 관련된 엔터티를 선택 하는 탐색 속성이입니다.

따라서이 경로 1 제품을 공급 업체 선택 합니다.

> [!NOTE]
> OData 경로 세그먼트 URI 세그먼트를 항상 일치 하지 않습니다. 예를 들어, "1" 경로 세그먼트를 간주 됩니다.


**컨트롤러 이름입니다.** 컨트롤러 이름은 엔터티 집합 리소스 경로의 루트에서 항상 파생 됩니다. 예를 들어 리소스 경로가 `/Products(1)/Supplier`, Web API 라는 컨트롤러를 찾습니다 `ProductsController`합니다.

**작업 이름입니다.** 작업 이름은 다음 표에 나열 된 경로 세그먼트와 엔터티 데이터 모델 (EDM)에서 파생 됩니다. 일부 경우에 작업 이름에 대 한 두 가지 선택 해야합니다. 예를 들어, "Get" 또는 &quot;GetProducts&quot;합니다.

**엔터티 쿼리**

| 요청 | URI 예제 | 작업 이름 | 예제 작업 |
| --- | --- | --- | --- |
| /Entityset 가져오기 | / 제품 | GetEntitySet 또는 Get | GetProducts |
| /Entityset(key) 가져오기 | /Products(1) | GetEntityType 또는 Get | GetProduct |
| /Entityset (키)을 가져옵니다/캐스팅 | /Products(1)/Models.Book | GetEntityType 또는 Get | GetBook |

자세한 내용은 [읽기 전용 OData 끝점을 만드는](odata-v3/creating-an-odata-endpoint.md)합니다.

**만들기, 업데이트 및 엔터티를 삭제 합니다.**

| 요청 | URI 예제 | 작업 이름 | 예제 작업 |
| --- | --- | --- | --- |
| /Entityset 게시 | / 제품 | PostEntityType 또는 Post | PostProduct |
| /Entityset(key) 배치 | /Products(1) | PutEntityType 또는 Put | PutProduct |
| (키) /entityset PUT/캐스팅 | /Products(1)/Models.Book | PutEntityType 또는 Put | PutBook |
| /Entityset(key) 패치 | /Products(1) | PatchEntityType 또는 패치 | PatchProduct |
| (키) /entityset PATCH/캐스팅 | /Products(1)/Models.Book | PatchEntityType 또는 패치 | PatchBook |
| /Entityset(key) 삭제 | /Products(1) | DeleteEntityType 또는 삭제 | DeleteProduct |
| 캐스팅//entityset (키)를 삭제 | /Products(1)/Models.Book | DeleteEntityType 또는 삭제 | DeleteBook |

**탐색 속성 쿼리**

| 요청 | URI 예제 | 작업 이름 | 예제 작업 |
| --- | --- | --- | --- |
| GET /entityset (키) / 탐색 | / 제품 (1) / 공급자 | GetNavigationFromEntityType 또는 GetNavigation | GetSupplierFromProduct |
| (키) /entityset/캐스트/탐색 가져오기 | /Products(1)/Models.Book/Author | GetNavigationFromEntityType 또는 GetNavigation | GetAuthorFromBook |

자세한 내용은 [엔터티 관계 작업](odata-v3/working-with-entity-relations.md)합니다.

**만들기 및 링크 삭제**

| 요청 | URI 예제 | 작업 이름 |
| --- | --- | --- |
| POST /entityset (키) / $links/탐색 | / 제품 (1) / $ 링크/공급 업체 | CreateLink |
| PUT /entityset(key)/$links/navigation | / 제품 (1) / $ 링크/공급 업체 | CreateLink |
| DELETE /entityset (키) / $links/탐색 | / 제품 (1) / $ 링크/공급 업체 | DeleteLink |
| DELETE /entityset(key)/$links/navigation(relatedKey) | /Products/(1)/$links/Suppliers(1) | DeleteLink |

자세한 내용은 [엔터티 관계 작업](odata-v3/working-with-entity-relations.md)합니다.

**속성**

*Web API 2 필요*

| 요청 | URI 예제 | 작업 이름 | 예제 작업 |
| --- | --- | --- | --- |
| GET /entityset (키) / 속성 | / 제품 (1) / 이름 | GetPropertyFromEntityType 또는 GetProperty | GetNameFromProduct |
| (키) /entityset/캐스트/속성 가져오기 | /Products(1)/Models.Book/Author | GetPropertyFromEntityType 또는 GetProperty | GetTitleFromBook |

**작업**

| 요청 | URI 예제 | 작업 이름 | 예제 작업 |
| --- | --- | --- | --- |
| POST /entityset (키) / 작업 | / 제품 (1) / 속도 | ActionNameOnEntityType 또는 ActionName | RateOnProduct |
| 후 /entityset (키) / 캐스트/작업 | /Products(1)/Models.Book/CheckOut | ActionNameOnEntityType 또는 ActionName | CheckOutOnBook |

자세한 내용은 [OData 작업](odata-v3/odata-actions.md)합니다.

**메서드 시그니처**

메서드 서명에 대 한 몇 가지 규칙은 다음과 같습니다.

- 경로 키가 들어 하는 경우 작업 이라는 매개 변수가 있어야 *키*합니다.
- 탐색 속성에 키를 포함 하는 경로 경우 작업 이라는 매개 변수가 있어야 *relatedKey*합니다.
- 데코 레이트 *키* 하 고 *relatedKey* 매개 변수를 **[FromODataUri]** 매개 변수입니다.
- POST 및 PUT 요청 된 엔터티 형식의 매개 변수를 사용 합니다.
- 형식의 매개 변수를 사용 하는 PATCH 요청 **델타&lt;T&gt;** 여기서 *T* 엔터티 형식입니다.

참조에 대 한 모든 기본 OData 라우팅 규칙에 대 한 메서드 시그니처를 보여 주는 예제는 다음과 같습니다.

[!code-csharp[Main](odata-routing-conventions/samples/sample1.cs)]

<a id="custom"></a>
## <a name="custom-routing-conventions"></a>사용자 지정 라우팅 규칙

현재 기본 제공 규칙은 모든 가능한 OData Uri를 포함 되지 않습니다. 구현 하 여 새 규칙을 추가할 수 있습니다 합니다 **IODataRoutingConvention** 인터페이스입니다. 이 인터페이스에는 두 가지 방법이 있습니다.

[!code-csharp[Main](odata-routing-conventions/samples/sample2.cs)]

- **SelectController** 컨트롤러의 이름을 반환 합니다.
- **SelectAction** 동작의 이름을 반환 합니다.

두 방법 모두 해당 요청에 규칙을 적용 하지 않는 경우 메서드가 null을 반환 해야 합니다.

합니다 **ODataPath** 매개 변수를 구문 분석 된 OData 리소스 경로 나타냅니다. 목록이 **[된 ODataPathSegment](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatapathsegment.aspx)** 리소스 경로의 각 세그먼트에 대 한 인스턴스. **된 ODataPathSegment** 추상 클래스입니다; 각 세그먼트 형식에서 파생 된 클래스로 표현 됩니다 **된 ODataPathSegment**합니다.

합니다 **ODataPath.TemplatePath** 속성은 연결을 나타내는 문자열 경로 세그먼트의 모든. 예를 들어, URI가 `/Products(1)/Supplier`, 경로 템플릿을 &quot;~/entityset/key/navigation&quot;합니다. 세그먼트가 없는 URI 세그먼트에 직접 해당 하는 알 수 있습니다. 자체 엔터티 키 (1)가 표시 하는 예를 들어 **된 ODataPathSegment**합니다.

일반적으로 구현을 **IODataRoutingConvention** 다음을 수행 합니다.

1. 이 규칙은 현재 요청에 적용 되는 경우 참조 경로 템플릿을 비교 합니다. 적용 되지 않는 경우 null을 반환 합니다.
2. 규칙 적용 되는 경우의 속성을 사용 합니다 **된 ODataPathSegment** 인스턴스 컨트롤러 및 작업 이름만 가져오려고 합니다.
3. 작업에 대 한 작업 매개 변수 (일반적으로 엔터티 키)에 바인딩해야 하는 경로 사전에 값을 추가 합니다.

특정 예제를 살펴보겠습니다. 기본 제공 라우팅 규칙을 탐색 컬렉션으로 인덱싱 하는 것을 지원 하지 않습니다. 즉, 규칙은 없습니다 Uri에 대 한 다음과 같은:

[!code-javascript[Main](odata-routing-conventions/samples/sample3.js)]

다음은 이러한 유형의 쿼리를 처리 하는 사용자 지정 라우팅 규칙입니다.

[!code-csharp[Main](odata-routing-conventions/samples/sample4.cs)]

메모:

1. 컨트롤을 파생 **EntitySetRoutingConvention**이므로 합니다 **SelectController** 해당 클래스의 메서드는이 새 라우팅 규칙에 대 한 적절 한 합니다. 즉, 다시 구현할 필요가 없습니다 **SelectController**합니다.
2. 규칙에만 적용 됩니다 GET 요청을 경로 템플릿이 적용 되는 경우에 &quot;~/entityset/key/navigation/key&quot;합니다.
3. 작업 이름이 &quot;{EntityType} 가져옵니다&quot;, 여기서 *{EntityType}* 탐색 컬렉션의 형식입니다. 예를 들어 &quot;GetSupplier&quot;합니다. 원하는 모든 명명 규칙을 사용할 수 있습니다 &#8212; 있는지만 일치 컨트롤러 작업입니다.
4. 라는 두 개의 매개 변수를 사용 하는 동작 *키* 하 고 *relatedKey*합니다. (일부 미리 정의 된 매개 변수 이름의 목록을 보려면 참조 [ODataRouteConstants](https://msdn.microsoft.com/library/system.web.http.odata.routing.odatarouteconstants.aspx).)

다음 단계는 라우팅 규칙의 목록에 새 규칙을 추가 합니다. 이 상황이 다음 코드에 표시 된 대로 구성 하는 동안 발생 합니다.

[!code-csharp[Main](odata-routing-conventions/samples/sample5.cs)]

일부 다른 샘플 라우팅 규칙을 연구 하는 데 유용할 수는 다음과 같습니다.

- [CompositeKeyRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataCompositeKeySample/ODataCompositeKeySample/Extensions/CompositeKeyRoutingConvention.cs)
- [CustomNavigationRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataServiceSample/ODataService/Extensions/CustomNavigationRoutingConvention.cs)
- [NonBindableActionRoutingConvention](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataActionsSample/ODataActionsSample/NonBindableActionRoutingConvention.cs)
- [ODataVersionRouteConstraint](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/ODataVersioningSample/ODataVersioningSample/Extensions/ODataVersionRouteConstraint.cs)

볼 수 있도록 오픈 소스는 웹 API 자체는 물론 합니다 [소스 코드](http://aspnetwebstack.codeplex.com/) 기본 제공 라우팅 규칙에 대 한 합니다. 에 정의 된 이러한 합니다 **System.Web.Http.OData.Routing.Conventions** 네임 스페이스입니다.
