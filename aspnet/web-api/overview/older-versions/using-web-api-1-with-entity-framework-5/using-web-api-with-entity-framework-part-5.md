---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: '5 부: Knockout.js를 사용 하 여 동적 UI 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: aspnetcontent
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: 7d8bd4732ecf73c14251ceebfd667310f6e197b4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37801695"
---
<a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a>5 부: Knockout.js를 사용 하 여 동적 UI 만들기
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a>Knockout.js를 사용 하 여 동적 UI 만들기

이 섹션에서는 관리 보기에 기능을 추가할 Knockout.js 사용 하겠습니다.

[Knockout.js](http://knockoutjs.com/) 쉽게 HTML 컨트롤 데이터를 바인딩할 수 있도록 하는 Javascript 라이브러리입니다. Knockout.js-Model-view-viewmodel (MVVM) 패턴을 사용합니다.

- 합니다 *모델* 사례, 제품 및 주문) (에 비즈니스 도메인에 있는 데이터의 서버 쪽 표현입니다.
- 합니다 *보기* 는 프레젠테이션 계층 (HTML).
- 합니다 *뷰 모델* 는 모델 데이터를 보유 하는 Javascript 개체입니다. 보기-모델은 ui 코드 추상화 합니다. 이 HTML 표현의 알지 못합니다. 대신 "항목을 목록"와 같은 뷰의 추상 기능을 나타냅니다.

뷰는 데이터 바인딩된 뷰 모델입니다. 보기-모델에 대 한 업데이트 보기에서 자동으로 반영 됩니다. 보기-모델은 또한 단추 클릭 같은 보기에서 이벤트를 가져옵니다 하 고 주문 만들기와 같은 모델에 대 한 작업을 수행 합니다.

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

먼저 보기-모델 정의 됩니다. 그런 다음 HTML 태그를 보기-모델에 바인딩합니다.

다음 Razor 섹션 Admin.cshtml를 추가 합니다.

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

이 섹션에서는 파일에서 아무 곳 이나 추가할 수 있습니다. 뷰를 렌더링할 때 HTML 페이지의 맨 아래에 표시 되는 섹션을 닫기 전에 오른쪽 &lt;본문/&gt; 태그입니다.

이 페이지에 대 한 스크립트의 모든 주석으로 표시 하는 스크립트 태그 내에서 이동 합니다.

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

첫째, 보기 모델 클래스를 정의 합니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

**ko.observableArray** Knockout, 호출의 개체는 특별 한는 *observable*합니다. [Knockout.js 설명서](http://knockoutjs.com/documentation/observables.html):는 관찰 가능 개체는 "JavaScript 개체 변경 내용에 대 한 구독자에 알릴 수 있는." 관찰 가능 개체의 내용이 변경 되 면 뷰 일치 하도록 자동 업데이트 됩니다.

채우는 데는 `products` 배열, 웹 API에 AJAX 요청을 확인 합니다. 뷰 모음에서 API에 대 한 기본 URI를 저장 했습니다 회수 (참조 [4 부](using-web-api-with-entity-framework-part-4.md) 자습서).

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

다음으로, 만들기, 업데이트 및 삭제할 제품 보기-모델 함수를 추가 합니다. 이러한 함수는 웹 API에 대 한 AJAX 호출을 제출 하 고 보기-모델을 업데이트 하는 결과 사용 하 여 합니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

가장 중요 한 부분은 이제: 경우 DOM은 fulled 로드를 호출 합니다 **ko.applyBindings** 함수 및의 새 인스턴스를 전달 합니다 `ProductsViewModel`:

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

합니다 **ko.applyBindings** 메서드 Knockout을 활성화 하 고 보기 모델 보기에 연결 합니다.

보기-모델을 만들었으므로 이제 해당 바인딩을 만들 수 있습니다. Knockout.js,이 작업을 수행을 더하여 `data-bind` HTML 요소에 특성입니다. 예를 들어, 배열에 바인딩하는 HTML 목록에 사용 된 `foreach` 바인딩:

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

`foreach` 바인딩 배열에서 반복 및 배열에 있는 자식 각 개체에 대 한 요소를 만듭니다. 자식 요소에 바인딩을 배열 개체의 속성을 참조할 수 있습니다.

다음 바인딩 "업데이트 제품" 목록에 추가 합니다.

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

합니다 `<li>` 요소가 범위 내에서 발생 합니다 **foreach** 바인딩. Knockout 됩니다 의미에서 각 제품에 한 번씩 요소를 렌더링 하는 `products` 배열입니다. 모든 내에서 바인딩에 `<li>` 요소는 제품 인스턴스를 참조 합니다. 예를 들어 `$data.Name` 가리킵니다는 `Name` 제품에는 속성입니다.

텍스트 입력의 값을 설정 하려면 사용 된 `value` 바인딩. 모델-뷰, 함수에 바인딩된 단추를 사용 하는 `click` 바인딩. Product 인스턴스의 각 함수에 매개 변수로 전달 됩니다. 자세한 내용은 합니다 [Knockout.js 설명서](http://knockoutjs.com/documentation/observables.html) 다양 한 바인딩의 좋은 설명 했습니다.

그런 다음에 대 한 바인딩을 추가 합니다 **제출** 제품 추가 폼에서 이벤트:

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

이 바인딩 호출을 `create` 새 제품을 만드는 보기 모델에는 함수입니다.

관리 보기에 대 한 전체 코드는 다음과 같습니다.

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

응용 프로그램을 실행 하 고 관리자 계정으로 로그인 "Admin" 링크를 클릭 합니다. 제품의 목록을 보려면를 만들기, 업데이트 또는 제품을 삭제 하는 일을 할 수 있습니다.

> [!div class="step-by-step"]
> [이전](using-web-api-with-entity-framework-part-4.md)
> [다음](using-web-api-with-entity-framework-part-6.md)
