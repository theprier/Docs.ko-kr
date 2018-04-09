---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
title: 등급 컨트롤 (VB) 만들기 | Microsoft Docs
author: wenz
description: 전자 상거래 커뮤니티 사이트로에서 대부분의 웹 사이트 속도 문서 또는 항목에 사용자에 게 제공할 합니다. 이 일반적으로 일부 코딩 작업 필요 하지만 대 한는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 6d0d70f4-725e-4258-8ae8-24a6ba1ddbf7
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
msc.type: authoredcontent
ms.openlocfilehash: c19f36dfe1b72a3954db61ff1845e99c02e47c14
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="creating-a-rating-control-vb"></a>등급 컨트롤 (VB) 만들기
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0VB.pdf)

> 전자 상거래 커뮤니티 사이트로에서 대부분의 웹 사이트 속도 문서 또는 항목에 사용자에 게 제공할 합니다. 이 일반적으로 일부 코딩 작업 필요 했지만 우리의 받고 제어 도구 키트가 않습니다.


## <a name="overview"></a>개요

전자 상거래 커뮤니티 사이트로에서 대부분의 웹 사이트 속도 문서 또는 항목에 사용자에 게 제공할 합니다. 이 일반적으로 일부 코딩 작업 필요 했지만 우리의 받고 제어 도구 키트가 않습니다.

## <a name="steps"></a>단계

(이상)의 두 종류의 이미지를 필요한 우선,: 채워진는 대 한 등급 항목 및 빈 등급 항목에 대 한 합니다. 등급 항목은 일반적으로 별모양 또는 웃는 합니다. 이 시나리오에 대 한이 자습서에 대 한 소스 코드 다운로드의 일부로 세 개의 파일, smiley.png empty.png 및 웃는 done.png를 찾을 있습니다.

그런 다음 새 ASP.NET 파일을 만들고 추가 작업부터 시작는 `ScriptManager` 를 제어 합니다.

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample1.aspx)]

그런 다음 추가 `Rating` ASP.NET AJAX 컨트롤 도구 키트에서 제어 합니다. 이 예제에 대 한 설정 해야 하는 다음 특성:

- `CurrentRating` 사용할 초기 등급
- `MaxRating` 최대 등급
- `EmptyStarCssClass` 등급 항목 (별) 비어 있을 때 사용 하는 CSS 클래스
- `FilledStarCssClass` 등급 항목 (별)을 채울 때 사용 하는 CSS 클래스
- `StarCssClass` 표시 상태에 대 한 사용 하는 CSS 클래스
- `WaitingStarCssClass` 별 등급 서버에 다시 보내는 동안 사용 하는 CSS 클래스

태그를 5 개 등급 컨트롤을 만드는 것는 none 입력 처음 항목 (smileys):

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample2.aspx)]

세 개의 참조 된 CSS 클래스 이제 해야 할 적절 한 이미지 파일 보기 CSS를 사용 하 여 작업을 수행 하는 하기가 쉽습니다.

[!code-css[Main](creating-a-rating-control-vb/samples/sample3.css)]

세 개의 이미지의 높이 너비를 제공, 그렇지 않으면 디스플레이를 약간 messed 표시 될 수 있는지 확인 합니다.

마지막으로, 등급의 결과 해야 될 사용자에 게 표시 (또는 이상 데이터베이스에 저장) 합니다. 따라서 등급 폼을 서버에 다시 게시 하는 문자 메시지 및 전송 단추가의 출력에 대 한 레이블을 추가 합니다.

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample4.aspx)]

서버 쪽 코드를 통해 등급 컨트롤에 액세스 해당 `ID` 다음 액세스 해당 `CurrentRating` 선택한 등급 항목 예에서 0에서 5 사이의 값 수에 해당 하는 속성이 있습니다.

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample5.aspx)]

페이지를 저장 하 고 브라우저에 로드 합니다. JavaScript 효과 발생 (처음 비어 있음) 등급 항목 위로 마우스를 가져가면: 등급 변경 합니다. 별점 집합을 클릭할 때 현재 등급 유지 됩니다. 마지막으로, 양식을 전송 하면 서버 쪽 코드는 선택한 등급이 출력 됩니다.


[![최소한의 코드를 사용 하 여 등급 시스템 만들기](creating-a-rating-control-vb/_static/image2.png)](creating-a-rating-control-vb/_static/image1.png)

최소한의 코드를 사용 하 여 등급 시스템 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-rating-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](creating-a-rating-control-cs.md)
