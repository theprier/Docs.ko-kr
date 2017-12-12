---
uid: web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
title: "FormView의 템플릿 (VB)를 사용 하 여 | Microsoft Docs"
author: rick-anderson
description: "DetailsView, 달리 FormView 하지 가지 필드로 구성 됩니다. 대신, FormView 템플릿을 사용 하 여 렌더링 됩니다. 이 자습서의 6.를 사용 하 여 검토 합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 67b25f4c-2823-42b6-b07d-1d650b3fd711
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
msc.type: authoredcontent
ms.openlocfilehash: 05e97ce5efeaf72192ed294b946e2249c60007d1
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="using-the-formviews-templates-vb"></a>FormView의 템플릿 (VB)를 사용 하 여
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_14_VB.exe) 또는 [PDF 다운로드](using-the-formview-s-templates-vb/_static/datatutorial14vb1.pdf)

> DetailsView, 달리 FormView 하지 가지 필드로 구성 됩니다. 대신, FormView 템플릿을 사용 하 여 렌더링 됩니다. 이 자습서를 검토 합니다 FormView 컨트롤을 사용 하 여 데이터의 덜 엄격한 표시를 제공 합니다.


## <a name="introduction"></a>소개

마지막 두 개의 자습서에 GridView 및 DetailsView 컨트롤 출력 TemplateFields를 사용 하 여 사용자 지정 하는 방법에 살펴보았습니다. 특정 필드를 사용자 지정할 높은 수에 대 한 내용에 대 한 TemplateFields 허용 하지만, 결국에서 GridView와 DetailsView 모양이 아니라 얻을, 눈금. 대부분의 시나리오에 대 한 표 형식 레이아웃은 적절 하지만 유연한, 더 융통성 디스플레이 필요 때때로 합니다. 단일 레코드를 표시할 때 이러한 유체 레이아웃은 FormView 컨트롤을 사용 하 여 가능 합니다.

DetailsView, 달리 FormView 하지 가지 필드로 구성 됩니다. BoundField 또는 TemplateField는 FormView에 추가할 수 없습니다. 대신, FormView 템플릿을 사용 하 여 렌더링 됩니다. FormView 단일 TemplateField를 포함 하는 DetailsView 컨트롤 라고 생각 됩니다. FormView 다음 서식 파일을 지원합니다.

- `ItemTemplate`FormView에서 표시 되는 특정 레코드를 렌더링 하는 데 사용
- `HeaderTemplate`선택적 헤더 행을 지정 하는 데 사용
- `FooterTemplate`선택적 바닥글 행을 지정 하는 데 사용
- `EmptyDataTemplate`때 FormView의 `DataSource` 에 게 없는 경우 모든 레코드는 `EmptyDataTemplate` 대신에 사용 되는 `ItemTemplate` 컨트롤의 태그를 렌더링 하기 위한
- `PagerTemplate`페이징이 설정 되어 FormViews에 대 한 페이징 인터페이스를 사용자 지정 하는 데 사용할 수 있습니다.
- `EditItemTemplate` / `InsertItemTemplate`이러한 기능을 지 원하는 FormViews에 대 한 편집 인터페이스 또는 삽입 인터페이스를 사용자 지정 하는 데 사용

이 자습서를 검토 합니다 FormView 컨트롤을 사용 하 여 제품의 표시를 더 융통성을 제공 합니다. 이름, 범주, 공급자 및 이런 식으로 FormView의에 대 한 필드는 것이 아니라 `ItemTemplate` 헤더 요소를 조합 하 여 이러한 값이 표시 됩니다는 및 `<table>` (그림 1 참조).


[![FormView는 DetailsView에 표 모양의 레이아웃의 분류](using-the-formview-s-templates-vb/_static/image2.png)](using-the-formview-s-templates-vb/_static/image1.png)

**그림 1**: FormView 벗어나는 Grid-Like 레이아웃 표시 DetailsView에서 ([전체 크기 이미지를 보려면 클릭](using-the-formview-s-templates-vb/_static/image3.png))


## <a name="step-1-binding-the-data-to-the-formview"></a>1 단계: FormView에 데이터 바인딩

열기는 `FormView.aspx` 페이지 하 고는 FormView 디자이너 도구 상자에서 끌어 옵니다. FormView를 처음 추가할 때 지시 우리는 회색 상자로 표시 하는 `ItemTemplate` 필요 합니다.


[![FormView에 ItemTemplate 제공 될 때까지 디자이너에서 렌더링할 수 없습니다.](using-the-formview-s-templates-vb/_static/image5.png)](using-the-formview-s-templates-vb/_static/image4.png)

**그림 2**:는 디자이너 될 때까지에서 렌더링할 수는 FormView 없는 `ItemTemplate` 제공 됩니다 ([전체 크기 이미지를 보려면 클릭](using-the-formview-s-templates-vb/_static/image6.png))


`ItemTemplate` 또는 FormView 디자이너를 통해 데이터 소스 컨트롤에 바인딩하여 자동 생성 될 수 있습니다 (선언적 구문)를 통해 직접 만들 수 있습니다. 자동 생성이 `ItemTemplate` 는 목록 이름 각 필드 및 레이블을 컨트롤 HTML이 포함 되어 `Text` 속성 필드의 값에 바인딩합니다. 이 방법은 자동-만듭니다는 `InsertItemTemplate` 및 `EditItemTemplate`, 둘 다 채워집니다 입력된 컨트롤의 각 데이터 소스 제어에서 반환 된 데이터 필드에 대 한 합니다.

호출 하는 새 ObjectDataSource 컨트롤 추가 FormView의 스마트 태그에서 서식 파일을 자동 생성 하려는 경우는 `ProductsBLL` 클래스의 `GetProducts()` 메서드. 이렇게 하면와 FormView 만들어집니다는 `ItemTemplate`, `InsertItemTemplate`, 및 `EditItemTemplate`합니다. 소스 뷰에서 제거는 `InsertItemTemplate` 및 `EditItemTemplate` म에 관심이 있으므로 FormView 지 원하는 만들기 편집 하거나 아직 삽입 합니다. 다음 내에서 태그를 비웁니다는 `ItemTemplate` 백지에서 작동 하도록 할 수 있도록 합니다.

만들려면 하는 경우는 `ItemTemplate` 추가 디자이너 도구 상자에서 끌어서는 ObjectDataSource를 구성 하는 수동으로 합니다. 그러나 설정 하지 않습니다 FormView의 데이터 원본 디자이너에서. 대신, 소스 보기로 이동 하 고 수동으로 FormView의 설정 `DataSourceID` 속성을는 `ID` 는 ObjectDataSource의 값입니다. 다음에 수동으로 추가 된 `ItemTemplate`합니다.

어떤 방법에 관계 없이 되려면,이 시점에서 FormView의 선언적 태그 보기와 같은 모습 결정:


[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample1.aspx)]

FormView의 스마트 태그; 페이징 사용 확인란을 확인 하려면 잠시 이렇게 하면 추가 됩니다는 `AllowPaging="True"` 특성을 FormView의 선언 구문입니다. 또한 설정에서 `EnableViewState` 속성을 false로 합니다.

## <a name="step-2-defining-theitemtemplates-markup"></a>2 단계: 정의`ItemTemplate`의 태그

페이징을 지원 하기 위해 FormView ObjectDataSource 컨트롤에 바인딩된 구성 및 사용에 대 한 콘텐츠를 지정 하려면 준비 되었는지는 `ItemTemplate`합니다. 이 자습서에서는 죠 제품의 이름에 표시 되는 `<h3>` 제목입니다. 그런 다음, HTML을 사용해 봅시다 `<table>` 첫 번째 및 세 번째 열에 속성 이름을 나열 하 고 해당 값을 목록에서 두 번째 및 네 번째 네 열 테이블의 나머지 제품 속성을 표시 합니다.

이 태그는 FormView의 템플릿 디자이너에서 편집 인터페이스를 통해에 입력 또는 선언적 구문을 통해 수동으로 입력할 수 있습니다. 템플릿으로 작업 하는 경우 일반적으로 찾습니까 신속 하 게 선언적 구문와 직접 작동 하지만 자유롭게 모든 기술을 익숙해지면 가장을 사용할 수입니다.

다음 태그 후 FormView 선언적 태그를 보여 줍니다.는 `ItemTemplate`의 구조 완료 되었습니다.


[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample2.aspx)]

구문이- `<%# Eval("ProductName") %>`, 예제 서식 파일의 출력에 직접 삽입 될 수 있습니다. 즉,이 필요에 할당할 수 없습니다 레이블 컨트롤의 `Text` 속성입니다. 예를 들어는 `ProductName` 값에 표시 되는 `<h3>` 요소를 사용 하 여 `<h3><%# Eval("ProductName") %></h3>`, 렌더링 하는 제품에 대 한 Chai로 `<h3>Chai</h3>`합니다.

`ProductPropertyLabel` 및 `ProductPropertyValue` CSS 클래스를 제품 속성 이름 및 값의 스타일을 지정 하는 데 사용 되는 `<table>`합니다. 이러한 CSS 클래스에 정의 된 `Styles.css` 발생할 속성 이름을 굵은 하 고 오른쪽 맞춤 하 고 속성 값에 안쪽 여백에 대 한 권한을 추가 합니다.

이어서 없습니다 CheckBoxFields FormView를 사용할 수 있는 보여 주기 위해는 `Discontinued` 값 된 확인란으로 고유한 CheckBox 컨트롤을 추가 해야 합니다. `Enabled` 속성이 False, 읽기 전용, 설정 및 확인란의 `Checked` 속성의 값에 바인딩되는 `Discontinued` 데이터 필드입니다.

와 `ItemTemplate` 완료 제품 정보는 유연한 방식으로 표시 됩니다. FormView (그림 4)이이 자습서에서 생성 된 출력 된 마지막 자습서 (그림 3)에서 DetailsView 출력을 비교 합니다.


[![고정 된 관계로 DetailsView 출력](using-the-formview-s-templates-vb/_static/image8.png)](using-the-formview-s-templates-vb/_static/image7.png)

**그림 3**: 고정 된 관계로 DetailsView 출력 ([전체 크기 이미지를 보려면 클릭](using-the-formview-s-templates-vb/_static/image9.png))


[![유체 FormView 출력](using-the-formview-s-templates-vb/_static/image11.png)](using-the-formview-s-templates-vb/_static/image10.png)

**그림 4**: 유체 FormView 출력 ([전체 크기 이미지를 보려면 클릭](using-the-formview-s-templates-vb/_static/image12.png))


## <a name="summary"></a>요약

GridView 및 DetailsView 컨트롤 TemplateFields를 사용 하 여 사용자 지정 출력 있을 수 있지만, 둘 다 여전히 자신의 데이터에에서 표 모양의 얻을으로 제공 합니다. 단일 레코드를 표시 해야 하는 경우 해당 시간에 대 한 더 융통성 레이아웃을 사용 하 여 FormView는 응용 프로그램을 합니다. DetailsView, 같은 FormView에서 하나의 레코드를 렌더링 해당 `DataSource`, 있지만 DetailsView 달리 템플릿의 구성 하 고 필드를 지원 하지 않습니다.

이 자습서에서 살펴본 것 처럼 단일 레코드를 표시할 때 FormView 보다 유연한 레이아웃에 있습니다. 이후 자습서 살펴봅니다 있는 DataList 및 반복기 컨트롤을 동일한 수준의 FormsView,으로 유연성을 제공 하지만 (예: GridView) 여러 레코드를 표시할 수 있습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자가 E.R. Gilmore 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](using-templatefields-in-the-detailsview-control-vb.md)
[다음](displaying-summary-information-in-the-gridview-s-footer-vb.md)
