---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: "ASP.NET Web API 2.2 사용 하 여 OData v4의 엔터티 관계 | Microsoft Docs"
author: MikeWasson
description: "엔터티 간의 관계를 정의 하는 대부분의 데이터 집합: 고객이 주문을; 갖고 책에는 한 작성자입니다. 제품 공급 업체에는 합니다. OData를 사용 하 여 클라이언트를 탐색할 수 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2014
ms.topic: article
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 4127fb2fa83f513a4faeb222068ca99f234ece22
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a>ASP.NET Web API 2.2 사용 하 여 OData v4의 엔터티 관계
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

> 엔터티 간의 관계를 정의 하는 대부분의 데이터 집합: 고객이 주문을; 갖고 책에는 한 작성자입니다. 제품 공급 업체에는 합니다. OData를 사용 하 여, 엔터티 관계를 통해 클라이언트를 탐색할 수 있습니다. 제품에 지정 된 경우 공급자를 찾을 수 있습니다. 만들 하거나 관계를 제거할 수 있습니다. 예를 들어 제품 공급 업체를 설정할 수 있습니다.
> 
> 이 자습서에는 ASP.NET Web API를 사용 하 여 OData v4에서 이러한 작업을 지 원하는 방법을 보여 줍니다. 이 자습서를 기반으로 자습서 [OData v4 Endpoint를 사용 하 여 ASP.NET 웹 API 2 만들](create-an-odata-v4-endpoint.md)합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - Web API 2.1
> - OData v4
> - [Visual Studio 2013 업데이트 2](https://www.visualstudio.com/downloads/download-visual-studio-vs)
> - Entity Framework 6
> - .NET 4.5
> 
> 
> ## <a name="tutorial-versions"></a>자습서 버전
> 
> OData 버전 3에 대 한 참조 [OData v 3의 엔터티 관계를 지 원하는](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations)합니다.


## <a name="add-a-supplier-entity"></a>Supplier 엔터티 추가

> [!NOTE]
> 이 자습서를 기반으로 자습서 [OData v4 Endpoint를 사용 하 여 ASP.NET 웹 API 2 만들](create-an-odata-v4-endpoint.md)합니다.


첫째, 관련된 엔터티를 해야합니다. 라는 클래스를 추가 `Supplier` Models 폴더에 있습니다.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

탐색 속성을 추가 하는 `Product` 클래스:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

새로 추가 **DbSet** 에 `ProductsContext` 클래스를 Entity Framework 데이터베이스에서 공급자 테이블 포함 됩니다.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

WebApiConfig.cs에 추가 &quot;Suppliers&quot; 엔터티 데이터 모델에 엔터티 집합:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a>공급 업체 컨트롤러 추가

추가 `SuppliersController` 컨트롤러 폴더에는 클래스입니다.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

필자는이 컨트롤러에 대 한 CRUD 작업을 추가 하는 방법을 표시 되지 않습니다. 단계는 Products 컨트롤러의 경우와 동일 (참조 [OData v4 끝점을 만드는](create-an-odata-v4-endpoint.md)).

## <a name="getting-related-entities"></a>관련된 엔터티를 가져오는 중

공급 업체는 제품에 대 한을 가져오려면 클라이언트는 GET 요청을 보냅니다.

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

이 요청을 지원 하려면 다음 메서드를 추가 `ProductsController` 클래스:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

이 메서드는 기본 명명 규칙을 사용합니다.

- 메서드 이름: GetX, 여기서 X는 탐색 속성입니다.
- 매개 변수 이름: *키*

이 명명 규칙을 따르는 경우 Web API HTTP 요청을 컨트롤러 메서드를 자동으로 매핑합니다.

예제에서는 HTTP 요청:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

예제에서는 HTTP 응답:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a>관련된 컬렉션 가져오기

이전 예제에서는 제품에는 한 공급 있습니다. 탐색 속성 컬렉션을 반환할 수도 있습니다. 다음 코드는 공급자에 대 한 제품을 가져옵니다.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

메서드가 반환 하는 경우에 **IQueryable** 대신는 **SingleResult&lt;T&gt;**

예제에서는 HTTP 요청:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

예제에서는 HTTP 응답:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a>엔터티 간 관계 만들기

OData를 만들거나 기존 두 엔터티 간의 관계 제거를 지원 합니다. 관계는 OData v4 용어에서는 &quot;참조&quot;합니다. (관계 호출 된 OData v 3는 *링크*합니다. 프로토콜 차이이 자습서에 대 한 중요 하지 않습니다.)

참조에 폼과 자체 URI `/Entity/NavigationProperty/$ref`합니다. 예를 들어 다음은 제품과 공급 업체 간의 참조 주소를 지정 하는 URI입니다.

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

관계를 추가 하려면 클라이언트는이 주소는 POST 또는 PUT 요청을 보냅니다.

- 탐색 속성은 단일 엔터티를 같은 경우 `Product.Supplier`합니다.
- 탐색 속성은 컬렉션와 같은 경우 게시 `Supplier.Products`합니다.

요청 본문은 관계의 다른 엔터티의 URI를 포함 합니다. 다음은 예제 요청이입니다.

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

이 예제에서는 클라이언트 PUT 요청을 보냅니다. `/Products(6)/Supplier/$ref`에 대 한 $ref URI 되는 `Supplier` ID로 제품의 = 6. 요청이 성공 하면 204 (콘텐츠 없음) 응답을 서버에 보냅니다.

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

다음은에 대 한 관계를 추가 하려면 컨트롤러 메서드는 `Product`:

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

*navigationProperty* 어떤 관계를 설정할 매개 변수를 지정 합니다. (더 추가할 수는 엔터티에서 탐색 속성이 둘 이상 있으면 `case` 문.)

*링크* 매개 변수는 공급자의 URI를 포함 합니다. Web API에는 자동으로이 매개 변수에 대 한 값을 요청 본문 구문 분석 합니다.

ID (또는 키), 해야 공급자를 조회할의 일부인는 *링크* 매개 변수입니다. 이렇게 하려면 다음 도우미 메서드를 사용 합니다.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

기본적으로,이 메서드는 URI 경로 세그먼트로 분할 키를 포함 하는 세그먼트를 찾고, 키를 올바른 형식으로 변환 하는 OData 라이브러리를 사용 합니다.

## <a name="deleting-a-relationship-between-entities"></a>엔터티 간의 관계를 삭제 하면

관계를 삭제 하려면 클라이언트 $ref URI HTTP DELETE 요청을 보냅니다.

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

제품 및 협력 업체 간의 관계를 삭제 하려면 컨트롤러 메서드는 다음과 같습니다.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

이 경우 `Product.Supplier` 는 &quot;1&quot; 설정 하 여 관계를 제거할 수 있는 1 대 다 관계의 끝 `Product.Supplier` 를 `null`합니다.

에 &quot;많은&quot; 는 관련 엔터티를 제거 하는 클라이언트는 관계의 끝 지정 해야 합니다. 이렇게 하려면 클라이언트는 관련 엔터티의 URI 요청의 쿼리 문자열에 보냅니다. 예를 들어, "Product 1"에서 제거 하려면 "1" 공급 업체:

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

에 추가 매개 변수를 포함 하도록 설정 해야이 Web API에서 지원는 `DeleteRef` 메서드. 여기에서 제품을 제거 하려면 컨트롤러 메서드는는 `Supplier.Products` 관계입니다.

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

*키* 매개 변수는가 공급 업체에 대 한 키 및 *relatedKey* 매개 변수는에서 제거할 제품에 대 한 키의 `Products` 관계입니다. 웹 API는 쿼리 문자열에서 키를 자동으로 가져옵니다는 note 합니다.
