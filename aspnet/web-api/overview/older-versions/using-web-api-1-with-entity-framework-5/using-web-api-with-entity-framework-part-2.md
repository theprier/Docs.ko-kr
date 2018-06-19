---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: '2 단계: 도메인 모델을 만드는 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/03/2012
ms.topic: article
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: 84631494c1be266c21e5e5702182df717b1d29b0
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30878583"
---
<a name="part-2-creating-the-domain-models"></a>2 단계: 도메인 모델 만들기
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a>모델 추가

Entity Framework 방식을 사용 하는 방법은 세 가지가 있습니다.

- 데이터베이스 중심: 데이터베이스와 함께 시작 하 고 Entity Framework 코드를 생성 합니다.
- 모델 우선: 시각적 모델로 시작 하 고 엔터티 프레임 워크는 데이터베이스와 코드를 생성 합니다.
- 코드 중심: 코드를 시작 하 고 Entity Framework는 데이터베이스를 생성 합니다.

도메인 개체 POCOs (일반 이전 CLR 개체)으로 정의 하 여 시작 하므로 코드 중심 접근 방식을 사용 했습니다. 코드 중심 접근 방식으로 도메인 개체는 데이터베이스 계층 예: 거래 또는 지 속성을 지원 하기 위해 모든 추가 코드가 필요 하지 않습니다. (특히 필요가에서 상속 하는 [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) 클래스입니다.) Entity Framework 데이터베이스 스키마를 생성 하는 방법을 제어 하려면 데이터 주석을 여전히 사용할 수 있습니다.

POCOs 설명 하는 모든 추가 속성을 전송 하지 않기 때문에 [데이터베이스 상태](https://msdn.microsoft.com/library/system.data.entitystate.aspx), JSON 또는 XML에 쉽게 serialize 할 수 있습니다. 그러나 의미는 아닙니다 항상 클라이언트에 게 직접 Entity Framework 모델을 노출 해야 볼 수 있겠지만,이 자습서의 뒷부분에 나오는 합니다.

다음 POCOs을 만들겠습니다.

- 제품
- 순서
- OrderDetail

각 클래스를 만들려면 솔루션 탐색기에서 모델 폴더를 마우스 오른쪽 단추로 클릭 합니다. 상황에 맞는 메뉴에서 선택 **추가** 선택한 후 **클래스입니다.**

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

추가 `Product` 다음 구현 된 클래스:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

Entity Framework 사용 하 여 일반적으로는 `Id` 속성의 기본 키로 데이터베이스 테이블에 id 열에 매핑합니다. 만들 새 `Product` 인스턴스에 값을 설정 하지 않습니다 `Id`데이터베이스 값을 생성 하기 때문에, 합니다.

**ScaffoldColumn** 특성 지시 하지 않으려면 ASP.NET MVC는 `Id` 속성 편집기 폼을 생성 하는 경우. **필요한** 특성 모델의 유효성을 검사 하는 데 사용 됩니다. 지정 하는 `Name` 속성에는 비어 있지 않은 문자열 이어야 합니다.

추가 된 `Order` 클래스:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

추가 된 `OrderDetail` 클래스:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a>외래 키 관계

많은 주문 세부 정보를 포함 하는 주문 고 각 주문 정보는 단일 제품 합니다. 이러한 관계를 나타내기 위해는 `OrderDetail` 클래스 라는 속성을 정의 `OrderId` 및 `ProductId`합니다. Entity Framework에는 이러한 속성 외래 키를 나타내고 데이터베이스에 외래 키 제약 조건을 추가 합니다 유추 합니다.

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

`Order` 및 `OrderDetail` 클래스 관련된 개체에 대 한 참조를 포함 하는 "탐색" 속성을 포함 합니다. 주문, 지정 된 탐색 속성에 따라 순서로 제품에 이동할 수 있습니다.

지금 프로젝트를 컴파일하십시오. Entity Framework 리플렉션을 사용 하 여 컴파일된 어셈블리는 데이터베이스 스키마를 만들 필요는 모델의 속성을 검색 합니다.

## <a name="configure-the-media-type-formatters"></a>미디어 유형 포맷터를 구성 합니다.

A [미디어 유형 포맷터](../../formats-and-model-binding/media-formatters.md) 는 Web API HTTP 응답 본문을 쓸 때 데이터를 serialize 하는 개체입니다. 기본 제공 포맷터 JSON 및 XML 출력을 지원 합니다. 기본적으로 값으로 모든 개체를 serialize 모두 이러한 포맷터입니다.

개체 그래프에 순환 참조가 포함 된 경우는 문제가 발생 하는 값으로 직렬화 합니다. 해당 되는 경우와 정확히는 `Order` 및 `OrderDetail` 다른에 대 한 참조를 보유 하는 각 있기 때문에 있습니다. 포맷터는 참조, 값, 각 개체를 쓰는 따르고 맴에서 이동 합니다. 따라서 기본 동작을 변경 해야 합니다.

솔루션 탐색기에서 응용 프로그램을 확장\_폴더를 시작 하 고 WebApiConfig.cs 라는 파일을 엽니다. `WebApiConfig` 클래스에 다음 코드를 추가합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

이 코드는 개체 참조를 유지 하는 JSON 포맷터를 설정 하 고 파이프라인에서 XML 포맷터를 완전히 제거 합니다. (개체 참조를 유지 하는 XML 포맷터를 구성할 수 있습니다 하지만 약간 더 많은 작업을 이며이 응용 프로그램에 대 한 JSON만 필요 합니다. 자세한 내용은 참조 [순환 개체 참조를 처리](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)

> [!div class="step-by-step"]
> [이전](using-web-api-with-entity-framework-part-1.md)
> [다음](using-web-api-with-entity-framework-part-3.md)
