---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
title: 클라이언트 쪽 코드 (C#)를 사용 하 여 애니메이션 변경 | Microsoft Docs
author: wenz
description: ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 애니메이션을 선택 하십시오.
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 2bfbc5cc-f942-44b7-a62d-a29520f1da9a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 9711e93ee6f119ec1825e32bdad64535435970c9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37808958"
---
<a name="changing-an-animation-using-client-side-code-c"></a>클라이언트 쪽 코드 (C#)를 사용 하 여 애니메이션 변경
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11CS.pdf)

> ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 애니메이션은 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 변경할 수 있습니다.


## <a name="overview"></a>개요

ASP.NET AJAX Control Toolkit에서 애니메이션 컨트롤 컨트롤 뿐 이지만 컨트롤에 애니메이션을 추가 하는 전체 프레임 워크 아닙니다. 애니메이션은 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 변경할 수 있습니다.

## <a name="steps"></a>단계

첫째, 포함 된 `ScriptManager` 페이지 그런 다음 ASP.NET AJAX 라이브러리 로드 되 면 컨트롤 도구 키트를 사용 하 여:

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample1.aspx)]

그러면 다음과 같은 텍스트 패널에 애니메이션 적용 됩니다.

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample2.aspx)]

패널에 대 한 연결 된 CSS 클래스에 유용한 배경 색을 정의 하 고 패널 고정된 너비를 설정할 수도:

[!code-css[Main](changing-an-animation-using-client-side-code-cs/samples/sample3.css)]

실제 애니메이션은 HTML 단추를 통해 시작 됩니다.

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample4.aspx)]

그런 다음 추가 `AnimationExtender` 페이지에서 제공 하는 `ID`, `TargetControlID` 특성과 필수 항목 이지만 `runat="server"`:

[!code-aspx[Main](changing-an-animation-using-client-side-code-cs/samples/sample5.aspx)]

없습니다 `<Animations>` 내에서 노드를 `AnimationExtender` 제어 합니다. 사용자 지정 JavaScript 코드는 컨트롤을 사용 하 여 사용할 애니메이션을 위해 사용 됩니다.

서버 API와 마찬가지로 `AnimationExtender`을 extender에 애니메이션을 아직 할당할 간편한 방법이 없습니다. 하지만 다양 한 이벤트를 사용 하 여 등록 된 extender는 읽기 및 쓰기 애니메이션 하는 여러 메서드를 노출 하는 (`OnClick`, `OnLoad`등). 다음은 몇 가지 예입니다.

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

반환 값의 형식을 `get_*()` 의 인수 형식과 함수는 `set_*()` 함수는 JSON 문자열 것 XML 태그의 개체 표현을 제공 합니다. 현재, 개체를 전달할 방법이 없기 하지만 지정 된 애니메이션에서 개체를 읽을 수 있습니다 (`get_OnXXXBehavior()` 메서드).

JSON 문자열은 다음과 같습니다 (구분 따옴표 없이 원활 하 게 서식이 지정) 단추를 트리거한 애니메이션을 나타내는 이지만 패널 크기를 조정 하 여 동시에 페이드아웃 애니메이션 합니다.

[!code-json[Main](changing-an-animation-using-client-side-code-cs/samples/sample6.json)]

다음 JavaScript 코드를이 JSON descripting 할당 된 `OnClick` 현재 extender의 애니메이션 실행:

[!code-html[Main](changing-an-animation-using-client-side-code-cs/samples/sample7.html)]


[![마우스 클릭 하지 않고 (및 거의 태그를 사용 하 여)이 애니메이션은 즉시 실행](changing-an-animation-using-client-side-code-cs/_static/image2.png)](changing-an-animation-using-client-side-code-cs/_static/image1.png)

마우스 클릭 하지 않고과 거의 태그를 사용 하 여 애니메이션은 즉시 실행 ([클릭 하 여 큰 이미지 보기](changing-an-animation-using-client-side-code-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](executing-animations-using-client-side-code-cs.md)
> [다음](animating-an-updatepanel-control-cs.md)
