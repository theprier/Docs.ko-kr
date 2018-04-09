---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: 데이터 전송 개체 Dto ()를 만들 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: 35e01f959072b96204de3e2ce3d507635720e110
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="create-data-transfer-objects-dtos"></a>데이터 전송 개체 (Dto) 만들기
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](https://github.com/MikeWasson/BookService)

이제, 오른쪽 웹 API를 클라이언트 데이터베이스 엔터티를 노출합니다. 클라이언트는 데이터베이스 테이블에 직접 매핑되는 데이터를 받습니다. 그러나 없는 항상는 것이 좋습니다. 클라이언트에 보낸 데이터의 모양을 변경 하려는 경우가 있습니다. 예를 들어, 다음을 수행합니다.

- (이전 단원 참조) 순환 참조를 제거 합니다.
- 클라이언트를 보려면 안 특정 속성을 숨깁니다.
- 페이로드 크기를 줄이기 위해 일부 속성을 생략 합니다.
- 클라이언트에 대 한 더 편리 하 게 하려면 중첩 된 개체를 포함 하는 개체 그래프를 평면화 합니다.
- "게시 과도 하 게" 보안 문제를 방지 합니다. (참조 [모델 유효성 검사](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) 과도 하 게 게시에 대 한 내용은.)
- 데이터베이스 계층에서 서비스 계층을 통해 분리 합니다.

이를 위해 정의할 수 있습니다는 *데이터 전송 개체* (DTO). 한 DTO는 네트워크를 통해 데이터가 전송 되는 방법을 정의 하는 개체입니다. 책 엔터티와 함께 작동 하는 방법을 살펴보겠습니다. 모델 폴더에서 두 개의 DTO 클래스를 추가 합니다.

[!code-csharp[Main](part-5/samples/sample1.cs)]

`BookDetailDTO` 클래스는 점을 제외 하 고 책 모델에서 속성을 모두 포함 `AuthorName` 사람의 이름을 포함 하는 문자열입니다. `BookDTO` 클래스에서 속성의 하위 집합에 포함 되어 `BookDetailDTO`합니다.

두 개의 GET 메서드를 다음으로 바꾸기는 `BooksController` Dto 반환 하는 버전의 클래스. LINQ를 사용 합니다 **선택** 책 엔터티에서 Dto로 변환 하는 문입니다.

[!code-csharp[Main](part-5/samples/sample2.cs)]

다음은 새에 의해 생성 된 SQL `GetBooks` 메서드. EF LINQ 변환 있는지 확인할 수 있습니다 **선택** SQL SELECT 문으로 합니다.

[!code-sql[Main](part-5/samples/sample3.sql)]

마지막으로 수정 된 `PostBook` 메서드를 한 DTO 반환 합니다.

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> 이 자습서에서는 변환 대상 Dto 수동으로 코드에서. 또 다른 옵션은 같은 라이브러리를 사용 하도록 [AutoMapper](http://automapper.org/) 변환이 자동으로 처리 하는 합니다.
> 
> [!div class="step-by-step"]
> [이전](part-4.md)
> [다음](part-6.md)
