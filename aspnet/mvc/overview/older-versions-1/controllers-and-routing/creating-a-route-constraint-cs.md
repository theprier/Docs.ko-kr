---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: "경로 제약 조건 (C#) 만들기 | Microsoft Docs"
author: StephenWalther
description: "이 자습서에서는 Stephen Walther 브라우저 정규식과 경로 제약 조건을 만들어 일치 경로 요청 하는 방법을 제어 하는 방법을 보여 줍니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/16/2009
ms.topic: article
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: ee83a134dcbdd1abfb296f3126a64c7d4ebab7f5
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="creating-a-route-constraint-c"></a>경로 제약 조건 (C#) 만들기
====================
으로 [Stephen Walther](https://github.com/StephenWalther)

> 이 자습서에서는 Stephen Walther 브라우저 정규식과 경로 제약 조건을 만들어 일치 경로 요청 하는 방법을 제어 하는 방법을 보여 줍니다.


경로 제약 조건을 사용 하 여 특정 경로 일치 하는 브라우저 요청을 제한 합니다. 경로 제약 조건을 지정 하는 정규식을 사용할 수 있습니다.

예를 들어 있는지 정의한 경로 목록 1의 Global.asax 파일에 한다고 가정 합니다.

**1-Global.asax.cs 나열**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

목록 1 제품을 라는 경로 포함 합니다. 브라우저 요청 목록 2에 포함 된 ProductController에 매핑할 제품 경로 사용할 수 있습니다.

**2-Controllers\ProductController.cs 나열**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

제품 컨트롤러에 의해 노출 Details() 작업을 허용 하도록 productId 라는 단일 매개 변수를 확인 합니다. 이 매개 변수는 정수 매개 변수입니다.

목록 1에 정의 된 경로 다음 Url 중 하 나와 일치 합니다.

- / 제품/23
- / 제품/7

안타깝게도, 경로 다음 Url 일치 합니다.

- / 제품/핵심 성과 지표
- / 제품/apple

Details() 작업에서 정수 매개 변수를 기대 하기 때문에 정수 값 이외의 값을 포함 하는 요청을 만드는 오류가 발생 합니다. 예를 들어 URL /Product/apple 브라우저에 입력 하는 경우 다음 받아볼 수 오류 페이지에는 그림 1에 있습니다.


[![새 프로젝트 대화 상자](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)

**그림 01**: 분해 페이지가 표시 ([전체 크기 이미지를 보려면 클릭](creating-a-route-constraint-cs/_static/image2.png))


실제로 필요한 것 작업을 수행 하는 적절 한 정수 productId를 포함 하는 Url만 일치 합니다. 경로 일치 하는 Url을 제한 하는 제약 조건 경로 정의 하는 경우 사용할 수 있습니다. 목록 3에서 수정 된 제품 경로 정수에만 일치 하는 정규식 제약 조건을 포함 합니다.

**3-Global.asax.cs 나열**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

정규식 \d+ 하나 이상의 정수 일치합니다. 이 제한 사항으로 인해 다음 Url을 일치 시킬 제품 경로의:

- / 제품/3
- / 제품/8999

하지만 다음 Url에 없습니다.

- / 제품/apple
- / 제품

- 다른 경로에서 이러한 브라우저 요청을 처리 되는 일치 하는 경로가 없는 경우 또는 *리소스를 찾을 수* 오류가 반환 됩니다.

>[!div class="step-by-step"]
[이전](creating-custom-routes-cs.md)
[다음](creating-a-custom-route-constraint-cs.md)
