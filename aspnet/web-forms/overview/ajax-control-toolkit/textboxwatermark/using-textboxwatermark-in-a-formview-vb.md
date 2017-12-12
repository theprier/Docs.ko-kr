---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
title: "TextBoxWatermark FormView (VB)에서 사용 하 여 | Microsoft Docs"
author: wenz
description: "들어에서 TextBoxWatermark 컨트롤 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다. 상자에는 사용자가 클릭할 때 그 i..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 41497361-7fba-4825-b36c-f58d79522a88
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
msc.type: authoredcontent
ms.openlocfilehash: ad75d9729c068f7d512cf076b2ae156291fe76ec
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-textboxwatermark-in-a-formview-vb"></a>TextBoxWatermark FormView (VB)에서 사용 하 여
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1VB.pdf)

> 들어에서 TextBoxWatermark 컨트롤 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다. 상자에 사용자가 클릭, 비어 있습니다. 사용자가 상자 텍스트를 입력 하지 않고를 완료 하는 경우에 미리 채워진된 텍스트 다시 나타납니다. FormView 컨트롤 내에서 가능한 이기도합니다.


## <a name="overview"></a>개요

`TextBoxWatermark` 들어에서 컨트롤 텍스트 상자 내에서 표시 되도록 입력란을 확장 합니다. 상자에 사용자가 클릭, 비어 있습니다. 사용자가 상자 텍스트를 입력 하지 않고를 완료 하는 경우에 미리 채워진된 텍스트 다시 나타납니다. 내에서 가능한 이기도 한 `FormView` 제어 합니다.

## <a name="steps"></a>단계

첫째, 데이터 소스는 필요 합니다. 이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다. 데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며에서 별도 다운로드로 제공 됩니다 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)합니다. AdventureWorks 데이터베이스의 SQL Server 2005 예제 및 예제 데이터베이스의 일부인 (다운로드에서 [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Microsoft SQL Server Management Studio Express를 사용 하는 데이터베이스를 설정 하는 가장 쉬운 방법은 ([https://www.microsoft.com/downloads/details.aspx? FamilyID c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796 =&amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.

이 샘플에 대 한 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다. 설정에 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.

ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample1.aspx)]

그런 다음 데이터 원본을 지 원하는 페이지에 추가 `DELETE`, `INSERT` 및 `UPDATE` SQL 문입니다. Visual Studio 도우미를 데이터 소스를 만드는 데 사용 하는 경우 유의 현재 버전의 버그 테이블 이름이 붙지 않습니다 (`Vendor`)와 `Purchasing`합니다. 다음 태그를 올바른 구문을 보여 줍니다.

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample2.aspx)]

이름을 기억할 (`ID`)에 사용 되므로 데이터 원본의 `DataSourceID` 의 속성은 `FormView` 제어 합니다. `<InsertItemTemplate>` 의 섹션은 `FormView` 포함 하 여 확장 된 텍스트 상자는 `TextBoxWatermarkExtender` 제어 합니다. Extender 있는 템플릿의 범위를 벗어나지 않고 있는지 확인 합니다.

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample3.aspx)]

이제 변경 될 때 사용자의 삽입 모드로 `FormView` 컨트롤, 텍스트 필드에 감사 드립니다 미리 채워지는 새 공급 업체는 `TextBoxWatermarkExtender` 컨트롤입니다. 한 번의 클릭 하 고 입력란 내의 필러 텍스트를 사라질 수 있습니다.


[![Extender에서 제공 되는 필드에서 워터 마크](using-textboxwatermark-in-a-formview-vb/_static/image2.png)](using-textboxwatermark-in-a-formview-vb/_static/image1.png)

Extender에서 제공 되는 필드에서 워터 마크 ([전체 크기 이미지를 보려면 클릭](using-textboxwatermark-in-a-formview-vb/_static/image3.png))

>[!div class="step-by-step"]
[이전](using-textboxwatermark-with-validation-controls-cs.md)
[다음](using-textboxwatermark-with-validation-controls-vb.md)
