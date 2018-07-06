---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: (VB) ReorderList에 포스트백 사용 | Microsoft Docs
author: wenz
description: ReorderList 컨트롤이 AJAX Control Toolkit에서 끌어서 놓기를 통해 사용자에 의해 다시 정렬할 수 있는 목록을 제공 합니다. 목록 순서를 바꿀 때마다 po...
ms.author: aspnetcontent
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 20214db1c038f417944bd374bdaa8ce55d6d44aa
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37839001"
---
<a name="using-postbacks-with-reorderlist-vb"></a>(VB) ReorderList에 포스트백 사용
====================
[Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)

> ReorderList 컨트롤이 AJAX Control Toolkit에서 끌어서 놓기를 통해 사용자에 의해 다시 정렬할 수 있는 목록을 제공 합니다. 목록 순서를 바꿀 때마다 포스트백 됩니다 변경의 서버를 게 알립니다.


## <a name="overview"></a>개요

`ReorderList` AJAX Control Toolkit 컨트롤 끌어서 놓기를 통해 사용자에 의해 다시 정렬할 수 있는 목록을 제공 합니다. 목록 순서를 바꿀 때마다 포스트백 됩니다 변경의 서버를 게 알립니다.

## <a name="steps"></a>단계

에 대 한 몇 가지 가능한 데이터 원본이 `ReorderList` 제어 합니다. 하나를 사용 하는 것을 `XmlDataSource` 제어 합니다.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

이 XML을 바인딩하려면는 `ReorderList` 컨트롤과 사용 포스트백, 다음과 같은 특성을 설정 해야 합니다.

- `DataSourceID`데이터 원본 ID:
- `SortOrderField`정렬 기준: 속성
- `AllowReorder`: 목록 요소 순서를 변경 하려면 사용자 여부
- `PostBackOnReorder`: 목록 다시 정렬 됩니다 될 때마다 다시 게시를 만들려면 여부

컨트롤에 대 한 적절 한 태그는 다음과 같습니다.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

내 합니다 `ReorderList` 를 사용 하 여 컨트롤, 데이터 원본에서 특정 데이터를 바인딩할 수 있습니다는 `Eval()` 메서드:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

페이지에는 임의의 위치에서 마지막 재정렬 발생 했을 때 레이블을 정보가 보관 됩니다.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

이 레이블은 포스트백 처리 서버 쪽 코드에서 텍스트를 사용 하 여 채워집니다.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

마지막으로, ASP.NET AJAX와 Control Toolkit의 기능을 활성화 하기 위해는 `ScriptManager` 페이지에서 설정 해야 하는 컨트롤:

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]


[![포스트백 트리거 각 순서 변경](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)

각 다시 정렬 포스트백을 트리거합니다 ([클릭 하 여 큰 이미지 보기](using-postbacks-with-reorderlist-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](drag-and-drop-via-reorderlist-cs.md)
> [다음](drag-and-drop-via-reorderlist-vb.md)
