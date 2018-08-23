---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
title: CascadingDropDown (C#)를 사용 하 여 목록 항목 미리 설정 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 anoth에 있도록 DropDownList 컨트롤을 확장 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 04c79748-0f21-4a3b-aba5-e1ce3161c32e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 2599b5015f288b2e8d02577a0865252a862574a4
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837001"
---
<a name="presetting-list-entries-with-cascadingdropdown-c"></a>CascadingDropDown (C#)를 사용 하 여 목록 항목 미리 설정
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)

> AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다. 약간의 코드를 사용 하 여 데이터를 동적으로 로드 되 면 목록 요소는 미리 선택 가능한 됩니다.


## <a name="overview"></a>개요

AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다. (예를 들어 미국 주 목록을 제공 하는 하나의 목록 및 해당 상태의 주요 도시를 사용 하 여 다음 목록에 다음 채워집니다.) 약간의 코드를 사용 하 여 데이터를 동적으로 로드 되 면 목록 요소는 미리 선택 가능한 됩니다.

## <a name="steps"></a>단계

ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample1.aspx)]

DropDownList 컨트롤은 그런 다음이 필요 합니다.

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample2.aspx)]

이 목록에 대 한 웹 서비스 URL 및 메서드 정보를 제공 하는 CascadingDropDown extender 추가 됩니다.

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample3.aspx)]

CascadingDropDown extender 비동기적으로 호출 된 다음 메서드 시그니처를 사용 하 여 웹 서비스:

[!code-csharp[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample4.cs)]

메서드는 CascadingDropDown 값 형식의 배열을 반환합니다. 목록 항목의 캡션 및 값 형식의 생성자에 먼저 인수가 (HTML `value` 특성). 세 번째 인수를 설정 하는 경우 true, 목록에 요소가 자동으로 선택 됩니다 브라우저에서 합니다.

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample5.aspx)]

브라우저에서 페이지 로드 입력 3 개 공급 업체를 사용 하 여 드롭다운 목록 미리 선택 되 고 두 번째 됩니다.


[![목록 채우기 및 자동으로 미리 선택](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)

목록 채우기 및 자동으로 미리 선택 ([클릭 하 여 큰 이미지 보기](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](using-cascadingdropdown-with-a-database-cs.md)
> [다음](using-auto-postback-with-cascadingdropdown-cs.md)
