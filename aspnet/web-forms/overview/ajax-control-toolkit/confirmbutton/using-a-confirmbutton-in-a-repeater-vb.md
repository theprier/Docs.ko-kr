---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
title: "ConfirmButton 반복기 (VB)에서 사용 하 여 | Microsoft Docs"
author: wenz
description: "들어에서 ConfirmButton extender 만듭니다 Yes/사용자가 단추를 클릭할 때 없음 팝업 (LinkButton 컨트롤 포함). 경우에만 예는..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 18c31709-3f9d-4d93-8b01-f1356bf610b4
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: 5da8491c157ad6f35c2c25803680f262a35ce6e1
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-a-confirmbutton-in-a-repeater-vb"></a>ConfirmButton 반복기 (VB)에서 사용 하 여
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)

> 들어에서 ConfirmButton extender 만듭니다 Yes/사용자가 단추를 클릭할 때 없음 팝업 (LinkButton 컨트롤 포함). 만 예을 클릭할 경우 단추의 동작이 취소 그렇지 않은 경우 실행 됩니다. 반복기에서 가능한 이기도합니다.


## <a name="overview"></a>개요

들어에서 ConfirmButton extender 만듭니다 Yes/사용자가 단추를 클릭할 때 없음 팝업 (LinkButton 컨트롤 포함). 만 예을 클릭할 경우 단추의 동작이 취소 그렇지 않은 경우 실행 됩니다. 반복기에서 가능한 이기도합니다.

## <a name="steps"></a>단계

첫째, 데이터 소스는 필요 합니다. 이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다. 데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며에서 별도 다운로드로 제공 됩니다 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)합니다. AdventureWorks 데이터베이스의 SQL Server 2005 예제 및 예제 데이터베이스의 일부인 (다운로드에서 [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Microsoft SQL Server Management Studio Express를 사용 하는 데이터베이스를 설정 하는 가장 쉬운 방법은 ([https://www.microsoft.com/downloads/details.aspx? FamilyID c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796 =&amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.

이 샘플에 대 한 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다. 설정에 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.

ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample1.aspx)]

그런 다음 데이터 소스는 필요 합니다. 간단한 설명을 위해 AdventureWorks의 공급 업체 테이블의 처음 5 개 항목만 검색 됩니다. 데이터 소스 테이블 이름을 만들려면 Visual Studio 마법사를 사용할 때 (`Vendors`)가 현재 제대로로 시작 하지 않는 `Purchasing`합니다. 다음 태그는 가장 적합 합니다.

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample2.aspx)]

이 데이터 원본은 반복기 내에서 사용할 수 있습니다. 일반적으로 `DataBinder.Eval()` 메서드는 데이터 원본에서 데이터를 검색 합니다. `ConfirmButtonExtender` 다음 내에서 컨트롤을 배치 해야 합니다는 `<ItemTemplate>` 섹션 반복기에 대 한 데이터 원본에서 모든 항목에 표시 되도록 합니다.

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample3.aspx)]


[![데이터 원본의 각 항목 옆에 확인 단추 표시](using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)

확인 단추가 데이터 원본의 각 항목 옆에 나타납니다 ([전체 크기 이미지를 보려면 클릭](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png))

>[!div class="step-by-step"]
[이전](using-a-confirmbutton-in-a-repeater-cs.md)
