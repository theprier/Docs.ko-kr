---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: "모델 및 컨트롤러를 추가 합니다. | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: b75eae11fd99b60864256f79d4770a3007487964
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="add-models-and-controllers"></a>모델 및 컨트롤러를 추가 합니다.
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](https://github.com/MikeWasson/BookService)

이 섹션에서는 데이터베이스 엔터티를 정의 하는 모델 클래스를 추가 합니다. 그런 다음 이러한 엔터티에 대 한 CRUD 작업을 수행 하는 Web API 컨트롤러를 추가 합니다.

## <a name="add-model-classes"></a>모델 클래스를 추가 합니다.

이 자습서에서는 "Code First" 접근 방식 Entity Framework (EF)를 사용 하 여 데이터베이스를 만들겠습니다. Code First를 데이터베이스 테이블에 해당 하는 C# 클래스를 작성 하 고 EF 데이터베이스를 만듭니다. (자세한 내용은 참조 [Entity Framework 개발 방법](https://msdn.microsoft.com/en-us/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)

도메인 개체 POCOs (일반 이전 CLR 개체)으로 정의 하 여 시작 합니다. 다음 POCOs을 만들겠습니다.

- 만든 이
- 북

솔루션 탐색기에서 마우스 오른쪽 단추로 모델 폴더를 클릭 합니다. 선택 **추가**을 선택한 후 **클래스**합니다. 클래스 이름을 `Author`로 지정합니다.

![](part-2/_static/image1.png)

모든 Author.cs에 상용구 코드 다음 코드로 바꿉니다.

[!code-csharp[Main](part-2/samples/sample1.cs)]

라는 다른 클래스를 추가 `Book`, 다음 코드를 사용 합니다.

[!code-csharp[Main](part-2/samples/sample2.cs)]

Entity Framework 데이터베이스 테이블을 만드는 이러한 모델을 사용 합니다. 각 모델에 대해는 `Id` 속성은 데이터베이스 테이블의 기본 키 열이 됩니다.

Book 클래스에는 `AuthorId` 에 외래 키 정의 `Author` 테이블입니다. (간단한 설명을 위해 필자가 가정 하 고 각 책에는 단일 작성자입니다.) 책 클래스는 관련 항목에 탐색 속성이 포함 되어 `Author`합니다. 탐색 속성을 사용 하 여 관련 액세스 `Author` 코드에서입니다. 내가 말하는 바로 그 4, 부분에 탐색 속성에 대 한 자세한 [처리 엔터티 관계](part-4.md)합니다.

## <a name="add-web-api-controllers"></a>Web API 컨트롤러 추가

이 섹션에서는 Web API 컨트롤러 CRUD 작업을 지 원하는 추가 합니다 (만들기, 읽기, 업데이트 및 삭제) 합니다. 데이터베이스 계층와 통신 하는 컨트롤러 Entity Framework를 사용 합니다.

첫째, Controllers/ValuesController.cs 파일을 삭제할 수 있습니다. 이 파일에는 예제 웹 API 컨트롤러 포함 되어 있지만이 자습서에 대 한 필요 하지 않습니다.

![](part-2/_static/image2.png)

다음으로 프로젝트를 빌드하십시오. Web API 스 캐 폴딩 리플렉션을 사용 하 여 되므로 컴파일된 어셈블리 원래 모델 클래스를 찾을 수 있습니다.

솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다. 선택 **추가**을 선택한 후 **컨트롤러**합니다.

![](part-2/_static/image3.png)

에 **추가 스 캐 폴드** 대화 상자에서 "Web API 2 Entity Framework를 사용 하 여 작업, 컨트롤러"입니다. **추가**를 클릭합니다.

![](part-2/_static/image4.png)

에 **컨트롤러 추가** 대화 상자에서 다음을 수행 합니다.

1. 에 **모델 클래스** 드롭다운을 선택 된 `Author` 클래스입니다. (경우 보이지 않으면 드롭다운에 나열 된 것을 해야 프로젝트를 빌드.)
2. "비동기 컨트롤러 동작 사용"을 확인 합니다.
3. 으로 컨트롤러 이름을 둡니다 &quot;AuthorsController&quot;합니다.
4. 클릭 더하기 (+) 단추 옆에 **데이터 컨텍스트 클래스가**합니다.

![](part-2/_static/image5.png)

에 **새 데이터 컨텍스트에** 대화 상자에서 기본 이름을 그대로 두고 클릭 **추가**합니다.

![](part-2/_static/image6.png)

클릭 **추가** 완료 하는 **컨트롤러 추가** 대화 상자. 프로젝트에 두 개의 클래스를 추가 하는 대화 상자:

- `AuthorsController`Web API 컨트롤러를 정의합니다. 컨트롤러는 클라이언트가 사용 작성자의 목록에서 CRUD 작업을 수행 하는 REST API를 구현 합니다.
- `BookServiceContext`데이터베이스에 데이터는 데이터베이스, 변경 내용 추적 및 데이터 유지를 사용 하 여 개체를 채우는 포함 하는 런타임 시 엔터티 개체를 관리 합니다. 상속 된 `DbContext`합니다.

![](part-2/_static/image7.png)

이 시점에서 프로젝트를 다시 빌드하십시오. 에 대 한 API 컨트롤러를 추가 하려면 동일한 단계를 수행해 이제 `Book` 엔터티. 선택이 시간 `Book` 기존 선택한 모델 클래스에 대 한 `BookServiceContext` 데이터 컨텍스트 클래스에 대 한 클래스입니다. (새 데이터 컨텍스트를 만들지 않습니다.) 클릭 **추가** 컨트롤러를 추가 합니다.

![](part-2/_static/image8.png)

>[!div class="step-by-step"]
[이전](part-1.md)
[다음](part-3.md)
