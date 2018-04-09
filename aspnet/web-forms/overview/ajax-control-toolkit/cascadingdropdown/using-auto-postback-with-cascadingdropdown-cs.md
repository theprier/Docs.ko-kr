---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
title: 자동 다시 게시를 사용 하 여 CascadingDropDown (C#)와 | Microsoft Docs
author: wenz
description: 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 anoth에 있도록 DropDownList 컨트롤을 확장 하는 AJAX 컨트롤 도구 키트에서 CascadingDropDown 컨트롤 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 6755d8d9-14be-4a1d-86e5-1a6110f3dea8
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 04e0914dd1057f9ce490f68ae3fa9c56766beafb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="using-auto-postback-with-cascadingdropdown-c"></a>자동 다시 게시 CascadingDropDown (C#) 사용
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)

> 들어에서 CascadingDropDown 컨트롤 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다. 그러나 ASP CascadingDropDown 컨트롤을 사용 하는 경우. 목록에 데이터를 비동기적으로 로드 자체는 (불필요 한) 포스트백을 생성 하므로 NET의 DropDownList 컨트롤 AutoPostBack 기능이 작동 하지 않습니다. 일부 JavaScript 코드와 함께이 효과 방지할 수 있습니다.


## <a name="overview"></a>개요

들어에서 CascadingDropDown 컨트롤 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다. (예를 들어, 하나의 목록에는 상태, 우리 목록이 및 다음 목록에는 다음 4 개 주요 도시 해당 상태에 채워집니다.) 그러나 ASP CascadingDropDown 컨트롤을 사용 하는 경우. 목록에 데이터를 비동기적으로 로드 자체는 (불필요 한) 포스트백을 생성 하므로 NET의 DropDownList 컨트롤 AutoPostBack 기능이 작동 하지 않습니다. 일부 JavaScript 코드와 함께이 효과 방지할 수 있습니다.

## <a name="steps"></a>단계

ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 &lt; `form` &gt; 요소):

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample1.aspx)]

그런 다음 DropDownList 컨트롤이 필요 합니다.

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample2.aspx)]

이 목록에 대 한 웹 서비스 URL과 메서드 정보를 제공 하는 CascadingDropDown extender 추가 됩니다.

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample3.aspx)]

CascadingDropDown extender 다음 비동기적으로 호출 다음 메서드 서명 사용 하 여 웹 서비스:

[!code-csharp[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample4.cs)]

메서드가는 CascadingDropDown 값 형식의 배열을 반환합니다. 목록 항목의 캡션 및 값 형식의 생성자에 먼저 인수가 (HTML `value` 특성).

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample5.aspx)]

브라우저에서 페이지를 로드를 채워 드롭다운 목록 3 개 공급 업체에 미리 선택 되 고 두 번째 식 있습니다. 또한 ASP.NET 정의 `__doPostBack()` JavaScript 메서드. 페이지가 로드 되 면이 JavaScript 호출만 하는 경우에이 요소가 있지만 드롭다운 목록에 추가 됩니다. 목록에 요소가 있는 경우 제어 도구 키트를 현재 로드, 하므로 JavaScript 코드는 제한 시간을 사용 하 여 하 고 1/2 초 후에 다시 시도 합니다.

[!code-html[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample6.html)]

이러한 방식으로 목록 실제로 요소는이 고 사용자가 항목을 선택할 때 포스트백 실행만 됩니다.


[![포스트백 목록 요소를 선택 하면](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)

포스트백 목록 요소를 선택 하면 ([전체 크기 이미지를 보려면 클릭](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](presetting-list-entries-with-cascadingdropdown-cs.md)
> [다음](filling-a-list-using-cascadingdropdown-vb.md)
