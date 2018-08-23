---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: 웹 API 2 OData v3의 엔터티 관계 지원 | Microsoft Docs
author: MikeWasson
description: '엔터티 간의 관계를 정의 하는 대부분의 데이터 집합: 고객은 주문; 온라인 설명서가 작성자; 제품 공급 업체에 있습니다. OData를 사용 하 여 클라이언트를 탐색할 수 있습니다...'
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: fc1c6b938c4e4be379edf1a495ca47f5f5f2eb4f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836374"
---
<a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a>웹 API 2 OData v3의 엔터티 관계 지원
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> 엔터티 간의 관계를 정의 하는 대부분의 데이터 집합: 고객은 주문; 온라인 설명서가 작성자; 제품 공급 업체에 있습니다. OData를 클라이언트 엔터티 관계 탐색할 수 있습니다. 제품에 지정 된 공급자를 찾을 수 있습니다. 만들기 또는 관계를 제거할 수도 있습니다. 예를 들어, 제품 공급 업체를 설정할 수 있습니다.
> 
> 이 자습서에서는 ASP.NET Web API에서 이러한 작업을 지 원하는 방법을 보여줍니다. 이 자습서를 기반으로 한 자습서 [Web API 2 OData v3 엔드포인트 만들기](creating-an-odata-endpoint.md)합니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>이 자습서에 사용 되는 소프트웨어 버전
> 
> 
> - Web API 2
> - OData 버전 3
> - Entity Framework 6


## <a name="add-a-supplier-entity"></a>Supplier 엔터티를 추가 합니다.

먼저 새 엔터티 형식이 OData 피드를 추가 해야 합니다. 추가할 것을 `Supplier` 클래스입니다.

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

이 클래스는 엔터티 키에 대 한 문자열을 사용합니다. 실제로 정수 키를 사용 하 여 보다는 덜 일반적인 수 있습니다. 하지만 OData 정수 외에도 다른 키 유형을 처리 하는 방법을 보는 것입니다.

다음으로 만들겠습니다 관계를 추가 하 여는 `Supplier` 속성을는 `Product` 클래스:

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

새 **DbSet** 에 `ProductServiceContext` 클래스를 Entity Framework에 포함 되도록는 `Supplier` 데이터베이스의 테이블입니다.

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

WebApiConfig.cs에서 EDM 모델에 "공급 업체" 엔터티를 추가 합니다.

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a>탐색 속성

제품에 대 한 공급자를 가져오려면 클라이언트는 GET 요청을 보냅니다.

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

여기 "공급자"은 탐색 속성에는 `Product` 형식입니다. 이 경우 `Supplier` 참조 속성은 단일 항목을 탐색 하는 컬렉션 (1 대 다 또는 다 대 다 관계)을 반환할 수도 있습니다.

이 요청을 지원 하려면 다음 메서드를 추가 합니다 `ProductsController` 클래스:

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

합니다 *키* 매개 변수는 제품의 키입니다. 이 경우 메서드가 반환 관련된 된 엔터티 & amp;#8212는 `Supplier` 인스턴스. 메서드 이름과 매개 변수 이름 둘 다 중요 합니다. 일반적으로 탐색 속성의 이름이 "X", "GetX" 라는 메서드를 추가 해야 합니다. 메서드는 라는 매개 변수가 없어야 합니다. "*키*" 부모의 키의 데이터 형식과 일치 하는 합니다.

포함 하는 일을 해야 이기도 합니다 **[FromOdataUri]** 특성을 *키* 매개 변수. 이 특성은 요청 URI에서에서 키를 구문 분석할 때 OData 구문 규칙을 사용 하는 웹 API에 알립니다.

## <a name="creating-and-deleting-links"></a>만들기 및 링크 삭제

OData는 두 엔터티 간의 관계를 만들거나 제거를 지원합니다. OData 용어 관계의 "링크"입니다. 각 링크에 폼을 사용 하 여 URI *엔터티*/$links /*엔터티*합니다. 예를 들어, 공급 업체에 대 한 제품에서 링크는 다음과 같습니다.

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

새 링크를 만들려면 클라이언트 링크 URI에 POST 요청을 보냅니다. 요청 본문은 대상 엔터티의 URI입니다. 예를 들어, "CTSO" 키를 사용 하 여 공급자가 있으며 클라이언트는 "Product(1)"에서 "Supplier('CTSO')"로 링크를 만들려면 다음과 같은 요청을 보냅니다.

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

링크를 삭제 하려면 클라이언트가 링크 URI에 DELETE 요청을 보냅니다.

**링크 만들기**

제품 공급자 링크를 만들려면 클라이언트를 사용 하려면 다음 코드를 추가 합니다 `ProductsController` 클래스:

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

이 메서드는 세 개의 매개 변수를 사용합니다.

- *키*: 키를 부모 엔터티 (제품)
- *navigationProperty*: 탐색 속성의 이름입니다. 이 예제에서는 유효한 탐색 속성이 "공급자"입니다.
- *링크*: 관련 엔터티의 OData URI입니다. 이 값은 요청 본문에서 가져옵니다. 예를 들어 링크 URI 않을 "`http://localhost/odata/Suppliers('CTSO')`, 즉 ID 사용 하 여 공급자 'CTSO' =.

메서드는 공급자를 조회 하 링크를 사용 합니다. 메서드를 설정 하는 일치 하는 공급자가 있으면는 `Product.Supplier` 속성 데이터베이스에 결과 저장 합니다.

가장 어려운 부분은 링크 URI를 구문 분석 됩니다. 기본적으로, URI에 GET 요청을 전송 하는 결과 시뮬레이션 해야 합니다. 다음 도우미 메서드는이 작업을 수행 하는 방법을 보여 줍니다. 메서드는 Web API 라우팅 프로세스를 호출 하 고 다시 가져옵니다는 **ODataPath** 구문 분석 된 OData 경로 나타내는 인스턴스입니다. 링크 URI 세그먼트 중 하나의 엔터티 키가 있어야 합니다. (그러지 않으면 클라이언트는 잘못 된 URI를 전송 합니다.)

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

**링크 삭제**

링크를 삭제 하려면 다음 코드를 추가 합니다 `ProductsController` 클래스:

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

이 예제에서는 탐색 속성은 단일 `Supplier` 엔터티. 컬렉션 탐색 속성을 사용 하는 경우 링크를 삭제 하려면 URI는 관련된 엔터티에 대 한 키를 포함 해야 합니다. 예를 들어:

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

이 요청 고객 1에서에서 1을 순서를 제거합니다. 이 경우 DeleteLink 메서드는 다음 서명을 가질 됩니다.

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

합니다 *relatedKey* 매개 변수는 관련된 엔터티에 대 한 키를 제공 합니다. 따라서 프로그램 `DeleteLink` 메서드를 조회 하 여 기본 엔터티는 *키* 매개 변수를 하 여 관련된 엔터티를 찾을 *relatedKey* 매개 변수를 제거한 다음, 연결 합니다. 데이터 모델에 따라서는 버전을 모두 구현 해야 `DeleteLink`합니다. 웹 API는 요청 URI에 따라 올바른 버전을 호출 합니다.
