---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: AJAX 컨트롤 도구 키트 컨트롤 및 컨트롤 Extenders 사용 (C#)를 사용 하 여 | Microsoft Docs
author: microsoft
description: ASP.NET 페이지에 AJAX Control Toolkit 컨트롤 및 extender를 추가 하는 방법에 알아봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 54e3ec3cc608c4fab877b4135e3c180319ea8432
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389981"
---
<a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a>AJAX 컨트롤 도구 키트 컨트롤 및 컨트롤 Extenders 사용 (C#)를 사용 하 여
====================
[Microsoft](https://github.com/microsoft)

> ASP.NET 페이지에 AJAX Control Toolkit 컨트롤 및 extender를 추가 하는 방법에 알아봅니다.


AJAX Control Toolkit 컨트롤 및 컨트롤 extenders 집합이 포함 되어 있습니다. 이 간략 한 자습서는 ASP.NET 페이지에 컨트롤 및 컨트롤 extenders 사용을 추가 하는 방법을 알아봅니다.

> [!NOTE] 
> 
> AJAX Control Toolkit을 설치 하 고 Visual Studio/Visual Web Developer 도구 상자에 AJAX Control Toolkit을 추가 하는 방법은 자습서를 참조 하세요 [AJAX Control Toolkit 시작](get-started-with-the-ajax-control-toolkit-cs.md)합니다.


## <a name="using-ajax-control-toolkit-controls"></a>AJAX 컨트롤 도구 키트 컨트롤을 사용 하 여

AJAX Control Toolkit 컨트롤을 일반적인 ASP.NET 컨트롤 처럼 작동합니다. ASP.NET 페이지를 도구 상자에서 컨트롤을 끌 수 있습니다. 디자인 뷰 또는 원본 보기 페이지로 컨트롤을 추가할 수 있습니다.

AJAX Control Toolkit에서 컨트롤을 사용 하는 경우 특별 한 요구 사항 중 하나가 있습니다. 페이지에 ScriptManager 컨트롤을 포함 해야 합니다. ScriptManager 컨트롤은 모두 AJAX Control Toolkit 컨트롤에 필요한 필요한 JavaScript를 비롯 한 담당 합니다.

예를 들어, AJAX Control Toolkit 탭에는 편집기 컨트롤 이라는 컨트롤을 포함 합니다. 이 컨트롤에 풍부한 HTML 편집기를 표시합니다. 페이지에는 편집기 컨트롤을 추가 하려면 다음이 단계를 수행 합니다.

1. ShowEditor.aspx 라는 새로운 ASP.NET 페이지 만들기
2. 도구 상자에서 AJAX 확장명 탭 아래 ScriptManager 컨트롤을 선택 하 고 컨트롤을 페이지로 끌어다 놓습니다.
3. 도구 상자에서 AJAX Control Toolkit 탭 아래 편집기 컨트롤을 선택 하 고 컨트롤을 페이지로 끌어 (그림 1 참조). 디자이너는 그림 2와 같습니다.
4. 메뉴 옵션을 선택 하 여 웹 사이트를 실행할 **디버그, 디버깅 시작** F5 키를 눌러 또는 합니다.
5. 그림 3에는 페이지가 표시 됩니다.


[![HTML 편집기 컨트롤 선택](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)

**그림 01**: HTML 편집기 컨트롤을 선택 하면 ([큰 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))


[![ScriptManager 및 편집 컨트롤을 사용 하 여 visual Studio 디자이너](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)

**그림 02**: ScriptManager 및 편집 컨트롤을 사용 하 여 Visual Studio Designer ([큰 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))


[![DisplayEditor.aspx 페이지](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)

**그림 03**: The DisplayEditor.aspx 페이지 ([큰 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))


## <a name="using-ajax-control-toolkit-control-extenders"></a>AJAX 컨트롤 도구 키트 컨트롤 Extender를 사용 하 여

AJAX Control Toolkit 컨트롤 extenders를 사용에 포함 되어 있습니다. 해당 이름에서 알 수 있듯이 컨트롤 extender를 기존 컨트롤의 기능을 확장 합니다. 예를 들어 ConfirmButton 컨트롤 extender는 표준 ASP.NET Button 컨트롤을 확장합니다. Extender는 단추를 클릭 하면 확인 대화 상자가 표시 되도록 단추 컨트롤의의 동작을 변경 합니다.

컨트롤 extender는 AJAX Control Toolkit 컨트롤 처럼 ScriptManager 컨트롤에 필요합니다. 페이지에서 컨트롤 extender를 사용 하려면 먼저 페이지에 ScriptManager 컨트롤을 추가 해야 합니다.

컨트롤 같이 ConfirmButton extender를 사용 하려면 다음이 단계를 수행 합니다.

1. ShowConfirmButton.aspx 라는 새로운 ASP.NET 페이지 만들기
2. AJAX 확장명 탭 아래 페이지 컨트롤을 끌어 페이지에 ScriptManager 컨트롤을 추가 합니다.
3. 표준 탭 아래 단추를 도구 상자에서 디자이너 화면에 끌어 페이지에 표준 단추 컨트롤을 추가 합니다.
4. 클릭 합니다 **Extender 추가** 작업 옵션 (그림 4 참조).
5. Extender 선택 대화 상자에서 ConfirmButtonExtender 선택 (그림 5 참조) 확인 단추를 클릭 합니다.
6. 디자이너에서 단추 컨트롤을 선택 하 고 Extender가 Button1 확장\_속성 창에서 ConfirmButtonExtender 노드 (그림 6 참조). 값을 할당 *실제로?* ConfirmText 속성입니다.
7. 메뉴 옵션을 선택 하 여 페이지를 실행할 **디버그, 디버깅 시작** 또는 F5 키를 누릅니다.


[![Extender 추가 작업 옵션](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)

**그림 04**: Extender 추가 작업 옵션 ([큰 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))


[![컨트롤 같이 ConfirmButton extender를 선택합니다.](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)

**그림 05**: 컨트롤 같이 ConfirmButton extender를 선택 하면 ([큰 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))


[![ConfirmButton 속성 설정](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)

**그림 06**: ConfirmButton 속성을 설정 ([큰 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))


페이지가 열릴 때 단추가 표시 됩니다. 단추를 클릭 하면 그림 7에서 확인 대화 상자를 가져옵니다.


[![확인 대화 상자를 표시합니다.](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)

**그림 07**: 확인 대화 상자를 표시 합니다. ([큰 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))


일반적으로 끌어 오지 않은 컨트롤 extender를 페이지를 확인 합니다. 대신 사용 합니다 **Extender 추가** extender를 페이지에 이미 추가한 컨트롤에 추가 하는 옵션을 작업 합니다. 확인, 또한 컨트롤 extender 속성 설정 되는 확장 된 컨트롤의 속성 시트를 열어 합니다.

여러 컨트롤 extenders 사용 하 여 단일 ASP.NET 컨트롤을 확장할 수 있습니다. 확장 된 컨트롤에 대 한 속성 시트 컨트롤과 연결 된 컨트롤 extender의 모든를 나열 됩니다.

> [!div class="step-by-step"]
> [이전](get-started-with-the-ajax-control-toolkit-cs.md)
> [다음](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
