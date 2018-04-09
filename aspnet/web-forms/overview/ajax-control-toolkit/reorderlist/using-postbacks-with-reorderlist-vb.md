---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: 포스트백 ReorderList (VB)를 사용 하 여 | Microsoft Docs
author: wenz
description: 끌어 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 하는 들어에서 ReorderList 컨트롤입니다. 목록 순서를 변경할 때마다 po...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: ef43471f7d8cc94c1a82a368e27acef05f474f81
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="using-postbacks-with-reorderlist-vb"></a>포스트백을 사용 하 여 ReorderList (VB)으로
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)

> 끌어 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 하는 들어에서 ReorderList 컨트롤입니다. 목록 순서를 변경할 때마다이 포스트백은 변경의 서버를 알립니다.


## <a name="overview"></a>개요

`ReorderList` 들어에서 컨트롤 끌어 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다. 목록 순서를 변경할 때마다이 포스트백은 변경의 서버를 알립니다.

## <a name="steps"></a>단계

에 대 한 여러 가능한 데이터 소스는 `ReorderList` 제어 합니다. 하나 사용 하는 `XmlDataSource` 제어:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

이 XML을 바인딩하는 데는 `ReorderList` 제어를 사용 하도록 설정한 포스트백을 다음과 같은 특성을 설정 해야 합니다.

- `DataSourceID`: 데이터 원본 ID
- `SortOrderField`정렬 기준: 속성
- `AllowReorder`: 사용자는 목록 요소를 다시 정렬할 수 있도록 여부
- `PostBackOnReorder`: 목록 다시 정렬 될 때마다 다시 게시를 만들려면 여부

컨트롤에 대 한 적절 한 태그는 다음과 같습니다.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

내에서 `ReorderList` 컨트롤, 데이터 원본의 특정 데이터를 사용 하 여 바인딩할 수 있습니다는 `Eval()` 메서드:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

페이지에서 임의의 위치에서 마지막 다시 정렬 발생 했을 때 레이블을 정보가 보관 됩니다.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

이 레이블은 포스트백을 처리 하는 서버 쪽 코드의 텍스트도 채워집니다.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

마지막으로, ASP.NET AJAX 및 제어 Toolkit의 기능을 활성화 하는 데는 `ScriptManager` 페이지에 컨트롤을 배치 해야 합니다.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]


[![포스트백을 트리거합니다 각 순서 변경](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)

포스트백 트리거합니다 각 순서 변경 ([전체 크기 이미지를 보려면 클릭](using-postbacks-with-reorderlist-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](drag-and-drop-via-reorderlist-cs.md)
> [다음](drag-and-drop-via-reorderlist-vb.md)
