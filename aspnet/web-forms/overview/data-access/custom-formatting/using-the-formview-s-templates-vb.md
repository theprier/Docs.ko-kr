---
uid: web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
title: FormView의 템플릿 (VB)를 사용 하 여 | Microsoft Docs
author: rick-anderson
description: 하지 DetailsView를 달리 FormView 필드로 구성 됩니다. 대신, FormView 템플릿을 사용 하 여 렌더링 됩니다. 이 자습서의 6.를 사용 하 여 살펴보겠습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 67b25f4c-2823-42b6-b07d-1d650b3fd711
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-vb
msc.type: authoredcontent
ms.openlocfilehash: 66ad79c0c385afed75c1888b81328220ee048d19
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37389916"
---
<a name="using-the-formviews-templates-vb"></a>FormView의 템플릿 (VB)를 사용 하 여
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_14_VB.exe) 또는 [PDF 다운로드](using-the-formview-s-templates-vb/_static/datatutorial14vb1.pdf)

> 하지 DetailsView를 달리 FormView 필드로 구성 됩니다. 대신, FormView 템플릿을 사용 하 여 렌더링 됩니다. 살펴보겠습니다이 자습서를 사용 하 여 FormView 컨트롤 데이터의 덜 엄격한 표시를 제공 합니다.


## <a name="introduction"></a>소개

마지막 두 자습서에서 TemplateFields 사용 하는 GridView 및 DetailsView 컨트롤의 출력을 사용자 지정 하는 방법에 살펴보았습니다. TemplateFields 고도로 사용자 지정, 특정 필드에 대 한 내용에 대 한 허용 하지만 끝 GridView 및 DetailsView에 대신 얻을, 표 형태의 모양을 합니다. 다양 한 시나리오에 대 한 표 형식 레이아웃을 이러한 이상적 이지만 유연한, 덜 엄격한 표시 필요한 시간에. 단일 레코드를 표시할 때 이러한 유연한 레이아웃은 FormView 컨트롤을 사용 하 여 합니다.

하지 DetailsView를 달리 FormView 필드로 구성 됩니다. FormView BoundField 또는 TemplateField를 추가할 수 없습니다. 대신, FormView 템플릿을 사용 하 여 렌더링 됩니다. FormView 단일 templatefield로 포함 된 DetailsView 컨트롤 이라고 생각 됩니다. FormView 다음 템플릿을 지원합니다.

- `ItemTemplate` FormView에서 표시 되는 특정 레코드를 렌더링 하는 데 사용
- `HeaderTemplate` 선택적 헤더 행을 지정 하는 데 사용
- `FooterTemplate` 선택적 바닥글 행을 지정 하는 데 사용
- `EmptyDataTemplate` 때 FormView의 `DataSource` 모든 레코드에는 `EmptyDataTemplate` 대신 사용 되는 `ItemTemplate` 컨트롤의 태그를 렌더링 하는 것에 대 한
- `PagerTemplate` 페이징을 사용 있는 FormViews에 대 한 페이징 인터페이스를 사용자 지정할 수 있습니다.
- `EditItemTemplate` / `InsertItemTemplate` 이러한 기능을 지 원하는 FormViews 삽입 인터페이스를 편집 인터페이스 사용자 지정 하는 데 사용

살펴보겠습니다이 자습서를 사용 하 여 FormView 컨트롤이 제품의 표시를 더 융통성을 제공 합니다. 필드 이름, 범주, 공급자 및 등과 FormView의에 대 한 것이 아니라 `ItemTemplate` 헤더 요소를 조합 하 여 이러한 값을 표시 및 `<table>` (그림 1 참조).


[![FormView는 DetailsView 나온 표 형태의 레이아웃의 분류](using-the-formview-s-templates-vb/_static/image2.png)](using-the-formview-s-templates-vb/_static/image1.png)

**그림 1**: FormView 중단 Grid-Like 레이아웃 표시 DetailsView에서 ([큰 이미지를 보려면 클릭](using-the-formview-s-templates-vb/_static/image3.png))


## <a name="step-1-binding-the-data-to-the-formview"></a>1 단계: FormView에 데이터 바인딩

열기는 `FormView.aspx` 페이지 및 디자이너 도구 상자에서 FormView 끕니다. FormView를 처음으로 추가 우리를 지시 하는 회색 상자로 표시 하는 `ItemTemplate` 필요 합니다.


[![FormView는 ItemTemplate 제공 될 때까지 디자이너에서 렌더링할 수 없습니다.](using-the-formview-s-templates-vb/_static/image5.png)](using-the-formview-s-templates-vb/_static/image4.png)

**그림 2**:는 디자이너까지에서 렌더링할 수는 FormView 없는 `ItemTemplate` 제공 됩니다 ([클릭 하 여 큰 이미지 보기](using-the-formview-s-templates-vb/_static/image6.png))


`ItemTemplate` (선언적 구문)를 통해 직접 만들 수 있습니다 또는 FormView 디자이너를 통해 데이터 소스 컨트롤에 바인딩하여 자동으로 생성 될 수 있습니다. 자동 생성이 `ItemTemplate` HTML는 목록 이름을 각 필드 및 레이블을 컨트롤 포함 `Text` 속성 필드의 값에 바인딩합니다. 이 방법은 자동-만듭니다는 `InsertItemTemplate` 및 `EditItemTemplate`, 모두 채워집니다 입력된 컨트롤이 포함 된 각 데이터 소스 컨트롤에서 반환 하는 데이터 필드에 대 한 합니다.

호출 하는 새 ObjectDataSource 컨트롤을 추가 FormView의 스마트 태그에서 템플릿을 자동 생성 하려는 경우는 `ProductsBLL` 클래스의 `GetProducts()` 메서드. 사용 하 여 FormView 만들어집니다는 `ItemTemplate`, `InsertItemTemplate`, 및 `EditItemTemplate`합니다. 소스 보기에서 제거 합니다 `InsertItemTemplate` 및 `EditItemTemplate` 하지에 관심이 있으므로 FormView을 지 원하는 만들기 편집 하거나 아직 삽입 합니다. 다음 내에서 태그를 지웁니다는 `ItemTemplate` 백지에서 작업할 수 있도록 합니다.

대신 작성 하는 경우는 `ItemTemplate` 추가 디자이너 도구 상자에서 끌어와 ObjectDataSource를 구성 하는 수동으로. 그러나 없는 디자이너에서 FormView의 데이터 원본을 설정 합니다. 대신, 소스 뷰로 이동 하 고 수동으로 FormView의를 설정할 `DataSourceID` 속성을는 `ID` ObjectDataSource의 값입니다. 다음으로, 수동으로 추가 된 `ItemTemplate`합니다.

어떤 접근 방식에 관계 없이 되려면,이 시점에서 FormView의 선언적 태그 어떻게 표시 해야 결정:


[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample1.aspx)]

FormView의 스마트 태그를 페이징 사용 확인란을 확인 하려면 잠시 이 추가 `AllowPaging="True"` FormView의 선언적 구문에 대 한 특성입니다. 또한 설정 된 `EnableViewState` 속성을 false로 합니다.

## <a name="step-2-defining-theitemtemplates-markup"></a>2 단계: 정의 된`ItemTemplate`의 태그

페이징을 지원 하기 위해 FormView ObjectDataSource 컨트롤에 바인딩되고 구성를 사용 하 여 준비가 내용을 지정 된 `ItemTemplate`합니다. 이 자습서에서는 저에 표시 되는 제품의 이름을 `<h3>` 제목입니다. 다음 HTML을 사용 하겠습니다 `<table>` 여기서 첫 번째 및 세 번째 열에 속성 이름을 나열 하 고 해당 값을 목록에서 두 번째 및 네 번째 네 열 테이블에 나머지 제품 속성을 표시 합니다.

이 태그는 디자이너에서 FormView의 템플릿 편집 인터페이스를 통해 입력 또는 선언적 구문을 통해 수동으로 입력할 수 있습니다. 템플릿을 사용 하 여 작업 하는 경우 일반적으로 찾을 있습니까 선언적 구문을 통해 직접 작동 하지만 자유롭게 사용 하 여 모든 기술을 익숙한 가장 빠르게입니다.

다음 태그 후 FormView 선언적 태그를 보여 줍니다.를 `ItemTemplate`의 구조 완료 되었습니다.


[!code-aspx[Main](using-the-formview-s-templates-vb/samples/sample2.aspx)]

데이터 바인딩 구문을- `<%# Eval("ProductName") %>`에 예제를 템플릿의 출력에 직접 삽입할 수 있습니다. 즉,이 필요한에 할당할 수 없습니다 레이블 컨트롤의 `Text` 속성입니다. 있다고 예를 들어를 `ProductName` 에 표시 된 값을 `<h3>` 요소를 사용 하 여 `<h3><%# Eval("ProductName") %></h3>`, 렌더링 하는 제품에 대 한 Chai로 `<h3>Chai</h3>`.

`ProductPropertyLabel` 및 `ProductPropertyValue` CSS 클래스 제품 속성 이름과 값의 스타일을 지정 하는 데 사용 되는 `<table>`합니다. 이러한 CSS 클래스에 정의 된 `Styles.css` 발생할 속성 이름을 굵은 하 고 오른쪽 맞춤 및 안쪽 여백 속성 값 오른쪽에 추가 합니다.

개 있으므로 없습니다 CheckBoxFields FormView, 사용할 수 있는 표시 하기 위해는 `Discontinued` 값 확인란으로 고유한 CheckBox 컨트롤을 추가 해야 합니다. `Enabled` 속성을 False로 읽기 전용으로 만들기 확인란의 `Checked` 속성의 값에 바인딩되는 `Discontinued` 데이터 필드입니다.

사용 하 여는 `ItemTemplate` 완료 제품 정보를 훨씬 더 유연한 방식으로 표시 됩니다. FormView (그림 4)이이 자습서에서 생성 된 출력을 사용 하 여 마지막 자습서 (그림 3)의 DetailsView 출력을 비교 합니다.


[![고정 된 DetailsView 출력](using-the-formview-s-templates-vb/_static/image8.png)](using-the-formview-s-templates-vb/_static/image7.png)

**그림 3**: 고정 된 DetailsView 출력 ([큰 이미지를 보려면 클릭](using-the-formview-s-templates-vb/_static/image9.png))


[![유연한 FormView 출력](using-the-formview-s-templates-vb/_static/image11.png)](using-the-formview-s-templates-vb/_static/image10.png)

**그림 4**: 유체 FormView 출력 ([큰 이미지를 보려면 클릭](using-the-formview-s-templates-vb/_static/image12.png))


## <a name="summary"></a>요약

GridView 및 DetailsView 컨트롤에서 TemplateFields 사용 하 여 사용자 지정 출력을 가질 수 있지만 둘 다 여전히 해당 데이터 표 형태의 얻을 형식 제공 합니다. 단일 레코드를 표시 해야 하는 경우 해당 시간에 대 한 더 융통성 레이아웃을 사용 하 여, FormView는 이상적인 합니다. FormView의 DetailsView와 같은 단일 레코드를 렌더링 해당 `DataSource`, 이지만 DetailsView 달리 템플릿의 구성 이며 필드를 지원 하지 않습니다.

이 자습서에서 살펴본 것 처럼 단일 레코드를 표시할 때 FormView 레이아웃의 유연성이 있습니다. 나중에 자습서 살펴보겠습니다 있는 DataList 및 반복기 컨트롤을 동일한 수준의 FormsView, 유연성을 제공 하지만 (예: GridView) 여러 레코드를 표시할 수 있습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자가 E.R. Gilmore 합니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](using-templatefields-in-the-detailsview-control-vb.md)
> [다음](displaying-summary-information-in-the-gridview-s-footer-vb.md)
