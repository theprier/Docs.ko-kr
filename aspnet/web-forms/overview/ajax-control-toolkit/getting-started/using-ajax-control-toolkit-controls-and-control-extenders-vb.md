---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
title: AJAX 컨트롤 Toolkit 컨트롤 및 컨트롤 Extender (VB)를 사용 하 여 | Microsoft Docs
author: microsoft
description: ASP.NET 페이지 들어 컨트롤과 extender를 추가 하는 방법을 알아봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/12/2009
ms.topic: article
ms.assetid: 763650a9-ffde-46a9-b779-7a9145dd5d88
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-vb
msc.type: authoredcontent
ms.openlocfilehash: 080dd65677d80fb75ab37a20f6c385a38af4e353
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30873042"
---
<a name="using-ajax-control-toolkit-controls-and-control-extenders-vb"></a>AJAX 컨트롤 Toolkit 컨트롤 및 컨트롤 Extender (VB)를 사용 하 여
====================
by [Microsoft](https://github.com/microsoft)

> ASP.NET 페이지 들어 컨트롤과 extender를 추가 하는 방법을 알아봅니다.


들어 컨트롤 및 컨트롤 extender 집합이 포함 되어 있습니다. 이 간략 한 자습서를 ASP.NET 페이지에 컨트롤 및 컨트롤 extender를 모두 추가 하는 방법에 설명 합니다.

> [!NOTE] 
> 
> 에 대 한 들어를 설치 하 고 Visual Studio/Visual Web Developer 도구 상자에 들어 추가 참조 자습서 [들어 시작](get-started-with-the-ajax-control-toolkit-vb.md)합니다.


## <a name="using-ajax-control-toolkit-controls"></a>AJAX 컨트롤 Toolkit 컨트롤을 사용 하 여

들어 컨트롤은 일반적인 ASP.NET 제어와 마찬가지로 작동합니다. ASP.NET 페이지 도구 상자에서 컨트롤을 끌 수 있습니다. 디자인 뷰 또는 소스 뷰 페이지에 컨트롤을 추가할 수 있습니다.

들어에서 컨트롤을 사용 하는 경우 특별 한 요구 사항이 하나 있습니다. 페이지에 ScriptManager 컨트롤을 포함 해야 합니다. ScriptManager 컨트롤은 모든 들어 컨트롤에 필요한 필요한 JavaScript를 포함 하는 것에 대 한 합니다.

예를 들어 들어 탭은 편집기 컨트롤 이라는 컨트롤을 포함 합니다. 이 컨트롤은 서식 있는 HTML 편집기를 표시 합니다. 페이지에는 편집기 컨트롤을 추가 하려면 다음이 단계를 수행 합니다.

1. ShowEditor.aspx 이라는 새 ASP.NET 페이지 만들기
2. 도구 상자에서 AJAX 확장 탭 아래 ScriptManager 컨트롤을 선택 하 고 컨트롤을 페이지로 끕니다.
3. 도구 상자에서 들어 탭 아래 편집기 컨트롤을 선택 하 고 컨트롤을 페이지로 끌어 (그림 1 참조). 디자이너는 그림 2와 같아야 합니다.
4. 메뉴 옵션을 선택 하 여 웹 사이트를 실행 **디버그, 디버깅 시작** 또는 F5 키를 방문 합니다.
5. 그림 3에 페이지가 나타납니다.


[![HTML 편집기 컨트롤 선택](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image1.png)

**그림 01**: HTML 편집기 컨트롤을 선택 하면 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.png))


[![ScriptManager 및 편집 컨트롤과 visual Studio 디자이너](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.png)

**그림 02**: ScriptManager 및 편집 컨트롤과 Visual Studio 디자이너 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.png))


[![DisplayEditor.aspx 페이지](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.png)

**그림 03**: The DisplayEditor.aspx 페이지 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.png))


## <a name="using-ajax-control-toolkit-control-extenders"></a>AJAX 컨트롤 Toolkit 컨트롤 Extender를 사용 하 여

또한 들어 extender 컨트롤을 포함합니다. 해당 이름에서 알 수 있듯이 컨트롤 extender는 기존 컨트롤의 기능을 확장 합니다. 예를 들어 ConfirmButton 컨트롤 extender 표준 ASP.NET Button 컨트롤을 확장합니다. Extender는 단추 클릭 하면 확인 대화 상자를 표시 하도록 단추 컨트롤의 동작을 변경 합니다.

들어 제어와 마찬가지로 컨트롤 extender에는 ScriptManager 컨트롤이 필요 합니다. Extender 컨트롤을 사용 하 여 페이지에서를 시작 하기 전에 페이지에 ScriptManager 컨트롤을 추가 해야 합니다.

ConfirmButton 컨트롤 extender를 사용 하려면 다음이 단계를 수행 합니다.

1. ShowConfirmButton.aspx 이라는 새 ASP.NET 페이지 만들기
2. AJAX 확장 탭 아래 페이지에 컨트롤을 끌어 페이지에 ScriptManager 컨트롤을 추가 합니다.
3. 도구 상자는 디자이너 화면에서 표준 탭 아래 단추를 끌어 페이지에 표준 단추 컨트롤을 추가 합니다.
4. 클릭는 **Extender 추가** 작업 옵션 (그림 4 참조).
5. Extender 선택 대화 상자에서 ConfirmButtonExtender 선택 (그림 5 참조) 확인 단추를 클릭 합니다.
6. 디자이너에서 단추 컨트롤을 선택 하 고 Button1 Extender 확장\_속성 창에서 ConfirmButtonExtender 노드 (그림 6 참조). 값을 할당 *실제로?* ConfirmText 속성에 있습니다.
7. 메뉴 옵션을 선택 하 여 페이지를 실행 **디버그, 디버깅 시작** 또는 F5 키를 누릅니다.


[![Extender 추가 작업 옵션](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.png)

**그림 04**: Extender 추가 작업 옵션 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image8.png))


[![ConfirmButton 컨트롤 extender를 선택합니다.](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image9.png)

**그림 05**: ConfirmButton 컨트롤 extender를 선택 하면 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image10.png))


[![ConfirmButton 속성 설정](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image11.png)

**그림 06**: ConfirmButton 속성 설정 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image12.png))


페이지가 열릴 때 단추를 표시 되어야 합니다. 단추를 클릭할 경우 그림 7에 확인 대화 상자를 가져옵니다.


[![확인 대화 상자를 표시합니다.](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image13.png)

**그림 07**: 확인 대화 상자 표시 ([전체 크기 이미지를 보려면 클릭](using-ajax-control-toolkit-controls-and-control-extenders-vb/_static/image14.png))


일반적으로 끌어 오지 않은 컨트롤 extender 페이지를 확인 합니다. 대신, 사용 하 여는 **Extender 추가** extender 컨트롤을 추가 하는 페이지에 이미 추가 옵션을 작업 합니다. 또한 설정한 컨트롤 extender 속성을 확장 하 고 컨트롤에 대 한 속성 시트를 열어 확인할 수 있습니다.

여러 컨트롤 extender에서 단일 ASP.NET 컨트롤을 확장할 수 있습니다. 확장 하 고 컨트롤에 대 한 속성 시트 컨트롤에 연결 된 컨트롤 extender의 모든 나열 됩니다.

> [!div class="step-by-step"]
> [이전](get-started-with-the-ajax-control-toolkit-vb.md)
> [다음](creating-a-custom-ajax-control-toolkit-control-extender-vb.md)
