---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
title: 유효성 검사 컨트롤 (C#) TextBoxWatermark 사용 | Microsoft Docs
author: wenz
description: 들어에서 TextBoxWatermark 컨트롤 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다. 상자에는 사용자가 클릭할 때 그 i...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: d49940cb-d38c-456a-b800-5f0eb705d09f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: b5cc7974f3444b54770cba54b991aab7b103f753
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868882"
---
<a name="using-textboxwatermark-with-validation-controls-c"></a>TextBoxWatermark를 사용 하 여 유효성 검사 컨트롤 (C#)
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)

> 들어에서 TextBoxWatermark 컨트롤 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다. 상자에 사용자가 클릭, 비어 있습니다. 사용자가 상자 텍스트를 입력 하지 않고를 완료 하는 경우에 미리 채워진된 텍스트 다시 나타납니다. ASP.NET 유효성 검사 컨트롤 같은 페이지에이 충돌할 수 있습니다 하지만 이러한 문제를 해결할 수 있습니다.


## <a name="overview"></a>개요

`TextBoxWatermark` 들어에서 컨트롤 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다. 상자에 사용자가 클릭, 비어 있습니다. 사용자가 상자 텍스트를 입력 하지 않고를 완료 하는 경우에 미리 채워진된 텍스트 다시 나타납니다. ASP.NET 유효성 검사 컨트롤 같은 페이지에이 충돌할 수 있습니다 하지만 이러한 문제를 해결할 수 있습니다.

## <a name="steps"></a>단계

샘플의 기본 설정에는 다음과 같습니다:는 `TextBox` 제어를 사용 하 여 워터은 `TextBoxWatermarkExtender` 제어 합니다. 다시 게시를 트리거한 다음 단추는 나중에 트리거하는 데 사용할 페이지에서 유효성 검사 컨트롤. 또한 한 `ScriptManager` 컨트롤은 ASP.NET AJAX를 초기화 하는 데 필요 합니다.

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample1.aspx)]

이제 추가 `RequiredFieldValidator` 있는지 여부를 확인 텍스트 필드에 폼이 전송 될 때 제어 합니다. `InitialValue` 유효성 검사기의 속성에 사용 되는 동일한 값으로 설정 해야 합니다는 `TextBoxWatermarkExtender` 제어: 폼이 전송 변경 되지 않은 입력란의 값은 그 안에 워터 마크 값:

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample2.aspx)]

그러나이 방법을 사용 하는 한 가지 문제는: 클라이언트는 JavaScript를 비활성화, 텍스트 필드 하지 미리 채워지는 워터 마크 텍스트로 따라서는 `RequiredFieldValidator` 오류 메시지를 트리거하지 않습니다. 따라서 두 번째 `RequiredFieldValidator` 컨트롤입니다. 필요한 빈 텍스트 상자에 대 한 확인 (생략 된 `InitialValue` 특성).

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample3.aspx)]

두 유효성 검사기를 사용 하므로 `Display` = `"Dynamic"`, 최종 사용자는 두 명의 유효성 검사기 중 어떤 발생 시각적 모양에서 구분할 수 없습니다; 대신, 것 같습니다. 둘 중 하나만 있습니다.

마지막으로 없는 유효성 검사기는 오류 메시지를 발급 하는 경우 필드의 텍스트를 출력 하는 서버 쪽 코드를 추가 합니다.

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample4.aspx)]


[![유효성 검사기 불만 없는 텍스트 필드에 있다는 것을 표시합니다](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)

유효성 검사기 필드에 텍스트가 불만 ([전체 크기 이미지를 보려면 클릭](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](using-textboxwatermark-in-a-formview-cs.md)
> [다음](using-textboxwatermark-in-a-formview-vb.md)
