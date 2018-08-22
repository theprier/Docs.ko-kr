---
uid: web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-cs
title: 페이징 및 정렬 보고서 데이터 (C#) | Microsoft Docs
author: rick-anderson
description: 페이징 및 정렬 기능이 두 가지 매우 일반적인 온라인 응용 프로그램에서 데이터를 표시 하는 경우입니다. 이 자습서에서는 살펴보겠습니다는 첫 번째 정렬를 추가 하 고...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 811a6ef2-ec66-4c8e-a089-6f795056e288
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ebef919deeda409cfa6805b603f67ef96ff003e
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829670"
---
<a name="paging-and-sorting-report-data-c"></a>페이징 및 정렬 보고서 데이터 (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_24_CS.exe) 또는 [PDF 다운로드](paging-and-sorting-report-data-cs/_static/datatutorial24cs1.pdf)

> 페이징 및 정렬 기능이 두 가지 매우 일반적인 온라인 응용 프로그램에서 데이터를 표시 하는 경우입니다. 이 자습서에서 나중에 자습서를 따라 작성 했습니다는 보고서에 대 한 페이징 및 정렬 추가 소개를 알아보겠습니다.


## <a name="introduction"></a>소개

페이징 및 정렬 기능이 두 가지 매우 일반적인 온라인 응용 프로그램에서 데이터를 표시 하는 경우입니다. 예를 들어, 온라인 서 점에서에서 ASP.NET 설명서를 검색할 때 등의 서적 수백 있을 수 있지만 검색 결과 나열 하는 보고서 페이지당 10 번만 일치 항목을 나열 합니다. 또한 제목, 가격, 페이지 수, 저자 이름으로 결과 정렬할 수 있습니다. 과거 23 자습서에는 다양 한 데이터, 추가, 편집 및 삭제를 허용 하는 인터페이스를 포함 하 여 보고서를 작성 하는 방법을 검사 한 동안에서는 ve 데이터 및 경우에을 정렬 하는 방법을 확인 하지 페이징 예에서는 FormView 및 DetailsView ve 표시 되었습니다 컨트롤입니다.

이 자습서에서는 정렬 및 페이징을 몇 확인란을 선택 하면 작업을 수행할 수 있는 보고서를 추가 하는 방법에 살펴보겠습니다. 그러나 이러한 간단한 구현에도 정렬 인터페이스 많았습니다 약간 벗어날 단점이 및 페이징 루틴은 큰 결과 집합을 효율적으로 페이징 설계 되지 않았습니다. 이후 자습서에는-의-기본 페이징 및 정렬 솔루션의 한계를 극복 하는 방법을 살펴봅니다.

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>1 단계: 페이징 추가 및 자습서 웹 페이지를 정렬 합니다.

이 자습서를 시작 하기 전에 먼저 시간을 내어이 자습서에는 다음 세 해야 ASP.NET 페이지를 추가 하는 s 수 있습니다. 이라는 프로젝트에 새 폴더를 만들어 시작 `PagingAndSorting`합니다. 다음으로 마스터 페이지를 사용 하도록 구성 된 모든 것이 폴더에 다음 5 개의 ASP.NET 페이지를 추가 `Site.master`:

- `Default.aspx`
- `SimplePagingSorting.aspx`
- `EfficientPaging.aspx`
- `SortParameter.aspx`
- `CustomSortingUI.aspx`


![PagingAndSorting 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.](paging-and-sorting-report-data-cs/_static/image1.png)

**그림 1**: PagingAndSorting 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.


을 엽니다는 `Default.aspx` 끌어서 페이지를 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `UserControls` 디자인 화면으로 폴더입니다. 만든이 사용자 정의 컨트롤을 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-cs.md) 자습서에서는 사이트 맵을 열거 하 고 글머리 기호 목록에 현재 섹션에서 이러한 자습서를 표시 합니다.


![Default.aspx SectionLevelTutorialListing.ascx 사용자 컨트롤 추가](paging-and-sorting-report-data-cs/_static/image2.png)

**그림 2**: Default.aspx SectionLevelTutorialListing.ascx 사용자 컨트롤 추가


글머리 기호 목록에 표시할 페이징 및 자습서를 만들 것을 정렬 하려면 사이트 맵을 추가 해야 합니다. 열기는 `Web.sitemap` 파일을 편집, 삽입, 및 삭제 사이트 맵 노드 태그 뒤에 다음 태그를 추가 합니다.


[!code-xml[Main](paging-and-sorting-report-data-cs/samples/sample1.xml)]


![사이트 맵을 업데이트 하 여 새 ASP.NET 페이지를 포함 합니다.](paging-and-sorting-report-data-cs/_static/image3.png)

**그림 3**: 사이트 맵을 업데이트 하 여 새 ASP.NET 페이지를 포함 합니다.


## <a name="step-2-displaying-product-information-in-a-gridview"></a>GridView의 제품 정보를 표시 하는 2 단계:

에서는 실제로 페이징 및 정렬 기능을 구현 하기 전에 먼저를 표준 비-srotable, 제품 정보를 나열 하는 페이징할 수 없는 GridView를 만든 수 있습니다. 이 작업은 우리가 ve 살지 않는 여러 번이 자습서 시리즈 전체에서 이러한 단계에 알고 있어야 합니다. 열어서 시작 합니다 `SimplePagingSorting.aspx` 페이지 및 설정 디자이너 도구 상자에서 GridView 컨트롤을 끌어 해당 `ID` 속성을 `Products`입니다. 다음에 s ProductsBLL 클래스를 사용 하는 새 ObjectDataSource 만듭니다 `GetProducts()` 모든 제품 정보를 반환 하는 방법입니다.


![모든 GetProducts() 메서드를 사용 하 여 제품에 대 한 정보를 검색 합니다.](paging-and-sorting-report-data-cs/_static/image4.png)

**그림 4**: 모든 GetProducts() 메서드를 사용 하 여 제품에 대 한 정보를 검색 합니다.


이 보고서는 읽기 전용 보고서 있는 s 없습니다 때문에 매핑해야 ObjectDataSource s `Insert()`, `Update()`, 또는 `Delete()` 에 해당 하는 방법 `ProductsBLL` 메서드 따라서 삽입, 업데이트에 대 한 드롭다운 목록에서 선택 (없음) 탭 삭제 하 고 있습니다.


![선택 탭 삭제 및 삽입, 업데이트, 드롭 다운 목록에서 옵션 (없음)](paging-and-sorting-report-data-cs/_static/image5.png)

**그림 5**: 선택 탭 삭제 및 삽입, 업데이트, 드롭 다운 목록에서 옵션 (없음)


다음으로, s를 제품 이름, 공급 업체, 범주, 가격 및 지원 되지 않는 상태 표시 되도록 GridView의 필드를 사용자 지정할 수 있습니다. 조정 등 모든 필드 수준 서식 지정 되도록 자유롭게 변경 또한는 `HeaderText` 속성 또는 통화와 가격의 형식을 지정 합니다. 이러한 변경 이후 GridView가 선언적 태그는 다음과 같아야 합니다.


[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample2.aspx)]

그림 6 브라우저를 통해 볼 때 지금 진행 상황을 보여줍니다. 페이지의 각 s 제품 이름, 범주, 공급자, 가격을 보여 주는 한 화면에서 제품의 모든를 나열 하 고 상태를 중단 note 합니다.


[![나열 된 각 제품](paging-and-sorting-report-data-cs/_static/image7.png)](paging-and-sorting-report-data-cs/_static/image6.png)

**그림 6**: 나열 된 각 제품 ([큰 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image8.png))


## <a name="step-3-adding-paging-support"></a>3 단계: 추가 페이징 지원

나열 *모든* 한 화면에서 제품 데이터를 읽는 데 사용자에 대 한 정보 오버 로드에 발생할 수 있습니다. 결과 보다 잘 관리할 수 있도록 하려면 수 데이터의 작은 페이지에 데이터를 분할 하 고 사용자가 한 번에 데이터 한 페이지를 단계별로 실행 하도록 허용 합니다. 위해이 단순히 확인란 페이징 사용 GridView가 스마트 태그에서 (GridView가 설정 [ `AllowPaging` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowpaging.aspx) 하려면 `true`).


[![확인란을 사용 하도록 설정 페이징 페이징 지원을 추가 하려면](paging-and-sorting-report-data-cs/_static/image10.png)](paging-and-sorting-report-data-cs/_static/image9.png)

**그림 7**: 페이징 확인란을 사용 하도록 설정 페이징 지원 추가 ([큰 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image11.png))


페이지당 표시 되는 레코드의 수를 제한 하 고 추가 페이징을 사용 하도록 설정 된 *페이징 인터페이스* GridView에 있습니다. 그림 7 에서처럼 기본 페이징 인터페이스는 일련의 페이지 번호를 사용자가 다른 데이터 한 페이지에서 빠르게 탐색할 수 있도록 합니다. 이 페이징 인터페이스 것으로 분명히 익숙하게 느껴질 ve 이전 자습서에서 FormView 및 DetailsView 컨트롤 페이징 지원을 추가할 때이 표시 합니다.

FormView 및 DetailsView 컨트롤 페이지당 단일 레코드를 표시합니다. 그러나 GridView consult 해당 [ `PageSize` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.pagesize.aspx) 페이지당 표시할 레코드 수를 확인 하려면 (이 속성의 기본값은 10).

다음 속성을 사용 하 여이 DetailsView GridView, FormView의 페이징 인터페이스를 사용자 지정할 수 있습니다.

- `PagerStyle` 페이징 인터페이스에 대 한 스타일 정보를 나타냅니다. 와 같은 설정을 지정할 수 있습니다 `BackColor`, `ForeColor`를 `CssClass`, `HorizontalAlign`등입니다.
- `PagerSettings` 페이징 인터페이스의 기능을 사용자 지정할 수 있는 속성을 포함 합니다. `PageButtonCount` (기본값은 10) 페이징 인터페이스에 표시할 숫자 페이지 번호의 최대 수를 나타내는; [ `Mode` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pagersettings.mode.aspx) 페이징 인터페이스를 작동 하 고 설정할 수 있는 방법을 나타냅니다. 

    - `NextPrevious` 앞 이나 뒤로 한 번에 한 페이지 단계 사용자 수 있도록 다음 및 이전 단추를 보여 줍니다.
    - `NextPreviousFirstLast` 다음 및 이전 단추 외에도 첫 번째 및 마지막 단추도 포함 된 데이터의 첫 번째 또는 마지막 페이지로 빠르게 이동할 수 있도록 허용
    - `Numeric` 일련의 페이지 번호를 사용자가 원하는 페이지로 바로 이동할 수를 보여 줍니다.
    - `NumericFirstLast` 페이지 번호 외에 사용자가 데이터의 첫 번째 또는 마지막 페이지를 신속 하 게 이동할 수 있도록 첫 번째 및 마지막 단추를 포함 합니다. 첫 번째/마지막 단추만 모든 숫자 페이지 번호를 표시할 수 없는 경우 표시 됩니다.

또한 GridView, DetailsView 및 FormView 모든 제공 합니다 `PageIndex` 및 `PageCount` 속성을 각각 표시 되는 현재 페이지 및 페이지 데이터의 총 수를 나타냅니다. 합니다 `PageIndex` 속성은 데이터의 첫 페이지를 볼 때 사용자에 게 즉 0부터 인덱싱됩니다 `PageIndex` 0은 같습니다. `PageCount`을 1부터 계산, 즉 다른 한편으로 시작 `PageIndex` 0 사이의 값으로 제한 됩니다 및 `PageCount - 1`합니다.

S를 GridView의 페이징 인터페이스의 기본 모양을 개선 하기 위해 잠시 시간이 걸릴 수 있습니다. 특히, 오른쪽 맞춤은 밝은 회색 배경으로 페이징 인터페이스가 s 수 있습니다. GridView s 통해 직접 이러한 속성을 설정 하는 대신 `PagerStyle` 속성을 통해의 CSS 클래스를 만듭니다 `Styles.css` 라는 `PagerRowStyle` 할당 합니다 `PagerStyle` s `CssClass` 는 테마를 통해 속성입니다. 열어서 시작 `Styles.css` 및 클래스 정의 다음 CSS를 추가 합니다.


[!code-css[Main](paging-and-sorting-report-data-cs/samples/sample3.css)]

을 엽니다는 `GridView.skin` 파일을 `DataWebControls` 내에 폴더를 `App_Themes` 폴더. 설명한 대로 합니다 *마스터 페이지 및 사이트 탐색* 웹 컨트롤에 대 한 기본 속성 값을 지정 하려면 자습서, 스킨 파일을 사용할 수 있습니다. 따라서 설정을 포함 하도록 기존 설정을 보강 합니다 `PagerStyle` s `CssClass` 속성을 `PagerRowStyle`입니다. Let s 숫자 5 페이지 단추를 사용 하 여 최대 표시할 페이징 인터페이스를 구성 하는 또한는 `NumericFirstLast` 페이징 인터페이스입니다.


[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample4.aspx)]

## <a name="the-paging-user-experience"></a>페이징 사용자 환경

그림 8 GridView s 페이징 사용 확인란을 선택 된 후 브라우저를 통해 방문할 때 웹 페이지를 보여 줍니다. 및 `PagerStyle` 하 고 `PagerSettings` 구성을 통해 이루어졌습니다는 `GridView.skin` 파일. 참고 하는 방법만 10 개의 레코드가 표시 됩니다 및 페이징 인터페이스는 데이터의 첫 번째 페이지를 보고 있는 것을 나타냅니다.


[![한 번에 레코드의 하위 집합만 표시 됩니다 페이징 사용](paging-and-sorting-report-data-cs/_static/image13.png)](paging-and-sorting-report-data-cs/_static/image12.png)

**그림 8**: 페이징 사용 레코드의 하위 집합만 표시 되는 한 번에 ([큰 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image14.png))


사용자가 페이징 인터페이스의 페이지 번호 중 하나에서 포스트백 근거가 시간과 페이지를 보여 주는 페이지의 레코드를 요청 하는 다시 로드 합니다. 그림 9는 데이터의 마지막 페이지를 보려면 선택 후 결과 보여 줍니다. 마지막 페이지에만 하나의 레코드는 알 수 있습니다. 전체적으로 8 페이지의 유일한 레코드를 사용 하 여 페이지와 페이지 당 10 개의 레코드에서 결과 81 레코드가 때문입니다.


[![포스트백을 발생 시키는 페이지 번호를 클릭 하 고 적절 한 레코드 하위 집합을 보여 줍니다.](paging-and-sorting-report-data-cs/_static/image16.png)](paging-and-sorting-report-data-cs/_static/image15.png)

**그림 9**: 포스트백을 발생 시키는 페이지 번호를 클릭 하 고 적절 한 레코드 하위 집합을 보여 줍니다 ([큰 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image17.png))


## <a name="paging-s-server-side-workflow"></a>페이징의 서버 쪽 워크플로

최종 사용자가 페이징 인터페이스에서 단추를 클릭 하면 포스트백 근거가 하 고 다음 서버 쪽 워크플로 시작 합니다.

1. GridView s (또는 DetailsView를 FormView) `PageIndexChanging` 이벤트 발생
2. ObjectDataSource 다시 요청 *모든* BLL;에서 데이터의 GridView s `PageIndex` 고 `PageSize` 속성 값은 GridView에 표시 해야 하는 BLL에서 반환 된 레코드를 결정 하는 데 사용 됩니다
3. GridView의 `PageIndexChanged` 이벤트 발생

2 단계에서에서 ObjectDataSource를 요청 하는 데이터 원본에서 데이터를 모두 다시 합니다. 페이징이 스타일은 일반적으로 라고 *기본 페이징은*를 그대로 s 페이징 동작 기본적으로 설정할 때 사용 합니다 `AllowPaging` 속성을 `true`. 기본값은 아무렇게나 데이터 웹 컨트롤 페이징 검색 데이터의 각 페이지에 대 한 모든 레코드 레코드의 하위 집합만 실제로 렌더링 되는 HTML로 브라우저로 전송 하는 s도 합니다. BLL 또는 ObjectDataSource 데이터베이스 데이터를 캐시 하지 않는 한에 기본 페이징을 많은 동시 사용자를 사용 하 여 웹 응용 프로그램 또는 충분히 큰 결과 집합에 대 한 제한이 있어서는 안 됩니다.

다음 자습서에서는 검토를 구현 하는 방법 *사용자 지정 페이징을*합니다. 사용자 지정 페이징을 사용 하 여만 레코드 데이터의 요청된 된 페이지에 필요한 정확한 집합을 검색 하는 ObjectDataSource 특히 지시할 수 있습니다. 상상할 수 있듯이 사용자 지정 페이징을 큰 결과 집합을 통해 페이징 효율성을 크게 향상 시킵니다.

> [!NOTE]
> 사용자 지정 페이징을 자세한 변경 내용 및 구현 하기 위해 필요 하 고 (있는 그대로 기본 확인란으로 간단 하지 않습니다 충분히 큰 결과 집합을 통해 또는 사이트에 대 한 여러 동시 사용자가 있는 페이징 하는 경우에 기본 페이징을 적합 하지 않습니다, 하지만 실현 페이징). 따라서 기본 페이징은 적합 한 작은, 트래픽이 낮은 웹 사이트 또는 하므로 비교적 작은 결과 통해 페이징 설정 하면 수 s 훨씬 더 쉽고 빠르게 구현할 수 있습니다.


예를 들어 됩니다 하지 했으므로 100 개가 넘는 제품 데이터베이스에서 알고 있다면, 사용자 지정 페이징을 여 최소한의 성능 향상 가능성이 구현 하는 데 필요한 작업 만큼 오프셋 됩니다. 그러나에서는 하루 있을 수천 또는 수만 개의 제품을 하는 경우 *되지* 응용 프로그램의 확장성을 크게 꺾을 사용자 지정 페이징을 구현 합니다.

## <a name="step-4-customizing-the-paging-experience"></a>4 단계: 페이징 환경 사용자 지정

데이터 웹 컨트롤 다양 한 사용자가의 페이징 환경을 개선 하기 위해 사용할 수 있는 속성을 제공 합니다. 합니다 `PageCount` 속성을 예를 들어, 총 페이지 수를 나타냅니다 동안는 `PageIndex` 속성 되 고 있는 현재 페이지를 나타내며 특정 페이지로 사용자를 신속 하 게 이동할 설정할 수 있습니다. 사용자가의 페이징 환경을 개선할 레이블을 추가 하는 s를 이러한 속성을 사용 하는 방법을 설명 하기 위해 웹 컨트롤을 페이지를 사용자에 게 알려 주는 가격 페이지는 특정된 페이지를 신속 하 게 이동할 수 있도록 DropDownList 제어와 함께 현재 방문 다시 .

먼저 페이지에 레이블 웹 컨트롤을 추가 하 여 설정 합니다 해당 `ID` 속성을 `PagingInformation`를 지울 및 해당 `Text` 속성입니다. 다음으로 GridView s에 대 한 이벤트 처리기를 만듭니다 `DataBound` 이벤트 다음 코드를 추가 합니다.


[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample5.cs)]

이 이벤트 처리기를 할당 합니다 `PagingInformation` 레이블 s `Text` 방문 하는 것은 현재 페이지를 사용자에 게 알리는 메시지에 속성 `Products.PageIndex + 1` 총 페이지 수가 부족 `Products.PageCount` (1을 추가 합니다 `Products.PageIndex` 속성 때문에 `PageIndex` 0부터 인덱싱됨). 이 레이블은의 할당을 선택 `Text` 속성에는 `DataBound` 이벤트 처리기 달리를 `PageIndexChanged` 이벤트 처리기 때문에 `DataBound` 이벤트가 발생 될 때마다 반면 데이터 GridView에 바인딩됩니다는 `PageIndexChanged` 이벤트 처리기만 페이지 인덱스가 변경 될 때 발생 합니다. 를 방문할 때 GridView 처음에 첫 페이지에 바인딩된 데이터를 `PageIndexChanging` 이벤트 대상이 t 화재 (반면는 `DataBound` 이벤트).

사용자는이 추가 사용 하 여 어떤 페이지를 방문 하는 것 이며 데이터의 총 페이지 수를 나타내는 메시지를 이제 표시 됩니다.


[![현재 페이지 번호와 총 페이지 수 표시 됩니다.](paging-and-sorting-report-data-cs/_static/image19.png)](paging-and-sorting-report-data-cs/_static/image18.png)

**그림 10**:의 현재 페이지 번호와 총 페이지 수 표시 됩니다 ([큰 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image20.png))


레이블 컨트롤 외에도 s를 현재 표시 된 선택 페이지를 사용 하 여 GridView의 페이지 번호를 나열 하는 DropDownList 컨트롤을 추가할 수도 있습니다. 여기서는 사용자 신속 하 게 이동할 수는 현재 페이지에서 다른 드롭다운 목록에서 새 페이지 인덱스를 선택 하 여 됩니다. DropDownList 설정 디자이너에 추가 하 여 시작 해당 `ID` 속성을 `PageList` 스마트 태그에서 AutoPostBack을 사용 하도록 설정 옵션을 확인 합니다.

다음으로 돌아갑니다는 `DataBound` 이벤트 처리기 다음 코드를 추가 합니다.


[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample6.cs)]

항목의 선택을 취소 하면이 코드가 시작 되는 `PageList` DropDownList 합니다. 하나의 비현실적 t를 변경 하려면 페이지 수가 예상 하지만 다른 사용자가 동시에 시스템을 사용 하 여, 추가 되었거나에서 레코드를 제거 하므로, 불필요 한 보일 수 있지만이 `Products` 테이블입니다. 이러한 삽입 또는 삭제는 데이터 페이지 수를 변경할 수 있습니다.

다음으로 페이지 번호를 다시 만들고 보유 하 고 현재 GridView에 매핑되는 해야 `PageIndex` 기본적으로 선택 합니다. 0에서 루프를 사용 하 여이 위해서는 `PageCount - 1`, 새 추가 `ListItem` 설정 및 각 반복에서 해당 `Selected` 속성을 현재 반복 인덱스를 GridView가 같으면 true `PageIndex` 속성입니다.

마지막으로, DropDownList s에 대 한 이벤트 처리기를 생성 해야 `SelectedIndexChanged` 사용자 목록에서 다른 항목이 선택 될 때마다 발생 하는 이벤트입니다. 이 이벤트 처리기를 만들려면 디자이너에서 DropDownList를 두 번 클릭 하기만 하면 다음 다음 코드를 추가 합니다.


[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample7.cs)]

그림 11에서 알 수 있듯이, 단순히 GridView s 변경 `PageIndex` 속성 하면 데이터가 GridView에 바인딩됩니다. GridView `DataBound` 이벤트 처리기를 적절 한 DropDownList `ListItem` 을 선택 합니다.


[![사용자가 자동으로 여섯 번째 페이지 선택을 선택 하면 페이지 6 드롭 다운 목록 항목 이동](paging-and-sorting-report-data-cs/_static/image22.png)](paging-and-sorting-report-data-cs/_static/image21.png)

**그림 11**: 사용자는 여섯 번째 페이지 선택을 선택 하면 페이지 6 드롭 다운 목록 항목에 자동으로 수행 됩니다 ([큰 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image23.png))


## <a name="step-5-adding-bi-directional-sorting-support"></a>5 단계: 양방향 정렬 지원 추가

GridView가 스마트 태그에서 정렬 사용 옵션을 선택 하기만 하면 됩니다 페이징 지원을 추가 하는 데 하기만 양방향 정렬 지원 추가 (GridView가 설정 하는 [ `AllowSorting` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowsorting.aspx) 하려면 `true`). 이 렌더링 각각의 GridView가의 필드의 머리글 Linkbutton를 클릭할 때, 포스트백을 발생 하 고 클릭 한 열을 오름차순으로 정렬 된 데이터를 반환 합니다. 동일한 헤더 LinkButton을 다시 클릭 하면 내림차순 데이터 다시 정렬 합니다.

> [!NOTE]
> 입력 데이터 집합이 아닌 사용자 지정 데이터 액세스 계층을 사용 하는 경우 못할 수도 있습니다 정렬 사용 옵션에서 GridView가 스마트 태그에 있습니다. 기본적으로 정렬을 지 원하는 데이터 원본에 연결 하는 Gridview만이 확인란을 사용할 수 있는 경우 ADO.NET DataTable 제공 하므로 형식화 된 데이터 집합에 기본 제공 정렬 지원을 제공을 `Sort` 메서드를 호출 하는 경우 지정 된 조건을 사용 하 여 Datarow의 DataTable s를 정렬 합니다.


경우에 DAL DAL에서 고유 하 게 정렬 된 데이터를 정렬 하거나 데이터를 보유 하는 비즈니스 논리 계층으로 정렬 정보를 전달 하는 ObjectDataSource 구성 해야 정렬을 지 원하는 개체를 반환 하지 않습니다. 이후 자습서에서 비즈니스 논리에서 데이터 및 데이터 액세스 계층을 정렬 하는 방법을 살펴봅니다.

정렬 Linkbutton 머리글 행의 배경색을 사용 하 여 현재 색 (진한 빨간색 열어 본된 링크에 대 한 링크를 열어 보지 않은에 파란색) 충돌 HTML 하이퍼링크로 렌더링 됩니다. Let s 여부에 관계 없이 흰색으로 표시 하는 모든 헤더 행 링크를가 하는 대신 이러한 ve 된 여부를 방문 합니다. 다음을 추가 하 여이 수행할 수 있습니다는 `Styles.css` 클래스:


[!code-css[Main](paging-and-sorting-report-data-cs/samples/sample8.css)]

이 구문은 HeaderStyle 클래스를 사용 하는 요소 내에서 하이퍼링크를 표시 하는 경우 흰색 텍스트를 사용 하도록 나타냅니다.

이 CSS 추가 후 브라우저를 통해 페이지를 방문할 때 화면 비슷합니다 그림 12. 특히, 그림 12 가격 필드의 헤더 링크를 클릭 된 후 결과 보여줍니다.


[![UnitPrice 오름차순으로 정렬 하 여 결과 정렬 된 것](paging-and-sorting-report-data-cs/_static/image25.png)](paging-and-sorting-report-data-cs/_static/image24.png)

**그림 12**:의 결과 정렬 된 것에서 오름차순 순서로 UnitPrice ([큰 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image26.png))


## <a name="examining-the-sorting-workflow"></a>정렬 워크플로 검사합니다.

모든 GridView 필드를 TemplateField BoundField, CheckBoxField 있고 등을 `SortExpression` 필드 s 정렬 헤더 링크를 클릭할 때 데이터 정렬에 사용 해야 하는 식을 나타내는 속성입니다. GridView에는 `SortExpression` 속성입니다. GridView 필드 s 할당 하면 LinkButton 클릭 정렬 헤더 `SortExpression` 값을 해당 `SortExpression` 속성입니다. 데이터를 다시 ObjectDataSource에서 검색 하 고 GridView가 따라 정렬 하는 다음으로, `SortExpression` 속성입니다. 다음은 최종 사용자는 GridView의 데이터를 정렬 하면 다소 일련의 단계를 자세히 설명 합니다.

1. GridView s [Sorting 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorting(VS.80).aspx) 발생 합니다.
2. GridView s [ `SortExpression` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx) 로 설정 됩니다는 `SortExpression` 필드의 정렬 LinkButton 클릭 한 머리글
3. ObjectDataSource 다시 모든 BLL에서 데이터를 검색 하 고 GridView s를 사용 하 여 데이터를 정렬 `SortExpression`
4. GridView의 `PageIndex` 속성은 0으로 다시 설정, 사용자를 정렬할 때 즉 반환 됩니다 (페이징 지원을 구현한 것으로 가정) 되는 데이터의 첫 페이지
5. GridView s [ `Sorted` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorted(VS.80).aspx) 발생 합니다.

기본 페이징을 사용 하 여 기본 정렬 옵션 다시 검색 하는 등 *모든* BLL에 있는 레코드가 있습니다. 페이징 없이 정렬을 사용 하는 경우 또는 정렬을 사용 하는 경우 페이징, 여기서 s이이 성능 데이터를 캐싱하는 데이터베이스) (짧은 저하를 피할 수 없으므로 기본입니다. 그러나 이후 자습서에서 살펴보겠지만,이 사용자 지정 페이징을 사용 하는 경우 데이터를 효율적으로 정렬 하 합니다.

각 GridView 필드에 자동으로 ObjectDataSource GridView가 스마트 태그에서 드롭다운 목록을 통해 GridView에 바인딩할 때 해당 `SortExpression` 속성에서 데이터 필드의 이름에 할당 된 `ProductsRow` 클래스. 예를 들어 합니다 `ProductName` BoundField s `SortExpression` 로 설정 된 `ProductName`다음 선언적 태그에 표시 된 것 처럼:


[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample9.aspx)]

필드를 구성할 수 있습니다 있도록 것을 지우는 불가능 s 해당 `SortExpression` 속성 (빈 문자열에 할당). 이 예는 imagine에서는 하지 않으려는 고객 가격으로 제품을 정렬할 수 있도록 합니다. 합니다 `UnitPrice` BoundField의 `SortExpression` 선언적 태그 또는 (액세스할 수 있는 GridView가 스마트 태그에 있는 열 편집 링크를 클릭 하 여) 필드 대화 상자를 통해 속성을 제거할 수 있습니다.


![UnitPrice 오름차순으로 정렬 하 여 결과 정렬 된 것](paging-and-sorting-report-data-cs/_static/image27.png)

**그림 13**: UnitPrice 오름차순으로 정렬 하 여 결과 정렬 된 것


한 번 합니다 `SortExpression` 속성에 대 한 제거 되었습니다는 `UnitPrice` BoundField 헤더 price가 데이터 정렬에서 사용자를 방지 하므로 링크가 아니라 텍스트로 렌더링 됩니다.


[![SortExpression 속성을 제거 하 여 정렬을 수행할 수 없습니다 더 이상 제품 가격](paging-and-sorting-report-data-cs/_static/image29.png)](paging-and-sorting-report-data-cs/_static/image28.png)

**그림 14**: SortExpression 속성을 제거 하 여 정렬을 수행할 수 없습니다 더 이상 제품에서 가격 ([큰 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image30.png))


## <a name="programmatically-sorting-the-gridview"></a>GridView를 프로그래밍 방식으로 정렬

GridView s를 사용 하 여 GridView의 콘텐츠를 프로그래밍 방식으로 정렬할 수도 있습니다 [ `Sort` 메서드](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sort.aspx)합니다. 에 전달 하기만 하면를 `SortExpression` 함께 정렬할 값을 [ `SortDirection` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sortdirection.aspx) (`Ascending` 또는 `Descending`), GridView의 데이터 다시 정렬 됩니다.

기준으로 정렬 하는 해제 되어에서는 이유 imagine는 `UnitPrice` 이어서 고객 가격이 낮은 제품만 구매할 것 단순히 걱정 있었습니다. 그러나 d에서는 같은 순서로 정렬 하려면 제품 가격, 아니라 가장 비싼 가격의 최소 수 있으므로 가장 비용이 많이 드는 제품을 구입할 수 있도록 유도 하고자 합니다.

수행이 컨트롤을 추가 단추 웹 페이지로 설정 해당 `ID` 속성을 `SortPriceDescending`, 및 해당 `Text` 가격으로 정렬 하는 속성입니다. 다음으로 s 단추에 대 한 이벤트 처리기를 만듭니다 `Click` 이벤트 디자이너에서 단추 컨트롤을 두 번 클릭 합니다. 이 이벤트 처리기에 다음 코드를 추가 합니다.


[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample10.cs)]

이 단추를 클릭 하면 사용자 첫 페이지에 가격에서 가장 비용이 저렴 (그림 15 참조) 별로 정렬 된 제품을 사용 하 여 반환 합니다.


[![제품에서 가장 비용이 많이 드는 정렬 단추를 클릭 하면 가장 적은를](paging-and-sorting-report-data-cs/_static/image32.png)](paging-and-sorting-report-data-cs/_static/image31.png)

**그림 15**: 제품에서의 가장 많은 비용이 가장 적은에 정렬 단추를 클릭 하면 ([큰 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image33.png))


## <a name="summary"></a>요약

기본 페이징 및 정렬 기능을 구현 하는 방법에 살펴보았습니다이 자습서는 두 개는 확인란을 선택 하는 것 만큼 쉽습니다! 사용자 정렬 하거나 데이터를 통해 페이지에 유사한 워크플로 펼칩니다.

1. 포스트백 근거가
2. 데이터 웹 컨트롤의 이벤트 발생을 미리 수준 (`PageIndexChanging` 또는 `Sorting`)
3. ObjectDataSource 다시 검색 된 모든 데이터
4. 데이터 웹 컨트롤의 이벤트 발생을 사후 수준 (`PageIndexChanged` 또는 `Sorted`)

간편해 집니다 인 기본 페이징 및 정렬을 구현 하는 동안 더 효율적인 사용자 지정 페이징을 사용 또는 페이징 또는 정렬 인터페이스를 좀 더 강화 하려면 더 많은 노력이 역량 해야 합니다. 이후 자습서에서는 다음이 항목을 살펴봅니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [다음](efficiently-paging-through-large-amounts-of-data-cs.md)
