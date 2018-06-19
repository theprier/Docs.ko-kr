---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
title: CascadingDropDown (C#)와 목록 항목을 미리 설정 | Microsoft Docs
author: wenz
description: 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 anoth에 있도록 DropDownList 컨트롤을 확장 하는 AJAX 컨트롤 도구 키트에서 CascadingDropDown 컨트롤 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 04c79748-0f21-4a3b-aba5-e1ce3161c32e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: d87da6c19f6dbdff70eff410ba7573c3e26884fb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868830"
---
<a name="presetting-list-entries-with-cascadingdropdown-c"></a>CascadingDropDown (C#)와 목록 항목을 미리 설정
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingDropDown2CS.pdf)

> 들어에서 CascadingDropDown 컨트롤 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다. 약간의 코드와 불가능 한 데이터를 동적으로 로드 되 면 목록 요소는 미리 선택 됩니다.


## <a name="overview"></a>개요

들어에서 CascadingDropDown 컨트롤 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다. (예를 들어, 하나의 목록에는 상태, 우리 목록이 및 다음 목록에는 다음 4 개 주요 도시 해당 상태에 채워집니다.) 약간의 코드와 불가능 한 데이터를 동적으로 로드 되 면 목록 요소는 미리 선택 됩니다.

## <a name="steps"></a>단계

ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample1.aspx)]

그런 다음 DropDownList 컨트롤이 필요 합니다.

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample2.aspx)]

이 목록에 대 한 웹 서비스 URL과 메서드 정보를 제공 하는 CascadingDropDown extender 추가 됩니다.

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample3.aspx)]

CascadingDropDown extender 다음 비동기적으로 호출 다음 메서드 서명 사용 하 여 웹 서비스:

[!code-csharp[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample4.cs)]

메서드가는 CascadingDropDown 값 형식의 배열을 반환합니다. 목록 항목의 캡션 및 값 형식의 생성자에 먼저 인수가 (HTML `value` 특성). 세 번째 인수를 설정 하는 경우 true, 목록에 요소가 자동으로 선택 됩니다 브라우저에서 합니다.

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-cs/samples/sample5.aspx)]

브라우저에서 페이지를 로드를 채워 드롭다운 목록 3 개 공급 업체에 미리 선택 되 고 두 번째 식 있습니다.


[![목록 채우기 및 자동으로 미리 선택](presetting-list-entries-with-cascadingdropdown-cs/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-cs/_static/image1.png)

목록 채우기 및 자동으로 미리 선택 ([전체 크기 이미지를 보려면 클릭](presetting-list-entries-with-cascadingdropdown-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](using-cascadingdropdown-with-a-database-cs.md)
> [다음](using-auto-postback-with-cascadingdropdown-cs.md)
