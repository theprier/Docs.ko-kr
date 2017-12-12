---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
title: "포스트백 ModalPopup (VB)에서 처리 | Microsoft Docs"
author: wenz
description: "들어에서 ModalPopup 컨트롤을 클라이언트 쪽 방법을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. Pos 때 특별히 주의 해야 합니다..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: f70ac2b3-900f-40fa-858f-ab057904506b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: 7915d555fef363f41aa51bd77f0183c97c2f3769
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="handling-postbacks-from-a-modalpopup-vb"></a>포스트백 ModalPopup (VB)에서 처리
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3VB.pdf)

> 들어에서 ModalPopup 컨트롤을 클라이언트 쪽 방법을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 팝업 내에서 다시 게시를 만들 때 특별히 주의 해야 합니다.


## <a name="overview"></a>개요

들어에서 ModalPopup 컨트롤을 클라이언트 쪽 방법을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 팝업 내에서 다시 게시를 만들 때 특별히 주의 해야 합니다.

## <a name="steps"></a>단계

ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample1.aspx)]

다음으로 모달 팝업으로 사용 되는 패널을 추가 합니다. 사용자 이름 및 전자 메일 주소를 입력할 수 있습니다. 팝업을 닫고 정보를 저장 하는 단추 사용 됩니다. `OnClick` 특성을 설정 하 여 포스트백이이 단추를 클릭할 때 발생 합니다.

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample2.aspx)]

페이지 자체 정확히 동일한 정보에 대 한 두 개의 레이블로 구성 됩니다: 이름 및 전자 메일 주소입니다. 모달 팝업을 트리거하는 단추 사용 됩니다.

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample3.aspx)]

팝업 표시를 확인 하기 위해 추가 된 `ModalPopupExtender` 제어 합니다. 설정의 `PopupControlID` 패널의 ID에 특성 및 `TargetControlID` 단추의 id:

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample4.aspx)]

이제 때마다는 `Save` 모달 팝업 내에서 단추를 클릭 하면 서버 쪽 `SaveData()` 메서드를 실행 합니다. 여기에 데이터 저장소에 입력 한 데이터를 저장할 수 있습니다. 간단한 설명을 위해 새 데이터 레이블을 출력 방금 되:

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample5.vb)]

또한 모달 팝업 내의 textbox 컨트롤의 현재 이름 및 전자 메일으로 채워야 합니다. 그러나는 필요한 경우에 포스트백에서 발생 합니다. 다시 게시 인 경우 ASP.NET viewstate 기능을 자동으로 해당 값을 갖는 텍스트 상자를 채웁니다.

[!code-vb[Main](handling-postbacks-from-a-modalpopup-vb/samples/sample6.vb)]


[![모달 팝업은 포스트백을 발생 시킵니다.](handling-postbacks-from-a-modalpopup-vb/_static/image2.png)](handling-postbacks-from-a-modalpopup-vb/_static/image1.png)

모달 팝업 포스트백 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-modalpopup-vb/_static/image3.png))

>[!div class="step-by-step"]
[이전](using-modalpopup-with-a-repeater-control-vb.md)
[다음](positioning-a-modalpopup-vb.md)
