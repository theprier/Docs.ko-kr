---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
title: CascadingDropDown (C#)를 사용 하 여 목록 채우기 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 anoth에 있도록 DropDownList 컨트롤을 확장 하는 중...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: f949aafa-fe57-43b0-b722-f0dd33a900be
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: f48343e811bd41a8fa8ba6965f1e53643bef7fcb
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37806640"
---
<a name="filling-a-list-using-cascadingdropdown-c"></a>CascadingDropDown (C#)를 사용 하 여 목록 채우기
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)

> AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다. (예를 들어 미국 주 목록을 제공 하는 하나의 목록 및 해당 상태의 주요 도시를 사용 하 여 다음 목록에 다음 채워집니다.) 첫 번째 문제를 해결 하려면 실제로이 컨트롤을 사용 하 여 드롭다운 목록을 채우는 방법은입니다.


## <a name="overview"></a>개요

AJAX Control Toolkit에서 CascadingDropDown 컨트롤 하나 DropDownList 로드 변경에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다. (예를 들어 미국 주 목록을 제공 하는 하나의 목록 및 해당 상태의 주요 도시를 사용 하 여 다음 목록에 다음 채워집니다.) 첫 번째 문제를 해결 하려면 실제로이 컨트롤을 사용 하 여 드롭다운 목록을 채우는 방법은입니다.

## <a name="steps"></a>단계

ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

DropDownList 컨트롤은 그런 다음이 필요 합니다.

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

이 목록에 대해 CascadingDropDown extender 추가 됩니다. 이 비동기 요청을 한 다음 목록에 표시할 항목의 목록을 반환 하는 웹 서비스에 전송할 수 있습니다. 이렇게 하려면 다음 CascadingDropDown 특성 설정 해야 합니다.

- `ServicePath`: 목록 항목을 제공 하는 웹 서비스의 URL
- `ServiceMethod`합니다: 목록 항목을 제공 웹 메서드
- `TargetControlID`: 드롭다운 목록의 ID
- `Category`: 웹 메서드 호출에 제출 된 범주 정보
- `PromptText`: 비동기적으로 서버에서 목록 데이터를 로드할 때 표시 되는 텍스트

여기에 대 한 태그는 `CascadingDropDown` 요소입니다. C# 및 VB 간의 유일한 차이점은 연결 된 웹 서비스의 이름.

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

들어오는 JavaScript 코드는 `CascadingDropDown` extender는 다음 서명 사용 하 여 웹 서비스 메서드를 호출 합니다.

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

중요 한 점은 메서드 형식의 배열을 반환 해야 하므로 `CascadingDropDownNameValue` (ASP.NET AJAX Control Toolkit에서 정의 됨). 에 `CascadingDropDownNameValue` 생성자를 첫 번째 목록 항목의 텍스트를 가져온 다음 해당 값을 지정 해야 합니다 처럼 `<option value="VALUE">NAME</option>` HTML에서. 몇 가지 샘플 데이터는 다음과 같습니다.

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

브라우저에서 페이지 로드 3 개 공급 업체를 사용 하 여 채울 목록을 트리거할 수 있습니다.


[![자동으로 채워집니다.](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)

자동으로 채워집니다 ([클릭 하 여 큰 이미지 보기](filling-a-list-using-cascadingdropdown-cs/_static/image3.png))

> [!div class="step-by-step"]
> [다음](using-cascadingdropdown-with-a-database-cs.md)
