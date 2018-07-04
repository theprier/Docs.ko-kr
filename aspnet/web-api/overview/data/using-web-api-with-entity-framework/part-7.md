---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: 보기 (UI) 만들기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
ms.technology: dotnet-webapi
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: e9ebe60f88ecbf65a6f8d04de9a23d72a72fda83
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37364983"
---
<a name="create-the-view-ui"></a>보기 (UI) 만들기
====================
[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

이 섹션에서는 앱에 대 한 HTML을 정의 하 고 HTML 및 보기 모델 간의 데이터 바인딩을 추가를 시작 합니다.

Views/Home/Index.cshtml 파일을 엽니다. 해당 파일의 전체 내용을 다음으로 대체 합니다.

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

대부분의 합니다 `div` 요소에 대 한 사항이 [부트스트랩](http://getbootstrap.com/) 스타일을 지정 합니다. 중요 한 요소는 사용 하 여 `data-bind` 특성입니다. 이 특성을 뷰 모델로 HTML을 연결합니다.

예를 들어:

[!code-html[Main](part-7/samples/sample2.html)]

이 예제에서는 합니다 &quot; `text` &quot; 원인 바인딩를 `<p>` 값을 표시 하는 요소는 `error` 뷰 모델에서 속성. 이전에 설명한 대로 `error` 로 선언 된 `ko.observable`:

[!code-javascript[Main](part-7/samples/sample3.js)]

새 값을 할당할 때마다 `error`, Knockout 텍스트를 업데이트 합니다 `<p>` 요소입니다.

합니다 `foreach` 바인딩 지시 Knockout의 내용을 반복 하는 `books` 배열입니다. Knockout 배열의 각 항목에 대해 새로 만들고 &lt;li&gt; 요소입니다. 컨텍스트 내에서 바인딩에 `foreach` 배열 항목의 속성을 참조 하세요. 예를 들어:

[!code-html[Main](part-7/samples/sample4.html)]

여기서는 `text` 바인딩 각 책의 저자 속성을 읽습니다.

이제 응용 프로그램을 실행 하는 경우 다음과 같아야 합니다.

![](part-7/_static/image1.png)

책의 목록이 페이지가 로드 된 후 비동기적으로 로드 합니다. 지금 바로 합니다 &quot;세부 정보&quot; 링크는 작동 하지 않습니다. 다음 섹션에서이 기능을 추가 하겠습니다.

> [!div class="step-by-step"]
> [이전](part-6.md)
> [다음](part-8.md)
