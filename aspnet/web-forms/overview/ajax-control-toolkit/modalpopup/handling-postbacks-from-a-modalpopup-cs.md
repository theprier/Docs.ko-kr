---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
title: (C#) ModalPopup에서 포스트백 처리 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. Pos 때 특별히 주의 해야 하는 중...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: 7963890b-4ea3-4a1c-b65d-6098a3d56f62
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 0f27d28b9851f8e26c207a6bc495e98ad70577a2
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37838124"
---
<a name="handling-postbacks-from-a-modalpopup-c"></a>(C#) ModalPopup에서 포스트백 처리
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)

> AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 팝업 내에서 다시 게시를 만들 때 특별히 주의 해야 합니다.


## <a name="overview"></a>개요

AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 팝업 내에서 다시 게시를 만들 때 특별히 주의 해야 합니다.

## <a name="steps"></a>단계

ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample1.aspx)]

다음으로 모달 팝업으로 사용 되는 패널을 추가 합니다. 사용자 이름 및 전자 메일 주소를 입력할 수 있습니다. 단추 정보를 저장 하 고 팝업을 닫습니다 됩니다. `OnClick` 특성을 설정 하 여 포스트백이이 단추를 클릭할 때 발생 합니다.

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample2.aspx)]

정확히 동일한 정보에 대 한 두 레이블의 페이지 자체 구성 됩니다: 이름 및 전자 메일 주소입니다. 모달 팝업을 트리거할 단추 사용 됩니다.

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample3.aspx)]

팝업 표시를 하려면 추가 `ModalPopupExtender` 제어 합니다. 설정 된 `PopupControlID` 패널의 id 특성 및 `TargetControlID` 단추의 id:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample4.aspx)]

이제 때마다 합니다 `Save` 모달 팝업 내의 단추 서버 쪽 `SaveData()` 메서드를 실행 합니다. 여기에서 데이터 저장소에 입력 된 데이터를 저장할 수 있습니다. 간단히 하기 위해 새 데이터 레이블에 출력만:

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample5.cs)]

또한 현재 이름 및 전자 메일을 사용 하 여 모달 팝업에 textbox 컨트롤이 채워야 합니다. 그러나는 필요한 경우에 포스트백이 발생 합니다. 다시 게시 인 경우 ASP.NET viewstate 기능을 자동으로 적절 한 값을 사용 하 여 텍스트 상자를 채웁니다.

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample6.cs)]


[![모달 팝업은 포스트백을 발생 시키는](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)

모달 팝업은 포스트백을 발생 시키는 ([클릭 하 여 큰 이미지 보기](handling-postbacks-from-a-modalpopup-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](using-modalpopup-with-a-repeater-control-cs.md)
> [다음](positioning-a-modalpopup-cs.md)
