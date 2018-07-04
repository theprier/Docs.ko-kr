---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: '3 부: 관리 컨트롤러 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/04/2012
ms.topic: article
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: b9d21edec7b5006beea83395cdfc5ae181992e7d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365047"
---
<a name="part-3-creating-an-admin-controller"></a>3 부: 관리 컨트롤러 만들기
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a>관리 컨트롤러를 추가 합니다.

이 섹션에서는 CRUD를 지 원하는 웹 API 컨트롤러를 추가 합니다 (만들기, 읽기, 업데이트 및 삭제) 제품에 대 한 작업입니다. 컨트롤러는 데이터베이스 계층을 사용 하 여 통신 하도록 Entity Framework를 사용 합니다. 관리자만이 컨트롤러를 사용할 수 없게 됩니다. 고객은 다른 컨트롤러를 통해 제품을 액세스 합니다.

솔루션 탐색기에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 합니다. 선택 **추가할** 차례로 **컨트롤러**합니다.

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

에 **컨트롤러 추가** 대화 상자에서 컨트롤러 이름 `AdminController`입니다. 아래 **템플릿을**를 선택 &quot;읽기/쓰기 작업을 Entity Framework를 사용 하 여 포함 된 API 컨트롤러&quot;합니다. 아래 **모델 클래스**, "Product (ProductStore.Models)"를 선택 합니다. 아래 **데이터 컨텍스트**을 선택 "&lt;새 데이터 컨텍스트에&gt;"입니다.

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> 경우는 **모델 클래스** 드롭다운 표시 하지 않습니다 모든 모델 클래스를 프로젝트를 컴파일 되었는지 확인 합니다. Entity Framework 컴파일된 어셈블리를 해야 하므로 리플렉션을 사용 합니다.


선택 "&lt;새 데이터 컨텍스트에&gt;" 열립니다 합니다 **새 데이터 컨텍스트에** 대화 합니다. 데이터 컨텍스트 이름을 `ProductStore.Models.OrdersContext`입니다.

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

클릭 **확인** 해제 하는 **새 데이터 컨텍스트에** 대화 합니다. 에 **컨트롤러 추가** 대화 상자에서 클릭 **추가**합니다.

프로젝트에 추가 되었습니다 기능 다음과 같습니다.

- 클래스가 `OrdersContext` 에서 파생 된 **DbContext**합니다. 이 클래스는 POCO 모델 및 데이터베이스 간의 연결을 제공합니다.
- 명명 된 Web API 컨트롤러 `AdminController`합니다. 이 컨트롤러에서 CRUD 작업 지원 `Product` 인스턴스. 사용 된 `OrdersContext` Entity Framework와 통신 하는 클래스입니다.
- Web.config 파일에서 새 데이터베이스 연결 문자열입니다.

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

OrdersContext.cs 파일을 엽니다. 생성자는 데이터베이스 연결 문자열의 이름을 지정 하는지 확인 합니다. 이 이름은 Web.config에 추가 된 연결 문자열을 가리킵니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

`OrdersContext` 클래스에 다음 속성을 추가합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

A **DbSet** 쿼리할 수 있는 엔터티 집합을 나타냅니다. 에 대 한 전체 목록은 다음과 같습니다는 `OrdersContext` 클래스:

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

`AdminController` 클래스 기본 CRUD 기능 구현 하는 5 개의 메서드를 정의 합니다. 각 메서드는 클라이언트가 호출할 수 있는 URI에 해당 됩니다.

| 컨트롤러 메서드 | 설명 | URI | HTTP 메서드 |
| --- | --- | --- | --- |
| GetProducts | 모든 제품을 가져옵니다. | api/제품 | 가져오기 |
| GetProduct | 제품을 id를 찾습니다. | api/products/*id* | 가져오기 |
| PutProduct | 제품을 업데이트합니다. | api/products/*id* | PUT |
| PostProduct | 새 제품을 만듭니다. | api/제품 | 올리기 |
| DeleteProduct | 제품을 삭제합니다. | api/products/*id* | Delete |

각 메서드를 호출 `OrdersContext` 데이터베이스를 쿼리 합니다. 컬렉션 (PUT, POST 및 DELETE)을 수정 하는 메서드의 호출 `db.SaveChanges` 데이터베이스로 변경 사항을 유지 합니다. 컨트롤러는 HTTP 요청에 따라 생성 및 메서드 반환 되기 전에 변경 내용을 유지 하는 데 필요한 이므로 다음 삭제 됩니다.

## <a name="add-a-database-initializer"></a>데이터베이스 이니셜라이저를 추가 합니다.

Entity Framework에는 시작 시 데이터베이스를 채우고 모델 변경 될 때마다 데이터베이스를 자동으로 다시 사용 하면 멋진 기능입니다. 이 기능은 모델을 변경 하는 경우에 일부 테스트 데이터를 항상 있기 때문에 개발 하는 동안 유용 합니다.

솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭 하 고 라는 새 클래스를 만듭니다 `OrdersContextInitializer`합니다. 다음 구현에 붙여 넣습니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

상속 하 여는 **DropCreateDatabaseIfModelChanges** 클래스를 Entity Framework 모델 클래스 수정 될 때마다 데이터베이스를 삭제 하도록 지시 했습니다. Entity Framework (만들거나 다시) 데이터베이스를 호출 합니다 **시드** 메서드는 테이블을 채웁니다. 사용 된 **시드** 일부 예제에서는 제품 및 예제 주문을 추가 하는 방법.

테스트를 위해이 기능은 유용 하지만 사용 하지 않는 합니다 **DropCreateDatabaseIfModelChanges** 모델 클래스 변경 되 면 데이터를 손실 될 수 있으므로 프로덕션, 클래스입니다.

다음으로, Global.asax를 열고 다음 코드를 추가 합니다 **응용 프로그램\_시작** 메서드:

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a>컨트롤러에 요청 보내기

이 시점에서 클라이언트 코드를 작성 하지 않은 것 이지만 웹 디버깅 하는 HTTP 또는 웹 브라우저를 사용 하 여 API와 같은 도구를 호출할 수 있습니다 [Fiddler](http://www.fiddler2.com/fiddler2/)합니다. Visual Studio에서 f5 키를 눌러 디버깅을 시작 합니다. 웹 브라우저가 열립니다 `http://localhost:*portnum*/`, 여기서 *portnum* 일부 포트 번호입니다.

HTTP 요청을 보내는 "`http://localhost:*portnum*/api/admin`합니다. Entify 프레임 워크를 만들고 데이터베이스를 시드하고 해야 하기 때문에 첫 번째 요청을 완료 하려면 느려질 수 있습니다. 응답에 다음과 비슷한 수행 해야합니다.

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> [이전](using-web-api-with-entity-framework-part-2.md)
> [다음](using-web-api-with-entity-framework-part-4.md)
