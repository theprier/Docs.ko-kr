---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
title: 등급 컨트롤 (VB) 만들기 | Microsoft Docs
author: wenz
description: 전자 상거래 커뮤니티 사이트에서 여러 웹 사이트 비율 문서 또는 항목을 사용자에 게 제공합니다. 이 일반적으로 몇 가지 코딩 작업이 필요 하지만 사항은 합니다...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6d0d70f4-725e-4258-8ae8-24a6ba1ddbf7
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
msc.type: authoredcontent
ms.openlocfilehash: b229d0155fbab0437c644b41424164e4c655f5e5
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41823804"
---
<a name="creating-a-rating-control-vb"></a>등급 컨트롤 (VB) 만들기
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0VB.pdf)

> 전자 상거래 커뮤니티 사이트에서 여러 웹 사이트 비율 문서 또는 항목을 사용자에 게 제공합니다. 이 일반적으로 몇 가지 코딩 작업이 필요 하지만 Control Toolkit 목표인 필요가 합니다.


## <a name="overview"></a>개요

전자 상거래 커뮤니티 사이트에서 여러 웹 사이트 비율 문서 또는 항목을 사용자에 게 제공합니다. 이 일반적으로 몇 가지 코딩 작업이 필요 하지만 Control Toolkit 목표인 필요가 합니다.

## <a name="steps"></a>단계

먼저, (적어도) 두 종류의 이미지 해야: 채워진 프로그램용 등급 항목 및 빈 등급 항목에 대 한 합니다. 등급 항목은 일반적으로 별 또는 웃는 얼굴을 합니다. 이 시나리오에서는 찾아야 세 파일, smiley.png empty.png 및 웃는 done.png이이 자습서에 대 한 소스 코드 다운로드의 일부로.

그런 다음 새 ASP.NET 파일을 만들고 추가 시작을 `ScriptManager` 컨트롤을 합니다.

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample1.aspx)]

그런 다음 추가 `Rating` ASP.NET AJAX Control Toolkit에서 제어 합니다. 다음 특성을이 예제에 대해 설정 해야 합니다.

- `CurrentRating` 사용할 초기 등급
- `MaxRating` 최대 등급
- `EmptyStarCssClass` 등급 항목이 (별표)를 사용 하는 CSS 클래스 비어 있습니다.
- `FilledStarCssClass` 등급 항목이 (별표)를 사용 하는 CSS 클래스 작성
- `StarCssClass` 표시 상태에 사용할 CSS 클래스
- `WaitingStarCssClass` 별 등급을 서버에 다시 보내는 동안 사용 하는 CSS 클래스

다음은 등급 컨트롤 5를 사용 하 여 만드는 태그는 none 작성 처음에 항목 (smileys):

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample2.aspx)]

세 개의 참조 된 CSS 클래스 이제 필요 적절 한 이미지 파일을 표시 하려면 CSS를 사용 하 여 작업을 수행 하는 간단 합니다.

[!code-css[Main](creating-a-rating-control-vb/samples/sample3.css)]

수 있도록 세 개의 이미지의 높이 너비를 제공한 그렇지 않은 경우 표시를 잠시 messed 보일 수 있습니다.

마지막으로, 등급의 결과 해야 될 사용자에 게 표시 (또는 최소한 데이터베이스에 저장). 따라서 등급 폼을 서버에 다시 게시 하는 텍스트 메시지 및 전송 단추가의 출력에 대 한 레이블을 추가 합니다.

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample4.aspx)]

서버 쪽 코드를 통해 등급 컨트롤에 액세스할 해당 `ID` 액세스 하면 해당 `CurrentRating` 예제 값을 0에서 5 사이의 등급 선택한 항목을 숫자 속성입니다.

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample5.aspx)]

페이지를 저장 하 고 브라우저에 로드 합니다. JavaScript 효과 발생 (처음에 비어 있음) 등급 항목 위로 마우스를 가져가면: 등급 변경 합니다. 별 집합이 클릭 하면 현재 등급 유지 됩니다. 마지막으로 폼을 전송 하면 서버 쪽 코드를 선택한 등급을 출력 합니다.


[![최소한의 코드를 사용 하 여 등급 시스템 만들기](creating-a-rating-control-vb/_static/image2.png)](creating-a-rating-control-vb/_static/image1.png)

최소한의 코드를 사용 하 여 등급 시스템 만들기 ([클릭 하 여 큰 이미지 보기](creating-a-rating-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](creating-a-rating-control-cs.md)
