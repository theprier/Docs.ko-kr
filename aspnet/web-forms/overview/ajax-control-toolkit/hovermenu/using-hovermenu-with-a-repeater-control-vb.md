---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
title: 반복기 컨트롤 (VB) HoverMenu 사용 | Microsoft Docs
author: wenz
description: 에 들어 HoverMenu 컨트롤은 간단한 팝업 효과 제공:는 specifi에 팝업이 표시 되는 마우스 포인터가 요소 위로 가져가면...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 7f07c112-cd4f-4427-9699-57cfab2791fd
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: aa107a7483683d965f3a510e6a43f174a386da0c
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30868401"
---
<a name="using-hovermenu-with-a-repeater-control-vb"></a>반복기 컨트롤 (VB) HoverMenu 사용
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1VB.pdf)

> 에 들어 HoverMenu 컨트롤은 간단한 팝업 효과 제공: 지정된 된 위치에서 팝업이 표시 되는 마우스 포인터가 요소 위로 가져가면 합니다. 도 한 반복기 내에서이 컨트롤을 사용 하는 것이 가능 합니다.


## <a name="overview"></a>개요

`HoverMenu` 들어에서 컨트롤은 간단한 팝업 효과 제공: 지정된 된 위치에서 팝업이 표시 되는 마우스 포인터가 요소 위로 가져가면 합니다. 도 한 반복기 내에서이 컨트롤을 사용 하는 것이 가능 합니다.

## <a name="steps"></a>단계

첫째, 데이터 소스는 필요 합니다. 이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다. 데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며에서 별도 다운로드로 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다. AdventureWorks 데이터베이스의 SQL Server 2005 예제 및 예제 데이터베이스의 일부인 (다운로드에서 [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e &amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Microsoft SQL Server Management Studio Express를 사용 하는 가장 쉬운 방법은 데이터베이스를 설정 하는 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.

이 샘플에 대 한 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다. 설정에 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.

ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample1.aspx)]

페이지 데이터 소스를 추가 합니다. 제한 된 양의 데이터를 사용 하려면만 선택 처음 5 개 항목 AdventureWorks 데이터베이스의 Vendor 테이블에 있습니다. Visual Studio 도우미를 데이터 소스를 만드는 데 사용 하는 경우 유의 현재 버전의 버그 테이블 이름이 붙지 않습니다 (`Vendor`)와 `Purchasing`합니다. 다음 태그를 올바른 구문을 보여 줍니다.

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample2.aspx)]

다음으로 모달 팝업으로 사용 되는 패널을 추가 합니다.

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample3.aspx)]

이제는 `HoverMenuExtender` 을 발휘 합니다. 반복기의 내 extender를 넣으십시오 수 있도록 데이터 소스에서 모든 요소는 자체 팝업, `<ItemTemplate>` 섹션. 다음은 태그입니다.

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample4.aspx)]

데이터 원본에 있는 모든 항목 오른쪽에는 팝업을 표시 하는 이제 (`PopupPosition` 특성) 50 밀리초의 지연 후 (`PopDelay` 특성).


[![반복기의 각 항목 옆에 호버 메뉴 표시](using-hovermenu-with-a-repeater-control-vb/_static/image2.png)](using-hovermenu-with-a-repeater-control-vb/_static/image1.png)

호버 메뉴 반복기의 각 항목 옆에 나타납니다 ([전체 크기 이미지를 보려면 클릭](using-hovermenu-with-a-repeater-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](using-hovermenu-with-a-repeater-control-cs.md)
