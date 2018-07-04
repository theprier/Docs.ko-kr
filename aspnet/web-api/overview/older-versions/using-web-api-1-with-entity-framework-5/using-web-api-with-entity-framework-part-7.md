---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: '7 부: 만드는 주 페이지 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/04/2012
ms.topic: article
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: b748813046637b9972bc96e22c35d2eeb9b57f9d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37378899"
---
<a name="part-7-creating-the-main-page"></a>7 부: 기본 만들기 페이지
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a>기본 만들기 페이지

이 섹션에서는 주요 응용 프로그램 페이지를 만듭니다. 이 페이지에서는 여러 단계에서 접근 됩니다 있도록 관리 페이지에서 보다 복잡 한 됩니다. 이 과정에서 몇 가지 고급 Knockout.js 기술을 볼 수 있습니다. 페이지의 기본 레이아웃은 다음과 같습니다.

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- "제품" 제품의 배열을 보유합니다.
- "Cart" 수량을 사용 하 여 제품의 배열을 보유합니다. "Add to Cart"를 클릭 하 여 카트를 업데이트 합니다.
- "Orders" 주문 Id의 배열을 보유합니다.
- "세부 정보" 항목 (제품 수량을 사용 하 여)의 배열 되는 주문 세부 정보를 보유 합니다.

데이터 바인딩이 없거나 스크립트를 사용 하 여 html, 일부 기본 레이아웃을 정의 하 여 시작 하겠습니다. Views/Home/Index.cshtml 파일을 열고 모든 콘텐츠를 다음으로 바꿉니다.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

다음으로, 스크립트 섹션을 추가 하 고 빈 보기-모델을 만듭니다.

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

보기 모델 스케치 이전 디자인에 따라 제품, 카트, 주문 및 세부 정보에 대 한 관찰 가능 개체를 해야 합니다. 다음 변수를 추가 합니다 `AppViewModel` 개체:

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

사용자가 장바구니에에 제품 목록에서 항목을 추가 하 고 장바구니에서 항목을 제거할 수 있습니다. 이러한 함수를 캡슐화 하는 제품을 나타내는 다른 보기 모델 클래스를 만들어 보겠습니다. 다음 코드를 `AppViewModel`에 추가합니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

합니다 `ProductViewModel` 클래스에 카트에서 제품을 이동 하는 데 사용 되는 두 가지 함수가 포함 되어 있습니다.: `addItemToCart` 장바구니에 제품의 단위를 하나 추가 및 `removeAllFromCart` 제품의 수량을 제거 합니다.

사용자는 기존 주문을 선택 하 고 주문 세부 정보를 가져올 수 있습니다. 이 기능은 다른 보기 모델에 캡슐화 했습니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

`OrderDetailsViewModel` 순서를 사용 하 여 초기화 됩니다 및 AJAX 요청을 서버로 전송 하 여 주문 세부 정보를 가져옵니다.

또한 합니다 `total` 속성에는 `OrderDetailsViewModel`합니다. 이 속성은 특수 한 유형의 호출 하는 관찰 가능 개체를 [관찰 가능 개체를 계산](http://knockoutjs.com/documentation/computedObservables.html)합니다. 이름에서 알 수 있듯이 계산된 observable 사용 하면 계산 된 값을 데이터 바인딩&#8212;주문의 총 비용이 예제의 경우.

이러한 함수를 다음으로, 추가 `AppViewModel`:

- `resetCart` 카트에서 모든 항목을 제거합니다.
- `getDetails` 주문에 대 한 세부 정보를 가져옵니다 (새 pusing 하 여 `OrderDetailsViewModel` 에 `details` 목록).
- `createOrder` 새 주문을 만들고 장바구니를 비웁니다.


[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

마지막으로, 제품 및 주문에 대 한 AJAX 요청을 만들어 뷰 모델을 초기화 합니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

그렇다면 코드의 많은 하지만 빌드 하였습니다 up 단계별 여러분도 이러한 디자인은의 선택을 취소 합니다. 이제 html 일부 Knockout.js 바인딩을 추가할 수 있습니다.

**제품**

제품 목록에 대 한 바인딩을 다음과 같습니다.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

이 제품 배열을 반복 하 고 이름과 가격을 표시 합니다. "순서에 추가" 단추를 사용자가 로그인 하는 경우에 표시 됩니다.

"순서에 추가" 단추 호출 `addItemToCart` 에 `ProductViewModel` 제품에 대 한 인스턴스. Knockout.js의 뛰어난 기능을 보여 줍니다: 다른 보기 모델에 포함 되어 있으면 보기-모델 내부 모델에 해당 바인딩을 적용할 수 있습니다. 이 예제에서는 내에서 바인딩에 합니다 `foreach` 각각에 적용 되는 `ProductViewModel` 인스턴스. 이 방법은 단일 보기-모델에 배치 하는 모든 기능 보다 훨씬 더 명확 합니다.

**카트**

카트 바인딩을 다음과 같습니다.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

이 카트 배열을 반복 하 고 이름, 가격 및 수량을 표시 합니다. 연결 "제거" 및 "주문 작성" 단추를 뷰 모델 함수에 바인딩되어 있는지 note 합니다.

**주문**

주문 목록에 대 한 바인딩을 다음과 같습니다.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

이 주문이 될 때까지 반복 하 고 주문 ID를 보여 줍니다. 링크의 click 이벤트 바인딩되는 `getDetails` 함수입니다.

**주문 세부 정보**

주문 세부 정보에 대 한 바인딩을 다음과 같습니다.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

이 순서 대로 항목을 반복 하 고 제품, 가격 및 수량을 표시 합니다. 주변 div 세부 정보 배열 하나 이상의 항목을 포함 하는 경우에 표시 됩니다.

## <a name="conclusion"></a>결론

이 자습서에서는 ASP.NET Web API 데이터 계층을 기반으로 공용 인터페이스를 제공 하 고 데이터베이스를 사용 하 여 통신 하기 위해 Entity Framework를 사용 하는 응용 프로그램을 만들었습니다. ASP.NET MVC 4 렌더링할 HTML 페이지 및 Knockout.js 및 jQuery 페이지를 다시 로드 하지 않고 동적 상호 작용을 제공 하려면 사용 합니다.

추가 리소스:

- [ASP.NET 데이터 액세스 콘텐츠 맵](https://msdn.microsoft.com/library/6759sth4.aspx)
- [Entity Framework 개발자 센터](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [이전](using-web-api-with-entity-framework-part-6.md)
