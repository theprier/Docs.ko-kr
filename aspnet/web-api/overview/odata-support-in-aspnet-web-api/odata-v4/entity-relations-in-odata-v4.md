---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: ASP.NET Web API 2.2 사용 하 여 OData v4의 엔터티 관계 | Microsoft Docs
author: MikeWasson
description: '엔터티 간의 관계를 정의 하는 대부분의 데이터 집합: 고객은 주문; 온라인 설명서가 작성자; 제품 공급 업체에 있습니다. OData를 사용 하 여 클라이언트를 탐색할 수 있습니다...'
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: d07ddab83462ee1bc84ba8ab15fe906937f506e6
ms.sourcegitcommit: 7890dfb5a8f8c07d813f166d3ab0c263f893d0c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48795394"
---
<a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a>ASP.NET Web API 2.2 사용 하 여 OData v4의 엔터티 관계
====================
[Mike Wasson](https://github.com/MikeWasson)

> 엔터티 간의 관계를 정의 하는 대부분의 데이터 집합: 고객은 주문; 온라인 설명서가 작성자; 제품 공급 업체에 있습니다. OData를 클라이언트 엔터티 관계 탐색할 수 있습니다. 제품에 지정 된 공급자를 찾을 수 있습니다. 만들기 또는 관계를 제거할 수도 있습니다. 예를 들어, 제품 공급 업체를 설정할 수 있습니다.
>
> 이 자습서에는 ASP.NET Web API를 사용 하 여 OData v4의 이러한 작업을 지 원하는 방법을 보여 줍니다. 자습서를 기반으로 한 자습서 [OData v4 끝점 사용 하 여 ASP.NET 웹 API 2 만들](create-an-odata-v4-endpoint.md)합니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
>
> - Web API 2.1
> - OData v4
> - Visual Studio 2013 (Visual Studio 2017 다운로드 [여기](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))
> - Entity Framework 6
> - .NET 4.5
>
> ## <a name="tutorial-versions"></a>자습서 버전
>
> OData 버전 3에 대 한 참조 [OData v3의 엔터티 관계를 지 원하는](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations)합니다.

## <a name="add-a-supplier-entity"></a>Supplier 엔터티를 추가 합니다.

> [!NOTE]
> 자습서를 기반으로 한 자습서 [OData v4 끝점 사용 하 여 ASP.NET 웹 API 2 만들](create-an-odata-v4-endpoint.md)합니다.

첫째, 관련된 엔터티를 해야합니다. 라는 클래스를 추가 `Supplier` Models 폴더에 있습니다.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

탐색 속성을 추가 하 여 `Product` 클래스:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

새 **DbSet** 에 `ProductsContext` 클래스, Entity Framework에 공급 업체 테이블 데이터베이스에 포함 되도록 합니다.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

WebApiConfig.cs에서 추가 된 &quot;공급 업체&quot; 엔터티 데이터 모델 엔터티 집합:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a>공급 업체 컨트롤러 추가

추가 된 `SuppliersController` 클래스 Controllers 폴더를 합니다.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

이 컨트롤러에 대 한 CRUD 작업을 추가 하는 방법을 표시 하지 않습니다. 단계는 Products 컨트롤러 동일 (참조 [OData v4 엔드포인트 만들기](create-an-odata-v4-endpoint.md)).

## <a name="getting-related-entities"></a>관련된 엔터티를 가져오는 중

제품에 대 한 공급자를 가져오려면 클라이언트는 GET 요청을 보냅니다.

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

이 요청을 지원 하려면 다음 메서드를 추가 합니다 `ProductsController` 클래스:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

이 메서드는 기본 명명 규칙

- 메서드 이름: GetX, 여기서 X는 탐색 속성입니다.
- 매개 변수 이름: *키*

이 명명 규칙을 따르는 경우 Web API 컨트롤러 메서드에 HTTP 요청을 자동으로 매핑합니다.

예제 HTTP 요청:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

예제 HTTP 응답:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a>관련된 컬렉션 가져오기

이전 예제에서는 제품에는 공급자가 있습니다. 탐색 속성 컬렉션을 반환할 수도 있습니다. 다음 코드는 공급자에 대 한 제품을 가져옵니다.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

메서드를 반환 하는 경우에 **IQueryable** 대신에 **SingleResult&lt;T&gt;**

예제 HTTP 요청:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

예제 HTTP 응답:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a>엔터티 간의 관계 만들기

OData를 만들거나 기존 두 엔터티 간의 관계를 제거를 지원 합니다. 관계의 OData v4 용어는 &quot;참조&quot;합니다. (관계 호출한 OData v3에는 *링크*합니다. 프로토콜 차이점이이 자습서에 대 한 중요 하지 않습니다.)

참조에 폼을 사용 하 여 고유한 URI `/Entity/NavigationProperty/$ref`합니다. 예를 들어, 다음은 제품 및 공급 업체 간의 참조를 해결 하기 위해 URI입니다.

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

관계를 추가 하려면 클라이언트는이 주소로 POST 또는 PUT 요청을 보냅니다.

- 탐색 속성은 단일 엔터티를 같은 경우 `Product.Supplier`합니다.
- 탐색 속성은 컬렉션 등 게시 `Supplier.Products`합니다.

관계의 다른 엔터티의 URI를 포함 하는 요청의 본문입니다. 요청 예제는 다음과 같습니다.

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

이 예에서 클라이언트는 PUT 요청을 보냅니다 `/Products(6)/Supplier/$ref`, $ref URI는는 `Supplier` ID 사용 하 여 제품의 = 6. 요청이 성공 하는 경우 서버는 204 (내용 없음) 응답을 보냅니다.

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

같습니다. 관계를 추가할 컨트롤러 메서드는 `Product`:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

합니다 *navigationProperty* 매개 변수 설정 하는 관계를 지정 합니다. (엔터티의 탐색 속성이 둘 이상 있으면 더 추가할 수 있습니다 `case` 문.)

합니다 *링크* 매개 변수는 공급자의 URI를 포함 합니다. 웹 API에는 자동으로이 매개 변수에 대 한 값을 검색할 요청 본문 구문 분석 합니다.

ID (또는 키), 해야 공급자를 조회 하의 일부인 합니다 *링크* 매개 변수입니다. 이 작업을 수행 하려면 다음 도우미 메서드를 사용 합니다.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

기본적으로,이 메서드가 URI 경로 세그먼트로 분할할 키를 포함 하는 세그먼트를 찾고, 키를 올바른 형식으로 변환 하는 OData 라이브러리를 사용 합니다.

## <a name="deleting-a-relationship-between-entities"></a>엔터티 간의 관계를 삭제합니다.

관계를 삭제 하려면 클라이언트가 $ref URI에 HTTP DELETE 요청을 보냅니다.

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

제품 및 공급자 간의 관계를 삭제 하려면 컨트롤러 메서드는 다음과 같습니다.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

이 예에서 `Product.Supplier` 은 &quot;1&quot; 1 대 다 관계를 설정 하 여 관계를 제거할 수 있도록 끝 `Product.Supplier` 를 `null`.

에 &quot;많은&quot; 클라이언트 관계의 end는 관련 엔터티를 제거 하려면을 지정 해야 합니다. 이렇게 하려면 클라이언트는 관련 엔터티의 URI 요청의 쿼리 문자열에 보냅니다. 예를 들어 "제품 1"을 제거 하려면 "1" 공급자:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

이 지 원하는 웹 api에서에 추가 매개 변수를 포함 해야 합니다 `DeleteRef` 메서드. 여기에서 제품을 제거 하려면 컨트롤러 메서드는는 `Supplier.Products` 관계입니다.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

*키* 매개 변수는 공급자에 대 한 키 및 *relatedKey* 매개 변수는에서 제거할 제품에 대 한 키를 `Products` 관계입니다. Web API는 쿼리 문자열에서 키를 자동으로 가져옵니다는 note 합니다.
