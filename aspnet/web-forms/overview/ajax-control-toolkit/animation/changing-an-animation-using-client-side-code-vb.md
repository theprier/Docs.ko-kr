---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
title: 클라이언트 쪽 코드 (VB)를 사용 하 여 애니메이션 변경 | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 애니메이션을 선택 하십시오.
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: a7fe5de5-a964-4780-ae5e-70821dfb50a0
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 7f9b72576cc3a9e91827cfb40983821704621060
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30879155"
---
<a name="changing-an-animation-using-client-side-code-vb"></a>클라이언트 쪽 코드 (VB)를 사용 하 여 애니메이션을 변경 합니다.
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 애니메이션을 변경할 수도 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트에서 애니메이션 컨트롤은 컨트롤 뿐 아니라 애니메이션 컨트롤을 추가 하는 전체 프레임 워크. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 애니메이션을 변경할 수도 있습니다.

## <a name="steps"></a>단계

우선, 포함 된 `ScriptManager` 페이지; 그런 다음 ASP.NET AJAX 라이브러리 로드 되는 제어 도구 키트를 사용 하 여:

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample1.aspx)]

그러면 다음과 같은 텍스트의 패널에 애니메이션 적용 됩니다.

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스 좋은 배경색을 정의 하 고도 패널 고정된 폭을 설정 합니다.

[!code-css[Main](changing-an-animation-using-client-side-code-vb/samples/sample3.css)]

실제 애니메이션은 HTML 단추를 통해 시작 됩니다.

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample4.aspx)]

그런 다음 추가 `AnimationExtender` 페이지에 제공 하는 `ID`, `TargetControlID` 특성과 반드시 `runat="server"`:

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample5.aspx)]

없는 `<Animations>` 내에서 노드는 `AnimationExtender` 제어 합니다. 사용자 지정 JavaScript 코드는 애니메이션 컨트롤과 함께 사용할 수 있도록 사용 됩니다.

서버 API와 마찬가지로 `AnimationExtender`, 아직 extender에 애니메이션을 할당할 쉽게 방법은 없습니다. 하지만 다양 한 이벤트와 함께 등록 된 extender 않습니다 여러 가지 방법으로 읽기 및 쓰기 애니메이션을 노출 (`OnClick`, `OnLoad`등). 다음은 몇 가지 예입니다.

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

반환 값의 형식은 `get_*()` 함수 및 형식에 대 한 인수는 `set_*()` 함수는 XML 태그는 것이 무엇 인지의 개체 표현을 제공 하는 JSON 문자열입니다. 현재 개체를 전달할 수 있는 방법이 있지만 지정 된 애니메이션에서 개체를 읽을 수는 (`get_OnXXXBehavior()` 메서드).

여기에 JSON 문자열 (구분 따옴표 없이 적절 하 게 서식이 지정)는 단추에 의해 트리거되는 애니메이션 나타내는 하지만 패널의 크기를 조정 하 고 동시에이 페이드 애니메이션:

[!code-json[Main](changing-an-animation-using-client-side-code-vb/samples/sample6.json)]

다음 JavaScript 코드에이 JSON descripting 할당는 `OnClick` 현재 extender의 애니메이션 실행:

[!code-html[Main](changing-an-animation-using-client-side-code-vb/samples/sample7.html)]


[![마우스 클릭 하지 않고 (및 거의 태그로) 애니메이션 즉시 실행](changing-an-animation-using-client-side-code-vb/_static/image2.png)](changing-an-animation-using-client-side-code-vb/_static/image1.png)

애니메이션 실행: 마우스 클릭 하지 않고 (및 거의 태그로) 즉시 ([전체 크기 이미지를 보려면 클릭](changing-an-animation-using-client-side-code-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](executing-animations-using-client-side-code-vb.md)
> [다음](animating-an-updatepanel-control-vb.md)
