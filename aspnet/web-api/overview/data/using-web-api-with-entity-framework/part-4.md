---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: 엔터티 관계 처리 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 06/16/2014
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: fcfddb3d56d0be641d2df9d92c334776975621be
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37826159"
---
<a name="handling-entity-relations"></a>엔터티 관계 처리
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

이 섹션에서는 EF에서 관련된 엔터티를 로드 하는 방법 및 모델 클래스에 순환 탐색 속성을 처리 하는 방법을 자세히 설명 합니다. (이 섹션에서는 배경 지식을 제공 하 고 자습서를 완료할 필요가 없습니다. 원하는 경우 건너뛸 [5 부.](part-5.md).)

## <a name="eager-loading-versus-lazy-loading"></a>즉시 로드 지연 로딩 비교

EF를 사용 하 여 관계형 데이터베이스를 사용 하 여 때 EF 관련 된 데이터를 로드 하는 방법을 이해 해야 합니다.

EF를 생성 하는 SQL 쿼리를 확인 하는 것이 유용 합니다. SQL 추적, 코드를 다음 줄을 추가 합니다 `BookServiceContext` 생성자:

[!code-csharp[Main](part-4/samples/sample1.cs)]

/Api/books GET 요청을 보낼 경우 다음과 같은 JSON 반환 합니다.

[!code-console[Main](part-4/samples/sample2.cmd)]

책 유효한 AuthorId를 포함 하는 경우에 작성자 속성이 null 임을 볼 수 있습니다. EF는 관련된 저자 엔터티를 로드 하지 때문입니다. SQL 쿼리 추적 로그는이 확인합니다.

[!code-console[Main](part-4/samples/sample3.sql)]

SELECT 문의 책 테이블에서 가져오고 만든 테이블을 참조 하지 않습니다.

참조를 위해 여기에서 메서드는는 `BooksController` 책 목록을 반환 하는 클래스입니다.

[!code-csharp[Main](part-4/samples/sample4.cs)]

만든 JSON 데이터의 일부로 반환 하는 방법을 살펴보겠습니다. Entity Framework의 관련된 데이터를 로드 하는 방법은 세 가지가 있습니다: 선행 로딩, 지연 로드 및 명시적 로드 합니다. 작동 방식을 이해 하는 것이 중요 하므로 각 기법을 절충을 있습니다.

### <a name="eager-loading"></a>즉시 로드

사용 하 여 *로딩과*, EF는 초기 데이터베이스 쿼리의 일환으로 관련된 엔터티를 로드 합니다. 즉시 로드를 수행 하려면 사용 합니다 **System.Data.Entity.Include** 확장 메서드.

[!code-csharp[Main](part-4/samples/sample5.cs)]

쿼리에서 만든 데이터를 포함 하는 EF를 인지를 나타냅니다. 이 변경을 수행 하 고 앱을 실행 하는 경우 이제 JSON 데이터를 다음과 같습니다.

[!code-console[Main](part-4/samples/sample6.cmd)]

추적 로그 EF 수행 책과 저자 테이블의 조인을 보여 줍니다.

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a>지연 로드

지연 로드를 사용 하 여 EF 때 자동으로 로드 관련된 엔터티를 해당 엔터티에 대 한 탐색 속성 역참조 됩니다. 지연 로드를 사용 하도록 설정 하려면 탐색 속성을 가상 확인 합니다. 예를 들어, 책 클래스에:

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

다음 코드를 살펴보겠습니다.

[!code-csharp[Main](part-4/samples/sample9.cs)]

지연 로드를 사용 하는 경우에 액세스 하는 `Author` 속성을 `books[0]` 작성자에 대 한 데이터베이스를 쿼리 하는 EF를 발생 합니다.

지연 로드 EF는 관련된 엔터티의 검색 될 때마다 쿼리가 데이터베이스로 전송 하기 때문에 여러 데이터베이스 왕복 해야 합니다. 일반적으로 지연 로딩을 serialize 할 수 있는 개체에 대 한 비활성화 해야 합니다. Serializer에 모두 트리거 관련된 엔터티를 로드 하는 모델의 속성을 읽을 수 있습니다. 예를 들어, EF 사용 하도록 설정 하는 지연 로드를 사용 하 여 책의 목록이 serialize 하는 경우 SQL 쿼리를 같습니다. 세 가지 별도 쿼리를 수행할 수 있습니다 세 작성자를 위한 EF는 볼 수 있습니다.

[!code-console[Main](part-4/samples/sample10.sql)]

시간 지연 로드를 사용 하려는 경우 아직 있습니다. 즉시 로드는 매우 복잡 한 조인을 생성 하는 EF를 발생할 수 있습니다. 관련된 엔터티 데이터의 작은 하위 집합에 대해 필요할 수 있고 지연 로딩 보다 효율성이 합니다.

Serialization 문제를 방지 하는 한 가지 방법은 데이터 전송 개체 (Dto) 대신 엔터티 개체를 serialize 하는 것입니다. 문서의 뒷부분에서이 방법을 설명할 것입니다.

### <a name="explicit-loading"></a>명시적 로드

명시적 로드는 비슷하지만 지연 로드를 제외 하 고 코드에서 명시적으로 관련된 데이터를 가져옵니다. 탐색 속성에 액세스할 때 자동으로 발생 하지 않습니다. 명시적 로드 관련된 데이터를 로드 하는 경우 더 많은 제어를 제공 하지만 추가 코드가 필요 합니다. 명시적 로드에 대 한 자세한 내용은 참조 하세요. [관련 엔터티 로드](https://msdn.microsoft.com/data/jj574232#explicit)합니다.

## <a name="navigation-properties-and-circular-references"></a>탐색 속성 및 순환 참조

탐색 속성에 정의 책 및 작성자 모델을 정의한 경우는 `Book` 책 저자 관계에 대 한 클래스 반대 방향으로 탐색 속성을 정의 하지 않았으므로 있습니까 있지만 합니다.

해당 탐색 속성을 추가 하는 경우는 `Author` 클래스?

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

아쉽게도이 모델을 serialize 할 때 문제가 있습니다. 관련된 데이터를 로드 하는 경우 순환 개체 그래프를 만듭니다.

![](part-4/_static/image1.png)

JSON 또는 XML 포맷터를 그래프를 serialize 하려고 하면 예외가 throw 됩니다. 두 포맷터를 다른 예외 메시지를 throw 합니다. JSON 포맷터에 대 한 예는 다음과 같습니다.

[!code-console[Main](part-4/samples/sample12.cmd)]

XML 포맷터는 다음과 같습니다.

[!code-xml[Main](part-4/samples/sample13.xml)]

하나의 솔루션 다음 섹션에서 설명 하는 Dto를 사용 하는 것입니다. 또는 그래프 주기를 처리 하는 JSON 및 XML 포맷터를 구성할 수 있습니다. 자세한 내용은 [개체 순환 참조가 처리](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)합니다.

이 자습서에서는 필요 하지 않습니다는 `Author.Book` 탐색 속성을 둘 수 있습니다.

> [!div class="step-by-step"]
> [이전](part-3.md)
> [다음](part-5.md)
