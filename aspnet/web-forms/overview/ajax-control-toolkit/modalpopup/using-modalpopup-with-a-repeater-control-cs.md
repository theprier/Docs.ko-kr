---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
title: 반복기 컨트롤 (C#) ModalPopup 사용 | Microsoft Docs
author: wenz
description: 들어에서 ModalPopup 컨트롤을 클라이언트 쪽 방법을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 이 contr.를 사용 하는 것도 가능...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: d686d84a-1c58-492e-8a77-3eb5a0cfe918
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/using-modalpopup-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 7124ca3fc346d78c3b235d1756695b008afb47aa
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30872948"
---
<a name="using-modalpopup-with-a-repeater-control-c"></a>반복기 컨트롤 (C#) ModalPopup 사용
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup2.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup2CS.pdf)

> 들어에서 ModalPopup 컨트롤을 클라이언트 쪽 방법을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 도 한 반복기 내에서이 컨트롤을 사용 하는 것이 가능 합니다.


## <a name="overview"></a>개요

들어에서 ModalPopup 컨트롤을 클라이언트 쪽 방법을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 도 한 반복기 내에서이 컨트롤을 사용 하는 것이 가능 합니다.

## <a name="steps"></a>단계

첫째, 데이터 소스는 필요 합니다. 이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다. 데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며에서 별도 다운로드로 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다. AdventureWorks 데이터베이스의 SQL Server 2005 예제 및 예제 데이터베이스의 일부인 (다운로드에서 [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e &amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Microsoft SQL Server Management Studio Express를 사용 하는 가장 쉬운 방법은 데이터베이스를 설정 하는 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다. 이 샘플에 대 한 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다. 설정에 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다. ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample1.aspx)]

페이지 데이터 소스를 추가 합니다. 제한 된 양의 데이터를 사용 하려면만 선택 처음 5 개 항목 AdventureWorks 데이터베이스의 Vendor 테이블에 있습니다. Visual Studio 도우미를 데이터 소스를 만드는 데 사용 하는 경우 유의 현재 버전의 버그 테이블 이름이 붙지 않습니다 (`Vendor`)와 `Purchasing`합니다. 다음 태그를 올바른 구문을 보여 줍니다.

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample2.aspx)]

다음으로 모달 팝업으로 사용 되는 패널을 추가 합니다. 포함 된 `Button` 컨트롤을 다시 여 팝업을 닫습니다.

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample3.aspx)]

팝업 반복기, 내에서 작업할 수 있도록는 `ModalPopupExtender` 컨트롤 내에 배치 해야 합니다는 `<ItemTemplate>` 반복기의 섹션입니다. 따라서 패널 반복 벗어나지만 extender는 내부에 있습니다. 반복기에 대 한 태그는 다음과 같습니다.

[!code-aspx[Main](using-modalpopup-with-a-repeater-control-cs/samples/sample4.aspx)]

그런 다음 데이터 원본에 있는 모든 항목은 모달 팝업을 트리거하는 단추를 클릭 함께 표시 됩니다.


[![모든 데이터 원본 항목에 대 한 모달 팝업을 트리거할 수 있습니다.](using-modalpopup-with-a-repeater-control-cs/_static/image2.png)](using-modalpopup-with-a-repeater-control-cs/_static/image1.png)

모든 데이터 원본 항목에 대 한 모달 팝업을 트리거할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](using-modalpopup-with-a-repeater-control-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](launching-a-modal-popup-window-from-server-code-cs.md)
> [다음](handling-postbacks-from-a-modalpopup-cs.md)
