---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
title: 클라이언트 쪽 코드 (VB)를 사용 하 여 애니메이션 실행 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 애니메이션을 실행 하는 중...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: f7073f50-d765-456d-9957-926ce60f35f6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 9b180ad17e0e3d2dffa6262d10a83a8353e0a1d0
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37811888"
---
<a name="executing-animations-using-client-side-code-vb"></a>클라이언트 쪽 코드 (VB)를 사용 하 여 실행 중인 애니메이션
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)

> ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 애니메이션 실행 트리거될 수도 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 애니메이션 실행 트리거될 수도 있습니다.

## <a name="steps"></a>단계

첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample1.aspx)]

그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:

[!code-css[Main](executing-animations-using-client-side-code-vb/samples/sample3.css)]

그런 다음 추가 `AnimationExtender` 페이지에서 제공 하는 `ID`, `TargetControlID` 특성과 필수 항목 이지만 `runat="server"`:

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample4.aspx)]

내 합니다 `<Animations>` 노드를 사용 하 여 `<OnClick>` 애니메이션 사용자 한 번만 실행 패널에서 클릭 합니다. Parallelly 실행할 두 애니메이션을 추가 합니다.

[!code-xml[Main](executing-animations-using-client-side-code-vb/samples/sample5.xml)]

데모를 위해이 애니메이션 (컨트롤 도구 키트를 사용 하 여 만든 다른 애니메이션) 실행 되는 페이지가 실행 되 면 JavaScript 코드를 사용 하 여 합니다. 모든 것에 대 한 액세스는 `AnimationExtender` 제어 합니다. ASP.NET AJAX 라이브러리에서 제공 된 `$find()` 이 작업에 대 한 함수:

[!code-csharp[Main](executing-animations-using-client-side-code-vb/samples/sample6.cs)]

합니다 `AnimationExtender` 컨트롤의 XML 태그에 사용 되는 이벤트 처리기에 동일한 이름의 메서드를 포함 하 여 다양 한 API를 노출: `OnClick()`, `OnLoad()`등입니다. 예를 들어 호출을 `OnClick()` 메서드 내에서 애니메이션을 실행 합니다 `<OnClick>` 요소의 `AnimationExtender` 컨트롤:

[!code-javascript[Main](executing-animations-using-client-side-code-vb/samples/sample7.js)]

페이지가 완전히 로드 되 면 패널에서 클릭을 에뮬레이트하는 전체 클라이언트 쪽 JavaScript 코드를 확인 하는 다음과 같습니다는 `pageLoad()` 함수 이름 이라고 하는 ASP.NET AJAX에서 한 번의 페이지를 사용 하 되 고 모든 포함 된 라이브러리는 JavaScript 로드 합니다.

[!code-html[Main](executing-animations-using-client-side-code-vb/samples/sample8.html)]


[![이 애니메이션은 마우스 클릭 하지 않고 즉시 실행](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)

마우스 클릭 하지 않고 애니메이션은 즉시 실행 ([클릭 하 여 큰 이미지 보기](executing-animations-using-client-side-code-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](modifying-animations-from-the-server-side-vb.md)
> [다음](changing-an-animation-using-client-side-code-vb.md)
