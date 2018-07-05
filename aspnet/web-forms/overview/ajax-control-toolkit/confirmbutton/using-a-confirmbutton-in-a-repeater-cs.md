---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
title: (C#) Repeater에 ConfirmButton 사용 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 ConfirmButton extender 만듭니다 Yes/사용자가 단추를 클릭할 때 팝업 없습니다 (LinkButton 컨트롤 포함). 경우에만 예는...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: a973ed3e-400c-4925-ace2-0b086b479301
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
msc.type: authoredcontent
ms.openlocfilehash: d3706578427442a7a1034596bdd9bd89eecf5f67
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37369753"
---
<a name="using-a-confirmbutton-in-a-repeater-c"></a>(C#) Repeater에 ConfirmButton 사용
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1CS.pdf)

> AJAX Control Toolkit의 ConfirmButton extender 만듭니다 Yes/사용자가 단추를 클릭할 때 팝업 없습니다 (LinkButton 컨트롤 포함). 만 예는 단추를 클릭 하면 단추의 작업 취소 그렇지 않은 경우 실행 됩니다. Repeater에는이 가능합니다.


## <a name="overview"></a>개요

AJAX Control Toolkit의 ConfirmButton extender 만듭니다 Yes/사용자가 단추를 클릭할 때 팝업 없습니다 (LinkButton 컨트롤 포함). 만 예는 단추를 클릭 하면 단추의 작업 취소 그렇지 않은 경우 실행 됩니다. Repeater에는이 가능합니다.

## <a name="steps"></a>단계

첫째, 데이터 소스는 필요 합니다. 이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다. 데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며 아래에 있는 별도 다운로드로도 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다. AdventureWorks 데이터베이스의 SQL Server 2005 샘플 및 예제 데이터베이스의 일부인 (에서 다운로드할 [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). 데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express를 사용 하는 것 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.

이 샘플에서는 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다. 설정이 다른 경우에 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.

ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample1.aspx)]

그런 다음 데이터 소스는 필요 합니다. 간단히 하기 위해 AdventureWorks의 공급 업체 테이블의 처음 5 개 항목만 검색 됩니다. Visual Studio 마법사를 사용 하 여 데이터 원본에 테이블 이름을 만들려면 때 (`Vendors`)은 현재 올바르게로 시작 하지 않는 `Purchasing`합니다. 다음 태그는 올바른 것 같습니다.

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample2.aspx)]

Repeater 내에서이 데이터 원본을 사용할 수 있습니다. 일반적으로 `DataBinder.Eval()` 메서드 데이터 원본에서 데이터를 검색 합니다. 합니다 `ConfirmButtonExtender` 컨트롤 내에 다음 배치 해야 합니다는 `<ItemTemplate>` 데이터 소스의 모든 항목에 대 한 표시 되도록 반복기 섹션입니다.

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample3.aspx)]


[![데이터 원본의 각 항목 옆에 있는 확인 단추를 표시 됩니다.](using-a-confirmbutton-in-a-repeater-cs/_static/image2.png)](using-a-confirmbutton-in-a-repeater-cs/_static/image1.png)

데이터 원본의 각 항목 옆에 있는 확인 단추를 표시 됩니다 ([클릭 하 여 큰 이미지 보기](using-a-confirmbutton-in-a-repeater-cs/_static/image3.png))

> [!div class="step-by-step"]
> [다음](using-a-confirmbutton-in-a-repeater-vb.md)
