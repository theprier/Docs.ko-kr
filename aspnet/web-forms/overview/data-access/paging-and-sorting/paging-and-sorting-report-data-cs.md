---
uid: web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-cs
title: 페이징 및 정렬에 대 한 보고서 데이터 (C#) | Microsoft Docs
author: rick-anderson
description: 페이징 및 정렬과 온라인 응용 프로그램에서 데이터를 표시할 때 두 매우 공통적인 기능이 있습니다. 이 자습서에서 소개 정렬 추가 이동 합니다 및...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/15/2006
ms.topic: article
ms.assetid: 811a6ef2-ec66-4c8e-a089-6f795056e288
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 06a907f2af0adb2eb8aef5a814c2d767b62db69a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="paging-and-sorting-report-data-c"></a>페이징 및 정렬에 대 한 보고서 데이터 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_24_CS.exe) 또는 [PDF 다운로드](paging-and-sorting-report-data-cs/_static/datatutorial24cs1.pdf)

> 페이징 및 정렬과 온라인 응용 프로그램에서 데이터를 표시할 때 두 매우 공통적인 기능이 있습니다. 이 자습서에서 소개 정렬 및 페이징을 사용은 보고서를 작성 합니다. 그런 다음 나중에 자습서에는 추가 이동 합니다.


## <a name="introduction"></a>소개

페이징 및 정렬과 온라인 응용 프로그램에서 데이터를 표시할 때 두 매우 공통적인 기능이 있습니다. 예를 들어 온라인 서 점에서에서 ASP.NET 설명서를 검색할 때는 이러한 책의 수백 있을 수 있습니다 하지만 검색 결과 나열 하는 보고서 페이지 당 10 번만 일치 항목을 나열 합니다. 또한, 제목, 가격, 페이지 수, 만든이 이름으로 결과 정렬할 수 있습니다. 과거 23 자습서에는 다양 한 추가, 편집 및 삭제를 허용 하는 인터페이스를 포함 하 여 보고서를 작성 하는 방법을 검사 한 동안 म 하지 데이터 및 경우에을 정렬 하는 방법을 살펴 했습니다 예제 페이징 म DetailsView 및 FormView 했습니다 표시 된 제어 합니다.

이 자습서에서는 정렬 및 페이징을 단순히 몇 가지 확인란을 선택 하 여 수행할 수 있습니다이 보고서에 추가 하는 방법을 살펴보겠습니다. 아쉽게도 이러한 간단한 구현도 단점이 정렬 인터페이스 많았습니다 비트 유지 및 페이징 루틴 효율적으로 많은 결과 집합을 페이징 하기 위해 설계 되지 않았습니다. 이후 자습서에는-의-즉시 페이징 및 정렬과 솔루션의 한계를 극복 하는 방법을 살펴봅니다.

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>1 단계: 추가 페이징 및 자습서 웹 페이지를 정렬 합니다.

이 자습서를 시작 하기 전에 먼저이 자습서와 다음 3에 대 한 해야 ASP.NET 페이지를 추가 하려면 잠시 s가 있습니다. 시작 이라는 프로젝트에 새 폴더를 만들어서 `PagingAndSorting`합니다. 다음으로 마스터 페이지를 사용 하도록 구성 된 모두이 폴더에 다음과 같은 5 개의 ASP.NET 페이지를 추가 `Site.master`:

- `Default.aspx`
- `SimplePagingSorting.aspx`
- `EfficientPaging.aspx`
- `SortParameter.aspx`
- `CustomSortingUI.aspx`


![PagingAndSorting 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.](paging-and-sorting-report-data-cs/_static/image1.png)

**그림 1**: PagingAndSorting 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.


을 열고는 `Default.aspx` 끌어서 페이지는 `SectionLevelTutorialListing.ascx` 에서 사용자 정의 컨트롤의 `UserControls` 디자인 화면으로 폴더입니다. 만든이 사용자 정의 컨트롤의 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-cs.md) 자습서에서는 사이트 맵을 열거 하 고 글머리 기호 목록에서 현재 섹션의 해당 자습서를 표시 합니다.


![Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가](paging-and-sorting-report-data-cs/_static/image2.png)

**그림 2**: Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가


페이징 및 정렬 자습서에서는 만들게 됩니다 표시 글머리 기호 목록을 가지려면 사이트 맵을 추가 해야 합니다. 열기는 `Web.sitemap` 파일을 편집, 삽입, 및 삭제 하는 중 사이트 맵 노드 태그 뒤에 다음 태그를 추가 합니다.


[!code-xml[Main](paging-and-sorting-report-data-cs/samples/sample1.xml)]


![새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트](paging-and-sorting-report-data-cs/_static/image3.png)

**그림 3**: 새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트


## <a name="step-2-displaying-product-information-in-a-gridview"></a>2 단계:는 GridView에 제품 정보를 표시합니다.

에서는 실제로 페이징 및 정렬 기능을 구현 하기 전에 먼저는 표준 비-srotable, 제품 정보를 나열 하는 페이징할 수 없는 GridView 만든이 있습니다. 이 작업은 우리 하므로 이러한 단계가이 자습서 시리즈 전체에 걸쳐 여러 번 수행 했습니다 잘 알고 있어야 합니다. 열어 시작는 `SimplePagingSorting.aspx` 페이지 및 설정 디자이너 도구 상자에서 GridView 컨트롤을 끌어 해당 `ID` 속성을 `Products`합니다. 다음에 s ProductsBLL 클래스를 사용 하는 새 ObjectDataSource 만듭니다 `GetProducts()` 메서드를 모든 제품 정보를 반환 합니다.


![모든 GetProducts() 메서드를 사용 하 여 제품에 대 한 정보를 검색 합니다.](paging-and-sorting-report-data-cs/_static/image4.png)

**그림 4**: 모든 GetProducts() 메서드를 사용 하 여 제품에 대 한 정보를 검색 합니다.


이 보고서는 더 된 읽기 전용 보고서, 없어 s ObjectDataSource s를 매핑해야 할 `Insert()`, `Update()`, 또는 `Delete()` 에 해당 하는 메서드를 `ProductsBLL` 방식의 따라서 삽입, 업데이트에 대 한 드롭다운 목록에서 선택 (없음) 및 탭 삭제 합니다.


![선택 탭 삭제 및 삽입, 업데이트에서 드롭 다운 목록에서 옵션 (없음)](paging-and-sorting-report-data-cs/_static/image5.png)

**그림 5**: 선택 탭 삭제 및 삽입, 업데이트에서 드롭 다운 목록에서 옵션 (없음)


다음으로, 사용 s만 제품 이름, 공급 업체, 범주, 가격, 및 지원 되지 않는 상태 표시 되도록 GridView의 필드를 사용자 지정할 수 있습니다. 예: 조정 필드 수준 서식을 만들을 자유롭게 변경 또한는 `HeaderText` 속성 또는 통화로 가격의 형식을 지정 합니다. 이러한 변경 된 후 GridView s 선언 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample2.aspx)]

그림 6 브라우저를 통해 표시 될 때까지 진행률을 보여줍니다. Note 페이지 모든 각 s 제품 이름, 범주, 공급 업체, 가격, 보여 주는, 한 화면에서 제품이 나열 및 상태를 중단 합니다.


[![나열 된 각 제품의](paging-and-sorting-report-data-cs/_static/image7.png)](paging-and-sorting-report-data-cs/_static/image6.png)

**그림 6**: 나열 된 각 제품의 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image8.png))


## <a name="step-3-adding-paging-support"></a>3 단계: 추가 페이징 지원

나열 *모든* 한 화면에 제품의 데이터를 읽는 데 사용자에 대 한 정보 오버 로드에 발생할 수 있습니다. 결과 보다 잘 관리할 수 있도록 하려면 데이터의 작은 페이지에 대 한 데이터를 해제 하 고 사용자가 한 번에 한 페이지씩 데이터 단계별로 실행 하도록 허용 수 우리 됩니다. 수행 하기 위해이 확인 GridView s 스마트 태그에서 페이징 사용 확인란 (GridView s 설정 [ `AllowPaging` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowpaging.aspx) 를 `true`).


[![확인란을 사용 하도록 설정 페이징 페이징 지원을 추가 하려면](paging-and-sorting-report-data-cs/_static/image10.png)](paging-and-sorting-report-data-cs/_static/image9.png)

**그림 7**: 페이징 확인란을 사용 하도록 설정 페이징 지원 추가 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image11.png))


페이지당 표시 되는 레코드의 수를 제한 하 고 추가 페이징을 사용 하도록 설정 된 *페이징 인터페이스* GridView에 있습니다. 그림 7에 표시 된 기본 페이징 인터페이스는 일련의 페이지 번호를 사용자가 데이터의 한 페이지에서 다른 빠르게 탐색할 수 있도록 합니다. 이 페이징 인터페이스 익숙한 것으로 표시 됩니다 했습니다 지난 자습서에서 DetailsView 및 FormView 컨트롤 페이징 지원을 추가할 때이 표시 합니다.

DetailsView와 FormView 컨트롤만 각 페이지에 단일 레코드를 표시합니다. 하지만 GridView 참조 해당 [ `PageSize` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.pagesize.aspx) 페이지당 표시할 레코드를 확인 하려면 (이 속성의 기본값은 10).

이 GridView, DetailsView, 및 FormView의 페이징 인터페이스는 다음 속성을 사용 하 여 사용자 지정할 수 있습니다.

- `PagerStyle` 페이징 인터페이스;에 대 한 스타일 정보를 나타냅니다. 같은 설정으로 지정할 수 `BackColor`, `ForeColor`, `CssClass`, `HorizontalAlign`등입니다.
- `PagerSettings` 페이징 인터페이스;의 기능을 사용자 지정할 수 있는 속성의 표시를 포함 합니다. `PageButtonCount` (기본값은 10) 페이징 인터페이스에 표시 되는 숫자 페이지 번호의 최대 수를 나타내는; [ `Mode` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pagersettings.mode.aspx) 페이징 인터페이스 작동 하 고 설정할 수 있습니다 하는 방법을 나타냅니다. 

    - `NextPrevious` 사용자가 이전 이나 이후 위치로 한 번에 한 페이지씩 단계 수 있도록 다음 및 이전 단추를 보여 줍니다.
    - `NextPreviousFirstLast` 다음 및 이전 단추 외에도 첫 번째 및 마지막 단추 사항도 포함 되어, 사용자가 신속 하 게 첫 번째 또는 마지막 데이터 페이지로 이동할 수 있도록
    - `Numeric` 일련의 사용자가 즉시 원하는 페이지로 이동할 수 있도록 하는 페이지 번호를 보여 줍니다.
    - `NumericFirstLast` 페이지 번호 외에 첫 번째 및 마지막 단추를 사용자가 데이터의 첫 번째 또는 마지막 페이지에 빠르게 이동할 수 있도록 하는 첫 번째/마지막 단추만 숫자 페이지 번호를 모두 표시할 수 없는 경우 표시 됩니다.

또한 GridView, DetailsView, 및 모든 제공 FormView는 `PageIndex` 및 `PageCount` 속성으로, 각각 표시 되는 현재 페이지와 데이터를 페이지의 총 수를 나타냅니다. `PageIndex` 즉 데이터의 첫 번째 페이지를 볼 때 0부터 시작 하는 인덱싱된 속성은 `PageIndex` 0은 같습니다. `PageCount`을 1부터 계산, 즉 반면에 시작 `PageIndex` 0 사이의 값으로 제한 됩니다 및 `PageCount - 1`합니다.

우리는 GridView의 페이징 인터페이스의 기본 모양을 개선 하는 s를 사용 합니다. 특히, s를 밝은 회색 배경으로 오른쪽 맞춤 페이징 인터페이스가 있습니다. GridView s 통해 직접 이러한 속성을 설정 하는 대신 `PagerStyle` 속성을 통해의 CSS 클래스를 만듭니다 `Styles.css` 라는 `PagerRowStyle` 후 할당는 `PagerStyle` s `CssClass` 우리의 테마를 통해 속성입니다. 열어 시작 `Styles.css` 클래스 정의 다음 CSS를 추가 하 고 있습니다.


[!code-css[Main](paging-and-sorting-report-data-cs/samples/sample3.css)]

을 열고는 `GridView.skin` 파일에 `DataWebControls` 내의 폴더는 `App_Themes` 폴더입니다. 설명한 것 처럼는 *마스터 페이지 및 사이트 탐색* 웹 컨트롤에 대 한 기본 속성 값을 지정 하려면 자습서, 스킨 파일을 사용할 수 있습니다. 따라서 설정을 포함 하려면 기존 설정을 확장 하 고 `PagerStyle` s `CssClass` 속성을 `PagerRowStyle`합니다. Let s 표시할 최대 5 개의 숫자 페이지 단추를 사용 하 여 페이징 인터페이스를 구성 하는 또한는 `NumericFirstLast` 페이징 인터페이스입니다.


[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample4.aspx)]

## <a name="the-paging-user-experience"></a>페이징 사용자 환경

그림 8의 GridView s 페이징 사용 확인란 확인 된 후에 브라우저를 통해 방문할 때 웹 페이지를 보여 줍니다. 및 `PagerStyle` 및 `PagerSettings` 구성을 통해 이루어진는 `GridView.skin` 파일입니다. 참고 방법만 10 개의 레코드가 표시 되어 있으며, 페이징 인터페이스 데이터의 첫 번째 페이지를 보고 있는 것을 나타냅니다.


[![페이징 사용 레코드의 하위 집합만 표시 되는 한 번에](paging-and-sorting-report-data-cs/_static/image13.png)](paging-and-sorting-report-data-cs/_static/image12.png)

**그림 8**: 페이징 사용 레코드의 하위 집합만 표시 되는 한 번에 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image14.png))


페이징 인터페이스의 페이지 번호 중 하나에서 사용자가 포스트백 계속 페이지가 다시 로드 하는 페이지의 레코드 요청 표시 합니다. 그림 9을 사용 하 고 데이터의 마지막 페이지를 보려면 후 결과 보여 줍니다. 마지막 페이지만에 하나의 레코드입니다. 전체적으로 8 페이지의 단일 레코드와 페이지와 페이지 당 10 개의 레코드에 81 레코드가 때문입니다.


[![포스트백 페이지 번호를 클릭 하 고 레코드의 적절 한 하위 집합을 보여 줍니다.](paging-and-sorting-report-data-cs/_static/image16.png)](paging-and-sorting-report-data-cs/_static/image15.png)

**그림 9**: 포스트백 페이지 번호를 클릭 하 고 적절 한 레코드 하위 집합을 보여 줍니다 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image17.png))


## <a name="paging-s-server-side-workflow"></a>페이징의 서버 쪽 워크플로

최종 사용자가 페이징 인터페이스 단추를 클릭 하면 포스트백 계속 하 고 다음 서버 쪽 워크플로 시작 합니다.

1. GridView s (또는 DetailsView 또는 FormView) `PageIndexChanging` 이벤트 발생
2. ObjectDataSource 다시 요청 *모든* BLL;에서 데이터의 GridView s `PageIndex` 및 `PageSize` 속성 값을 GridView에 표시 해야 하는 BLL에서 반환 된 레코드 확인 사용
3. GridView의 `PageIndexChanged` 이벤트 발생

2 단계에서에서는 ObjectDataSource를 요청 하는 데이터 원본에서 데이터를 모두 다시 합니다. 페이징이 스타일은 일반적으로 라고 *기본 페이징*, 그대로 s 페이징 동작 기본적으로 설정할 때 사용 된 `AllowPaging` 속성을 `true`합니다. 기본값은 아무렇게나 웹 컨트롤 데이터를 페이징 검색 데이터의 각 페이지에 대 한 모든 레코드 브라우저에 보내지는 s 레코드의 하위 집합만 실제로 HTML로 렌더링 하는 경우에 합니다. 데이터베이스 데이터 BLL 또는 ObjectDataSource 캐시 하지 않는 한 기본 페이징 충분히 큰 결과 집합 또는 여러 동시 사용자가 있는 웹 응용 프로그램에 대 한 작업 가능한있지 않습니다.

다음 자습서에서는 구현 하는 방법을 검토 *사용자 지정 페이징*합니다. 사용자 지정 페이징을 사용 하 여 정확한 데이터의 요청 된 페이지에 필요한 레코드 집합이 검색 하려면 ObjectDataSource 특히 지시할 수 있습니다. 상상할 수 있듯이 사용자 지정 페이징에 매우 큰 결과 집합에 페이징의 효율성이 향상 됩니다.

> [!NOTE]
> 여러 동시 사용자가 있는 충분히 큰 결과 집합을 통해 또는 사이트에 대 한 페이징 하는 경우에 기본 페이징 적합 하지 않은, 동안 실현 사용자 지정 페이징 더 많은 변경과 구현 하기 위한 활동 필요 하 고 확인란 (기본 확인으로 간단 하지 않습니다 페이징)입니다. 따라서 기본 페이징 작은, 트래픽이 낮은 웹 사이트 또는 때 상대적으로 작은 결과 집합에 대해 페이징을 집합의 것에 대 한 이상적인 수 s 훨씬 쉽고 빠르게 구현할 수 있습니다.


예를 들어 합니다 되지 있는지 100 개가 넘는 제품 데이터베이스에를 알고 있으면 사용자 지정 페이징의 받을 최소한의 성능 향상에 도움이 될 가능성이 구현 하는 데 필요한 노력 만큼 오프셋 됩니다. 그러나 수 1 일 사항이 있는 경우 수천 또는 수만 제품 *하지* 사용자 지정 페이징을 구현 응용 프로그램의 확장성 크게 저하 시킬 합니다.

## <a name="step-4-customizing-the-paging-experience"></a>4 단계: 페이징 환경 사용자 지정

웹 컨트롤 데이터는 다양 한 사용자의 페이징 환경을 개선 하기 위해 사용할 수 있는 속성을 제공 합니다. `PageCount` 속성을 총 페이지 수는 예를 들어 나타냅니다 동안는 `PageIndex` 속성 방문 현재 페이지를 나타내고 신속 하 게 특정 페이지로 사용자 이동로 설정할 수 있습니다. 사용자의 페이징 환경을 보다 개선, 레이블을 추가 s 이러한 속성을 사용 하는 방법을 설명 하기 위해 웹 컨트롤을 페이지를 사용자에 게 알려 주는 가격 페이지는 특정된 페이지를 신속 하 게 이동할 수 있도록 해 주는 DropDownList 제어와 함께 현재 방문 다시 .

첫째, 페이지에 레이블 웹 컨트롤을 추가, 설정 해당 `ID` 속성을 `PagingInformation`, 지울 및 해당 `Text` 속성입니다. GridView s에 대 한 이벤트 처리기를 다음으로 만들고 `DataBound` 이벤트를 다음 코드를 추가 합니다.


[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample5.cs)]

이 이벤트 처리기를 할당는 `PagingInformation` 레이블 s `Text` 현재 방문 중인 페이지를 사용자에 게 알리는 메시지에 속성 `Products.PageIndex + 1` 총 페이지 수가 부족 `Products.PageCount` (1을 더하여 우리는 `Products.PageIndex` 속성 때문에 `PageIndex` 0부터 인덱싱됨). 이 레이블은의 할당 선택 `Text` 속성에는 `DataBound` 반대인 이벤트 처리기는 `PageIndexChanged` 이벤트 처리기 때문에 `DataBound` 반면 GridView에 바인딩된 데이터가 될 때마다이 이벤트가 발생는 `PageIndexChanged` 이벤트 처리기만 페이지 인덱스가 변경 되 면 발생 합니다. 방문 GridView 경우 처음 첫 페이지에 바인딩된 데이터의 `PageIndexChanging` 이벤트 원본이 t 화재 (반면는 `DataBound` 이벤트 않습니다).

이러한 추가 사용자 페이지 방문 하는 것에 관계 및 데이터의 총 페이지 수를 나타내는 메시지 이제 표시 됩니다.


[![현재 페이지 번호 및 총 페이지 수 표시 되는](paging-and-sorting-report-data-cs/_static/image19.png)](paging-and-sorting-report-data-cs/_static/image18.png)

**그림 10**: The 현재 페이지 번호와 총 페이지 수 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image20.png))


Label 컨트롤 외에도 s를 현재 표시 된 선택한 페이지와 함께 GridView의 페이지 번호를 나열 하는 DropDownList 컨트롤을 추가할 수도 있습니다. 여기서는 사용자 빠르게 이동할 수는 현재 페이지에서 다른 새 페이지 인덱스를 선택 하 여 드롭다운 목록에서입니다. 설정 디자이너에 DropDownList를 추가 하 여 시작 해당 `ID` 속성을 `PageList` 스마트 태그에서를 사용 하도록 설정 AutoPostBack 옵션을 선택 하 고 있습니다.

다음으로 돌아갑니다는 `DataBound` 이벤트 처리기를 다음 코드를 추가 합니다.


[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample6.cs)]

이 코드에 대 한 항목 선택을 취소 하 여 시작 된 `PageList` DropDownList 합니다. 하나의 비현실적 t 예상 페이지 변경할 수 있지만 다른 사용자가 될 수 있습니다 동시에 시스템을 사용 하 여, 추가 하거나 제거에서 레코드 하므로, 불필요 한 보일 수 있지만이 `Products` 테이블입니다. 이러한 삽입 또는 삭제는 데이터 페이지 수를 변경할 수 있습니다.

다음으로 페이지 번호를 다시 만드는 현재 GridView에 매핑되는 한이를 해야 `PageIndex` 기본적으로 선택 합니다. 0에서 루프와이 위해 `PageCount - 1`, 새 추가 `ListItem` 각 반복 및 설정에 해당 `Selected` 속성을 현재 반복 인덱스 GridView s 절과 같을 경우 true로 `PageIndex` 속성입니다.

마지막으로, DropDownList s에 대 한 이벤트 처리기를 만들려면 해야 `SelectedIndexChanged` 사용자 목록에서 다른 항목을 선택 될 때마다 발생 하는 이벤트입니다. 이 이벤트 처리기를 만들려면 디자이너에서 DropDownList를 두 번 클릭 다음을 지정 하면 다음 코드를 추가 합니다.


[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample7.cs)]

그림 11에서 볼 수 있듯이 단지 GridView s 변경 `PageIndex` 속성 문을 사용 하면 데이터가 GridView에 바인딩됩니다. GridView s에서 `DataBound` 이벤트 처리기를 적절 한 DropDownList `ListItem` 을 선택 합니다.


[![사용자는 여섯 번째 페이지 선택을 선택 하면 페이지 6 드롭 다운 목록 항목에 자동으로 수행 되는](paging-and-sorting-report-data-cs/_static/image22.png)](paging-and-sorting-report-data-cs/_static/image21.png)

**그림 11**: 사용자는 여섯 번째 페이지 선택을 선택 하면 페이지 6 드롭 다운 목록 항목에 자동으로 수행 됩니다 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image23.png))


## <a name="step-5-adding-bi-directional-sorting-support"></a>5 단계: 추가 양방향 정렬 지원

GridView s 스마트 태그에서 정렬 사용 옵션을 선택 하기만 하면 페이징 지원을 추가 하기 위한 단순하게 양방향 정렬 지원 추가 (GridView s를 설정 하는 [ `AllowSorting` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowsorting.aspx) 를 `true`). 이 렌더링 각각의 GridView의 필드의 머리글 링크 단추가 클릭할 때, 포스트백을 발생 하 고 클릭 한 열을 오름차순으로 정렬 된 데이터를 반환 합니다. 동일한 헤더 LinkButton을 다시 클릭 하면 내림차순 데이터 다시 정렬 합니다.

> [!NOTE]
> 형식화 된 데이터 집합이 아닌 사용자 지정 데이터 액세스 계층을 사용 하는 경우 없을 수 있습니다는 정렬 사용 옵션에서 GridView s 스마트 태그에 있습니다. 기본적으로 정렬을 지 원하는 데이터 원본에 연결 하는 Gridview만이 확인란을 사용할 수 있어야 합니다. ADO.NET DataTable 제공 하므로 형식화 된 데이터 집합에 기본적으로 정렬을 지원 제공는 `Sort` 메서드를 호출 하는 경우 지정 된 조건을 사용 하 여 Datarow DataTable s를 정렬 합니다.


경우에 DAL DAL에 고유 하 게 정렬 된 정렬 지원 구성 데이터를 정렬 하거나 데이터를 보유 하는 비즈니스 논리 계층에 정렬 정보를 전달 ObjectDataSource 해야 하는 개체를 반환 하지 않습니다. 이후 자습서의 비즈니스 논리에서 데이터 및 데이터 액세스 계층을 정렬 하는 방법을 살펴보겠습니다.

정렬 링크 단추가 머리글 행의 배경색 (파란색 열어 보지 않은 링크 및 방문한 링크에 대 한 진한 빨간색으로) 현재 색 충돌 HTML 하이퍼링크로 렌더링 됩니다. 대신 let s는 여부에 관계 없이 흰색으로 표시 되는 모든 헤더 행 링크는 했습니다 되었는지 여부를 방문 합니다. 다음을 추가 하 여이 작업을 수행할 수 있습니다는 `Styles.css` 클래스:


[!code-css[Main](paging-and-sorting-report-data-cs/samples/sample8.css)]

이 구문은 HeaderStyle 클래스를 사용 하는 요소 내에서 하이퍼링크를 표시할 때 흰색 텍스트를 사용 하도록 나타냅니다.

이 CSS 추가 후 브라우저를 통해 페이지를 방문 하는 경우 화면이 그림 12 비슷합니다 표시 합니다. 특히, 그림 12 Price 필드의 헤더 링크를 클릭 한 후 결과 보여줍니다.


[![결과는 UnitPrice 오름차순으로 정렬 해야](paging-and-sorting-report-data-cs/_static/image25.png)](paging-and-sorting-report-data-cs/_static/image24.png)

**그림 12**: The 결과 정렬 된 것으로 오름차순 순서로 UnitPrice ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image26.png))


## <a name="examining-the-sorting-workflow"></a>정렬 워크플로 검사합니다.

모든 GridView BoundField, CheckBoxField, TemplateField, 필드 및에 한 `SortExpression` 필드 s 정렬 헤더 링크를 클릭할 때 데이터 정렬 시 사용 해야 하는 식을 나타내는 속성입니다. GridView 역시는 `SortExpression` 속성입니다. GridView 필드 s 할당 정렬 헤더 LinkButton을 클릭할 때 `SortExpression` 값을 해당 `SortExpression` 속성입니다. 데이터는 ObjectDataSource에서 다시 검색 되 고 GridView s에 따라 정렬 되는 다음으로, `SortExpression` 속성입니다. 다음 목록에는 최종 사용자는 GridView의 데이터를 정렬 하면 그러한 일련의 단계를 자세히 설명 합니다.

1. GridView s [Sorting 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorting(VS.80).aspx) 발생 합니다.
2. GridView s [ `SortExpression` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx) 로 설정 되 고 `SortExpression` 필드의 LinkButton이 클릭 되었습니다 정렬 헤더에는
3. ObjectDataSource 다시 모든 BLL에서 데이터를 검색 하 고 GridView s를 사용 하 여 데이터를 정렬 `SortExpression`
4. GridView의 `PageIndex` 속성은 0으로 다시 설정, 데이터 (페이징 지원을 구현 된 것으로 가정)의 첫 페이지에 반환 되 사용자를 정렬할 때 즉
5. GridView s [ `Sorted` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorted(VS.80).aspx) 발생 합니다.

기본 페이징을 사용 하 여 기본 정렬 옵션 다시 검색 처럼 *모든* BLL에 있는 레코드가 있습니다. 페이징 없이 정렬을 사용 하는 경우 또는 사용한 정렬을 사용 하는 경우 페이징, 여기서 s (보다 짧은 데이터베이스 데이터 캐싱)이이 성능이 뚫을 수 없으므로 기본입니다. 그러나 이후 자습서에서 볼 수 있겠지만,이 s 사용자 지정 페이징을 사용 하는 경우 데이터를 효율적으로 정렬할 수 있습니다.

각 GridView 필드 자동으로 가지는 ObjectDataSource GridView s 스마트 태그에서 드롭 다운 목록에서 GridView에 바인딩할 때 해당 `SortExpression` 에 데이터 필드의 이름에 할당 된 속성의 `ProductsRow` 클래스입니다. 예를 들어는 `ProductName` BoundField s `SortExpression` 로 설정 된 `ProductName`다음 선언적 태그에 나타난 것 처럼:


[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample9.aspx)]

필드를 구성할 수 있도록 것 s 선택을 취소 하 여 정렬 해당 `SortExpression` 속성 (빈 문자열을 할당) 합니다. 상상할이 설명 하기 म 않았음에도 t가 가격으로 제품을 정렬 하는 고객을 활용할 수 있도록 하려면. `UnitPrice` BoundField의 `SortExpression` 선언 태그 또는 (액세스할 수 있는 GridView s 스마트 태그에 있는 열 편집 링크를 클릭 하 여) 필드 대화 상자를 통해 속성을 제거할 수 있습니다.


![결과는 UnitPrice 오름차순으로 정렬 해야](paging-and-sorting-report-data-cs/_static/image27.png)

**그림 13**: 결과 UnitPrice 오름차순으로 정렬 해야


한 번의 `SortExpression` 에 대 한 속성은 제거는 `UnitPrice` BoundField 헤더 하므로 가격으로 데이터 정렬에서 사용자가 방지 하는 링크, 아니라 텍스트로 렌더링 됩니다.


[![SortExpression 속성을 제거 하 여 사용자가 더 이상 ֳ ַ ׂ 가격으로 제품](paging-and-sorting-report-data-cs/_static/image29.png)](paging-and-sorting-report-data-cs/_static/image28.png)

**그림 14**: SortExpression 속성을 제거 하 여 사용자가 더 이상 ֳ ַ ׂ 가격으로 제품 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image30.png))


## <a name="programmatically-sorting-the-gridview"></a>GridView를 프로그래밍 방식으로 정렬

GridView s를 사용 하 여 GridView의 콘텐츠를 프로그래밍 방식으로 정렬할 수도 있습니다 [ `Sort` 메서드](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sort.aspx)합니다. 에 전달 하기만 하면는 `SortExpression` 와 함께 정렬 기준 값을는 [ `SortDirection` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sortdirection.aspx) (`Ascending` 또는 `Descending`), GridView의 데이터 다시 정렬 됩니다.

정렬할 해제 되어 म 이유 가정해 보세요.는 `UnitPrice` अ स म र 고객 가격이 낮은 제품만 구매할 것 단순히 걱정 때문에 있습니다. 그러나 d 좋아요 순서로 정렬 하려면 제품 가격, 아니라 가장 비싼 가격의 최소 수 있게 해야 하므로 비용이 가장 높은 제품을 구입 하도록 권장 하려고 합니다.

Button 웹 컨트롤을 페이지에서 추가이를 위해 설정 해당 `ID` 속성을 `SortPriceDescending`, 및 해당 `Text` 속성을 가격으로 정렬 합니다. 다음에 s 단추에 대 한 이벤트 처리기를 만들고 `Click` 디자이너에서 단추 컨트롤을 두 번 클릭 하 여 이벤트입니다. 이 이벤트 처리기에 다음 코드를 추가 합니다.


[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample10.cs)]

이 단추를 클릭 하면 사용자 첫 페이지로 기준으로 가격에서 가장 저렴 하다 (그림 15 참조)를 가장 비용이 많이 드는 정렬 제품과 함께 반환 합니다.


[![가장 비용이 많이 드는에서 제품 정렬 단추를 클릭 하면 가장 적은에](paging-and-sorting-report-data-cs/_static/image32.png)](paging-and-sorting-report-data-cs/_static/image31.png)

**그림 15**: 제품에서의 가장 많은 비용이 가장 적은에 정렬 단추를 클릭 하면 ([전체 크기 이미지를 보려면 클릭](paging-and-sorting-report-data-cs/_static/image33.png))


## <a name="summary"></a>요약

이 자습서에서는 기본 페이징 및 정렬 기능을 구현 하는 방법에 살펴보았습니다는 둘 다는 확인란을 선택 하는 것 만큼 쉽게! 사용자 정렬 하거나 데이터를 통해 페이지, 비슷한 워크플로가 펼칩니다.

1. 포스트백 계속
2. 웹 컨트롤의 데이터 이벤트 발생을 미리 수준 (`PageIndexChanging` 또는 `Sorting`)
3. ObjectDataSource 다시 검색 된 모든 데이터
4. 웹 컨트롤의 데이터 이벤트 발생을 사후 수준 (`PageIndexChanged` 또는 `Sorted`)

기본 페이징 및 정렬을 구현을 간단히 수행할 수 있도록 상태인 동안에 보다 효율적인 사용자 지정 페이징을 활용 하 여 또는 페이징 또는 정렬 인터페이스를 더욱 향상 시킬 더 많은 노력이 미친 해야 합니다. 이후 자습서는 다음이 항목을 탐색 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [다음](efficiently-paging-through-large-amounts-of-data-cs.md)
