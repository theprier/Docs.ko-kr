---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: "7 단계: 기본 만들기 페이지 | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/04/2012
ms.topic: article
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: 4d06e72bc664f707bbbe4603be41347158c58903
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="part-7-creating-the-main-page"></a>7 단계: 기본 만들기 페이지
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a>기본 만들기 페이지

이 섹션에서는 기본 응용 프로그램 페이지를 만들게 됩니다. 이 페이지 몇 개의 단계에서 않아도 됩니다 म 하므로 관리 페이지에서 보다 복잡 한 됩니다. 과정에서 몇 가지 고급 Knockout.js 기법을 볼 수 있습니다. 페이지의 기본 레이아웃 다음과 같습니다.

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- 제품의 배열을 포함 하는 "products"입니다.
- "Cart" 제품 수량을의 배열을 보유합니다. "Add to Cart"를 클릭 합니다. 그러면을 업데이트 됩니다.
- "Orders" 주문 Id의 배열을 보유합니다.
- "Details" 항목 (제품 수량이)의 배열이 있는 주문 세부 정보를 보유 합니다.

데이터 바인딩 또는 스크립트 없이 HTML의 몇 가지 기본적인 레이아웃을 정의 하 여 시작 합니다. Views/Home/Index.cshtml 파일을 열고 모든 내용을 다음으로 바꿉니다.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

다음으로 스크립트 섹션을 추가 하 고 빈 뷰 모델을 만듭니다.

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

예제의 보기 모델 이전 스케치 디자인에 따라, 제품, 카트, 주문 및 세부 정보에 대 한 관찰 가능 개체를 필요 합니다. 다음 변수를 추가 `AppViewModel` 개체:

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

사용자는 장바구니에 제품 목록에서 항목을 추가할 수 있습니다 및 카트에서 항목을 제거 합니다. 이러한 함수를 캡슐화 하는 제품을 나타내는 다른 뷰 모델 클래스를 만들어 보겠습니다. 다음 코드를 `AppViewModel`에 추가합니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

`ProductViewModel` 카트에서 제품을 이동 하는 데 사용 되는 두 개의 함수를 포함 하는 클래스: `addItemToCart` 카트에, 제품의 한 단위를 추가 하 고 `removeAllFromCart` 제품의 수량을 제거 합니다.

사용자가 기존 주문을 선택 하 고 주문 세부 정보를 가져올 수 있습니다. 다른 보기 모델에이 기능을 캡슐화 합니다 했습니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

`OrderDetailsViewModel` 는 순서를 사용 하 여 초기화는 서버에 AJAX 요청을 전송 하 여 주문 세부 정보를 인출 합니다.

또한는 `total` 속성에는 `OrderDetailsViewModel`합니다. 이 속성은 특수 한 유형의 호출 하는 observable는 [observable 계산](http://knockoutjs.com/documentation/computedObservables.html)합니다. 이름에서 알 수 있듯이 계산된 관찰 가능 개체를 수 있습니다. 계산 된 값을 & # 8212에 데이터 바인딩하는 주문의 총 비용이 경우.

다음으로, 이러한 함수를 추가 `AppViewModel`:

- `resetCart`그러면에서 모든 항목을 제거합니다.
- `getDetails`주문에 대 한 세부 정보를 가져옵니다 (새 pusing 여 `OrderDetailsViewModel` 에 `details` 목록).
- `createOrder`새 주문을 만들고 카트를 비웁니다.


[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

마지막으로, 제품 및 주문에 대 한 AJAX 요청을 수행 하 여 뷰 모델을 초기화 합니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

물론는 많은 코드, 하지만 빌드 했습니다를 단계별, 여러분도 이러한 디자인은 선택 취소 합니다. 이제 html 일부 Knockout.js 바인딩을 추가할 수 있습니다.

**제품**

제품 목록에 대 한 바인딩을 다음과 같습니다.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

이 제품 배열에 대해 반복 하 고 이름과 가격을 표시 합니다. "순서에 추가" 단추는 사용자가 로그인 하는 경우에 표시 됩니다.

"순서에 추가" 단추 호출 `addItemToCart` 에 `ProductViewModel` 제품에 대 한 인스턴스. 이 Knockout.js의 뛰어난 기능을 보여 줍니다: 뷰 모델 다른 뷰 모델을 포함 된 경우 내부 모델에 해당 바인딩을 적용할 수 있습니다. 이 예제에서는 바인딩 내에서 `foreach` 각에 적용 되는 `ProductViewModel` 인스턴스. 이 방법은 모든 기능이 단일 보기 모델에 배치 하는 것 보다 더 간단 합니다.

**카트**

그러면에 대 한 바인딩을 다음과 같습니다.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

카트 배열에 대해 반복 하 고 이름, 가격 및 수량이 표시 됩니다. "제거" 링크와 "주문 작성" 단추가 바인딩됨을 뷰 모델 함수 note 합니다.

**주문**

다음은 orders 목록에 대 한 바인딩을입니다.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

이 주문에 대해 반복 하 고 주문 ID를 표시 링크 클릭 이벤트에 바인딩된는 `getDetails` 함수입니다.

**주문 세부 정보**

주문 세부 정보에 대 한 바인딩을 다음과 같습니다.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

이 순서 대로 항목을 반복 하 고 제품, 가격 및 수량을 표시 합니다. 주변 div 세부 정보 배열 하나 이상의 항목을 포함 하는 경우에 표시 됩니다.

## <a name="conclusion"></a>결론

이 자습서에서는 데이터베이스 및 데이터 계층 위에 공용 인터페이스를 제공 하는 ASP.NET Web API와 통신 하기 위해 Entity Framework를 사용 하는 응용 프로그램을 만들었습니다. ASP.NET MVC 4을 사용 하 여 렌더링 된 HTML 페이지 및 Knockout.js + jQuery 페이지가 다시 로드 하지 않고 동적 상호 작용을 제공 했습니다.

추가 리소스:

- [ASP.NET 데이터 액세스 콘텐츠 맵](https://msdn.microsoft.com/library/6759sth4.aspx)
- [Entity Framework 개발자 센터](https://msdn.microsoft.com/data/ef)

>[!div class="step-by-step"]
[이전](using-web-api-with-entity-framework-part-6.md)
