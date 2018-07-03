---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-cs
title: DataList 컨트롤 (C#)를 사용 하 여 행 마다 여러 레코드 표시 | Microsoft Docs
author: rick-anderson
description: 이 간략 한 자습서에서는 해당 RepeatColumns 및 RepeatDirection 속성을 통해 DataList의 레이아웃을 사용자 지정 하는 방법을 살펴봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/13/2006
ms.topic: article
ms.assetid: cf5acaf5-d4f6-4957-badc-b89956b285f3
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 2655cceb799f70ae88fd84d96a2c1dc783768de9
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37402771"
---
<a name="showing-multiple-records-per-row-with-the-datalist-control-c"></a>DataList 컨트롤 (C#)를 사용 하 여 행 마다 여러 레코드 표시
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_31_CS.exe) 또는 [PDF 다운로드](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/datatutorial31cs1.pdf)

> 이 간략 한 자습서에서는 해당 RepeatColumns 및 RepeatDirection 속성을 통해 DataList의 레이아웃을 사용자 지정 하는 방법을 살펴봅니다.


## <a name="introduction"></a>소개

DataList 예제에서는 지난 두 자습서 에서처럼 ve 단일 열 HTML에 행으로 해당 데이터 소스에서 각 레코드를 렌더링 한 `<table>`합니다. DataList 기본적 이지만, 데이터 원본 항목을 여러 열과 다중 행이 테이블은 분산 되도록 DataList 표시를 사용자 지정 매우 쉽습니다. 또한 해당 데이터의 모든 가능한 원본 단일 행 및 다중 열 DataList에 표시 된 항목입니다.

DataList의 레이아웃을 통해 사용자 지정할 수는 `RepeatColumns` 및 `RepeatDirection` 각각 열 개수 렌더링 되 고 있는지 여부 해당 항목이 배치 되도록 가로 또는 세로로 표시 하는 속성입니다. 예를 들어, 그림 1에는 세 개의 열이 있는 테이블에서 제품 정보를 표시 하는 DataList 보여 줍니다.


[![DataList 행당 세 가지 제품을 보여 줍니다.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image2.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image1.png)

**그림 1**: The DataList 표시 제품이 행당 ([큰 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image3.png))


행당 여러 데이터 원본 항목을 표시 하면 DataList 가로 화면 공간을 보다 효과적으로 활용할 수 있습니다. 이 짧은 자습서에서는 이러한 두 DataList 속성을 살펴봅니다.

## <a name="step-1-displaying-product-information-in-a-datalist"></a>1 단계: DataList에서 제품 정보를 표시합니다.

살펴보기 전에 합니다 `RepeatColumns` 및 `RepeatDirection` 속성을 통해 s 먼저 만듭니다 DataList 표준 다중 행, 단일 열 테이블 레이아웃을 사용 하 여 제품 정보를 나열 하는 페이지입니다. 예를 들어 제품의 이름, 범주 및 다음 태그를 사용 하 여 가격을 표시 하는 s 수 있습니다.


[!code-html[Main](showing-multiple-records-per-row-with-the-datalist-control-cs/samples/sample1.html)]

에서는 ve 하므로 다음이 단계를 신속 하 게 이동 하겠습니다 이전 예에서 DataList에 데이터를 바인딩하는 방법을 표시 합니다. 열어서 시작 합니다 `RepeatColumnAndDirection.aspx` 페이지에 `DataListRepeaterBasics` 폴더 및 디자이너 도구 상자에서 끌어서 DataList 합니다. DataList s 스마트 태그에서 새 ObjectDataSource 만들고에서 해당 데이터를 가져오도록 구성 하도록 선택할 합니다 `ProductsBLL` s 클래스 `GetProducts` 메서드를 선택 (없음) s 삽입, 업데이트, 마법사에서 옵션 및 탭을 삭제 합니다.

Visual Studio에서 자동으로 만들고 새 ObjectDataSource DataList 바인딩 후 만듭니다는 `ItemTemplate` 각 제품 데이터 필드에 대 한 이름 및 값을 표시 하는 합니다. 조정 된 `ItemTemplate` 선언적 태그를 통해 직접 또는 템플릿 편집 옵션 DataList s 스마트 태그의 대체 위에 표시 된 태그를 사용 하는 *제품 이름*, *범주 이름* , 및 *가격* 적절 한 데이터 바인딩 구문을 사용 하 여 값을 할당 하는 레이블 컨트롤을 사용 하 여 텍스트 해당 `Text` 속성입니다. 업데이트 한 후를 `ItemTemplate`, s 페이지 선언적 태그는 다음과 유사 합니다.


[!code-aspx[Main](showing-multiple-records-per-row-with-the-datalist-control-cs/samples/sample2.aspx)]

통지를 ve의 형식 지정자를 포함 합니다 `Eval` 에 대 한 데이터 바인딩 구문을 `UnitPrice`, 통화로-반환된 된 값을 서식 지정 `Eval("UnitPrice", "{0:C}").`

시간을 내어 브라우저에서 페이지를 방문 합니다. 그림 2에서 알 수 있듯이, DataList 제품의 다중 행, 단일 열 테이블로 렌더링 합니다.


[![기본적으로 다중 행, 단일 열 테이블로 DataList 렌더링](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image5.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image4.png)

**그림 2**: 기본적으로, 단일 열을 다중 행 테이블으로 DataList 렌더링 ([큰 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image6.png))


## <a name="step-2-changing-the-datalist-s-layout-direction"></a>2 단계: DataList의 레이아웃 방향 변경

기본 동작 하는 동안 DataList 열과 다중 행이 단일 열 테이블에서에서 해당 항목을 레이아웃 하는 것이 동작은 쉽게 변경할 수 있습니다 DataList s 통해 [ `RepeatDirection` 속성](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatdirection.aspx)합니다. 합니다 `RepeatDirection` 속성의 두 가지 값 중 하나를 사용할 수 있습니다: `Horizontal` 또는 `Vertical` (기본값).

변경 하 여는 `RepeatDirection` 속성을 `Vertical` 에 `Horizontal`, DataList를 데이터 원본 항목 마다 하나의 열을 만드는 해당 레코드는 단일 행에 렌더링 합니다. 이 효과 보여 주기 위해 디자이너에서 DataList 클릭 한 다음 속성 창에서 변경 된 `RepeatDirection` 속성을 `Vertical` 에 `Horiztonal`입니다. 즉시이 작업을 수행 하면 디자이너 레이아웃 조정 합니다 DataList s, 단일 행 및 다중 열 인터페이스 만들기 (그림 3 참조).


[![RepeatDirection 속성 결정 하는 방법의 방향 DataList s 항목이 배치 아웃](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image8.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image7.png)

**그림 3**: 합니다 `RepeatDirection` 속성은 아웃 레이아웃 방향 DataList의 항목 하는 방법을 나타냅니다 ([클릭 하 여 큰 이미지 보기](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image9.png))


작은 양의 데이터를 단일 행을 표시 하는 경우 다중 열 테이블 화면 부동산을 최대화 하기 위한 이상적인 방법 수 있습니다. 그러나 더 큰 볼륨의 데이터를 단일 행을 여러 열을 푸시하는 해당 항목 오른쪽에 해제 화면에 맞게 해당 수 t 필요 합니다. 그림 4 제품을 단일 행 DataList 렌더링 되는 경우를 보여 줍니다. 여러 개의 제품 (80) 되므로 사용자 각 제품에 대 한 정보를 보려면 오른쪽 하단으로 떨어져 스크롤하여 해야 합니다.


[![충분히 큰 데이터 원본에 대 한 단일 열 DataList 가로 스크롤이 필요 합니다.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image11.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image10.png)

**그림 4**:에 대 한 충분히 큰 데이터 원본, 단일 열 DataList는 필요한 가로 스크롤 ([큰 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image12.png))


## <a name="step-3-displaying-data-in-a-multi-column-multi-row-table"></a>3 단계: 다중 열과 다중 행이 테이블에 데이터를 표시합니다.

여러 열과 다중 행 DataList를 만들려면 설정 해야 합니다 [ `RepeatColumns` 속성](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatcolumns.aspx) 표시할 열의 수입니다. 기본적으로 `RepeatColumns` 단일 행 또는 열에서 모든 해당 항목을 표시할 DataList 하면 0으로 설정 (값에 따라는 `RepeatDirection` 속성).

예를 들어 테이블 행당 세 가지 제품을 전시 s 수 있습니다. 따라서 설정 된 `RepeatColumns` 속성을 3으로 합니다. 이렇게 변경한 후 브라우저에서 결과 보려면 잠시 시간이 소요 됩니다. 그림 5에서 알 수 있듯이, 제품 이제 3 열과 다중 행 표에 나와 있습니다.


[![행당 제품이 표시 됩니다.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image14.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image13.png)

**그림 5**: 행당 제품이 표시 됩니다 ([큰 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image15.png))


`RepeatDirection` DataList 항목 레이아웃 되는 방법을 하는 속성에 영향을 줍니다. 그림 5는 사용 하 여 결과 `RepeatDirection` 속성이 설정 `Horizontal`합니다. 처음 세 개의 제품 Chai, 변경, 및 태양 체리 시럽 왼쪽에서 오른쪽, 위쪽에서 아래쪽 레이아웃 되 note 합니다. 다음 3 개 제품 (Chef 한 100의 케이준 Seasoning부터 시작) 아래에 있는 처음 3 개 행에 나타납니다. 그러나 변경 된 `RepeatDirection` 속성을 다시 `Vertical`, 이러한 제품은 위에서 아래로 레이아웃, 그림 6에서 볼 수 있듯이 왼쪽에서 오른쪽으로 합니다.


[![여기에서 제품은 세로로 배치 아웃](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image17.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image16.png)

**그림 6**: 여기에서 제품은 세로로 배치 아웃 ([큰 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image18.png))


결과 테이블에 표시 된 행 수가 DataList에 바인딩된 총 레코드 수에 따라 달라 집니다. 이 정확 하 게 최대 데이터 원본 항목의 총 수로 나눈 s는 `RepeatColumns` 속성 값입니다. 이후를 `Products` 테이블 현재 84 제품에는 3으로 나눌 수에 행이 28 개. 하는 경우 데이터 소스의 항목 수 및 `RepeatColumns` 속성 값을 나눌 수 없는 다음 마지막 행 또는 열에는 빈 셀을 갖습니다. 경우는 `RepeatDirection` 로 설정 된 `Vertical`, 마지막 열 경우; 빈 셀이 있어야 합니다 `RepeatDirection` 는 `Horizontal`, 마지막 행에 있는 빈 셀이 있어야 합니다.

## <a name="summary"></a>요약

DataList를 기본적으로 단일 templatefield로 사용 하 여 GridView의 레이아웃을 모방 하는 단일 열과 다중 행 테이블에서 해당 항목이 나열 됩니다. 이 기본 레이아웃을 적용할 수 있는 동안에 행당 여러 데이터 원본 항목을 표시 하 여 화면 부동산을 최대화할 수 있습니다 했습니다. 이 작업을 수행 하는 것은 s DataList를 설정 하는 단순히 `RepeatColumns` 행당 표시할 열의 수 속성입니다. 또한 DataList의 `RepeatDirection` 속성이 있는지 여부를 여러 열과 다중 행이 테이블의 내용을 배치 해야 가로로 왼쪽에서 오른쪽, 위쪽에서 아래쪽 또는 위쪽에서 아래쪽, 왼쪽에서 오른쪽 세로로 나타내는 데 사용할 수 있습니다.

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 John Suru 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](formatting-the-datalist-and-repeater-based-upon-data-cs.md)
> [다음](nested-data-web-controls-cs.md)
