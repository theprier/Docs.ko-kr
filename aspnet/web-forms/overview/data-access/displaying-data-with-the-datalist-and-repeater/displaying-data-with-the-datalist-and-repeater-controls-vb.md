---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
title: "DataList 및 반복기 컨트롤 (VB)를 사용 하 여 데이터를 표시 | Microsoft Docs"
author: rick-anderson
description: "이전 자습서에서 데이터를 표시 하는 GridView 컨트롤을 사용 했습니다. 와 일반적인 보고 패턴 작성 살펴보면이 자습서를 시작 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 09/13/2006
ms.topic: article
ms.assetid: 58618954-a9ed-4ca0-8c2d-95a5ffd9c03e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 20a092ee2886932664705c22c3aa88d8a2f7f0ef
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="displaying-data-with-the-datalist-and-repeater-controls-vb"></a>DataList 및 반복기 컨트롤 (VB)를 사용 하 여 데이터 표시
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_29_VB.exe) 또는 [PDF 다운로드](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/datatutorial29vb1.pdf)

> 이전 자습서에서 데이터를 표시 하는 GridView 컨트롤을 사용 했습니다. 이 자습서를 시작 의견에 귀 DataList 및 반복기 컨트롤이 있는 보고의 일반 패턴을 구축에 이러한 컨트롤을 사용 하 여 데이터를 표시 하는 기본적인으로 시작 합니다.


## <a name="introduction"></a>소개

모든 이전 전체에서 예제에서 우리 GridView 컨트롤에 설정 된 데이터 원본에서 여러 개의 레코드를 표시 해야 하는 경우 28 자습서입니다. GridView 열에 있는 s 레코드 데이터 필드를 표시 합니다. 데이터 원본의 각 레코드에 대 한 행을 렌더링 합니다. GridView를 통해 간단히 표시를 통해, 정렬, 편집 및 삭제 데이터 페이지, 모양이 약간 얻을입니다. 또한 책임 태그 GridView의 구조 수정에 대 한 포함 HTML `<table>` 테이블 행이 있는 (`<tr>`) 각 레코드 및 테이블 셀에 대 한 (`<td>`) 각 필드에 대 한 합니다.

ASP.NET 2.0을 사용자 지정 모양 및 렌더링 된 태그에는 더 높은 수준의 여러 레코드를 표시 하는 경우를 제공 하려면 DataList 및 반복기 컨트롤을 제공 합니다 (둘 다 된 ASP.NET 버전에서 사용할 수 또한 1.x). DataList 및 반복기 컨트롤 BoundFields, CheckBoxFields, ButtonFields, 대신 템플릿을 사용 하 여 콘텐츠 렌더링 등에입니다. GridView 처럼 DataList는 HTML로 렌더링 `<table>`, 되지만 보조 데이터베이스가 여러 데이터에 대 한 원본 레코드가 테이블 행당 표시 됩니다. 반면에 반복 어떤 명시적으로 지정 하는 이상적인 후보가 내보내집니다 태그 정밀 하 게 제어 해야 하는 경우 보다 없습니다 추가 태그를 렌더링 합니다.

수십 개 다음 자습서를 통해에서 살펴보게 DataList 및 반복기 컨트롤이 있는 일반적인 보고 패턴 작성 이러한 컨트롤 템플릿 사용 하 여 데이터를 표시 하는 기본적인으로 시작 합니다. 이러한 컨트롤 형식을 지정 하는 방법을 살펴보려는 DataList, 일반적인 시나리오는 마스터/세부 정보, 같은 방법으로 편집 하 여 데이터를 삭제 하는 데이터 원본 레코드의 레이아웃을 변경 하는 방법, 레코드를 통해 페이지 하는 방법입니다.

## <a name="step-1-adding-the-datalist-and-repeater-tutorial-web-pages"></a>1 단계: DataList 및 반복기 자습서 웹 페이지를 추가합니다.

이 자습서를 시작 하기 전에 먼저이 자습서와 DataList 및 반복기를 사용 하 여 데이터 표시를 다루는 다음 몇 가지 자습서 해야 ASP.NET 페이지를 추가 하려면 잠시 s를 사용 합니다. 시작 이라는 프로젝트에 새 폴더를 만들어서 `DataListRepeaterBasics`합니다. 다음으로 마스터 페이지를 사용 하도록 구성 된 모두이 폴더에 다음과 같은 5 개의 ASP.NET 페이지를 추가 `Site.master`:

- `Default.aspx`
- `Basics.aspx`
- `Formatting.aspx`
- `RepeatColumnAndDirection.aspx`
- `NestedControls.aspx`


![DataListRepeaterBasics 폴더를 만들고 자습서 ASP.NET 페이지를 추가 합니다.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image1.png)

**그림 1**: 만들기는 `DataListRepeaterBasics` 폴더 자습서 ASP.NET 페이지를 추가 합니다.


열기는 `Default.aspx` 끌어서 페이지는 `SectionLevelTutorialListing.ascx` 에서 사용자 정의 컨트롤의 `UserControls` 디자인 화면으로 폴더입니다. 만든이 사용자 정의 컨트롤의 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-vb.md) 자습서에서는 사이트 맵을 열거 하 고 글머리 기호 목록에서 현재 섹션의 자습서를 표시 합니다.


[![Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image3.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image2.png)

**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image4.png))


글머리 기호 목록을 표시 하기 위해 म 만들게 됩니다, DataList 및 반복기 자습서 해야 사이트 맵에 추가 합니다. 열기는 `Web.sitemap` 파일을 사용자 지정 단추 추가 사이트 맵 노드 태그 뒤에 다음 태그를 추가 합니다.


[!code-xml[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample1.xml)]


![새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image5.png)

**그림 3**: 새 ASP.NET 페이지를 포함 하도록 사이트 맵 업데이트


## <a name="step-2-displaying-product-information-with-the-datalist"></a>2 단계: datalist 제품 정보를 표시합니다.

FormView와 마찬가지로, DataList 컨트롤 렌더링 된 출력 s 서식 파일 대신 BoundFields, CheckBoxFields, 등에 따라 다릅니다. FormView, 달리 DataList는 고립 인터페이스가 아니라 레코드의 집합을 표시 하도록 설계 되었습니다. 이 자습서를 살펴보고 DataList에 제품 정보를 바인딩 시작 s를 사용 합니다. 열어 시작는 `Basics.aspx` 페이지에 `DataListRepeaterBasics` 폴더입니다. 그런 다음 디자이너 도구 상자에서 DataList를 끕니다. 그림 4 있듯이 DataList s 서식 파일을 지정 하기 전에 디자이너는 회색 상자로 표시 합니다.


[![DataList 디자이너 도구 상자에서 끌어 옵니다.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image7.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image6.png)

**그림 4**: DataList에서의 도구 상자에는 디자이너를 끌어 옵니다 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image8.png))


DataList s에서에서 스마트 태그 새 ObjectDataSource를 추가 하 고 사용 하도록 구성 된 `ProductsBLL` s 클래스 `GetProducts` 메서드. 마법사의 INSERT에서에서 드롭 다운 목록을 (없음)를 설정 읽기 전용 DataList이이 자습서에서 만드는 다시 म 하므로 업데이트 및 삭제 탭 합니다.


[![새 ObjectDataSource를 만들도록 선택한](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image10.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image9.png)

**그림 5**: 새 ObjectDataSource 만들기 하기로 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image11.png))


[![ObjectDataSource ProductsBLL 클래스를 사용 하도록 구성](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image13.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image12.png)

**그림 6**: 구성에 사용 하 여 ObjectDataSource는 `ProductsBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image14.png))


[![모든 GetProducts 메서드를 사용 하 여 제품에 대 한 정보를 검색 합니다.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image16.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image15.png)

**그림 7**: 검색 정보에 대 한 모든 사용 하 여 제품의 `GetProducts` 메서드 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image17.png))


Visual Studio는 ObjectDataSource를 구성 하 고 스마트 태그를 통해 DataList와 연결을 자동으로 만들어집니다는 `ItemTemplate` 이름 및 데이터 소스에서 반환 된 각 데이터 필드의 값을 표시 하 여 DataList의 (참조는 태그 아래)입니다. 이 기본 `ItemTemplate`의 모양을 데이터 원본 디자이너를 통해 FormView에 바인딩할 때 자동으로 생성 하는 템플릿의 동일 합니다.


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample2.aspx)]

> [!NOTE]
> 데이터 원본을 FormView s 스마트 태그를 통해 FormView 컨트롤을 바인딩하는 경우 Visual Studio 만들어졌는지 회수는 `ItemTemplate`, `InsertItemTemplate`, 및 `EditItemTemplate`합니다. 그러나 datalist만 `ItemTemplate` 만들어집니다. DataList 편집 및 FormView에서 제공 하는 지원 삽입 같은 기본 제공 없기 때문입니다. DataList 편집 및 삭제 관련 이벤트 증명이 있으며 편집 및 삭제 지원 추가할 수 있습니다 약간의 코드를 했지만 없어 s FormView로 없는 간단한 기본적으로 지원 합니다. 편집 및 이후 자습서에서 datalist 지원 삭제를 포함 하는 방법을 살펴보겠습니다.


S 잠시이 서식 파일의 모양을 향상 시킬 수 있도록 합니다. 모든 데이터 필드를 표시 하는 대신 s만 제품의 이름, 공급 업체, 범주, 각 단위 테스트 및 단가 가능한 트리거 수를 표시 하도록 합니다. Let s의 이름을 표시 하는 또한는 `<h4>` 제목 및 레이아웃을 사용 하 여 나머지 필드 지정는 `<table>` 제목 아래에 있습니다.

할 수 있습니다 이러한 변경을 수행 하려면 템플릿 편집에서 스마트 태그 템플릿 편집 링크를 클릭 하거나 수동으로 페이지 s 선언 구문을 통해 서식 파일을 수정할 수 있습니다 s DataList 디자이너에서 기능을 사용 하거나 합니다. 템플릿 편집 옵션을 사용 하 여 디자이너에서 결과 태그에 다음 태그를 정확 하 게 일치 하지 않을 수 있지만 브라우저를 통해 볼 때 다음 스크린샷에서 그림 8에서에 다음과 같이 나타납니다.


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample3.aspx)]

> [!NOTE]
> 사용 하 여 위의 예에서는 Label 웹 컨트롤 `Text` 속성 구문이의 값이 할당 됩니다. 또는 म 수를 생략 했습니다 레이블을 맵 한 데이터 바인딩 구문을 입력 합니다. 즉, 사용 하는 대신 `<asp:Label ID="CategoryNameLabel" runat="server" Text='<%# Eval("CategoryName") %>' />` 대신 사용할 수도 선언적 구문 `<%# Eval("CategoryName") %>`합니다.


그러나 레이블 웹 컨트롤에서 leaving, 두 가지 이점을 제공 합니다. 첫째, 볼 수 있겠지만, 다음 자습서에서 데이터를 기반으로 데이터 서식을 지정 하기 위한 더 쉽게 하는 방법을 제공 합니다. 둘째, 디자이너 대상이 t 디스플레이 선언적 데이터 바인딩 구문에서 템플릿 편집 옵션 나타나는 일부 웹 제어를 벗어나야 합니다. 대신 템플릿 편집 인터페이스 static 태그를 쉽게 처리할 수를 사용 하 고 웹 제어 하 고 웹 컨트롤의 스마트 태그에서 액세스할 수 있는 데이터 바인딩 편집 대화 상자를 통해 모든 데이터 바인딩은 것으로 가정 합니다.

따라서 datalist 편집으로 인해 디자이너를 통해 서식 파일 옵션을 제공 하는 작업 하는 경우 레이블 웹 컨트롤을 사용 하 여 콘텐츠 템플릿 편집 인터페이스를 통해 액세스할 수 있는 않겠습니다. 곧 볼 수 있겠지만, 반복기 템플릿의 내용을 소스 뷰에서 편집할 수 있도록 필요 합니다. 따라서, 포맷 해야 여부를 확인 하지 않는 한 컨트롤을 만들어 Label 웹 종종 생략 합니다 I s 템플릿에 때 데이터의 모양을 프로그래밍 논리를 기준으로 텍스트가 바인딩됩니다.


[![각 제품의 출력은 DataList의 ItemTemplate 사용 하 여 렌더링](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image19.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image18.png)

**그림 8**: 각 제품의 출력은 DataList s를 사용 하 여 렌더링 `ItemTemplate` ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image20.png))


## <a name="step-3-improving-the-appearance-of-the-datalist"></a>3 단계: DataList의 모양을 향상

DataList GridView 처럼 스타일 관련 속성의 숫자와 같은 제공 `Font`, `ForeColor`, `BackColor`, `CssClass`, `ItemStyle`, `AlternatingItemStyle`, `SelectedItemStyle`등입니다. 만든 스킨 파일에 GridView 및 DetailsView 컨트롤에서 작업할 때는 `DataWebControls` 미리 정의 된 테마는 `CssClass` 이 두 컨트롤에 대 한 속성 및 `CssClass` 자신의 하위 속성의 속성 (`RowStyle` `HeaderStyle`등). S DataList에 대 한 동일한 작업을 수행 하도록 합니다.

에 설명 된 대로 [the ObjectDataSource와 데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) 스킨 파일 웹 컨트롤에 대 한 기본 모양 관련 속성을 지정 합니다. 즉 테마를 정의 하는 스킨, CSS, 이미지 및 JavaScript 파일의 컬렉션에는 자습서 웹 사이트에 대 한 특정 모양 및 느낌입니다. 에 *the ObjectDataSource와 데이터 표시* 자습서에서 만든는 `DataWebControls` 테마 (내에 있는 폴더도 구현 되는 `App_Themes` 폴더) 있는, 현재 두 개의 스킨 파일- `GridView.skin` 및 `DetailsView.skin`. S를 추가 세 번째 스킨 파일 DataList에 대 한 미리 정의 된 스타일 설정을 지정할 수 있습니다.

스킨 파일을 추가 하려면 마우스 오른쪽 단추로 클릭는 `App_Themes/DataWebControls` 폴더를 새 항목 추가 선택 하 고 목록에서 스킨 파일 옵션을 선택 합니다. 파일 이름을 `DataList.skin`로 지정합니다.


[![DataList.skin 라는 새 스킨 파일 만들기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image22.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image21.png)

**그림 9**: 명명 된 새 스킨 파일 만들기 `DataList.skin` ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image23.png))


에 대 한 다음 태그를 사용 하 여는 `DataList.skin` 파일:


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample4.aspx)]

이러한 설정은 GridView 및 DetailsView 컨트롤 함께 사용 된 대로 적절 한 DataList 속성에 동일한 CSS 클래스를 할당 합니다. 여기에 사용 되는 CSS 클래스 `DataWebControlStyle`, `AlternatingRowStyle`, `RowStyle`등에 정의 된는 `Styles.css` 파일을 이전 자습서에서 추가 되었습니다.

이 스킨 파일을 추가 하 여 DataList의 모양은 (; 보기 메뉴에서 새 스킨 파일의 효과 확인 하려면 새로 고침 디자이너 뷰 새로 고침 해야 할 수 있습니다) 디자이너에 업데이트 됩니다. 그림 10과 같이 각 교대로 반복 되는 제품 연한 분홍색 배경색을 있습니다.


[![DataList.skin 라는 새 스킨 파일 만들기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image25.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image24.png)

**그림 10**: 명명 된 새 스킨 파일 만들기 `DataList.skin` ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image26.png))


## <a name="step-4-exploring-the-datalist-s-other-templates"></a>DataList s 다른 서식 파일을 탐색 하는 4 단계:

이외에 `ItemTemplate`, DataList는 6 개의 다른 옵션 템플릿을 지원 합니다.

- `HeaderTemplate`제공 된 경우 출력에 머리글 행을 추가 하 고이 행을 렌더링 하는 데 사용
- `AlternatingItemTemplate`대체 항목을 렌더링 하는 데 사용
- `SelectedItemTemplate`선택한 항목을 렌더링 하는 데 사용 선택한 항목은 s DataList에 해당 하는 인덱스를 포함 하는 항목 [ `SelectedIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.selectedindex.aspx)
- `EditItemTemplate`편집 중인 항목을 렌더링 하는 데 사용
- `SeparatorTemplate`제공 된 경우 각 항목 사이 구분 기호를 추가 하 고이 구분 기호를 렌더링 하는 데 사용
- `FooterTemplate`-를 입력 하면 바닥글 행이 추가 되며이 행을 렌더링 하는 데 사용

지정 하는 경우는 `HeaderTemplate` 또는 `FooterTemplate`, DataList 렌더링된 된 출력에 추가 머리글 또는 바닥글 행을 추가 합니다. 마찬가지로 GridView의 머리글 및 바닥글 행, 머리글 및 바닥글 DataList에 바인딩되지 않습니다 데이터. 데이터 바인딩 구문이 따라서는 `HeaderTemplate` 또는 `FooterTemplate` 에 바인딩된 데이터에 액세스 하려고 하면 빈 문자열을 반환 합니다.

> [!NOTE]
> 설명한 것 처럼는 [GridView의 바닥글의에서 요약 정보 표시](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md) 머리글 및 바닥글 행 t 지원 databinding 구문, 데이터 관련 정보를 하지 않는 동안 자습서에서 이러한 행에 직접 삽입 될 수 있습니다는 GridView의 `RowDataBound` 이벤트 처리기입니다. 이 기술은에 사용할 수 있습니다 누계를 계산 하는 둘 다 또는 기타 정보 데이터를 컨트롤에 바인딩된으로 바닥글에 해당 정보를 지정 합니다. DataList 및 반복기 제어;에이 개념을 적용할 수 있습니다. DataList와 반복기에 대 한 이벤트 처리기 만들기에 대 한 유일한 차이점은 하는 `ItemDataBound` 이벤트 (대신에 대 한는 `RowDataBound` 이벤트).


이 예에서는 s let가 제목에 DataList의 결과 위쪽에 표시 되는 제품 정보는 `<h3>` 제목입니다. 이를 위해 추가 `HeaderTemplate` 적절 한 태그로 합니다. 디자이너에서 이렇게 DataList s 스마트 태그에서 템플릿 편집 링크를 클릭 하면, 드롭 다운 목록에서 머리글 템플릿을 선택 드롭다운 스타일에서 제목 3 옵션을 선택한 후 텍스트에 입력 하 여 목록 (그림 11 참조).


[![텍스트 제품 정보 HeaderTemplate 추가](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image28.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image27.png)

**그림 11**: 추가 된 `HeaderTemplate` 텍스트 제품 정보 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image29.png))


또는 추가할 수 있습니다 선언적으로 내에 다음 태그를 입력 하 여는 `<asp:DataList>` 태그:


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample5.html)]

각 제품 목록 사이의 간격의 비트를 추가 하려면 추가 s 수는 `SeparatorTemplate` 각 섹션 사이 선을 포함 하는 합니다. 단락 구분선 태그 (`<hr>`), 이러한 구분선을 추가 합니다. 만들기는 `SeparatorTemplate` 다음 태그를 갖도록 합니다.


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample6.html)]

> [!NOTE]
> 와 같은 `HeaderTemplate` 및 `FooterTemplates`, `SeparatorTemplate` 데이터 원본의 모든 레코드에 바인딩되지 않은 하 고 따라서 데이터 원본 DataList에 바인딩된 레코드 액세스 직접 없습니다.


이 추가 확인 한 후 브라우저를 통해 페이지를 볼 때 그림 12 비슷합니다 표시 됩니다. 머리글 행과 각 제품 목록 사이의 선에 note 합니다.


[![DataList은 머리글 행과 각 제품 목록 간의 수평선 포함 됩니다.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image31.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image30.png)

**그림 12**: DataList 포함 머리글 행과는 가로 규칙 간의 각 제품 목록 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image32.png))


## <a name="step-5-rendering-specific-markup-with-the-repeater-control"></a>반복기 컨트롤을 사용 하 여 특정 태그를 렌더링 하는 5 단계:

그림 12의 DataList 예제를 방문할 때 브라우저에서 소스 보기/이렇게 하면 DataList는 HTML 내보냅니다 볼 수 있습니다 `<table>` 테이블 행이 포함 된 (`<tr>`) 단일 테이블 셀으로 (`<td>`)에 바인딩된 각 항목에는 DataList 합니다. 실제로이 출력은 단일 TemplateField 된 GridView에서 내보내는 동일 합니다. 이후 자습서에서 볼 수 있겠지만, DataList 수 있어 테이블 행당 여러 데이터 원본 레코드를 표시 하는 출력의 추가 사용자 지정을 허용지 않습니다.

HTML 내보내는 원하지 않는 경우 어떻게 `<table>`되지만? 총 및 완료를 효과적으로 제어 데이터 웹 컨트롤에 의해 생성 된 태그에서는 반복기 컨트롤을 사용 해야 합니다. DataList, 같은 반복기 서식 파일에 따라 생성 됩니다. 하지만 반복만 제공 다음과 같은 5 개의 템플릿:

- `HeaderTemplate`제공 된 경우에서 항목 앞에 지정된 된 태그 추가
- `ItemTemplate`항목을 렌더링 하는 데 사용
- `AlternatingItemTemplate`제공 된 대체 항목을 렌더링 하는 데 사용
- `SeparatorTemplate`제공 된 경우 각 항목 사이 지정된 된 태그 추가
- `FooterTemplate`-제공 된 경우 지정된 된 태그 항목 뒤에 추가

ASP.NET에서 제어 글머리 기호 목록의 일부 데이터 원본에서 가져온 데이터를 표시 하는 데 일반적으로 사용한 반복기 1.x 합니다. 이러한 경우는 `HeaderTemplate` 및 `FooterTemplates` 열기 및 닫기는 포함 `<ul>` 태그 각각 동안는 `ItemTemplate` 포함 됩니다 `<li>` databinding 구문 사용 하 여 요소입니다. 이 방법을 계속 사용할 수 있습니다 ASP.NET 2.0에서의 두 예제에서 살펴본 것 처럼는 [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-vb.md) 자습서:

- 에 `Site.master` 마스터 페이지는 반복기는 최상위 사이트 맵 콘텐츠 (기본 보고, 필터링 하는 보고서, 사용자 지정 서식 및 등)의 글머리 기호 목록을 표시 하는 데 사용 된; 다른, 중첩 된 반복기의 하위 섹션을 표시 하는 데 사용한는 최상위 섹션
- `SectionLevelTutorialListing.ascx`는 반복기는 하위 섹션이 현재 사이트 맵 섹션의 글머리 기호 목록이 표시 하는 데 사용한

> [!NOTE]
> ASP.NET 2.0을 새 소개 [BulletedList 컨트롤](https://msdn.microsoft.com/library/ms228101.aspx), 있는 간단한 글머리 기호 목록에 표시 하기 위해 데이터 소스 제어에 바인딩할 수 수 있습니다. BulletedList 컨트롤과 म 필요가 없습니다 목록 관련 HTML; 중 하나를 지정 합니다. 대신, 우리는 단순히 나타냅니다 각 목록 항목에 대 한 텍스트도 표시할 데이터 필드.


반복 모든 데이터 웹 컨트롤을 catch로 사용 됩니다. 필요한 태그를 생성 하는 기존 컨트롤 없으면 반복기 컨트롤 수 있습니다. 을 설명 하기 위해 반복기를 사용 하 여 s 2 단계에서에서 만든 제품 정보 DataList 위에 표시 되는 범주 목록이 남아 있을 수 있도록 합니다. 특히, s 수 있는 단일 행 HTML에 표시 되는 범주 `<table>` 각 범주로 테이블의 열으로 표시 합니다.

이를 위해 제품 정보 DataList 위에 디자이너 도구 상자에서 반복기 컨트롤을 끌어 시작 합니다. 와 마찬가지로 DataList, 반복기 처음 표시는 회색 상자로 해당 템플릿에 정의 된 될 때까지 합니다.


[![반복기는 디자이너에 추가](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image34.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image33.png)

**그림 13**:는 반복기는 디자이너에 추가 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image35.png))


여기서의 반복기 s 스마트 태그에 하나의 옵션만: 데이터 소스 선택 합니다. 새 ObjectDataSource를 만들고 사용 하도록 구성 하려는 경우는 `CategoriesBLL` s 클래스 `GetCategories` 메서드.


[![새 ObjectDataSource 만들기](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image37.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image36.png)

**그림 14**: 새 ObjectDataSource 만들기 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image38.png))


[![ObjectDataSource CategoriesBLL 클래스를 사용 하도록 구성](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image40.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image39.png)

**그림 15**: 구성에 사용 하 여 ObjectDataSource는 `CategoriesBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image41.png))


[![모든 GetCategories 메서드를 사용 하 여 범주에 대 한 정보를 검색 합니다.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image43.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image42.png)

**그림 16**: 검색 정보에 대 한 모든 사용 하 여 범주는 `GetCategories` 메서드 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image44.png))


DataList, 달리 Visual Studio 자동으로 만들어지지 않습니다는 ItemTemplate 반복기에 대 한 데이터 소스에 바인딩한 후 합니다. 또한 s 템플릿에 디자이너를 통해 구성할 수 없습니다 및 선언적으로 지정 해야 합니다.

범주는 단일 행으로 표시 하려면 `<table>` 각 범주에 대 한 열이 있는 반복기 다음과 같은 태그를 생성 해야 합니다.


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample7.html)]

이후는 `<td>Category X</td>` 텍스트는 부분을 반복이 반복기의 ItemTemplate에 표시 됩니다. -앞에 표시 되는 태그 `<table><tr>` -에 배치 됩니다는 `HeaderTemplate` 끝 태그를 액세스 하는 동안 `</tr></table>` -에 배치 됩니다는 `FooterTemplate`합니다. 이러한 템플릿 설정을 입력 하려면 다음 구문에 유형과 왼쪽된 아래 모서리에 원본 단추를 클릭 하 여 ASP.NET 페이지의 선언적 영역으로 이동:


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample8.aspx)]

반복기를 템플릿, 더 이상, nothing에 지정 된 대로 정확 하 게 태그를 내보냅니다. 그림 17 브라우저를 통해 볼 때 반복기의 출력을 보여 줍니다.


[![단일 행 HTML &lt;테이블&gt; 별도 열에 각 범주 나열](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image46.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image45.png)

**그림 17**: A 단일 행 HTML `<table>` 별도 열에 각 범주를 나열 ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image47.png))


## <a name="step-6-improving-the-appearance-of-the-repeater"></a>6 단계: 반복기의 모양을 향상

반복기 내보내는 해당 템플릿에 의해 지정 된 태그를 정확 하 게, 이후가 제공 올바르기도 반복기에 대 한 스타일 관련 속성이 없는 합니다. 반복기에 의해 생성 된 콘텐츠의 모양을 변경 하려면 s 템플릿에 직접 필요한 CSS 또는 HTML 콘텐츠를 수동으로 추가 해야 했습니다.

이 예에서는 s DataList의 대체 행과 같은 배경 색을 대체 범주 열이 있을 수 있도록 합니다. 이를 위해 할당 해야는 `RowStyle` 각 반복기 항목에는 CSS 클래스 및 `AlternatingRowStyle` CSS 클래스를 통해 각 대체 반복기 항목의 `ItemTemplate` 및 `AlternatingItemTemplate` 같이 템플릿:


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample9.aspx)]

S를 텍스트 제품 범주를 사용 하 여 출력에는 머리글 행을 추가할 수도 있습니다. T 열 개수를 결과 우리의 알고 있는 것 때문 `<table>` 는 구성의 모든 열에 걸쳐 보장 되는 머리글 행을 생성 하는 가장 간단한 방법은 사용 하는 *두* `<table>` s입니다. 첫 번째 `<table>` 머리글 행 및 두 번째, 단일 행을 포함 하는 행에는 두 개의 행을 포함 합니다 `<table>` 열이 있는 각 범주에 대 한 시스템에 있습니다. 즉, 다음과 같은 태그를 생성 하려면:


[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample10.html)]

다음 `HeaderTemplate` 및 `FooterTemplate` 원하는 태그가 생성:


[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample11.aspx)]

그림 18 이러한 변경이 이루어진 후 반복기를 보여 줍니다.


[![범주 열 배경색으로 대체 하 고 머리글 행이 포함 됩니다.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image49.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image48.png)

**그림 18**: The 범주 열 대체 배경색 및 머리글 행을 포함 합니다. ([전체 크기 이미지를 보려면 클릭](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image50.png))


## <a name="summary"></a>요약

GridView 컨트롤을 사용 하면 쉽게 표시, 편집, 삭제, 정렬 및 데이터의 페이지 모양은 매우 얻을 하 고 눈금. 모양 세부적 DataList 또는 반복기 컨트롤에 설정 해야 합니다. 두이 컨트롤 모두 BoundFields, CheckBoxFields, 등에 대신 템플릿을 사용 하 여 레코드 집합을 표시 합니다.

DataList는 HTML로 렌더링 `<table>` , 기본적으로 표시 하 각 데이터 원본 레코드를 단일 TemplateField 된 GridView 처럼 단일 테이블 행에 있습니다. 하지만 이후 자습서에서 알 수 있듯이 DataList는 허용 여러 레코드가 테이블 행당 표시 됩니다. 반복기, 반면에 엄격 하 게 내보내는 해당 템플릿;에 지정 된 태그 추가 태그를 추가 하지는 않습니다 하 고 따라서는 대개 아닌 다른 HTML 요소에 데이터를 표시 하는 `<table>` (글머리 기호 목록 등).

DataList 및 반복기는 렌더링 된 출력에서 더 많은 융통성을 제공 하는 동안 GridView에 기본 제공 기능을 많이 부족 합니다. 이후 자습서에서 살펴봅니다 이러한 기능 중 일부 너무 많은 노력을 않고도 다시 연결 될 수 있지만 않습니다 유지에 주의 사용 하 여 DataList 또는 GridView 대신이 구성 요소 반복기는 기능을 해당 기능을 구현 하지 않고도 사용할 수 제한 사용자 자신입니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Yaakov Ellis, Liz Shulok, Randy Schmidt 및 Stacy 공원 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](nested-data-web-controls-cs.md)
[다음](formatting-the-datalist-and-repeater-based-upon-data-vb.md)
