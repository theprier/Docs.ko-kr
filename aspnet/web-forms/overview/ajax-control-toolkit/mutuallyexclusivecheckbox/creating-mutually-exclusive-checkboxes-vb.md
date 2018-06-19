---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: 상호 배타적인 확인란 (VB) 만들기 | Microsoft Docs
author: wenz
description: '일련의 옵션 중 하나에만 선택할 수 있습니다, 라디오 단추는 일반적으로 사용 합니다. 그러나 한 가지 단점으로는: 그룹에 하나의 라디오 단추를 선택 하면...'
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: cdb93a080fb62cfdc7e3ff0604a1447e2bb99071
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30874254"
---
<a name="creating-mutually-exclusive-checkboxes-vb"></a>상호 배타적인 확인란 (VB) 만들기
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)

> 일련의 옵션 중 하나에만 선택할 수 있습니다, 라디오 단추는 일반적으로 사용 합니다. 그러나 한 가지 단점으로는: 모든 라디오 단추를 선택 취소 수 없는 그룹에 하나의 라디오 단추를 선택 합니다. 그러나 확인란은 언제 든 지 checked를 취소할 수, 배타적이 지 않습니다. 이 자습서에서는 두 방법 모두 환경의 제공: 함께 사용할 수 없는 확인란 합니다.


## <a name="overview"></a>개요

일련의 옵션 중 하나에만 선택할 수 있습니다, 라디오 단추는 일반적으로 사용 합니다. 그러나 한 가지 단점으로는: 모든 라디오 단추를 선택 취소 수 없는 그룹에 하나의 라디오 단추를 선택 합니다. 그러나 확인란은 언제 든 지 checked를 취소할 수, 배타적이 지 않습니다. 이 자습서에서는 두 방법 모두 환경의 제공: 함께 사용할 수 없는 확인란 합니다.

## <a name="steps"></a>단계

ASP.NET AJAX 컨트롤 Toolkit MutuallyExclusiveCheckBox extender를 포함합니다. 이렇게 하면 모든 확인란 그룹 이름에 할당 하는 프로그래머 (`Key` 특성). 모든 확인란 동일한 그룹 내의 하나에만 한 번에 선택할 수 있습니다.

새 ASP.NET 페이지에 배치 하는 확인란이 두 개부터 살펴보겠습니다. 더 될 수 있지만 그 중 두 요구 사항을 충족 하는 원칙을 보여 주기 위해:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

두 확인란이 모두 선택, MutuallyExclusiveCheckBoxExtender 컨트롤이 페이지에 배치 해야 합니다. 두 키 특성 값의 HTML 라디오 단추 요소가 특성을 자신이 속한 그룹을 나타내는 동일 해야 합니다. 값과 마찬가지로 해야 합니다. Extender의 targetcontrolid가 속성 확인란의 ID를 가리킵니다.

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

마지막으로, ASP.NET AJAX 포함 `ScriptManager` ASP.NET AJAX 컨트롤 도구 키트의 모든 요소에 필요한:

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

하지만 저장 하 고 페이지 실행: 확인 하 고 두 확인란의 선택을 취소 순식간에 확인란을 모두 체크 인할 수 있습니다.


[![한 번에 하나씩만 확인할 수 있습니다.](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)

한 번에 하나씩만 확인할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-mutually-exclusive-checkboxes-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](creating-mutually-exclusive-checkboxes-cs.md)
