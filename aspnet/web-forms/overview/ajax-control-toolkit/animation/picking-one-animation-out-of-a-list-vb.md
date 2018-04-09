---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
title: 선택 목록 (VB)에서 애니메이션 | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 프레임 워크 또한 허용...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 81ba9116-d485-40c0-8ff6-7e9ae23e0a0c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-vb
msc.type: authoredcontent
ms.openlocfilehash: f2bd1b3cc72595da7e8901786ea8415d7c1c524a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="picking-one-animation-out-of-a-list-vb"></a>선택 목록 (VB)에서 애니메이션
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 프레임 워크는 애니메이션 계산 일부 JavaScript 코드에 따라 목록에서 애니메이션을 선택 하는 프로그래머를 수도 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 프레임 워크는 애니메이션 계산 일부 JavaScript 코드에 따라 목록에서 애니메이션을 선택 하는 프로그래머를 수도 있습니다.

## <a name="steps"></a>단계

우선, 포함 된 `ScriptManager` 페이지; 그런 다음 ASP.NET AJAX 라이브러리 로드 되는 제어 도구 키트를 사용 하 여:

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample1.aspx)]

그러면 다음과 같은 텍스트의 패널에 애니메이션 적용 됩니다.

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스 좋은 배경색을 정의 하 고도 패널 고정된 폭을 설정 합니다.

[!code-css[Main](picking-one-animation-out-of-a-list-vb/samples/sample3.css)]

그런 다음 추가 `AnimationExtender` 페이지에 제공 하는 `ID`, `TargetControlID` 특성과 참가 `runat="server":`

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample4.aspx)]

내에서 `<Animations>` 노드를 사용 하 여 `<OnLoad>` 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다. 대신 일반 애니메이션 중 하나는 `<Case>` 요소에 발생 합니다. 해당 SelectScript 특성의 값이 계산 됩니다. 반환 값은 숫자 여야 합니다. 내에서 하위 애니메이션 중 하나는이 수에 따라 &lt;대/소문자&gt; 실행 됩니다. 예를 들어, SelectScript 2로 계산 되 면 컨트롤 도구 키트 내에서 세 번째 애니메이션 실행 &lt;대/소문자&gt; (개 0부터 시작)입니다.

태그를 다음 세 하위 애니메이션을 정의: 너비를 크기 조정, 높이 조정 하 고, 페이딩 합니다. JavaScript 코드 (`Math.floor(3 * Math.random())`) 다음 세 애니메이션 중 하나를 실행할 수 있도록 0, 2 사이의 숫자를 선택 합니다.

[!code-aspx[Main](picking-one-animation-out-of-a-list-vb/samples/sample5.aspx)]


[![가능한 세 가지 애니메이션 중 하나: 패널의 넓은 가져옵니다.](picking-one-animation-out-of-a-list-vb/_static/image2.png)](picking-one-animation-out-of-a-list-vb/_static/image1.png)

가능한 세 가지 애니메이션 중 하나: 패널의 넓은 가져옵니다 ([전체 크기 이미지를 보려면 클릭](picking-one-animation-out-of-a-list-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](animation-depending-on-a-condition-vb.md)
> [다음](animating-in-response-to-user-interaction-vb.md)
