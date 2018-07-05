---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: 상호 배타적인 확인란 (VB) 만들기 | Microsoft Docs
author: wenz
description: '일련의 옵션 중 하나만 선택할 수 있습니다, 라디오 단추는 일반적으로 사용 합니다. 그러나 단점은는: 그룹에 하나의 라디오 단추를 선택 하면...'
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: 6badd005ed4775cb248784f3e9991132db1b3969
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37828801"
---
<a name="creating-mutually-exclusive-checkboxes-vb"></a>상호 배타적인 확인란 만들기 (VB)
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)

> 일련의 옵션 중 하나만 선택할 수 있습니다, 라디오 단추는 일반적으로 사용 합니다. 그러나 단점은는: 그룹에 하나의 라디오 단추를 선택 하면 수 없으면 모든 라디오 단추를 선택 취소 합니다. 그러나 확인란 선택 취소할 수 있습니다 언제 든 지, 배타적이 지 않습니다. 이 자습서에는 두 가지 장점을 제공 합니다: 상호 배타적인 확인란 합니다.


## <a name="overview"></a>개요

일련의 옵션 중 하나만 선택할 수 있습니다, 라디오 단추는 일반적으로 사용 합니다. 그러나 단점은는: 그룹에 하나의 라디오 단추를 선택 하면 수 없으면 모든 라디오 단추를 선택 취소 합니다. 그러나 확인란 선택 취소할 수 있습니다 언제 든 지, 배타적이 지 않습니다. 이 자습서에는 두 가지 장점을 제공 합니다: 상호 배타적인 확인란 합니다.

## <a name="steps"></a>단계

ASP.NET AJAX Control Toolkit MutuallyExclusiveCheckBox extender를 포함합니다. 이렇게 하면 프로그래머가 모든 확인란 그룹 이름에 할당할 수 있습니다. (`Key` 특성). 동일한 그룹 내 모든 확인 상자에서 하나만 한 번에 선택할 수 있습니다.

새 ASP.NET 페이지에 확인란이 두 개를 배치로 시작 하겠습니다. 더 많은 될 수 있지만 그 중 두 가지 원칙을 보여 주기 위해 충분 합니다.

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

두 확인란에 대 한 페이지의 MutuallyExclusiveCheckBoxExtender 컨트롤을 배치 해야 합니다. 두 키 특성은 HTML 라디오 단추 요소의 특성은 자신이 속한 그룹을 나타내는 동일 해야 합니다. 값 처럼 동일한 값을 해야 합니다. Extender의 TargetControlID 속성 확인란의 ID를 가리킵니다.

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

마지막으로, ASP.NET AJAX를 포함 `ScriptManager` ASP.NET AJAX Control Toolkit의 모든 요소에서 필요한:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

하지만 저장 하 고 페이지를 실행 합니다: 확인을 모두 확인란의 선택을 취소 순식간에 확인란을 모두 확인할 수 있습니다.


[![한 번에 하나씩만 확인할 수 있습니다.](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)

한 번에 하나씩만 확인할 수 있습니다 ([클릭 하 여 큰 이미지 보기](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](creating-mutually-exclusive-checkboxes-cs.md)
