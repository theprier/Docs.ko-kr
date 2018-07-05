---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
title: Repeater 컨트롤 (C#)에 ModalPopup 사용 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 이 contr.를 사용 하는 것도 가능...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: d686d84a-1c58-492e-8a77-3eb5a0cfe918
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 7e6136bac48b7c1b0931cada66501d303be8e927
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37371079"
---
<a name="using-modalpopup-with-a-repeater-control-c"></a>Repeater 컨트롤 (C#)에 ModalPopup 사용
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2CS.pdf)

> AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. Repeater 내에서이 컨트롤을 사용 하는 것도 가능 합니다.


## <a name="overview"></a>개요

AJAX Control Toolkit의 ModalPopup 컨트롤 클라이언트 쪽 의미를 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. Repeater 내에서이 컨트롤을 사용 하는 것도 가능 합니다.

## <a name="steps"></a>단계

첫째, 데이터 소스는 필요 합니다. 이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다. 데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며 아래에 있는 별도 다운로드로도 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다. AdventureWorks 데이터베이스의 SQL Server 2005 샘플 및 예제 데이터베이스의 일부인 (에서 다운로드할 [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). 데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express를 사용 하는 것 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다. 이 샘플에서는 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다. 설정이 다른 경우에 데이터베이스에 대 한 연결 정보를 조정 해야 합니다. ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample1.aspx)]

그런 다음 페이지에 데이터 소스를 추가 합니다. 제한 된 양의 데이터를 사용 하려면만 선택 처음 5 개 항목을 AdventureWorks 데이터베이스의 Vendor 테이블의 합니다. Visual Studio 도우미를 데이터 소스를 만드는 데 사용 하는 경우 고려해 현재 버전의 버그로 테이블 이름 접두사 하지 않습니다 (`Vendor`)와 `Purchasing`합니다. 다음 태그에서는 올바른 구문을 보여 줍니다.

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample2.aspx)]

다음으로 모달 팝업으로 사용 되는 패널을 추가 합니다. 포함을 `Button` 컨트롤을 다시 팝업을 닫습니다.

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample3.aspx)]

팝업, 반복기 내에서 작업할 수 있도록 합니다 `ModalPopupExtender` 내에서 설정 해야 하는 컨트롤을 `<ItemTemplate>` 반복기 섹션. 따라서 패널 repeater, 외부 이지만 extender가 내부. 반복기에 대 한 태그는 다음과 같습니다.

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample4.aspx)]

그런 다음 데이터 원본에 있는 모든 항목은 모달 팝업을 트리거하는 옆에 있는 단추를 사용 하 여 표시 됩니다.


[![모든 데이터 원본 항목에 대 한 모달 팝업을 트리거할 수 있습니다.](using-modalpopup-with-a-repeater-control-cs/_static/image2.png)](using-modalpopup-with-a-repeater-control-cs/_static/image1.png)

모든 데이터 원본 항목에 대 한 모달 팝업을 트리거할 수 있습니다 ([클릭 하 여 큰 이미지 보기](using-modalpopup-with-a-repeater-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](launching-a-modal-popup-window-from-server-code-cs.md)
> [다음](handling-postbacks-from-a-modalpopup-cs.md)
