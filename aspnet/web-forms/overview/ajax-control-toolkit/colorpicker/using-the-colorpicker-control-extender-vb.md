---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: ColorPicker Control Extender (VB)를 사용 하 여 | Microsoft Docs
author: microsoft
description: ColorPicker 팝업 컨트롤의 UI를 사용 하 여 클라이언트 쪽 색 선택 기능을 제공 하는 ASP.NET AJAX extender입니다. 모든 ASP.NET에 연결할 수 있습니다...
ms.author: aspnetcontent
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: e7375dcfc354e931f30d2250081f424bd2149953
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37828133"
---
<a name="using-the-colorpicker-control-extender-vb"></a>ColorPicker Control Extender (VB)를 사용 하 여
====================
[Microsoft](https://github.com/microsoft)

> ColorPicker 팝업 컨트롤의 UI를 사용 하 여 클라이언트 쪽 색 선택 기능을 제공 하는 ASP.NET AJAX extender입니다. 모든 ASP.NET TextBox 컨트롤에 연결할 수 있습니다. 있습니다.


이 자습서의 목표는 AJAX Control Toolkit ColorPicker control extender를 사용 하는 방법을 설명 합니다. ColorPicker control extender는 색을 선택할 수 있는 팝업 대화 상자를 표시 합니다. ColorPicker는 색을 선택 하는 사용자에 대 한 직관적인 사용자 인터페이스를 제공 하려고 할 때마다 유용 합니다.

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>ColorPicker Control Extender 사용 하 여 TextBox 컨트롤 확장

예를 들어, 방문자가 사용자 지정된 비즈니스 카드를 만들 수 있는 웹 사이트를 만들려고 한다고 가정해 보겠습니다. 방문자는 비즈니스 카드에 대 한 텍스트를 입력 하 고 색을 선택할 수 있습니다. 목록 1의 ASP.NET 페이지 txtCardText 및 txtCardColor 라는 두 개의 텍스트 상자 컨트롤을 포함 합니다. 폼을 제출 하면 선택한 값이 표시 됩니다 (그림 1 참조).


[![명함을 만들기 위한 간단한 폼](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)

**그림 01**: 명함을 만들기 위한 간단한 폼 ([큰 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image2.png))


**1-CreateCard.aspx 나열**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

목록 1 작동 하지만 형태로 훌륭한 사용자 환경을 제공 하지 않습니다. 사용자는 색을 텍스트 상자에 입력 해야 합니다. 사용자가 특수 한 색-예를 들어 pea 녹색-사용자의 올바른 음영 방금 알아내야 도움이 없이 HTML 색 코드입니다.

더 나은 사용자 환경을 만들려면 ColorPicker control extender를 사용할 수 있습니다. ColorPicker는 TextBox 컨트롤에 포커스를 이동 하는 경우 색 대화 상자를 표시 합니다 (그림 2 참조).


[![ColorPicker Control Extender](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)

**그림 02**: The ColorPicker Control Extender ([큰 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image4.png))


목록 1 양식을 사용 하 여 ColorPicker control extender를 사용 하는 두 단계를 완료 해야 합니다.

1. 페이지에 ScriptManager 컨트롤을 추가 합니다.
2. ColorPicker control extender를 페이지에 추가 합니다.

ColorPicker를 사용 하려면 먼저 페이지에 ScriptManager를 추가 해야 합니다. 열기 서버 쪽 바로 아래는 ScriptManager를 추가 하는 것이 좋습니다 &lt;폼&gt; 태그입니다. (ScriptManager는 AJAX 확장명 탭 아래에 있습니다.)를 도구 상자에서 페이지로 ScriptManager를 끌 수 있습니다. 또는 서버 쪽 양식의 태그 아래에 있는 소스 뷰로 다음 태그를 입력할 수 있습니다.

&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;

디자인 뷰에서 가장 쉬운 방법은 ColorPicker control extender를 페이지에 추가할 경우 스마트 작업 옵션을 사용 하도록 설정 나타납니다 txtCardColor 텍스트 상자 위에 마우스를 놓으면 extender를 추가할 수 있습니다 (그림 3 참조). 이 옵션을 선택 하면 Extender 마법사 나타납니다 (그림 4 참조).


[![Extender를 추가합니다.](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)

**그림 03**: extender 추가 ([큰 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image6.png))


[![Extender 마법사를 사용 하 여 컨트롤 extender를 선택합니다.](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)

**그림 04**: Extender 마법사를 사용 하 여 컨트롤 extender를 선택 하면 ([큰 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image8.png))


ColorPicker extender 사용 하 여 텍스트 상자 txtCardColor 확장할 ColorPicker extender를 선택할 수 있습니다. 대화 상자를 닫으려면 확인을 클릭 합니다.

이러한 변경을 수행한 후 페이지에 대 한 원본 목록 2와 같습니다.

**2-(사용 하 여 ColorPicker) CreateCard.aspx 나열**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

페이지에 이제 txtCardColor TextBox 컨트롤 바로 아래 표시 되는 ColorPickerExtender 컨트롤 포함 확인 합니다. 색 선택 대화 상자가 표시 되도록 ColorPickerExtender 컨트롤 txtCardColor 컨트롤을 확장 합니다.

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>단추를 사용 하 여 색 선택 대화 상자를 시작 하려면

ColorPicker extender는 다음 속성을 지원합니다.

- PopupButtonId-ID 색 선택 대화 상자를 표시 하는 페이지의 단추입니다.
- Popupposition 속성은-색 선택 대화 상자의 대상 컨트롤에 상대적인 위치입니다. 가능한 값은 절대, Center, 왼쪽 맨 아래, 오른쪽 맨 아래, 왼쪽 맨 위, 오른쪽, 오른쪽 맨 위 및 왼쪽 (기본값인 왼쪽 맨 아래).
- SampleControlId-선택한 색을 표시 하는 컨트롤의 ID입니다.
- SelectedColor-는 ColorPicker 선택한 초기 색입니다.

색 선택 대화 상자가 표시 되는 방식 및 선택한 색이 표시 되는 방식을 사용자 지정 하려면 이러한 속성을 사용할 수 있습니다. 목록 3에서 페이지에서는 이러한 속성 중 일부를 사용 하는 방법을 보여 줍니다.

**3-CreateCardButton.aspx 나열**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

목록 3에서 페이지 포함 색 선택 단추 (그림 5 참조). 이 단추를 클릭할 때 텍스트 상자 위에 색 선택 대화 상자가 나타납니다. 대화 상자에서 색을 선택 하면 선택한 색 lblSample 레이블 컨트롤의 배경색으로 표시 됩니다.

ColorPicker PopupButtonID 속성 ColorPicker extender를 사용 하 여 색 선택 단추를 연결할 때 사용 됩니다. PopupButtonID 속성에 대 한 값을 제공 하면 색 선택 대화 상자는 더 이상 대상 컨트롤에 포커스가 있을 때 나타납니다. 대화 상자를 표시 하려면 단추를 클릭 해야 합니다.

ColorPicker 사용 하 여 선택한 색을 표시 하는 컨트롤을 연결할 SampleControlID 속성이 사용 됩니다. ColorPicker는 현재 선택한 색으로이 컨트롤의 배경색을 변경합니다.


[![단추를 사용 하 여 색 선택 대화 상자를 표시합니다.](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)

**그림 05**: 단추를 사용 하 여 색 선택 대화 상자 표시 ([큰 이미지를 보려면 클릭](using-the-colorpicker-control-extender-vb/_static/image10.png))


## <a name="summary"></a>요약

이 자습서에서는 ColorPicker control extender를 사용 하 여 팝업 색 선택 대화 상자를 표시 하는 방법을 알아보았습니다. 먼저 포커스가 TextBox 컨트롤을 이동 하는 경우 대화 상자에 표시 하는 방법을 살펴보았습니다. 다음으로 단추를 클릭 하면 색 선택 대화 상자를 표시 하는 단추를 만드는 방법을 알아보았습니다.

> [!div class="step-by-step"]
> [이전](using-the-colorpicker-control-extender-cs.md)
