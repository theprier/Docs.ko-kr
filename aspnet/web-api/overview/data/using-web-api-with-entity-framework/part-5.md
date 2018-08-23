---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: 데이터 전송 개체 (Dto) 만들기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: 95075dd748f0fe4eb6d1c52d6bfe4a4576653b4c
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41838521"
---
<a name="create-data-transfer-objects-dtos"></a>데이터 전송 개체 (Dto) 만들기
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

이제 오른쪽 웹 API 클라이언트에 데이터베이스 엔터티를 노출합니다. 클라이언트는 데이터베이스 테이블에 직접 매핑되는 데이터를 수신 합니다. 그러나 없는 항상 좋습니다. 클라이언트에 보내는 데이터의 모양을 변경 하려는 경우가 있습니다. 예를 들어, 다음을 수행합니다.

- (이전 섹션 참조) 하는 순환 참조를 제거 합니다.
- 클라이언트를 보려면 해야 하지는 특정 속성을 숨깁니다.
- 페이로드 크기를 줄이기 위해 일부 속성을 생략 합니다.
- 클라이언트에 대 한 편리한 있도록 중첩 된 개체를 포함 하는 개체 그래프를 평면화 합니다.
- "과도 한 게시" 취약점을 방지 합니다. (참조 [모델 유효성 검사](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) 과도 한 게시에 대 한 내용은.)
- 데이터베이스 계층에서 서비스 계층을 분리 합니다.

이를 위해 정의할 수 있습니다는 *데이터 전송 개체* (DTO). DTO는 네트워크를 통해 데이터가 전송 되는 방법을 정의 하는 개체입니다. 책 엔터티와 작동 하는 방법을 살펴보겠습니다. Models 폴더에서 두 개의 DTO 클래스를 추가 합니다.

[!code-csharp[Main](part-5/samples/sample1.cs)]

합니다 `BookDetailDTO` 클래스를 포함 한다는 점을 제외 하는 책 모델에서 속성을 모두 `AuthorName` 작성자 이름을 포함 하는 문자열입니다. 합니다 `BookDTO` 클래스에서 속성의 하위 집합을 포함 `BookDetailDTO`합니다.

두 개의 GET 메서드를 다음으로 대체 합니다 `BooksController` Dto를 반환 하는 버전을 사용 하 여 클래스입니다. LINQ를 사용 하 여 **선택** 책 엔터티에서 Dto로 변환 하는 문입니다.

[!code-csharp[Main](part-5/samples/sample2.cs)]

다음은 새 생성 된 SQL `GetBooks` 메서드. EF에 LINQ 변환는 볼 수 있습니다 **선택** SQL SELECT 문으로 합니다.

[!code-sql[Main](part-5/samples/sample3.sql)]

마지막으로 수정 된 `PostBook` DTO를 반환 하는 방법입니다.

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> 이 자습서에서는 것으로 변환 하 고 Dto로 수동으로 코드에서입니다. 같은 라이브러리를 사용 하는 다른 옵션도 [AutoMapper](http://automapper.org/) 변환이 자동으로 처리 하는 합니다.
> 
> [!div class="step-by-step"]
> [이전](part-4.md)
> [다음](part-6.md)
