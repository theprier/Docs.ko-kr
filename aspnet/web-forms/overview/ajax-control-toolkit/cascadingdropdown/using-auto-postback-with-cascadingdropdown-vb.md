---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
title: 자동 포스트백 (Vb)를 사용 하 여 사용 하 여 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 anoth에 있도록 DropDownList 컨트롤을 확장 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0b34f7f6-a0cc-4b9f-9761-643fb0bb3ece
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 31f24374714371f102a1e6bc7e8977713876b228
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836114"
---
<a name="using-auto-postback-with-cascadingdropdown-vb"></a>자동 포스트백 (Vb) 사용
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3VB.pdf)

> AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다. 그러나 ASP CascadingDropDown 컨트롤을 사용 하는 경우. 자체 (불필요 한) 포스트백을 생성 목록에 데이터를 비동기적으로 로드 되므로 NET의 DropDownList 컨트롤 AutoPostBack 기능이 작동 하지 않습니다. 일부 JavaScript 코드를 사용 하 여이 효과 방지할 수 있습니다.


## <a name="overview"></a>개요

AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다. (예를 들어 미국 주 목록을 제공 하는 하나의 목록 및 해당 상태의 주요 도시를 사용 하 여 다음 목록에 다음 채워집니다.) 그러나 ASP CascadingDropDown 컨트롤을 사용 하는 경우. 자체 (불필요 한) 포스트백을 생성 목록에 데이터를 비동기적으로 로드 되므로 NET의 DropDownList 컨트롤 AutoPostBack 기능이 작동 하지 않습니다. 일부 JavaScript 코드를 사용 하 여이 효과 방지할 수 있습니다.

## <a name="steps"></a>단계

ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내 합니다 &lt; `form` &gt; 요소):

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample1.aspx)]

DropDownList 컨트롤은 그런 다음이 필요 합니다.

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample2.aspx)]

이 목록에 대 한 웹 서비스 URL 및 메서드 정보를 제공 하는 CascadingDropDown extender 추가 됩니다.

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample3.aspx)]

CascadingDropDown extender 비동기적으로 호출 된 다음 메서드 시그니처를 사용 하 여 웹 서비스:

[!code-vb[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample4.vb)]

메서드는 CascadingDropDown 값 형식의 배열을 반환합니다. 목록 항목의 캡션 및 값 형식의 생성자에 먼저 인수가 (HTML `value` 특성).

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample5.aspx)]

브라우저에서 페이지 로드 입력 3 개 공급 업체를 사용 하 여 드롭다운 목록 미리 선택 되 고 두 번째 됩니다. 또한 ASP.NET 정의 `__doPostBack()` JavaScript 메서드. 페이지 로드 된 후이 JavaScript 호출만 하는 경우에이 요소가 있지만 드롭다운 목록에 추가 됩니다. 목록에 요소가 없는 경우 Control Toolkit을 현재 로드 하면 시간 제한을 사용 하 고 0.5 초 후에 다시 시도 하는 JavaScript 코드입니다.

[!code-html[Main](using-auto-postback-with-cascadingdropdown-vb/samples/sample6.html)]

이러한 방식으로 포스트백 때만 실행 됩니다 요소가 실제로 목록에서, 사용자가 항목을 선택 합니다.


[![포스트백을 발생 시키는 목록 요소를 선택 합니다.](using-auto-postback-with-cascadingdropdown-vb/_static/image2.png)](using-auto-postback-with-cascadingdropdown-vb/_static/image1.png)

포스트백을 발생 시키는 목록 요소를 선택 ([클릭 하 여 큰 이미지 보기](using-auto-postback-with-cascadingdropdown-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](presetting-list-entries-with-cascadingdropdown-vb.md)
