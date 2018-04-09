---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
title: 클라이언트 쪽 코드 (VB)를 사용 하 여 애니메이션 실행 | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션 실행 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: f7073f50-d765-456d-9957-926ce60f35f6
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: e2b8c499edaccc70d439a576feb80e91cb28c1c7
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="executing-animations-using-client-side-code-vb"></a>클라이언트 쪽 코드 (VB)를 사용 하 여 실행 중인 애니메이션
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션 실행 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 트리거될 수 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션 실행 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 트리거될 수 있습니다.

## <a name="steps"></a>단계

우선, 포함 된 `ScriptManager` 페이지; 그런 다음 ASP.NET AJAX 라이브러리 로드 되는 제어 도구 키트를 사용 하 여:

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample1.aspx)]

그러면 다음과 같은 텍스트의 패널에 애니메이션 적용 됩니다.

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스 좋은 배경색을 정의 하 고도 패널 고정된 폭을 설정 합니다.

[!code-css[Main](executing-animations-using-client-side-code-vb/samples/sample3.css)]

그런 다음 추가 `AnimationExtender` 페이지에 제공 하는 `ID`, `TargetControlID` 특성과 반드시 `runat="server"`:

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample4.aspx)]

내에서 `<Animations>` 노드를 사용 하 여 `<OnClick>` 패널에 사용자 애니메이션을 한 번 실행 하려면를 클릭 합니다. Parallelly 실행할 두 개의 애니메이션이 추가 합니다.

[!code-xml[Main](executing-animations-using-client-side-code-vb/samples/sample5.xml)]

으로이 애니메이션 (및 제어 도구 키트를 사용 하 여 만든 다른 애니메이션) 실행 되는 페이지 실행 되 면 JavaScript 코드를 사용 하 여 합니다. 모든 것에 대 한 액세스는 `AnimationExtender` 제어 합니다. ASP.NET AJAX 라이브러리에서 제공 된 `$find()` 이 작업에 대 한 함수:

[!code-csharp[Main](executing-animations-using-client-side-code-vb/samples/sample6.cs)]

`AnimationExtender` 제어와 이름이 같은 XML 태그에서 사용 하는 이벤트 처리기 메서드를 포함 하 여 다양 한 API를 노출: `OnClick()`, `OnLoad()`등입니다. 예를 들어, 호출은 `OnClick()` 메서드가 실행 내에서 애니메이션은 `<OnClick>` 의 요소는 `AnimationExtender` 컨트롤:

[!code-javascript[Main](executing-animations-using-client-side-code-vb/samples/sample7.js)]

페이지가 완전히 로드 되 면 패널 클릭을 에뮬레이션 하는 전체 클라이언트 쪽 JavaScript 코드를 확인 하는 다음과 같습니다는 `pageLoad()`에 의해 호출 되는 ASP.NET AJAX 한 번 페이지 함수 이름을 사용 하 고 모든 포함 된 라이브러리는 JavaScript 로드 합니다.

[!code-html[Main](executing-animations-using-client-side-code-vb/samples/sample8.html)]


[![애니메이션은 마우스 클릭 하지 않고 즉시 실행](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)

마우스 클릭 하지 않고 애니메이션 즉시 실행 ([전체 크기 이미지를 보려면 클릭](executing-animations-using-client-side-code-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](modifying-animations-from-the-server-side-vb.md)
> [다음](changing-an-animation-using-client-side-code-vb.md)
