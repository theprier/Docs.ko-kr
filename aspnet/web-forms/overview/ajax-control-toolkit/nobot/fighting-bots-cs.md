---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
title: 대체 봇 (C#) | Microsoft Docs
author: wenz
description: 자동화 된 봇 스팸, 사용자 개입 없이 주석 양식을 제출를 사용 하 여 웹 로그 및 기타 웹 사이트를 석고 합니다. ASP.NET AJAX Con NoBot 컨트롤 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0a1917e0-884a-4576-8e93-9ed660faae51
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
msc.type: authoredcontent
ms.openlocfilehash: 52ed34e7640cd125a3b4c3b50ab760a7c1d713f1
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829112"
---
<a name="fighting-bots-c"></a>대체 봇 (C#)
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)

> 자동화 된 봇 스팸, 사용자 개입 없이 주석 양식을 제출를 사용 하 여 웹 로그 및 기타 웹 사이트를 석고 합니다. ASP.NET AJAX Control Toolkit에서 NoBot 컨트롤 이러한 봇 싸 하는 데 도움이 됩니다.


## <a name="overview"></a>개요

자동화 된 봇 스팸, 사용자 개입 없이 주석 양식을 제출를 사용 하 여 웹 로그 및 기타 웹 사이트를 석고 합니다. ASP.NET AJAX Control Toolkit에서 NoBot 컨트롤 이러한 봇 싸 하는 데 도움이 됩니다.

## <a name="steps"></a>단계

봇을 무력화 하는 데 한 가지 일반적인 방법은 컴퓨터와 사용자 떨어져 CAPTCHAs 완전히 자동화 된 공용 Turing 테스트를 사용 하는 것입니다. Turing 테스트 원래 테스트 사람 또는 컴퓨터 통신 파트너 인지 여부를 결정 해야 사용자가 있습니다. 웹에서 CAPTCHA를 왜곡 되어 일부 문자를 사용 하 여 이미지의 일반적으로 구성 됩니다. OCR 알고리즘 실패 하는 반면 것만 사람이 이미지의 문자를 읽을 수 있도록입니다.

몇 가지 장점과이 방식의 단점은 있지만이 설명은이 자습서의 범위를 벗어납니다. 그러나 유사한 접근 방식을 제공 하는 ASP.NET AJAX Control Toolkit의 컨트롤: `NoBot`합니다. 대부분 스팸 시도 하는 경우 성공적인 간주 됩니다. 여기서 블로그 같은 웹 사이트에서 매우 잘 경우 약 48gb), 되며에 극복 CAPTCHA를 보다 쉽게 하지만 매우 쉽게 사용할 수는는 `NoBot` 제어 작업을 수행할 수 있습니다.

`NoBot` 이러한 조건 중 하나 이상이 충족 되 면 현재 ASP.NET web form의 포스트백을 가로채:

- 브라우저 JavaScript 퍼즐 실패 (예를 들어 경우 JavaScript가 비활성화)
- 사용자를 빠르게 양식을 제출
- 특정 시간 내에 너무 자주 양식을 제출 하는 클라이언트 IP 주소입니다.

이러한 조건을 확인 하기 위해는 `NoBot` 컨트롤 (모든 선택 사항) 이러한 특성이 필요 합니다.

- `ResponseMinimumDelaySeconds` 최소한의 포스트백 간격 (초)
- `CutoffWindowSeconds` 하나의 IP에서 포스트백에 측정 하는 시간 간격의 길이
- `CutoffMaximumInstances` 최대 시간 간격 (초)

다음 태그 요구는 적어도 2 초 포스트백 간에 경과 하 고 5 개만 포스트백을 가지는 작거나 30 초 간격 내에서:

[!code-aspx[Main](fighting-bots-cs/samples/sample1.aspx)]

다음 일반적인 방식으로 포함 해야 합니다 `ScriptManager` 페이지에서 ASP.NET AJAX library가 로드 하 고 컨트롤 도구 키트를 사용할 수 있도록 합니다.

[!code-aspx[Main](fighting-bots-cs/samples/sample2.aspx)]

대부분의 검사 이후 `NoBot` 수행 하는 서버 쪽에서 발생이 유효성 검사의 결과 확인 해야 합니다. 호출 하 여 이렇게 `NoBot`의 `IsValid()` 메서드. 에 인수가 하나 (으로 `out` 매개 변수 /`ByRef` 매개 변수)가 형식의 `NoBotState`합니다. 확인이 실패 하는 경우 해당 문자열 표현 이유를 포함 하 고 `Valid` 그렇지 않은 경우. 다음 코드에 따라 메시지를 출력 `NoBot`의 결과:

[!code-aspx[Main](fighting-bots-cs/samples/sample3.aspx)]

마지막으로 전송할 폼 및 레이블 요소를 메시지를 출력 해야 하 고 완료!

[!code-aspx[Main](fighting-bots-cs/samples/sample4.aspx)]

이 스크립트를 실행 및 JavaScript를 비활성화 또는 처음 2 초 안에 양식을 제출 하거나 30 초 내에 7 번 양식을 제출, 오류 메시지가 표시 됩니다. 그러나이 컨트롤을 현명 하 게 사용, 사용자의 약 90 95% 활성화 하는 JavaScript가 사용자의 5 ~ 10% 실패는 `NoBot`의 테스트 합니다.


[![이 오류 메시지는 봇 인해 발생할 수 있습니다.](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)

이 오류 메시지는 봇 인해 발생할 수 있습니다 ([클릭 하 여 큰 이미지 보기](fighting-bots-cs/_static/image3.png))

> [!div class="step-by-step"]
> [다음](fighting-bots-vb.md)
