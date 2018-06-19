---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
title: Accordion (VB)에 데이터 바인딩 | Microsoft Docs
author: wenz
description: 들어에서 Accordion 컨트롤 여러 창을 하며 한 번에 둘 중 하나를 표시할 수 있습니다. 일반적으로 패널 w 선언 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: b19f0875-7d3e-4ecf-baa1-a0c693c765b3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
msc.type: authoredcontent
ms.openlocfilehash: 0739e4ad263eb83f844a937eae4aa845df2f2593
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30869295"
---
<a name="databinding-to-an-accordion-vb"></a>Accordion (VB)에 데이터 바인딩
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)

> 들어에서 Accordion 컨트롤 여러 창을 하며 한 번에 둘 중 하나를 표시할 수 있습니다. 패널은 페이지 자체 내에서 일반적으로 선언 하지만 데이터 소스에 바인딩하지 더 많은 유연성을 제공 합니다.


## <a name="overview"></a>개요

들어에서 Accordion 컨트롤 여러 창을 하며 한 번에 둘 중 하나를 표시할 수 있습니다. 패널은 페이지 자체 내에서 일반적으로 선언 하지만 데이터 소스에 바인딩하지 더 많은 유연성을 제공 합니다.

## <a name="steps"></a>단계

첫째, 데이터 소스는 필요 합니다. 이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다. 데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며에서 별도 다운로드로 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다. AdventureWorks 데이터베이스의 SQL Server 2005 예제 및 예제 데이터베이스의 일부인 (다운로드에서 [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e &amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Microsoft SQL Server Management Studio Express를 사용 하는 가장 쉬운 방법은 데이터베이스를 설정 하는 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.

이 샘플에 대 한 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다. 설정에 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.

ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 제어 페이지에서 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample1.aspx)]

페이지 데이터 소스를 추가 합니다. 제한 된 양의 데이터를 사용 하려면만 선택 처음 5 개 항목 AdventureWorks 데이터베이스의 Vendor 테이블에 있습니다. Visual Studio 도우미를 데이터 소스를 만드는 데 사용 하는 경우 유의 현재 버전의 버그 테이블 이름이 붙지 않습니다 (`Vendor`)와 `Purchasing`합니다. 다음 태그를 올바른 구문을 보여 줍니다.

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample2.aspx)]

데이터 원본의 이름 (ID)를 기억 합니다. 이 매우 식별에 사용 해야 합니다는 `DataSourceID` Accordion 컨트롤의 속성:

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample3.aspx)]

Accordion 컨트롤 내에서 헤더를 포함 하는 컨트롤의 다양 한 부분에 대 한 서식 파일을 제공할 수 있습니다 (`<HeaderTemplate>`) 및 콘텐츠 (`<ContentTemplate>`). 이러한 요소 내에서 출력 하는 데이터에서 데이터 원본을 사용 하는 `DataBinder.Eval()` 메서드:

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample4.aspx)]

페이지가 로드 될 때 데이터 원본이 서버 쪽 코드로 accordion에 바인딩되어야 합니다.

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample5.aspx)]

이 샘플 되려면 Accordion 컨트롤에서 참조 되는 두 개의 CSS 클래스를 정의 해야 (속성만에서 `HeaderCssClass` 및 `ContentCssClass`). 다음 태그 모드로 `<head>` 페이지의 섹션:

[!code-css[Main](databinding-to-an-accordion-vb/samples/sample6.css)]


[![accordion의 데이터가 데이터 원본에서 직접 제공](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)

데이터 원본에서 직접는 accordion의 데이터를 가져옵니다 ([전체 크기 이미지를 보려면 클릭](databinding-to-an-accordion-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](dynamically-adding-an-accordion-pane-cs.md)
> [다음](dynamically-adding-an-accordion-pane-vb.md)
