---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
title: Accordion (C#)에 데이터 바인딩 | Microsoft Docs
author: wenz
description: AJAX Control Toolkit의 Accordion 컨트롤 여러 창을 제공 하 고 둘 중 한 번에 표시할 수 있습니다. 일반적으로 패널 w 선언 하는 중...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9c8f0054-e319-46f8-80c0-35b606d2fbd4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
msc.type: authoredcontent
ms.openlocfilehash: 930392bd33cfeb7dec52a6084a5d401a6134a7ef
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41839087"
---
<a name="databinding-to-an-accordion-c"></a>Accordion (C#)에 데이터 바인딩
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1CS.pdf)

> AJAX Control Toolkit의 Accordion 컨트롤 여러 창을 제공 하 고 둘 중 한 번에 표시할 수 있습니다. 패널은 일반적으로 페이지 자체 내에서 선언 하지만 데이터 소스에 바인딩하는 더 많은 유연성을 제공 합니다.


## <a name="overview"></a>개요

AJAX Control Toolkit의 Accordion 컨트롤 여러 창을 제공 하 고 둘 중 한 번에 표시할 수 있습니다. 패널은 일반적으로 페이지 자체 내에서 선언 하지만 데이터 소스에 바인딩하는 더 많은 유연성을 제공 합니다.

## <a name="steps"></a>단계

첫째, 데이터 소스는 필요 합니다. 이 샘플에서는 AdventureWorks 데이터베이스 및 Microsoft SQL Server 2005 Express Edition을 사용 합니다. 데이터베이스 (express edition 포함)는 Visual Studio 설치의 선택적 부분이 며 아래에 있는 별도 다운로드로도 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다. AdventureWorks 데이터베이스의 SQL Server 2005 샘플 및 예제 데이터베이스의 일부인 (에서 다운로드할 [ https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). 데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express를 사용 하는 것 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp; DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) 및 연결 된 `AdventureWorks.mdf` 데이터베이스 파일입니다.

이 샘플에서는 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다. 설정이 다른 경우에 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.

ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해 합니다 `ScriptManager` 컨트롤 페이지의 아무 곳 이나 배치 해야 합니다 (하지만 내는 `<form>` 요소):

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample1.aspx)]

그런 다음 페이지에 데이터 소스를 추가 합니다. 제한 된 양의 데이터를 사용 하려면만 선택 처음 5 개 항목을 AdventureWorks 데이터베이스의 Vendor 테이블의 합니다. Visual Studio 도우미를 데이터 소스를 만드는 데 사용 하는 경우 고려해 현재 버전의 버그로 테이블 이름 접두사 하지 않습니다 (`Vendor`)와 `Purchasing`합니다. 다음 태그에서는 올바른 구문을 보여 줍니다.

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample2.aspx)]

데이터 원본 이름 (ID)를 기억 합니다. 이 매우 식별에 사용 해야 합니다는 `DataSourceID` Accordion 컨트롤의 속성:

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample3.aspx)]

Accordion 컨트롤 내에서 헤더를 포함 하는 컨트롤의 다양 한 부분에 대 한 서식 파일을 제공할 수 있습니다 (`<HeaderTemplate>`) 및 콘텐츠 (`<ContentTemplate>`). 이러한 요소 내에서 출력 데이터의 데이터를 사용 하 여 소스를 `DataBinder.Eval()` 메서드:

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample4.aspx)]

페이지가 로드 될 때 데이터 원본은이 서버 쪽 코드를 사용 하 여 accordion에 바인딩되어야 합니다.

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample5.aspx)]

이 샘플 되려면 Accordion 컨트롤에서 참조 되는 두 개의 CSS 클래스를 정의 해야 (속성만에서 `HeaderCssClass` 고 `ContentCssClass`). 다음 태그 안에 `<head>` 페이지의 섹션:

[!code-css[Main](databinding-to-an-accordion-cs/samples/sample6.css)]


[![데이터 원본에서 직접 제공 되는 accordion에 데이터는](databinding-to-an-accordion-cs/_static/image2.png)](databinding-to-an-accordion-cs/_static/image1.png)

데이터 원본에서 직접 제공 되는 accordion에 데이터 ([클릭 하 여 큰 이미지 보기](databinding-to-an-accordion-cs/_static/image3.png))

> [!div class="step-by-step"]
> [다음](dynamically-adding-an-accordion-pane-cs.md)
