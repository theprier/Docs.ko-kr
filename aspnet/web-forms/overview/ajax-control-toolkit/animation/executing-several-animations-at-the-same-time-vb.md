---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
title: (VB) 동시에 여러 개의 애니메이션 실행 | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 떨어져서를 실행할 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 2469f7ea-1489-42fb-a8e1-414c90141ce9
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-vb
msc.type: authoredcontent
ms.openlocfilehash: 823764abd4444b5cb8d9bc6e8e8ed34d6f670310
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879441"
---
<a name="executing-several-animations-at-the-same-time-vb"></a>여러 개의 애니메이션 (VB) 동시에 실행
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 여러 개의 애니메이션 동시에서 실행 수 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 여러 개의 애니메이션 동시에서 실행 수 있습니다.

## <a name="steps"></a>단계

우선, 포함 된 `ScriptManager` 페이지; 그런 다음 ASP.NET AJAX 라이브러리 로드 되는 제어 도구 키트를 사용 하 여:

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample1.aspx)]

그러면 다음과 같은 텍스트의 패널에 애니메이션 적용 됩니다.

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스 좋은 배경색을 정의 하 고도 패널 고정된 폭을 설정 합니다.

[!code-css[Main](executing-several-animations-at-the-same-time-vb/samples/sample3.css)]

그런 다음 추가 `AnimationExtender` 페이지에 제공 하는 `ID`, `TargetControlID` 특성과 반드시 `runat="server"`:

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample4.aspx)]

내에서 `<Animations>` 노드를 사용 하 여 `<OnLoad>` 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다. 일반적으로 `<OnLoad>` 애니메이션만 허용 합니다. 애니메이션 프레임 워크를 수행 하 여에 여러 개의 애니메이션을 조인할 수는 `<Parallel>` 요소입니다. 내에서 모든 애니메이션이 `<Parallel>` 동시에 실행 됩니다.

다음은에 대 한 가능한 태그는 `AnimationExtender` 제어, 페이딩 및 동시에 패널 크기 조정:

[!code-aspx[Main](executing-several-animations-at-the-same-time-vb/samples/sample5.aspx)]

실제로 및: 패널 표시 되 면 조정이 스크립트를 실행 하는 경우 (threefolding 보다 더 많은 너비 및 halfing 높이가) 동시에 페이드 아웃 및 합니다.


[![패널은 페이드 하 고 (브라우저의 렌더링 엔진 덕분에 해당 콘텐츠 포함) 크기 조정](executing-several-animations-at-the-same-time-vb/_static/image2.png)](executing-several-animations-at-the-same-time-vb/_static/image1.png)

패널은 페이드 하 고 (브라우저의 렌더링 엔진 덕분에 해당 콘텐츠 포함) 크기 조정 ([전체 크기 이미지를 보려면 클릭](executing-several-animations-at-the-same-time-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](adding-animation-to-a-control-vb.md)
> [다음](executing-several-animations-after-each-other-vb.md)
