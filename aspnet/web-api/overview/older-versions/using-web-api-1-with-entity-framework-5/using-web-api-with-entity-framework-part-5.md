---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: '5 단계: Knockout.js를 사용 하 여 동적 UI를 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/04/2012
ms.topic: article
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: b63446d076fbb1143641dead788042967b996bf8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a>5 단계: Knockout.js와 동적 UI 만들기
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a>Knockout.js를 사용 하 여 동적 UI 만들기

이 섹션에서는 관리 보기에 기능을 추가 Knockout.js 사용 합니다.

[Knockout.js](http://knockoutjs.com/) HTML 컨트롤을 데이터 바인딩할 활용할 수 있는 Javascript 라이브러리입니다. Knockout.js 모델-뷰-MVVM () 패턴을 사용 합니다.

- *모델* (대/소문자, 제품 및 orders)에서 비즈니스 도메인에 있는 데이터의 서버 쪽 표현입니다.
- *보기* 프레젠테이션 계층 (HTML)입니다.
- *뷰 모델* 모델 데이터를 보유 하는 Javascript 개체입니다. 뷰 모델은 UI의 코드 추상화입니다. 그는 HTML 표현의 알지 못합니다. 대신, "목록 등의 항목" 보기의 추상 기능을 나타냅니다.

뷰 데이터 바인딩된 뷰 모델에 있습니다. 뷰 모델에 대 한 업데이트는 자동으로 보기에 반영 됩니다. 또한 뷰 모델 이벤트 단추 클릭 같은 보기에서 가져오고 주문을 만들기와 같은 모델에 대 한 작업을 수행 합니다.

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

먼저 뷰 모델을 정의 합니다. 그 후 우리는 HTML 태그에 바인딩합니다 뷰 모델.

Admin.cshtml를 다음 Razor 섹션을 추가 합니다.

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

파일에서 아무 곳 이나이 섹션을 추가할 수 있습니다. 닫기 전에 마우스 오른쪽 단추로 뷰를 렌더링할 때 HTML 페이지의 맨 아래에 표시 되는 섹션 &lt;/본문&gt; 태그입니다.

이 페이지에 대 한 스크립트의 모든 주석으로 표시 하는 스크립트 태그 안에 들어갈:

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

첫째, 뷰 모델 클래스를 정의 합니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

**ko.observableArray** 는 특별 한 유형의 Knockout, 호출의 개체는 *observable*합니다. [Knockout.js 설명서](http://knockoutjs.com/documentation/observables.html): observable은 "JavaScript 개체를 변경 하는 방법에 대 한 구독자에 게 알릴 수 있습니다." 관찰 가능 개체의 내용을 변경 하는 경우 보기와 일치 하도록 자동 업데이트 됩니다.

채우는 `products` 배열, 웹 API에 AJAX 요청을 확인 합니다. 뷰 모음에서 API에 대 한 기본 URI를 저장 했습니다 회수 (참조 [4 부](using-web-api-with-entity-framework-part-4.md) 자습서의).

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

다음으로 함수 생성, 업데이트 및 삭제 제품을 보기 모델에 추가 합니다. 이러한 함수 web API에 AJAX 호출을 제출 하 고 결과 사용 하 여 뷰 모델을 업데이트 합니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

가장 중요 한 부분은 이제: 때 DOM 로드 호출이 fulled는 **ko.applyBindings** 작동 하며의 새 인스턴스를 전달는 `ProductsViewModel`:

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

**ko.applyBindings** 메서드 Knockout를 활성화 하 고 뷰 모델 보기에 연결 합니다.

뷰 모델을 만들었으므로 이제 해당 바인딩을 만들 수 있습니다. Knockout.js,이 작업을 수행 추가 하 여 `data-bind` HTML 요소에 특성입니다. 예를 들어 HTML 목록 배열에 바인딩할 사용은 `foreach` 바인딩:

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

`foreach` 바인딩 배열에서 반복 하 고 배열에 있는 자식 각 개체에 대 한 요소를 만듭니다. 자식 요소에 바인딩을 배열 개체의 속성을 참조할 수 있습니다.

다음 바인딩은 "업데이트 제품" 목록에 추가 합니다.

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

`<li>` 요소 범위 내에서 발생 된 **foreach** 바인딩. 의미 Knockout는 각 제품에 대해 한 번 요소를 렌더링 하는 `products` 배열입니다. 모든 내 바인딩에 `<li>` 요소는 해당 제품 인스턴스를 참조 합니다. 예를 들어 `$data.Name` 참조 하는 `Name` 제품에는 속성입니다.

텍스트 입력의 값을 설정 하려면는 `value` 바인딩. 모델 뷰 단추와 기능에 연결이 바인딩됩니다.를 사용 하는 `click` 바인딩. 제품 인스턴스는 각 함수에 대 한 매개 변수로 전달 됩니다. 자세한 내용은 [Knockout.js 설명서](http://knockoutjs.com/documentation/observables.html) 다양 한 바인딩의 좋은 설명 했습니다.

그런 다음에 대 한 바인딩을 추가 **제출** 제품 추가 폼에서 이벤트:

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

이 바인딩은 호출는 `create` 새 제품을 작성 하려면 보기 모델에는 함수입니다.

관리 보기에 대 한 전체 코드는 다음과 같습니다.

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

응용 프로그램을 실행 하 고 관리자 계정으로 로그인 "Admin" 링크를 클릭 합니다. 제품 목록을 참조 하 고 만들기, 업데이트 또는 제품을 삭제 하는 작업을 할 수 해야 합니다.

> [!div class="step-by-step"]
> [이전](using-web-api-with-entity-framework-part-4.md)
> [다음](using-web-api-with-entity-framework-part-6.md)
