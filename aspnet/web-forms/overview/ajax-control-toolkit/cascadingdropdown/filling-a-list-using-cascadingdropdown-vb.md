---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
title: "CascadingDropDown (VB)를 사용 하는 목록 채우기 | Microsoft Docs"
author: wenz
description: "변경 내용을 하나의 DropDownList 부하에 관련 된 값이 anoth에 있도록 DropDownList 컨트롤을 확장 하는 AJAX 컨트롤 도구 키트에서 CascadingDropDown 컨트롤 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 5236695e-5c70-4887-baee-0bfb0afb3448
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 1c5cb23be4366365c73ce4774e6a53e452e2a6c0
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="filling-a-list-using-cascadingdropdown-vb"></a>CascadingDropDown (VB)를 사용 하는 목록 채우기
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0VB.pdf)

> 들어에서 CascadingDropDown 컨트롤 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다. (예를 들어, 하나의 목록에는 상태, 우리 목록이 및 다음 목록에는 다음 4 개 주요 도시 해당 상태에 채워집니다.) 첫 번째 문제를 해결 하는 실제로이 컨트롤을 사용 하 여 드롭다운 목록 채우기 되려고 합니다.


## <a name="overview"></a>개요

들어에서 CascadingDropDown 컨트롤 변경 내용을 하나의 DropDownList 부하에 관련 된 값이 다른 DropDownList에 있도록 DropDownList 컨트롤을 확장 합니다. (예를 들어, 하나의 목록에는 상태, 우리 목록이 및 다음 목록에는 다음 4 개 주요 도시 해당 상태에 채워집니다.) 첫 번째 문제를 해결 하는 실제로이 컨트롤을 사용 하 여 드롭다운 목록 채우기 되려고 합니다.

## <a name="steps"></a>단계

ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample1.aspx)]

그런 다음 DropDownList 컨트롤이 필요 합니다.

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample2.aspx)]

이 목록에 대해 CascadingDropDown extender 추가 됩니다. 다음 목록에 표시 되는 항목의 목록을 반환 하는 웹 서비스에 대 한 비동기 요청을 보내집니다. 이렇게 하려면 다음 CascadingDropDown 특성을 설정할 필요 합니다.

- `ServicePath`: 목록 항목을 제공 하는 웹 서비스의 URL
- `ServiceMethod`: 목록 항목을 제공 하는 웹 메서드
- `TargetControlID`: ID의 드롭다운 목록
- `Category`: 웹 메서드 호출에 제출한 범주 정보
- `PromptText`: 서버에서 목록 데이터를 비동기적으로 로드할 때 표시 되는 텍스트

다음은 대 한 태그는 `CascadingDropDown` 요소입니다. C# 및 VB 간의 유일한 차이점은 연결 된 웹 서비스의 이름.

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample3.aspx)]

제공 하는 JavaScript 코드는 `CascadingDropDown` extender 다음 서명 사용 하 여 웹 서비스 메서드를 호출 합니다.

[!code-vb[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample4.vb)]

메서드에 필요한 형식의 배열을 반환 하는 중요 한 요소 이므로 `CascadingDropDownNameValue` (ASP.NET AJAX 컨트롤 도구 키트에서 정의 됨). 에 `CascadingDropDownNameValue` 있는 생성자, 첫 번째 목록 항목의 텍스트와 해당 값을 지정 해야 합니다 마찬가지로 `<option value="VALUE">NAME</option>` html에서을 수행 합니다. 예제 데이터는 다음과 같습니다.

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-vb/samples/sample5.aspx)]

브라우저에서 페이지를 로드 3 개 공급 업체와 채울 목록을 트리거할 수 있습니다.


[![자동으로 채워진 목록](filling-a-list-using-cascadingdropdown-vb/_static/image2.png)](filling-a-list-using-cascadingdropdown-vb/_static/image1.png)

목록을 자동으로 채워집니다 ([전체 크기 이미지를 보려면 클릭](filling-a-list-using-cascadingdropdown-vb/_static/image3.png))

>[!div class="step-by-step"]
[이전](using-auto-postback-with-cascadingdropdown-cs.md)
[다음](using-cascadingdropdown-with-a-database-vb.md)
