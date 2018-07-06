---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: 모델 및 컨트롤러를 추가 합니다. | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 31e0fbf65c74a18677588cfa412dc34f7b25f78f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37806360"
---
<a name="add-models-and-controllers"></a>모델 및 컨트롤러를 추가 합니다.
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

이 섹션에서는 데이터베이스 엔터티를 정의 하는 모델 클래스를 추가 합니다. 그런 다음 해당 엔터티에 대 한 CRUD 작업을 수행 하는 Web API 컨트롤러를 추가 합니다.

## <a name="add-model-classes"></a>모델 클래스 추가

이 자습서에서는 "Code First" 접근 방식에 EF (Entity Framework)를 사용 하 여 데이터베이스를 만듭니다. Code First를 사용 하 여 데이터베이스 테이블에 해당 하는 C# 클래스를 작성 하 고 EF는 데이터베이스를 만듭니다. (자세한 내용은 [Entity Framework 개발 방법](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)

Poco (plain old CLR object)으로 도메인 개체를 정의 하 여 시작 합니다. 여기서 다음 Poco 만듭니다.

- 만든 이
- 책

솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭 합니다. 선택 **추가**을 선택한 후 **클래스**합니다. 클래스 이름을 `Author`로 지정합니다.

![](part-2/_static/image1.png)

모든 Author.cs의 상용구 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](part-2/samples/sample1.cs)]

라는 다른 클래스를 추가 `Book`, 다음 코드를 사용 합니다.

[!code-csharp[Main](part-2/samples/sample2.cs)]

Entity Framework이 모델 사용 하 여 이러한 데이터베이스 테이블을 만듭니다. 각 모델에 대해는 `Id` 속성 데이터베이스 테이블의 기본 키 열이 됩니다.

책 클래스에는 `AuthorId` 외래 키로 정의 `Author` 테이블입니다. (간단히 하기 위해 필자가 가정 하 고 각 책에는 단일 작성자.) Book 클래스 관련된 탐색 속성이 포함 `Author`합니다. 탐색 속성을 사용 하 여 관련 액세스 `Author` 코드에서입니다. 4 부에서 탐색 속성에 대해 자세히 말씀 [엔터티 관계 처리](part-4.md)합니다.

## <a name="add-web-api-controllers"></a>Web API 컨트롤러 추가

이 섹션에서는 CRUD 작업을 지 원하는 Web API 컨트롤러 추가 (만들기, 읽기, 업데이트 및 삭제). 컨트롤러는 데이터베이스 계층을 사용 하 여 통신 하도록 Entity Framework를 사용 합니다.

먼저 Controllers/ValuesController.cs 파일을 삭제할 수 있습니다. 이 파일 예제에서는 Web API 컨트롤러를 포함 하지만이 자습서에서는 필요 하지 않습니다.

![](part-2/_static/image2.png)

다음에 프로젝트를 빌드하십시오. Web API 스 캐 폴딩의 리플렉션을 사용 하 여 컴파일된 어셈블리를 해야 하므로 모델 클래스를 찾습니다.

솔루션 탐색기에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 합니다. 선택 **추가**을 선택한 후 **컨트롤러**합니다.

![](part-2/_static/image3.png)

에 **스 캐 폴드 추가** 대화 상자에서 "Web API 2 Entity Framework를 사용 하 여 작업을 사용 하 여 컨트롤러"입니다. **추가**를 클릭합니다.

![](part-2/_static/image4.png)

에 **컨트롤러 추가** 대화 상자에서 다음을 수행 합니다.

1. 에 **모델 클래스** 드롭다운을 `Author` 클래스입니다. (드롭다운에 나열 된 작업을 보이지 않으면 있는지 확인 프로젝트를 빌드할 수 있습니다.)
2. "사용 하 여 비동기 컨트롤러 동작"을 확인 합니다.
3. 컨트롤러 이름으로 그대로 둡니다 &quot;AuthorsController&quot;합니다.
4. 클릭 더하기 (+) 단추 옆에 **데이터 컨텍스트 클래스**합니다.

![](part-2/_static/image5.png)

에 **새 데이터 컨텍스트에** 대화 상자에서 기본 이름을 그대로 두고 클릭 **추가**합니다.

![](part-2/_static/image6.png)

클릭 **추가** 완료 하는 **컨트롤러 추가** 대화 합니다. 프로젝트에 두 개의 클래스를 추가 하는 대화 상자:

- `AuthorsController` Web API 컨트롤러를 정의합니다. 컨트롤러는 작성자의 목록에서 CRUD 작업을 수행 하려면 클라이언트를 사용 하는 REST API를 구현 합니다.
- `BookServiceContext` 런타임에 데이터를 데이터베이스에 데이터베이스, 변경 내용 추적 및 데이터 유지를 사용 하 여 개체를 채우는 포함 하는 엔터티 개체를 관리 합니다. 상속 `DbContext`합니다.

![](part-2/_static/image7.png)

이 시점에서 프로젝트를 다시 빌드하십시오. 이제 API 컨트롤러에 대 한 추가 하려면 동일한 단계를 진행할 `Book` 엔터티. 이 이번에 선택 `Book` 기존 선택한 모델 클래스에 대 한 `BookServiceContext` 데이터 컨텍스트 클래스에 대 한 클래스입니다. (새 데이터 컨텍스트를 만들지 마세요.) 클릭 **추가** 컨트롤러를 추가 합니다.

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> [이전](part-1.md)
> [다음](part-3.md)
