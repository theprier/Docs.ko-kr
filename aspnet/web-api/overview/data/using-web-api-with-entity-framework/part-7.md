---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: Create View (UI) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: 5052d7cca4a5c12a9ea56eb929d4794b19e82603
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30878804"
---
<a name="create-the-view-ui"></a>Create View (UI)
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](https://github.com/MikeWasson/BookService)

이 섹션에서는 응용 프로그램에 대 한 HTML를 정의 하 고 HTML 및 보기 모델 간의 데이터 바인딩을 추가할 시작 합니다.

Views/Home/Index.cshtml 파일을 엽니다. 해당 파일의 전체 내용을 다음으로 바꿉니다.

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

대부분의 `div` 요소에 대 한 사항이 [부트스트랩](http://getbootstrap.com/) 스타일을 지정 합니다. 중요 한 요소가 동작은 `data-bind` 특성입니다. 이 특성의 보기 모델에 HTML을 연결합니다.

예를 들어:

[!code-html[Main](part-7/samples/sample2.html)]

이 예제는 &quot; `text` &quot; 원인을 바인딩는 `<p>` 의 값을 표시 하는 요소는 `error` 의 보기 모델에서 속성입니다. 이전에 설명한 대로 `error` 선언 되었습니다. 한 `ko.observable`:

[!code-javascript[Main](part-7/samples/sample3.js)]

에 새 값이 할당 될 때마다 `error`, Knockout 텍스트를 업데이트는 `<p>` 요소입니다.

`foreach` 바인딩 지시 Knockout의 내용을 반복 하는 `books` 배열입니다. 배열의 각 항목에 대 한 Knockout에서는 새 &lt;li&gt; 요소입니다. 바인딩 컨텍스트 내부의 `foreach` 배열 항목에서 속성을 참조 하십시오. 예를 들어:

[!code-html[Main](part-7/samples/sample4.html)]

여기에서 `text` 바인딩 각도 서의 작성자 속성을 읽습니다.

지금 응용 프로그램을 실행 하는 경우 다음과 같이 표시 됩니다.

![](part-7/_static/image1.png)

책 목록을 페이지가 로드 된 후 비동기적으로 로드 합니다. 지금 바로 &quot;세부 정보&quot; 링크는 작동 하지 않습니다. 다음 섹션에서이 기능을 추가 합니다.

> [!div class="step-by-step"]
> [이전](part-6.md)
> [다음](part-8.md)
