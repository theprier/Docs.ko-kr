---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-cs
title: "DataList 컨트롤 (C#)와 행당 여러 레코드를 보여 주는 | Microsoft Docs"
author: rick-anderson
description: "이 간단한 자습서 RepeatColumns 및 RepeatDirection 속성 DataList의 레이아웃을 사용자 지정 하는 방법을 살펴보겠습니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/13/2006
ms.topic: article
ms.assetid: cf5acaf5-d4f6-4957-badc-b89956b285f3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-cs
msc.type: authoredcontent
ms.openlocfilehash: be0b831477e8f68768f1f9a0b52cbe90b3936d3f
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="showing-multiple-records-per-row-with-the-datalist-control-c"></a>DataList 컨트롤 (C#)와 행당 여러 레코드를 표시합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_31_CS.exe) 또는 [PDF 다운로드](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/datatutorial31cs1.pdf)

> 이 간단한 자습서 RepeatColumns 및 RepeatDirection 속성 DataList의 레이아웃을 사용자 지정 하는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

DataList 예제에서는 지난 두 자습서에 했습니다 단일 열 HTML에 행으로 해당 데이터 원본의 각 레코드를 렌더링 한 `<table>`합니다. 기본 DataList 동작 이지만, 데이터 원본 항목은 여러 열, 다중 행 테이블에 분산 되도록 DataList 디스플레이 사용자 지정할 매우 쉽습니다. 또한 해당 데이터의 일부 가능한 s 원본 단일 행, 다중 열 DataList에 표시 된 항목입니다.

통해 DataList의 레이아웃을 사용자 지정할 수 있습니다는 `RepeatColumns` 및 `RepeatDirection` 속성 각각 열 개수 렌더링 되 고 가로 또는 세로로 해당 항목이 배치 되는 여부를 나타낼 수 있습니다. 예를 들어, 그림 1에는 세 열이 있는 테이블의 제품 정보를 표시 하는 DataList 보여 줍니다.


[![DataList 행당 3 가지 제품을 보여 줍니다.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image2.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image1.png)

**그림 1**: The DataList 표시 3 가지 제품 행당 ([전체 크기 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image3.png))


행당 여러 데이터 원본 항목을 표시 하면 DataList 가로 화면 공간을 보다 효과적으로 활용할 수 있습니다. 이 간단한 자습서에서는이 두 DataList 속성을 살펴보겠습니다.

## <a name="step-1-displaying-product-information-in-a-datalist"></a>1 단계: DataList에서 제품 정보를 표시합니다.

살펴보기 전에 `RepeatColumns` 및 `RepeatDirection` 속성, let s 먼저 만듭니다 DataList 표준 단일 열, 다중 행 테이블 레이아웃을 사용 하 여 제품 정보를 나열 하는 가격 페이지에 있습니다. 이 예 에서는의 제품의 이름, 범주 및 가격에 다음 태그를 사용 하 여 표시를 통해 수 있습니다.


[!code-html[Main](showing-multiple-records-per-row-with-the-datalist-control-cs/samples/sample1.html)]

म 했습니다 하므로 이러한 단계를 신속 하 게 이동 하겠습니다 이전 예제에서 DataList에 데이터를 바인딩하는 방법을 표시 합니다. 열어 시작는 `RepeatColumnAndDirection.aspx` 페이지에 `DataListRepeaterBasics` 폴더와 디자이너 도구 상자에서 끌어서 DataList 합니다. DataList s 스마트 태그에서 새 ObjectDataSource 만들고에서 해당 데이터를 가져오도록 구성 하도록 선택할는 `ProductsBLL` s 클래스 `GetProducts` 선택 (없음) s INSERT, UPDATE, 마법사에서 옵션 메서드와 탭 삭제 합니다.

Visual Studio에서 자동으로 만들고 새 ObjectDataSource DataList 바인딩하 만듭니다는 `ItemTemplate` 각 제품 데이터 필드에 대 한 이름 및 값을 표시 하는 합니다. 조정 된 `ItemTemplate` DataList s 스마트 태그에 옵션 선언적 태그를 통해 직접 또는 템플릿 편집에서 대체 위에 표시 된 태그를 사용 하는 *제품 이름*, *범주 이름* , 및 *가격* 텍스트 값을 할당 하려면 적절 한 데이터 바인딩의 구문을 사용 하는 레이블 컨트롤로 자신의 `Text` 속성입니다. 업데이트 한 후의 `ItemTemplate`, s 페이지 선언 태그는 다음과 비슷해야 합니다.


[!code-aspx[Main](showing-multiple-records-per-row-with-the-datalist-control-cs/samples/sample2.aspx)]

공지를 보기에 형식 지정자를 포함 했습니다는 `Eval` 에 대 한 데이터 바인딩 구문을 `UnitPrice`, 통화로-반환 되는 값을 서식 지정`Eval("UnitPrice", "{0:C}").`

브라우저에서 페이지를 방문 하 여 보십시오. 그림 2에서 볼 수 있듯이 DataList 단일 열, 다중 행 테이블을 제품으로 렌더링 합니다.


[![기본적으로 단일 열, 다중 행 테이블으로 DataList 렌더링](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image5.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image4.png)

**그림 2**: 기본적으로, 단일 열, 다중 행 테이블으로 DataList 렌더링 ([전체 크기 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image6.png))


## <a name="step-2-changing-the-datalist-s-layout-direction"></a>2 단계: DataList의 레이아웃 방향 변경

기본 동작 하는 동안 DataList 레이아웃 단일 열, 다중 행 테이블 열에서 해당 항목을 지정 하는 것이 동작은 쉽게 변경할 수 있습니다 DataList s 통해 [ `RepeatDirection` 속성](https://msdn.microsoft.com/en-us/system.web.ui.webcontrols.datalist.repeatdirection.aspx)합니다. `RepeatDirection` 속성이 가능한 두 값 중 하나를 허용할 수: `Horizontal` 또는 `Vertical` (기본값).

변경 하 여는 `RepeatDirection` 속성 `Vertical` 를 `Horizontal`, DataList 단일 행에는 레코드 데이터 원본 항목 마다 하나의 열을 만들어 렌더링 합니다. 이 효과 보여 주기 위해 디자이너에서 DataList에서을 클릭 한 다음 속성 창에서 변경 된 `RepeatDirection` 속성 `Vertical` 를 `Horiztonal`합니다. 즉시 이렇게 되 면 디자이너 조정 DataList의 레이아웃 단일 행, 다중 열 인터페이스 만들기 (그림 3 참조).


[![배치 아웃 RepeatDirection 속성 지정 방법을 the 방향 DataList의 항목은](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image8.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image7.png)

**그림 3**:는 `RepeatDirection` 속성은 아웃 배치 방향 DataList의 항목이 되 지시 ([전체 크기 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image9.png))


적은 양의 데이터를 단일 행을 표시할 때 다중 열 테이블에는 실제 화면 공간을 최대화 하기 위한 이상적인 방법 수 있습니다. 그러나 데이터의 더 큰 볼륨에 대 한 단일 행 어떤 푸시 해당 항목 오른쪽 오프은 화면에 맞출 수 없습니다. 해당 하는 여러 개의 열 필요 합니다. 그림 4에서는 단일 행 DataList로 렌더링할 때 제품을 보여 줍니다. 많은 제품 (80)가 있을 경우 사용자까지 각 제품에 대 한 정보를 보려면 오른쪽으로 스크롤하여 해야 합니다.


[![충분히 큰 데이터 원본에 대 한 단일 열 DataList 내용의 가로 스크롤](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image11.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image10.png)

**그림 4**:에 대 한 충분히 큰 데이터 소스, 단일 열 DataList 됩니다 필요 가로 스크롤 ([전체 크기 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image12.png))


## <a name="step-3-displaying-data-in-a-multi-column-multi-row-table"></a>3 단계: 여러 열, 다중 행 테이블에 데이터를 표시합니다.

여러 열, 다중 행 DataList을 만들려면 설정 해야는 [ `RepeatColumns` 속성](https://msdn.microsoft.com/en-us/system.web.ui.webcontrols.datalist.repeatcolumns.aspx) 표시할 열의 수입니다. 기본적으로는 `RepeatColumns` 속성 단일 행 이나 열에 해당 항목이 모두 표시 하려면 DataList 발생할 수 있는 0으로 설정 됩니다 (값에 따라는 `RepeatDirection` 속성).

이 예에서는 테이블 행당 세 가지 제품을 전시 s를 사용 합니다. 따라서 설정 하는 `RepeatColumns` 속성을 3입니다. 이 변경 후 결과를 보려면 브라우저에서 보십시오. 그림 5에서 볼 수 있듯이 제품 이제는 3 개의 열, 다중 행 테이블에 나와 있습니다.


[![3 가지 제품 행당 표시 됩니다.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image14.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image13.png)

**그림 5**: 3 가지 제품 행당 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image15.png))


`RepeatDirection` 속성 DataList의 항목이 레이아웃 하는 방법에 적용 합니다. 그림 5는 결과와 `RepeatDirection` 속성이로 설정 `Horizontal`합니다. Note 왼쪽에서 오른쪽, 위쪽에서 아래쪽 Chai, 파일과, 변경 및 태양 체리 시럽 처음 세 개의 제품으로 배치 됩니다. (케이준 Seasoning Chef 한 100 s부터 시작) 하는 다음 세 개의 제품 처음 3 개 아래의 행에 표시 됩니다. 하지만 변경 된 `RepeatDirection` 속성을 다시 `Vertical`, 이러한 제품은 위에서 아래로 레이아웃, 그림 6와 같이 왼쪽에서 오른쪽입니다.


[![제품은 세로로 배치 아웃 여기에서 연결](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image17.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image16.png)

**그림 6**: 제품은 세로로 배치 아웃 여기에서 연결 ([전체 크기 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image18.png))


결과 테이블에 표시 되는 행 수가 DataList에 바인딩된 총 레코드 수에 따라 달라 집니다. 정확 하 게,이 s로 나눈 총 데이터 원본 항목의 최대는 `RepeatColumns` 속성 값입니다. 이후는 `Products` 테이블 현재에 84 제품과 3으로 나눌 수, 행이 28입니다. 하는 경우 데이터 원본에 있는 항목의 수 및 `RepeatColumns` 속성 값을 나눌 수 없는 다음 마지막 행 이나 열에는 빈 셀을 갖습니다. 경우는 `RepeatDirection` 로 설정 되어 `Vertical`, 경우 마지막 열에서 빈 셀;를 갖게 됩니다 다음 `RepeatDirection` 은 `Horizontal`, 마지막 행에 있는 빈 셀을 해야 합니다.

## <a name="summary"></a>요약

DataList, 기본적으로 단일 TemplateField 된 GridView의 레이아웃을 모방 하는 단일 열, 다중 행 테이블에서 해당 항목이 나와 있습니다. 이 기본 레이아웃을 적용할 수 있는 동안 행당 여러 데이터 원본 항목을 표시 하 여 화면 자원의 최대화할 수 있습니다. 이 작업을 수행 하는 것은 s DataList 설정 단순히 `RepeatColumns` 속성을 한 행에 표시할 열의 수입니다. 또한 DataList의 `RepeatDirection` 속성이 있는지 여부를 여러 열, 다중 행 테이블의 내용을 배치 해야 가로 방향으로 왼쪽에서 오른쪽, 위쪽에서 아래쪽 또는 위쪽에서 아래쪽, 왼쪽에서 오른쪽 세로로 나타내는 데 사용할 수 있습니다.

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 John Suru 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](formatting-the-datalist-and-repeater-based-upon-data-cs.md)
[다음](nested-data-web-controls-cs.md)
