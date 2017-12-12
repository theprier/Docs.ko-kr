---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: "항목 세부 정보를 표시 합니다. | Microsoft Docs"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 0b6ae9384843712cae824ea662b984a40f021e57
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="display-item-details"></a>항목 세부 정보를 표시
====================
으로 [Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트를 다운로드 합니다.](https://github.com/MikeWasson/BookService)

이 섹션에서는 각 책에 대 한 세부 정보를 볼 수 있는 기능을 추가 합니다. App.js의 보기 모델에 다음 코드를 추가 합니다.

[!code-javascript[Main](part-8/samples/sample1.js)]

Views/Home/Index.cshtml에서 세부 정보 링크에는 데이터를 바인딩 요소를 추가 합니다.

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

이 대 한 클릭 처리기를 바인딩하는 &lt;는&gt; 요소를는 `getBookDetail` 의 보기 모델에 대해 함수입니다.

동일한 파일에서 다음과 같은 마크업을 바꿉니다.

[!code-html[Main](part-8/samples/sample3.html)]

다음 코드로 바꿉니다.

[!code-html[Main](part-8/samples/sample4.html)]

이 태그의 속성에 데이터 바인딩된 하는 테이블을 만듭니다는 `detail` 보기 모델에 예측 가능한 합니다.

"&lt;!-ko-&gt; &quot; 구문을 사용 하면 DOM 요소의 외부 Knockout 바인딩을 포함할 수 있습니다. 이 경우에 `if` 바인딩 표시 되는 태그의이 섹션에서는 경우에만 `details` null입니다.

[!code-html[Main](part-8/samples/sample5.html)]

응용 프로그램을 실행 중 하나를 클릭 하는 경우 이제는 &quot;세부&quot; 링크, 응용 프로그램에는 책 세부 정보가 표시 됩니다.

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

>[!div class="step-by-step"]
[이전](part-7.md)
[다음](part-9.md)
