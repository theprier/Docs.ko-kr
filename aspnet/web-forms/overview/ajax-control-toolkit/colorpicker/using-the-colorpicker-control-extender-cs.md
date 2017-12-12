---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
title: "ColorPicker 컨트롤 Extender (C#)를 사용 하 여 | Microsoft Docs"
author: microsoft
description: "ColorPicker는 popup 컨트롤의 UI를 사용한 클라이언트 쪽 색 선택 기능을 제공 하는 ASP.NET AJAX extender입니다. 모든 ASP.NET에는 연결할 수 있습니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: 0d86a1e7-a910-4ab2-b85c-7a9ea6906c39
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: 5b3cde9552e8aecd5e7e651a825902fb79ae108c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-the-colorpicker-control-extender-c"></a>ColorPicker 컨트롤 Extender (C#)를 사용 하 여
====================
여 [Microsoft](https://github.com/microsoft)

> ColorPicker는 popup 컨트롤의 UI를 사용한 클라이언트 쪽 색 선택 기능을 제공 하는 ASP.NET AJAX extender입니다. ASP.NET TextBox 컨트롤에 연결 될 수 있습니다. 것입니다.


이 자습서의 목표 AJAX 컨트롤 Toolkit ColorPicker 컨트롤 extender를 사용 하는 방법을 설명 하는 것입니다. ColorPicker 컨트롤 extender 색을 선택할 수 있는 팝업 대화 상자를 표시 합니다. ColorPicker 색을 선택 하는 사용자에 대 한 직관적인 사용자 인터페이스를 제공 하려는 경우 유용 합니다.

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>ColorPicker 컨트롤 Extender 있는 TextBox 컨트롤을 확장합니다.

예를 들어 방문자가 사용자 지정 된 비즈니스 명함을 만들 수 있는 웹 사이트를 만들 것인지 한다고 가정 합니다. 방문자는 비즈니스 카드에 대 한 텍스트를 입력 하 고 색을 선택할 수 있습니다. 목록 1에서 ASP.NET 페이지 txtCardText 및 txtCardColor 라는 두 개의 TextBox 컨트롤을 포함 합니다. 폼을 제출 하면 선택 된 값이 표시 됩니다 (그림 1 참조).


[![명함을 만들기 위한 단순 양식](using-the-colorpicker-control-extender-cs/_static/image1.jpg)](using-the-colorpicker-control-extender-cs/_static/image1.png)

**그림 01**: 명함을 만들기 위한 간단한 형태 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-cs/_static/image2.png))


**1-CreateCard.aspx 나열**

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample1.aspx)]

폼 목록 1의 작동에는 뛰어난 사용자 환경을 제공 하지 않습니다. 사용자는 색 입력란에 입력 해야 합니다. 사용자가 특수 색상-예를 들어 pea 녹색-다음 사용자의 오른쪽 음영 방금 알아내야 모든 도움 없이 HTML 색상 코드입니다.

더 나은 사용자 환경을 만드는 ColorPicker 컨트롤 extender를 사용할 수 있습니다. ColorPicker TextBox 컨트롤에 포커스를 이동 하면 색 대화 상자를 표시 합니다 (그림 2 참조).


[![ColorPicker 컨트롤 Extender](using-the-colorpicker-control-extender-cs/_static/image2.jpg)](using-the-colorpicker-control-extender-cs/_static/image3.png)

**그림 02**: The ColorPicker 컨트롤 Extender ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-cs/_static/image4.png))


목록 1 양식을 사용 하 여 ColorPicker 컨트롤 extender를 사용 하는 두 단계를 완료 해야 합니다.

1. 페이지에 ScriptManager 컨트롤 추가
2. ColorPicker 컨트롤 extender 페이지에 추가

ColorPicker를 사용 하려면 먼저 페이지에 ScriptManager를 추가 해야 합니다. 여는 서버 쪽 바로 아래 ScriptManager를 추가 하는 데는 &lt;양식&gt; 태그입니다. (ScriptManager AJAX 확장 탭에 있습니다.)를 도구 상자에서 ScriptManager 페이지 끌 수 있습니다. 또는 여는 서버측 form 태그 아래에 있는 소스 보기에는 다음과 같은 태그를 입력할 수 있습니다.

&lt;asp: ScriptManager ID = "ScriptManager1" runat = "server" /&gt;

디자인 뷰에서 페이지로 ColorPicker 컨트롤 extender를 추가 하는 가장 쉬운 방법은 됩니다. 스마트 작업 옵션을 사용 하면 표시 TextBox txtCardColor 위로 마우스를 가져가면 extender를 추가할 수 있습니다 (그림 3 참조). 이 옵션을 선택 하면 Extender 마법사 (그림 4 참조)가 나타납니다.


[![Extender를 추가합니다.](using-the-colorpicker-control-extender-cs/_static/image3.jpg)](using-the-colorpicker-control-extender-cs/_static/image5.png)

**그림 03**: extender 추가 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-cs/_static/image6.png))


[![Extender 마법사로 컨트롤 extender를 선택합니다.](using-the-colorpicker-control-extender-cs/_static/image4.jpg)](using-the-colorpicker-control-extender-cs/_static/image7.png)

**그림 04**: Extender 마법사로 컨트롤 extender를 선택 하면 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-cs/_static/image8.png))


ColorPicker extender ColorPicker 확장기에 텍스트 상자에 붙여넣습니다 txtCardColor 확장를 선택할 수 있습니다. 확인 대화 상자를 닫으려면 클릭 합니다.

이러한 변경을 수행한 후 페이지에 대 한 소스 목록 2와 유사 합니다.

2-(ColorPicker)와 CreateCard.aspx 나열

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample2.aspx)]

페이지 이제 txtCardColor TextBox 컨트롤 바로 아래에 나타나는 ColorPickerExtender 컨트롤에 포함 되었는지 확인 합니다. 색 선택 대화 상자 표시 되도록 ColorPickerExtender 컨트롤 txtCardColor 컨트롤을 확장 합니다.

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>단추를 사용 하 여 색 선택 대화 상자를 시작 하려면

ColorPicker extender는 다음 속성을 지원합니다.

- PopupButtonId-단추의 색 선택 대화 상자를 표시 하는 페이지의 ID입니다.
- PopupPosition-대상 컨트롤의 색 선택 대화 상자에 상대적인 위치입니다. 가능한 값에는 절대, 가운데, 왼쪽 맨 아래 오른쪽 맨 아래, 왼쪽 맨 위, 오른쪽, 오른쪽 맨 위 및 왼쪽 (기본값인 왼쪽 맨 아래)은 합니다.
- SampleControlId-선택한 색을 표시 하는 컨트롤의 ID입니다.
- SelectedColor-는 ColorPicker가 선택한 초기 색입니다.

색 선택 대화 상자 표시 되는 방식 및 선택한 색 표시 되는 방식을 사용자 지정 하려면 이러한 속성을 사용할 수 있습니다. 페이지 보기 3에서 이러한 속성 중 몇 가지를 사용 하는 방법을 보여 줍니다.

**3-CreateCardButton.aspx 나열**

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample3.aspx)]

보기 3의 페이지에 색 선택 단추 (그림 5 참조). 이 단추를 클릭 하 고 입력란 위 색 선택 대화 상자 표시 됩니다. 대화 상자에서 색을 선택 하면 선택한 색 lblSample 레이블 컨트롤의 배경색으로 표시 됩니다.

ColorPicker PopupButtonID 속성 ColorPicker 확장기에 색 선택 단추를 연결할 때 사용 됩니다. PopupButtonID 속성에 대 한 값을 제공 하는 경우 대상 컨트롤에 포커스가 있을 때가 더 이상 색 선택 대화 상자에 나타납니다. 대화 상자를 표시 하려면 단추를 클릭 해야 합니다.

SampleControlID 속성은 ColorPicker와 선택한 색을 표시 하는 컨트롤을 연결할 때 사용 됩니다. ColorPicker 현재 선택 된 색이 컨트롤의 배경색을 변경합니다.


[![단추 색 선택 대화 상자를 표시합니다.](using-the-colorpicker-control-extender-cs/_static/image5.jpg)](using-the-colorpicker-control-extender-cs/_static/image9.png)

**그림 05**: 단추 색 선택 대화 상자 표시 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-cs/_static/image10.png))


## <a name="summary"></a>요약

이 자습서에서는 팝업 색 선택 대화 상자를 표시 하려면 ColorPicker 컨트롤 extender를 사용 하는 방법을 배웠습니다. 첫째, TextBox 컨트롤에 포커스를 이동할 때 대화 상자에 표시 하는 방법을 검사 합니다. 다음으로 단추를 클릭 하면 색 선택 대화 상자를 표시 하는 단추를 만드는 방법을 배웠습니다.

>[!div class="step-by-step"]
[다음](using-the-colorpicker-control-extender-vb.md)
