---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
title: DataList 및 반복기 컨트롤 (VB)를 사용 하 여 데이터를 표시 합니다. | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서 데이터를 표시 하는 GridView 컨트롤을 사용 했습니다. 이 자습서를 시작에 대해 살펴봅니다와 일반적인 보고 패턴을 작성 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/13/2006
ms.topic: article
ms.assetid: 58618954-a9ed-4ca0-8c2d-95a5ffd9c03e
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 9c6e4f8588fb8da2e9703f5de0032e6a21bb5a28
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37397667"
---
<a name="displaying-data-with-the-datalist-and-repeater-controls-vb"></a>DataList 및 반복기 컨트롤 (VB)를 사용 하 여 데이터 표시
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_29_VB.exe) 또는 [PDF 다운로드](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/datatutorial29vb1.pdf)

> 이전 자습서에서 데이터를 표시 하는 GridView 컨트롤을 사용 했습니다. 이 자습서를 사용 하 여부터 살펴봅니다 DataList 및 반복기 컨트롤을 사용 하 여 일반적인 보고 패턴을 작성 이러한 컨트롤을 사용 하 여 데이터를 표시 하는 기본 사항부터.


## <a name="introduction"></a>소개

모든 이전 전체 예제에서 28 자습서, GridView 컨트롤에 설정에서는 데이터 원본에서 여러 레코드를 표시 해야 하는 경우. GridView 열에 s 레코드 데이터 필드를 표시 합니다. 데이터 소스의 각 레코드에 대 한 행을 렌더링 합니다. GridView를 통해 간단히 표시, 페이징, 정렬, 편집 및 데이터 삭제, 모양을 약간 얻을입니다. 또한 책임 태그 GridView의 구조에서 고정 되어에 포함 한 HTML `<table>` 테이블 행을 사용 하 여 (`<tr>`) 각 레코드 및 테이블 셀에 대 한 (`<td>`) 각 필드에 대 한 합니다.

ASP.NET 2.0을 여러 레코드를 표시 하는 경우는 더 높은 수준의 사용자 지정 모양 및 렌더링 된 태그를 제공, DataList 및 반복기 컨트롤을 제공 합니다 (둘 다 되었습니다 ASP.NET 버전에서 사용할 수 있는 1.x). DataList 및 반복기 컨트롤 BoundFields, CheckBoxFields, ButtonFields, 대신 템플릿을 사용 하 여 해당 콘텐츠를 렌더링 등에입니다. GridView와 같은 DataList를 HTML로 렌더링 `<table>`, 하지만 수 있도록 여러 데이터 원본 테이블 행당 표시할 레코드입니다. Repeater, 반면에 보다 새로운 명시적으로 지정 하는 태그에 정해진 정밀 하 게 제어 해야 하는 경우 적합 한 후보가 없습니다 추가 태그를 렌더링 합니다.

다음 몇십 자습서를 통해 살펴보겠습니다 DataList 및 반복기 컨트롤을 사용 하 여 일반적인 보고 패턴을 작성 이러한 컨트롤 템플릿 사용 하 여 데이터 표시의 기본 사항을 시작 합니다. 이러한 컨트롤 서식 지정 하는 방법을 살펴보겠습니다 DataList, 일반적인 마스터/세부 정보 시나리오, 방법으로 편집 하 고 데이터를 삭제 하는 데이터 원본 레코드의 레이아웃을 변경 하는 방법을 레코드를 페이징 하는 방법입니다.

## <a name="step-1-adding-the-datalist-and-repeater-tutorial-web-pages"></a>DataList 및 Repeater 자습서 웹 페이지 1 단계: 추가

이 자습서를 시작 하기 전에 s를 먼저이 자습서 및 DataList 및 반복기를 사용 하 여 데이터 표시를 다루는 다음 몇 가지 자습서에 대 한 필요 하 여 ASP.NET 페이지 추가 잠시 시간이 걸릴 수 있습니다. 이라는 프로젝트에 새 폴더를 만들어 시작 `DataListRepeaterBasics`합니다. 다음으로 마스터 페이지를 사용 하도록 구성 된 모든 것이 폴더에 다음 5 개의 ASP.NET 페이지를 추가 `Site.master`:

- `Default.aspx`
- `Basics.aspx`
- `Formatting.aspx`
- `RepeatColumnAndDirection.aspx`
- `NestedControls.aspx`


![DataListRepeaterBasics 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image1.png)

**그림 1**: 만들기는 `DataListRepeaterBasics` 폴더 및 자습서 ASP.NET 페이지 추가


열기는 `Default.aspx` 끌어서 페이지를 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `UserControls` 디자인 화면으로 폴더입니다. 만든이 사용자 정의 컨트롤을 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-vb.md) 자습서에서는 사이트 맵을 열거 하 고 글머리 기호 목록에 현재 섹션의 자습서를 표시 합니다.


[![Default.aspx SectionLevelTutorialListing.ascx 사용자 컨트롤 추가](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image3.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image2.png)

**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 `Default.aspx` ([클릭 하 여 큰 이미지 보기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image4.png))


글머리 기호 목록을 표시 하기 위해 우리를 만들 수, DataList 및 반복기 자습서 해야 사이트 맵을 추가 합니다. 열기는 `Web.sitemap` 파일 및 사용자 지정 단추 추가 사이트 맵 노드 태그 뒤에 다음 태그를 추가 합니다.


[!code-xml[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample1.xml)]


![사이트 맵을 업데이트 하 여 새 ASP.NET 페이지를 포함 합니다.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image5.png)

**그림 3**: 사이트 맵을 업데이트 하 여 새 ASP.NET 페이지를 포함 합니다.


## <a name="step-2-displaying-product-information-with-the-datalist"></a>2 단계: DataList 사용 하 여 제품 정보를 표시합니다.

FormView와 마찬가지로, DataList 컨트롤 렌더링 된 출력의 템플릿 대신 BoundFields, CheckBoxFields, 등에 따라 다릅니다. FormView, 달리 DataList는 독립 하나 보다는 레코드 집합을 표시 하도록 설계 되었습니다. 이 자습서를 살펴보고 바인딩 제품 정보 DataList를 시작 하는 s 수 있습니다. 열어서 시작 합니다 `Basics.aspx` 페이지에 `DataListRepeaterBasics` 폴더입니다. 그런 다음 디자이너 도구 상자에서 DataList를 끕니다. DataList의 템플릿을 지정 하기 전에, 그림 4에서 볼 수 있듯이 디자이너는 회색 상자로 표시 합니다.


[![디자이너 도구 상자에서 DataList를 끌어 옵니다.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image7.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image6.png)

**그림 4**: DataList에서의 도구 상자에는 디자이너를 끌어 옵니다 ([큰 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image8.png))


DataList s에서에서 스마트 태그를 새 ObjectDataSource를 추가 하 고 사용 하도록 구성 합니다 `ProductsBLL` s 클래스 `GetProducts` 메서드. (없음) 드롭 다운 목록 삽입 마법사에서에서 설정에서는이 자습서에서는 읽기 전용 DataList 만들기 다시 있으므로 업데이트 하 고 탭을 삭제 합니다.


[![새 ObjectDataSource를 만들도록 선택합니다](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image10.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image9.png)

**그림 5**: 새 ObjectDataSource을 만들기 위해 최적화 ([큰 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image11.png))


[![ProductsBLL 클래스를 사용 하는 ObjectDataSource 구성](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image13.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image12.png)

**그림 6**: ObjectDataSource 사용 하도록 구성 된 `ProductsBLL` 클래스 ([클릭 하 여 큰 이미지 보기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image14.png))


[![모든 GetProducts 메서드를 사용 하 여 제품에 대 한 정보를 검색 합니다.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image16.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image15.png)

**그림 7**: 검색 정보에 대 한 모든 사용 하 여 제품을 `GetProducts` 메서드 ([클릭 하 여 큰 이미지 보기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image17.png))


Visual Studio에서 자동으로 ObjectDataSource를 구성 하 고 해당 스마트 태그를 통해 DataList를 사용 하 여 연결을 만듭니다는 `ItemTemplate` 이름과 데이터 소스에서 반환 된 각 데이터 필드의 값을 표시 하는 DataList에서 (참조는 태그 아래)입니다. 이 기본 `ItemTemplate` 모양 데이터 원본 디자이너를 통해 FormView 바인딩할 때 자동으로 생성 템플릿의 동일 합니다.


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample2.aspx)]

> [!NOTE]
> 데이터 원본 FormView s 스마트 태그를 통해 FormView 컨트롤을 바인딩하는 경우 Visual Studio 만들어졌는지 회수를 `ItemTemplate`, `InsertItemTemplate`, 및 `EditItemTemplate`합니다. 그러나 DataList와 함께는 `ItemTemplate` 만들어집니다. DataList 편집 및 삽입 지원 FormView에서 제공 하는 동일한 기본 제공 되지 않은 때문입니다. DataList는 편집 및 삭제에 관련 된 이벤트를 포함 및 편집 및 삭제 지원 추가할 수 있는 s 코드의 비트를 사용 하 여 지원 되지 않습니다 간단한 기본 제공으로 FormView 사용 하 여. 편집 및 이후 자습서에서 지원 DataList를 사용 하 여 삭제를 포함 하는 방법을 살펴보겠습니다.


가이 템플릿의 모양 향상을 위해 잠시 시간이 걸릴 수 있습니다. 모든 데이터 필드를 표시 하는 대신 s를 제품의 이름, 공급 업체, 범주, 단위 및 단가 수량을 표시할 수 있습니다. Let s의 이름을 표시 하는 또한는 `<h4>` 제목 및 사용 하 여 나머지 필드를 레이아웃를 `<table>` 제목 아래에 있습니다.

할 수 있습니다 이러한 변경을 수행 하려면 편집 s 스마트 태그 템플릿 편집 링크를 클릭 하거나 페이지 s 선언적 구문을 통해 수동으로 템플릿을 수정할 수 있습니다 DataList에서 디자이너에 기능 템플릿을 사용 하 여 중 하나입니다. 디자이너에서 템플릿 편집 옵션을 사용 하는 경우 결과 태그에 다음 태그를 정확 하 게 일치 하지 않을 수 있지만 브라우저를 통해 볼 때 스크린 샷을 그림 8에 표시 된 것과 매우 비슷합니다 표시 됩니다.


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample3.aspx)]

> [!NOTE]
> 사용 하 여 위의 예에서는 레이블 웹 컨트롤 `Text` 속성이 데이터 바인딩 구문 중 값이 할당 됩니다. 또는 없습니다가 생략 되었습니다 레이블을 모두 한 데이터 바인딩 구문을 입력 합니다. 즉, 사용 하는 대신 `<asp:Label ID="CategoryNameLabel" runat="server" Text='<%# Eval("CategoryName") %>' />` 대신 사용 하는 선언적 구문을 `<%# Eval("CategoryName") %>`합니다.


그러나 레이블 웹 컨트롤에 leaving, 두 가지 이점 제공 합니다. 먼저, 다음 자습서에서 살펴보겠지만 데이터를 기반으로 데이터를 서식 지정에 대 한 더 쉽게 하는 방법을 제공 합니다. 둘째, 디자이너 만들어지고 t 표시 선언적 데이터 바인딩 구문 템플릿 편집 옵션을 표시 되는 일부 웹 컨트롤 외부에서. 대신, 템플릿 편집 인터페이스는 정적 태그를 사용 하 여 작업을 활용 하도록 설계 되었습니다 및 웹 컨트롤 및 모든 데이터 바인딩 웹 컨트롤의 스마트 태그에서 액세스할 수 있는 데이터 바인딩 편집 대화 상자를 통해 수행 됩니다는 것으로 가정 합니다.

따라서 디자이너를 통해 템플릿을 편집 옵션을 제공 하는 DataList를 사용 하 여 작업 하는 경우 필자 선호 콘텐츠 템플릿 편집 인터페이스를 통해 액세스할 수 있도록 레이블을 웹 컨트롤을 사용 합니다. 앞으로 살펴보겠지만 곧, 반복기 템플릿의 내용을 소스 뷰에서 편집할 수 있도록 해야 합니다. 따라서 필자는 형식을 지정 해야 하지 않는 한 컨트롤 레이블 웹은 대개 생략 하겠습니다 Repeater가의 템플릿을 작성 하는 경우 데이터의 모양을 프로그래밍 논리를 기반으로 하는 텍스트가 바인딩됩니다.


[![각 출력 s 제품은 DataList의 ItemTemplate 사용 하 여 렌더링](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image19.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image18.png)

**그림 8**: 각 제품의 출력은 DataList s를 사용 하 여 렌더링 `ItemTemplate` ([클릭 하 여 큰 이미지 보기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image20.png))


## <a name="step-3-improving-the-appearance-of-the-datalist"></a>3 단계: DataList의 모양을 개선

DataList GridView와 같은 다양 한 스타일 관련 속성을 같은 제공 `Font`, `ForeColor`를 `BackColor`, `CssClass`를 `ItemStyle`를 `AlternatingItemStyle`, `SelectedItemStyle`등. 스킨 파일에는 GridView 및 DetailsView 컨트롤에서 작업할 때 만들었습니다 합니다 `DataWebControls` 미리 정의 된 테마를 `CssClass` 이 두 컨트롤에 대 한 속성 및 `CssClass` 다양 한 해당 하위 속성에 대 한 속성 (`RowStyle` 를 `HeaderStyle`등). S를 DataList에 대 한 동일한 작업을 수행할 수 있습니다.

에 설명 된 대로 합니다 [the ObjectDataSource 사용 하 여 데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) 자습서, 웹 컨트롤에 대 한 기본 모양 관련 속성을 지정 하는 스킨 파일은 테마를 정의 하는 스킨, CSS, 이미지 및 JavaScript 파일의 컬렉션 특정 모양과 느낌을 웹 사이트에 대 한 합니다. 에 *the ObjectDataSource 사용 하 여 데이터 표시* 만들었습니다 자습서에서는 `DataWebControls` 테마 (내에 폴더도 구현 되는 `App_Themes` 폴더) 있는, 현재, 두 스킨 파일- `GridView.skin` 및 `DetailsView.skin`. 가 세 번째 DataList에 대 한 미리 정의 된 스타일 설정을 지정 하려면 스킨 파일을 추가할 수 있습니다.

스킨 파일에 추가 하려면 마우스 오른쪽 단추로 클릭는 `App_Themes/DataWebControls` 폴더에 새 항목 추가 선택 하 고 목록에서 스킨 파일 옵션을 선택 합니다. 파일 이름을 `DataList.skin`로 지정합니다.


[![DataList.skin 라는 새 스킨 파일 만들기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image22.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image21.png)

**그림 9**: 명명 된 새 스킨 파일을 만듭니다 `DataList.skin` ([클릭 하 여 큰 이미지 보기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image23.png))


다음 태그를 사용 하 여 `DataList.skin` 파일:


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample4.aspx)]

이러한 설정은 GridView 및 DetailsView 컨트롤과 함께 사용 된 대로 적절 한 DataList 속성에 동일한 CSS 클래스를 할당 합니다. 여기에 CSS 클래스 `DataWebControlStyle`, `AlternatingRowStyle`를 `RowStyle`등과에 정의 된는 `Styles.css` 파일 및 이전 자습서에서 추가한 합니다.

이 스킨 파일의 추가, DataList 모양은 (새로 고치려면 디자이너 보기 보기 메뉴에서 새 스킨 파일의 효과 확인 하려면 새로 고침을 선택 해야 할) 디자이너에 업데이트 됩니다. 그림 10과 같이 교대로 반복 되는 각 제품에는 밝은 분홍색 배경색입니다.


[![DataList.skin 라는 새 스킨 파일 만들기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image25.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image24.png)

**그림 10**: 명명 된 새 스킨 파일을 만듭니다 `DataList.skin` ([클릭 하 여 큰 이미지 보기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image26.png))


## <a name="step-4-exploring-the-datalist-s-other-templates"></a>4 단계: DataList s 다른 템플릿 탐색

이외에 `ItemTemplate`, DataList 지원 다른 선택적 템플릿 6:

- `HeaderTemplate` 제공 하는 경우 출력에 머리글 행을 추가 하 고이 행을 렌더링 하는 데 사용 됩니다.
- `AlternatingItemTemplate` 교대로 반복 되는 항목을 렌더링 하는 데 사용
- `SelectedItemTemplate` 선택한 항목을 렌더링 하는 데 사용 선택한 항목은 DataList s에 해당 하는 인덱스에 있는 항목 [ `SelectedIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.selectedindex.aspx)
- `EditItemTemplate` 편집 중인 항목을 렌더링 하는 데 사용
- `SeparatorTemplate` 제공 된 경우 각 항목 사이 구분 기호를 추가 하 고이 구분 기호를 렌더링 하는 데 사용 됩니다.
- `FooterTemplate` -제공 하는 경우 출력에 바닥글 행을 추가 하 고이 행을 렌더링 하는 데 사용 됩니다

지정 하는 경우는 `HeaderTemplate` 또는 `FooterTemplate`, DataList 렌더링된 된 출력에 추가 머리글 또는 바닥글 행을 추가 합니다. 같은 GridView의 헤더와 바닥글 행, 헤더 및 바닥글 DataList에 바인딩되지 않은 데이터입니다. 따라서 모든 데이터 바인딩 구문을 합니다 `HeaderTemplate` 또는 `FooterTemplate` 바인딩된 데이터에 액세스 하려고 빈 문자열을 반환 합니다.

> [!NOTE]
> 설명한 것 처럼 합니다 [바닥글 GridView에서에서 요약 정보 표시](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md) 자습서, 머리글 및 바닥글 행 하지 t 지원 데이터 바인딩 구문을 데이터 관련 정보는 동안 이러한 행에 직접 삽입할 수 있습니다는 GridView의 `RowDataBound` 이벤트 처리기입니다. 이 기법을 사용할 수 있습니다 누계를 계산 하는 둘 다 또는 다른 데이터에서 컨트롤에 바인딩된 정보와 바닥글에 해당 정보를 할당 합니다. 이 개념 DataList 및 반복기 컨트롤에 적용할 수 있습니다. 유일한 차이점은 DataList 및 반복기를 만들기에 대 한 이벤트 처리기에 대 한 합니다 `ItemDataBound` 이벤트 (대신에 대 한는 `RowDataBound` 이벤트).


예를 들어 let s 타이틀이 DataList의 결과 위쪽에 표시 되는 제품 정보는 `<h3>` 제목입니다. 이렇게 하려면 추가 `HeaderTemplate` 적절 한 태그를 사용 하 여 합니다. 디자이너에서이 수 하면 DataList s 스마트 태그에 템플릿 편집 링크를 클릭 하 고 드롭다운 목록에서 머리글 템플릿을 선택 스타일 드롭다운 목록에서에서 3 제목 옵션을 선택한 후 텍스트를 입력 (그림 11 참조)를 나열 합니다.


[![텍스트 제품 정보를 사용 하 여 머리글을 템플릿의 추가](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image28.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image27.png)

**그림 11**: 추가 된 `HeaderTemplate` 텍스트 제품 정보를 사용 하 여 ([클릭 하 여 큰 이미지 보기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image29.png))


또는 추가할 수 있습니다 선언적으로 내에서 다음 태그를 입력 하 여는 `<asp:DataList>` 태그:


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample5.html)]

약간의 각 제품 목록 사이 공백 추가할 수 추가 s는 `SeparatorTemplate` 각 섹션 사이 선을 포함 합니다. 가로줄 태그 (`<hr>`), 구분선을 추가 합니다. 만들기는 `SeparatorTemplate` 다음 태그를 갖도록 합니다.


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample6.html)]

> [!NOTE]
> 같은 합니다 `HeaderTemplate` 및 `FooterTemplates`, `SeparatorTemplate` 데이터 원본의 모든 레코드에 바인딩되지 않은 이며 따라서 직접 DataList에 바인딩된 레코드는 데이터 소스 액세스 합니다.


이 또한이를 적용 한 후 브라우저를 통해 페이지를 볼 때 그림 12와 비슷하게 표시 됩니다. 머리글 행과 각 제품 목록 사이 있는 줄 note 합니다.


[![DataList은 머리글 행 및 각 제품 목록 간에 수평선 포함 되어 있습니다.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image31.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image30.png)

**그림 12**: DataList 머리글 행 및를 가로 규칙 간 각 제품 목록에 포함 되어 있습니다 ([큰 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image32.png))


## <a name="step-5-rendering-specific-markup-with-the-repeater-control"></a>5 단계: Repeater 컨트롤을 사용 하 여 특정 태그를 렌더링합니다.

그림 12에서 DataList 예제를 방문할 때 브라우저에서 소스 보기/이렇게 하면 표시는 DataList HTML를 내보냅니다 `<table>` 테이블 행을 포함 하는 (`<tr>`) 단일 표 셀을 사용 하 여 (`<td>`)에 바인딩된 각 항목에 대 한 합니다 DataList 합니다. 사실이 출력은 단일 templatefield로 사용 하 여 GridView에서 내보낼 수는 항목 동일 합니다. 이후 자습서에서 살펴보겠지만 DataList에서는 출력의 추가 사용자 지정 테이블 행당 여러 데이터 원본 레코드를 표시 하기를 사용 하도록 설정 합니다.

T HTML 내보내기를 하려는 경우에 어떻게 하지 `<table>`되지만? Repeater 컨트롤 데이터 웹 컨트롤에서 생성 된 태그를 통해 전체 및 전체 컨트롤에 대 한 사용 해야 합니다. Repeater, DataList와 같은 템플릿 기반 생성 됩니다. 그러나 Repeater,만 제공 다음 5 개의 템플릿이:

- `HeaderTemplate` 제공 하는 경우 지정된 된 태그 항목 앞에 추가
- `ItemTemplate` 항목을 렌더링 하는 데 사용
- `AlternatingItemTemplate` 교대로 반복 되는 항목을 렌더링 하는 데 제공 하는 경우
- `SeparatorTemplate` 제공 된 경우 각 항목 사이 지정된 된 태그 추가
- `FooterTemplate` -제공 된 경우 지정된 된 태그 항목 뒤에 추가

Asp.net에서 1.x에서 Repeater 컨트롤이 일반적으로 일부 데이터 원본에서 가져온 데이터가 있는 글머리 기호 목록을 표시 하는 데 사용 됩니다. 이러한 경우에는 `HeaderTemplate` 및 `FooterTemplates` 을 열고 닫는 포함 됩니다 `<ul>` 태그 하는 동안 각각의 `ItemTemplate` 포함 됩니다 `<li>` 데이터 바인딩 구문 사용 하 여 요소. 이 접근 방식을 계속 사용할 수 있습니다 ASP.NET 2.0에서의 두 예제에서 살펴본 것 처럼 합니다 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-vb.md) 자습서:

- 에 `Site.master` 마스터 페이지 (기본 보고, 보고서 필터링, 사용자 지정 서식 및 등) 최상위 사이트 맵 내용의 글머리 기호 목록을 표시 하려면 Repeater를 사용한; 다른, 중첩 된 반복기가의 하위 섹션을 표시 하는 데는 최상위 섹션
- `SectionLevelTutorialListing.ascx`, Repeater는 현재 사이트 맵 섹션의 자식 섹션의 글머리 기호 목록을 표시 하는 데 사용 되었습니다

> [!NOTE]
> ASP.NET 2.0에서는 새 [BulletedList 컨트롤](https://msdn.microsoft.com/library/ms228101.aspx)는 간단한 글머리 기호 목록을 표시 하기 위해 데이터 소스 컨트롤에 바인딩할 수 수 있습니다. BulletedList 컨트롤과에서는 필요가 없습니다 목록 관련 HTML; 중 하나를 지정 하려면 대신, 우리는 단순히 나타냅니다 각 목록 항목에 대 한 텍스트를 표시 하려면 데이터 필드.


반복기는 모든 데이터 웹 컨트롤을 catch로 사용 됩니다. 필요한 태그를 생성 하는 기존 컨트롤 없으면 Repeater 컨트롤 사용할 수 있습니다. Repeater를 사용 하 여를 보여 주기 위해 s를 2 단계에서에서 만든 제품 정보 DataList 위에 표시 되는 범주 목록이 남아 있을 수 있습니다. 특히, s 수 있는 단일 행 html에서 표시 되는 범주 `<table>` 테이블의 열으로 표시 하는 각 범주를 사용 하 여 합니다.

이렇게 하려면 위의 제품 정보 DataList 디자이너 도구 상자에서 반복기 컨트롤을 드래그 하 여 시작 합니다. DataList, 마찬가지로 Repeater 처음에 표시 회색 상자로 해당 템플릿을 정의한 될 때까지 합니다.


[![Repeater를 디자이너에 추가](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image34.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image33.png)

**그림 13**: Repeater를 디자이너에 추가할 ([큰 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image35.png))


반복기가 스마트 태그에 하나의 옵션만 여기 s: 데이터 소스 선택 합니다. 새 ObjectDataSource를 만들고 사용 하도록 구성 하도록 선택 합니다 `CategoriesBLL` s 클래스 `GetCategories` 메서드.


[![새 ObjectDataSource 만들기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image37.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image36.png)

**그림 14**: 새 ObjectDataSource 만듭니다 ([큰 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image38.png))


[![CategoriesBLL 클래스를 사용 하는 ObjectDataSource 구성](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image40.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image39.png)

**그림 15**: ObjectDataSource 사용 하도록 구성 된 `CategoriesBLL` 클래스 ([클릭 하 여 큰 이미지 보기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image41.png))


[![모든 GetCategories 메서드를 사용 하 여 범주에 대 한 정보를 검색 합니다.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image43.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image42.png)

**그림 16**: 검색 정보에 대 한 모든 사용 하 여 범주는 `GetCategories` 메서드 ([클릭 하 여 큰 이미지 보기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image44.png))


DataList를 달리 Visual Studio 자동으로 만들어지지는지 않습니다 ItemTemplate 반복기에 대 한 데이터 소스에 바인딩한 후. 또한 반복기의 템플릿 디자이너를 통해 구성할 수 없습니다 및 선언적으로 지정 해야 합니다.

단일 행으로 범주를 표시 하려면 `<table>` 각 범주에 대 한 열을 사용 하 여 반복기 다음과 유사한 태그를 생성 해야 합니다.


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample7.html)]

이후는 `<td>Category X</td>` 반복,이 반복기가의 ItemTemplate에 표시 하는 부분은 텍스트입니다. 것은 앞에 나타나는 태그 `<table><tr>` -에 배치 됩니다 합니다 `HeaderTemplate` 끝 태그-하는 동안 `</tr></table>` -에 배치 됩니다는 `FooterTemplate`합니다. 이러한 템플릿 설정에 입력 하려면 다음 구문에서 형식과 왼쪽된 아래 모서리에 있는 원본 단추를 클릭 하 여 ASP.NET 페이지의 선언적 부분에 이동 합니다.


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample8.aspx)]

Repeater 해당 템플릿, 뿐, 아무 작업도 수행 하 여 지정 된 대로 정확 하 게 태그를 내보냅니다. 그림 17 브라우저를 통해 볼 때 반복기가의 출력을 보여줍니다.


[![단일 행 HTML &lt;테이블&gt; 별도 열에서 각 범주 나열](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image46.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image45.png)

**그림 17**:는 단일 행 HTML `<table>` 별도 열에서 각 범주를 나열 ([클릭 하 여 큰 이미지 보기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image47.png))


## <a name="step-6-improving-the-appearance-of-the-repeater"></a>6 단계: 반복기의 모양을 개선

Repeater 내보내는 해당 템플릿에 의해 지정 된 태그를 정확 하 게, 이후 가져와야 놀라운 일이 아닙니다 반복기에 대 한 스타일 관련 속성이 없는 하 합니다. 반복기에서 생성 된 콘텐츠의 외관을 변경 하려면 Repeater가 서식 파일에 직접 필요한 HTML 또는 CSS 콘텐츠를 수동으로 추가 해야 했습니다.

예를 들어 s를 DataList에서 교대로 반복 되는 행과 같은 배경 색을 대체 범주 열이 있을 수 있습니다. 이를 위해 할당 해야 합니다 `RowStyle` 각 반복기 항목에 CSS 클래스 및 `AlternatingRowStyle` CSS 클래스를 통해 각 교대로 반복 되는 반복기 항목은 `ItemTemplate` 및 `AlternatingItemTemplate` 템플릿을 다음과 같이:


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample9.aspx)]

S를 텍스트 제품 범주를 사용 하 여 출력에 머리글 행을 추가할 수도 있습니다. T 열 개수를 결과 알고 있는 것 이므로 `<table>` 는 구성의 모든 열에 걸쳐 보장 되는 머리글 행을 생성 하는 가장 간단한 방법은 사용 하는 것 *두* `<table>` s입니다. 첫 번째 `<table>` 머리글 행과 행을 두 번째로, 단일 행을 포함 하는 두 개의 행이 포함 됩니다 `<table>` 시스템에서 각 범주에 대 한 열이 포함 된 합니다. 즉, 다음 태그를 내보냅니다 해야 합니다.


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample10.html)]

다음 `HeaderTemplate` 고 `FooterTemplate` 원하는 태그에서 발생 합니다.


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample11.aspx)]

이러한 변경이 이루어진 후 그림 18 Repeater를 보여 줍니다.


[![범주 열 배경색으로 대체 하 고 머리글 행이 포함 됩니다.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image49.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image48.png)

**그림 18**:의 범주 열 대체 배경색에 머리글 행을 포함 합니다. ([큰 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image50.png))


## <a name="summary"></a>요약

GridView 컨트롤을 사용 하면 쉽게 표시, 편집, 삭제, 정렬 및 데이터의 페이지 모양을 매우 얻을 하 고 표 형태의 합니다. 모양 세부적 DataList 또는 반복기 컨트롤에 설정 해야 합니다. 이러한 컨트롤은 모두 BoundFields, CheckBoxFields, 않고 템플릿을 사용 하 여 레코드 집합을 표시 합니다.

DataList를 HTML로 렌더링 `<table>` , 기본적으로 표시 하는 각 데이터 원본 레코드를 단일 TemplateField 사용 하 여 GridView와 마찬가지로 단일 테이블 행을 합니다. 그러나 이후 자습서에서 살펴볼 DataList 않습니다 여러 레코드를 허용 테이블 행 당 표시할 수 있습니다. Repeater, 다른 한편으로 엄격 하 게 내보내는 해당 템플릿에서;에 지정 된 태그 모든 추가 태그를 추가 하지 않습니다 하 고 따라서 일반적으로 아닌 다른 HTML 요소에 데이터를 표시 하는 `<table>` (글머리 기호 목록 등).

DataList 및 반복기를 렌더링 된 출력에 더 많은 유연성을 제공 하는 동안 GridView에 기본 제공 기능을 많이 부족 합니다. 이후 자습서에서 살펴봅니다 이러한 기능 중 일부 큰 노력을 들이지 않고 다시 연결 될 수 있지만 수행 유지에 사용 하는 DataList 또는 GridView 대신 반복기는 이러한 기능을 구현 하지 않고도 사용할 수 기능을 제한 직접입니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Yaakov Ellis, Liz Shulok, Randy Schmidt 및 Stacy Park 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](nested-data-web-controls-cs.md)
> [다음](formatting-the-datalist-and-repeater-based-upon-data-vb.md)
