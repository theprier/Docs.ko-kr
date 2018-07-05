---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: '2 부: 도메인 모델 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 07/03/2012
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: 605a3eb5d781db6b317369efe8698288d7b9f648
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37802272"
---
<a name="part-2-creating-the-domain-models"></a>2 부: 도메인 모델 만들기
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a>모델 추가

방법: Entity Framework는 다음과 같은 세 가지가 있습니다.

- 데이터베이스 중심: 데이터베이스를 사용 하 여 시작 하 고 Entity Framework 코드를 생성 합니다.
- 모델 우선: 시각적 모델을 사용 하 여 시작 하 고 Entity Framework에서는 데이터베이스와 코드를 생성 합니다.
- 코드 중심: 코드를 사용 하 여 시작 하 고 Entity Framework 데이터베이스를 생성 합니다.

Poco (plain old CLR object)으로 도메인 개체를 정의 하 여 시작 하죠 코드 우선 방식을 사용 하는 것입니다. 코드 우선 방식을 사용 하 여 도메인 개체 예: 거래 또는 지 속성 데이터베이스 계층을 지원 하기 위해 코드를 추가로 필요 하지 않습니다. (특히 필요가 없습니다에서 상속 하는 [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) 클래스입니다.) Entity Framework에서 데이터베이스 스키마를 만드는 방법을 제어 하려면 데이터 주석을 여전히 사용할 수 있습니다.

Poco 설명 하는 모든 추가 속성을 전송 하지 않기 때문 [데이터베이스 상태](https://msdn.microsoft.com/library/system.data.entitystate.aspx), JSON 또는 XML로 쉽게 직렬화 할 수 있습니다. 그러나 의미는 아닙니다 항상 클라이언트에 직접 Entity Framework 모델을 노출 해야 자습서 뒷부분에서 살펴보겠지만 합니다.

여기서 다음 Poco 만듭니다.

- 제품
- 순서
- OrderDetail

각 클래스를 만들려면 솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭 합니다. 상황에 맞는 메뉴에서 선택 **추가** 를 선택한 **클래스입니다.**

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

추가 된 `Product` 다음 구현 클래스:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

Entity Framework 사용 규칙에 따라는 `Id` 속성을 기본 키로 데이터베이스 테이블에 id 열에 매핑합니다. 새로 만들 때 `Product` 경우에 대 한 값을 설정 하지 `Id`이므로 데이터베이스에서 값을 생성 합니다.

합니다 **ScaffoldColumn** 특성은 표시 하지 않으려면 ASP.NET MVC를 지시를 `Id` 편집기 폼을 생성할 때 속성입니다. 합니다 **필요한** 특성 모델의 유효성을 검사 하는 데 사용 됩니다. 지정 된 `Name` 속성은 비어 있지 않은 문자열 이어야 합니다.

추가 된 `Order` 클래스:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

추가 된 `OrderDetail` 클래스:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a>외래 키 관계

주문을 여러 주문 세부 정보를 포함 하 고 각 주문 세부 정보를 단일 제품을 가리킵니다. 이러한 관계를 나타내는 합니다 `OrderDetail` 라는 속성을 정의 하는 클래스 `OrderId` 및 `ProductId`합니다. Entity Framework는 이러한 속성 외래 키를 나타내고 데이터베이스에 외래 키 제약 조건 추가 유추 합니다.

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

합니다 `Order` 고 `OrderDetail` 클래스 관련된 개체에 대 한 참조를 포함 하는 "탐색" 속성을 포함 합니다. 순서 지정, 탐색 속성에 따라 순서 대로 제품을 탐색할 수 있습니다.

이제 프로젝트를 컴파일하십시오. Entity Framework 리플렉션을 사용 하 여 컴파일된 어셈블리를 데이터베이스 스키마를 만들어야 하므로 모델의 속성을 검색 합니다.

## <a name="configure-the-media-type-formatters"></a>미디어 유형 포맷터를 구성 합니다.

A [미디어 유형 포맷터](../../formats-and-model-binding/media-formatters.md) 는 Web API HTTP 응답 본문을 쓸 때 데이터를 serialize 하는 개체입니다. 기본 제공 포맷터 JSON 및 XML 출력을 지원 합니다. 기본적으로 값으로 모든 개체를 serialize 모두 이러한 포맷터입니다.

Serialization 값으로 개체 그래프에 순환 참조가 포함 된 경우 문제를 만듭니다. 이 정확 하 게 사용 하 여 합니다 `Order` 및 `OrderDetail` 다른에 대 한 참조를 유지 하는 각 없으므로 클래스입니다. 포맷터는 각 개체를 값으로 작성 된 참조에 따라를 제자리에 맴에서 이동 합니다. 따라서 기본 동작을 변경 해야 합니다.

솔루션 탐색기에서 앱 확장\_폴더를 시작 하 고 WebApiConfig.cs 파일을 엽니다. `WebApiConfig` 클래스에 다음 코드를 추가합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

이 코드는 개체 참조를 유지 하는 JSON 포맷터를 설정 하 고 파이프라인에서 XML 포맷터를 완전히 제거 합니다. (개체 참조를 유지 하는 XML 포맷터를 구성할 수 있습니다 하지만 것이 좀 더 많은 작업 및이 응용 프로그램에 대 한 JSON만 필요 합니다. 자세한 내용은 [개체 순환 참조가 처리](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)

> [!div class="step-by-step"]
> [이전](using-web-api-with-entity-framework-part-1.md)
> [다음](using-web-api-with-entity-framework-part-3.md)
