---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
title: 끌어서 놓기 ReorderList (C#)를 통해 | Microsoft Docs
author: wenz
description: 끌어 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 하는 들어에서 ReorderList 컨트롤입니다. 목록의 현재 순서는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 6350ee8e-11d6-4aff-b51c-942878014835
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 42464d10f119e0ba51d5eebf2a67e76e3e419bda
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30873458"
---
<a name="drag-and-drop-via-reorderlist-c"></a>끌어 놓기를 통해 ReorderList (C#)
====================
으로 [Christian Wenz](https://github.com/wenz)

[코드를 다운로드](http://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)

> 끌어 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 하는 들어에서 ReorderList 컨트롤입니다. 서버에서 목록의 현재 순서를 유지 해야 합니다.


## <a name="overview"></a>개요

`ReorderList` 들어에서 컨트롤 끌어 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다. 서버에서 목록의 현재 순서를 유지 해야 합니다.

## <a name="steps"></a>단계

`ReorderList` 컨트롤은 목록에는 데이터베이스에서 데이터 바인딩 지원 합니다. 무엇 보다도 작성 변경 내용을 데이터 저장소 목록 요소 순서와 지원합니다.

이 샘플에서는 데이터 저장소로 Microsoft SQL Server 2005 Express Edition을 사용 합니다. 데이터베이스에는 express edition을 포함 하는 Visual Studio 설치의 선택 사항 (및 무료) 부분입니다. 별도 다운로드로 제공 됩니다 [ https://go.microsoft.com/fwlink/?LinkId=64064 ](https://go.microsoft.com/fwlink/?LinkId=64064)합니다. 이 샘플에 대 한 SQL Server 2005 Express Edition 인스턴스 라고 가정 `SQLEXPRESS` 웹 서버와 동일한 컴퓨터에 상주 하 고 기본 설정 이기도 합니다. 설정에 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.

Microsoft SQL Server Management Studio Express를 사용 하는 데이터베이스를 설정 하는 가장 쉬운 방법은 ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;4a83-b309-53b7b77edf78&displaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) ). 서버에 연결, 두 번 클릭 `Databases` 새 데이터베이스를 만듭니다 (마우스 오른쪽 단추로 클릭 하 고 선택 `New Database`) 라는 `Tutorials`합니다.

이 데이터베이스에서 라는 새 테이블을 만듭니다 `AJAX` 다음 4 개의 열을 포함 합니다.

- `id` (기본 키, 정수 id에 NULL이 아님)
- `char` (char(1), NULL)
- `description` (varchar(50), NULL)
- `position` (int, NULL)


[![AJAX 테이블의 레이아웃](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)

AJAX 테이블의 레이아웃 ([전체 크기 이미지를 보려면 클릭](drag-and-drop-via-reorderlist-cs/_static/image3.png))


그런 다음 몇 개 값으로 테이블을 채웁니다. `position` 열 요소의 정렬 순서를 보유 합니다.


[![AJAX 테이블의 초기 데이터](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)

AJAX 테이블의 데이터를 초기 ([전체 크기 이미지를 보려면 클릭](drag-and-drop-via-reorderlist-cs/_static/image6.png))


다음 단계를 생성 하는 데 필요한 프로그램 `SqlDataSource` 새 데이터베이스 및 테이블에 맞게와 통신 하는 컨트롤입니다. 데이터 소스를 지원 해야 합니다는 `SELECT` 및 `UPDATE` SQL 명령입니다. 목록 요소의 순서를 나중에 변경 하는 경우는 `ReorderList` 컨트롤 데이터 원본에 두 값을 자동으로 전송 `Update` 명령: 새 위치와 요소의 ID입니다. 따라서 데이터 원본 요구는 `<UpdateParameters>` 이 두 값에 대 한 섹션:

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

`ReorderList` 컨트롤이 다음 특성을 설정 해야 합니다.

- `AllowReorder`: 여부 목록 항목 수 있습니다.를 다시 정렬할 수
- `DataSourceID`: 데이터 원본 ID
- `DataKeyField`: 데이터 원본에 기본 키 열 이름
- `SortOrderField`목록 항목에 대 한 정렬 순서를 제공 하는 데이터 원본 열:

에 `<DragHandleTemplate>` 및 `<ItemTemplate>` 섹션 목록의 레이아웃 미세 조정할 수 있습니다. 데이터 바인딩 가능한은 또한를 사용 하는 `Eval()` 메서드를 다음 그림과 같이:

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

다음 CSS 스타일 정보 (에서 참조 되는 `<DragHandleTemplate>` 의 섹션은 `ReorderList` 컨트롤) 마우스 포인터가 적절 하 게 위에서 끌기 핸들 이동할 때 하면:

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

마지막으로, 한 `ScriptManager` 컨트롤 페이지에 대 한 ASP.NET AJAX를 초기화 합니다.

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

브라우저에서이 예제를 실행 하 고 약간 목록 항목 다시 정렬 합니다. 그런 다음 페이지를 다시 로드 및/또는 데이터베이스를 확인 합니다. 변경 된 위치 유지 관리 되었는지와 값을 기준으로 반영 됩니다는 `position` 는 데이터베이스에서 열 코드, 없이 모든 태그를 사용 하 여 바로 합니다.


[![데이터가 새 목록 항목 순서에 따라 데이터베이스 변경](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)

새 목록에 따라 데이터베이스 변경에서의 데이터 항목 순서 ([전체 크기 이미지를 보려면 클릭](drag-and-drop-via-reorderlist-cs/_static/image9.png))

> [!div class="step-by-step"]
> [이전](using-postbacks-with-reorderlist-cs.md)
> [다음](using-postbacks-with-reorderlist-vb.md)
