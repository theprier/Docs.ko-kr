---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
title: 봇 (C#)에 대처 | Microsoft Docs
author: wenz
description: 자동화 된 봇 웹 로그 및 기타 웹 사이트 사용자 상호 작용 없이 주석 양식 전송 스팸 석고 합니다. ASP.NET AJAX Con에서 NoBot 컨트롤 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 0a1917e0-884a-4576-8e93-9ed660faae51
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
msc.type: authoredcontent
ms.openlocfilehash: 1ea3aaa5461c2f58a927ae975568f18a34a4729b
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872015"
---
<a name="fighting-bots-c"></a>대처 봇 (C#)
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)

> 자동화 된 봇 웹 로그 및 기타 웹 사이트 사용자 상호 작용 없이 주석 양식 전송 스팸 석고 합니다. ASP.NET AJAX 컨트롤 도구 키트에서 NoBot 컨트롤 이러한 봇 방지 하는 데 도움이 됩니다.


## <a name="overview"></a>개요

자동화 된 봇 웹 로그 및 기타 웹 사이트 사용자 상호 작용 없이 주석 양식 전송 스팸 석고 합니다. ASP.NET AJAX 컨트롤 도구 키트에서 NoBot 컨트롤 이러한 봇 방지 하는 데 도움이 됩니다.

## <a name="steps"></a>단계

봇을 무력화 하는 한 가지 일반적인 방법은 컴퓨터와 사용자 떨어져 CAPTCHAs 완전히 자동화 된 공용 Turing 테스트를 사용 하는 합니다. Turing 테스트 원래 테스트 누군가가 통신 파트너 사람 또는 컴퓨터를 지 여부를 결정 하는 데 필요 합니다. 웹에서 CAPTCHA에 왜곡된 일부 문자를 사용 하 여 이미지의 일반적으로 구성 됩니다. 사람이 이미지에 문자를 읽을 수 있도록 반면 OCR 알고리즘 실패 합니다.

몇 가지 장점 및 단점이이 방법에 있지만이 설명은이 자습서의 범위를 벗어납니다. 그러나 유사한 방법을 제공 하는 ASP.NET AJAX 컨트롤 도구 키트에서 컨트롤: `NoBot`합니다. 대부분 스팸 시도 하는 경우 성공 간주 됩니다. 여기서 블로그 같은 웹 사이트에서 매우 잘 fares, 되며에 보다 CAPTCHA를 극복 하기 쉽게 알고리즘은 매우 쉽게 사용할 수 있지만는 `NoBot` 제어 작업을 수행할 수 있습니다.

`NoBot` 이러한 조건 중 하나 이상을 충족 될 경우에 현재 ASP.NET web form의 포스트백을 가로채:

- JavaScript 퍼즐을 해결 하기 위해 브라우저 실패 (예를 들어 JavaScript가 비활성화 된 경우)
- 사용자를 빠른 양식을 제출
- 특정 기간에 너무 자주 양식을 제출 하는 클라이언트 IP 주소입니다.

이러한 조건을 확인 하기 위해는 `NoBot` 컨트롤 (모든 옵션) 이러한 특성을 사용 하려면:

- `ResponseMinimumDelaySeconds` 최소한의 포스트백 간격 (초)
- `CutoffWindowSeconds` 하나의 IP에서 포스트백 측정값 되는 시간 간격의 길이
- `CutoffMaximumInstances` 시간 간격 (초)의 최대 크기

다음 태그 요구 2 초 해당 이상 게시 하는 동안 경과 5 개만 포스트백 있는지 이하의 30 초 간격 내에서:

[!code-aspx[Main](fighting-bots-cs/samples/sample1.aspx)]

다음 평소와 같이 포함 되었는지 확인는 `ScriptManager` 페이지에 있도록 ASP.NET AJAX 라이브러리를 로드 하 고 제어 도구 키트를 사용할 수 있습니다.

[!code-aspx[Main](fighting-bots-cs/samples/sample2.aspx)]

대부분의 검사 이후 `NoBot` 수행 하는 작업 서버 쪽에서 발생이 유효성 검사의 결과 확인 해야 합니다. 호출 하 여이 작업을 수행할 수 있습니다 `NoBot`의 `IsValid()` 메서드. 하나의 인수를 포함 (으로 `out` 매개 변수 /`ByRef` 매개 변수)가 형식의 `NoBotState`합니다. 문자열 표현 검사가 실패 한 경우 이유를 포함 하 고 `Valid` 그렇지 않은 경우. 다음 코드에 따라 메시지를 출력 `NoBot`의 발생:

[!code-aspx[Main](fighting-bots-cs/samples/sample3.aspx)]

마지막으로 폼을 제출 해야 label 요소는 메시지를 출력 하 고 작업이 완료 되!

[!code-aspx[Main](fighting-bots-cs/samples/sample4.aspx)]

이 스크립트를 실행 하 고 JavaScript 비활성화 처음 2 초 안에 폼을 제출 하거나 7 번 30 초 내에서는 양식을 제출, 오류 메시지가 얻게 됩니다. 그러나이 컨트롤을 현명 하 게 사용를 사용자의 약 90 95% 활성화 하는 JavaScript에 한 사용자의 5-10% 되지 것입니다 `NoBot`의 테스트 합니다.


[![이 오류 메시지는 bot 인해 발생 수 있습니다.](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)

이 오류 메시지는 bot 인해 발생 수 ([전체 크기 이미지를 보려면 클릭](fighting-bots-cs/_static/image3.png))

> [!div class="step-by-step"]
> [다음](fighting-bots-vb.md)
