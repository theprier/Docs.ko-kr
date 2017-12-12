---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-vb
title: "라디오 단추의 (VB) GridView 열 추가 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 라디오 단추의 열 단일 행을 선택 하는 보다 직관적인 방법으로 사용자를 제공 하는 GridView 컨트롤을 추가 하는 방법..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/06/2007
ms.topic: article
ms.assetid: 2e31b60b-8723-4f14-b7ee-37859454dc3b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-vb
msc.type: authoredcontent
ms.openlocfilehash: 9d34fb64984313e5e2844d36a70f3ab08560654e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="adding-a-gridview-column-of-radio-buttons-vb"></a>라디오 단추의 (VB) GridView 열 추가
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_51_VB.exe) 또는 [PDF 다운로드](adding-a-gridview-column-of-radio-buttons-vb/_static/datatutorial51vb1.pdf)

> 이 자습서에 GridView의 단일 행을 선택 하는 보다 직관적인 방법으로 사용자를 제공 하는 GridView 컨트롤의 라디오 단추 열을 추가 하는 방법을 살펴봅니다.


## <a name="introduction"></a>소개

GridView 컨트롤은 다양 한 기본 제공 기능을 제공합니다. 여러 텍스트, 이미지, 하이퍼링크 및 단추를 표시 하기 위한 여러 필드가 포함 됩니다. 추가 사용자 지정 서식 파일을 지원합니다. 마우스 클릭 몇 번 것 s 가능한 각 행을 단추를 선택할 수 있는 GridView로 만들거나 편집 또는 삭제 기능을 사용 하도록 설정 합니다. 제공 된 기능이 풍부한 불구 하 고 종종 경우가 추가는 지원 되지 않는 기능 추가할 필요 합니다. 이 자습서 및 다음 두 개의 추가 기능을 포함 하도록 GridView의 기능을 개선 하는 방법을 검토 합니다.

이 자습서와 다음 행 선택 프로세스 향상에 집중 합니다. 검사 하는 대로 [마스터/세부 정보 DetailView 선택 가능한 마스터 GridView 사용에 대해 자세히 설명](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md), 선택 단추를 포함 하는 GridView에는 CommandField 추가할 수 있습니다. 포스트백 계속 클릭 하면 및 GridView의 `SelectedIndex` 속성은 해당 선택 단추를 클릭 한 행의 인덱스를 업데이트 합니다. 에 [마스터/세부 정보 DetailView 선택 가능한 마스터 GridView 사용에 대해 자세히 설명](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md) 자습서, 선택된 된 GridView 행에 대 한 정보를 표시 하려면이 기능을 사용 하는 방법에 살펴보았습니다.

선택 단추 다양 한 상황에서 작동 하는 동안 다른 사용자도 작동 하지 않을 수 있습니다. 단추를 사용 하는 대신 다른 두 사용자 인터페이스 요소는 일반적으로 선택에 사용 되: 라디오 단추와 확인란을 선택 합니다. 하 고 선택 단추 대신 각 행 포함 확인란 또는 라디오 단추를 GridView를 추가할 수 있습니다. 시나리오에만 선택할 수는 GridView 레코드 중 하나에서 선택 단추를 통해 라디오 단추 기본 수 있습니다. 여기서는 사용자가 여러 개의 메시지를 삭제는 확인란을 선택 해야 하는 웹 기반 전자 메일 응용 프로그램의 여러 레코드와 같은 사용자 잠재적으로 선택할 수 있는 경우에 선택 단추 또는 라디오 단추에서 사용할 수 없는 기능을 제공 합니다. 사용자 인터페이스입니다.

이 자습서는 GridView에 라디오 단추의 열을 추가 하는 방법을 살펴봅니다. 확인란을 사용 하 여 탐색 하는 자습서를 진행 합니다.

## <a name="step-1-creating-the-enhancing-the-gridview-web-pages"></a>1 단계: 향상 GridView 웹 페이지 만들기

라디오 단추의 열을 포함 하도록 GridView 향상을 시작 하기 전에 s를 먼저 잠시과이 자습서는 다음 두 사용 해야 하는 웹 사이트 프로젝트에 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `EnhancedGridView`합니다. 다음에 해당 폴더에 있는 각 페이지에 연결할 수 있도록 다음 ASP.NET 페이지 추가 `Site.master` 마스터 페이지:

- `Default.aspx`
- `RadioButtonField.aspx`
- `CheckBoxField.aspx`
- `InsertThroughFooter.aspx`


![SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가](adding-a-gridview-column-of-radio-buttons-vb/_static/image1.gif)

**그림 1**: SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더에서와 같이 `Default.aspx` 에 `EnhancedGridView` 폴더는 해당 섹션의 자습서를 나열 합니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 이 기능을 제공 하는 사용자 정의 컨트롤입니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx`의 디자인 뷰에서 페이지 하려면 솔루션 탐색기에서 끌어서 합니다.


[![Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가](adding-a-gridview-column-of-radio-buttons-vb/_static/image2.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image1.png)

**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image2.png))


마지막으로, 이러한 4 개 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 특히, 사용 후에 다음 태그를 추가할 SqlDataSource 컨트롤 `<siteMapNode>`:


[!code-xml[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 브라우저를 통해 자습서 웹 사이트를 보려면 보십시오. 왼쪽 메뉴에는 이제 편집, 삽입 및 삭제 자습서에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 향상 GridView 자습서에 대 한 항목을 포함](adding-a-gridview-column-of-radio-buttons-vb/_static/image3.gif)

**그림 3**: 이제 사이트 맵 향상 GridView 자습서에 대 한 항목을 포함


## <a name="step-2-displaying-the-suppliers-in-a-gridview"></a>2 단계:는 GridView에 공급 업체를 표시합니다.

이 자습서에서는 사용 하는 GridView 생성할 s에 대 한 라디오 단추를 제공 하는 각 GridView 행과 미국에서 공급 업체를 나열 합니다. 라디오 단추를 통해 공급자를 선택한 후 사용자는 단추를 클릭 하 여 공급 업체의 제품을 볼 수 있습니다. 이 작업은 trivial 보일 수도, 동안 하기 까다로운 하는 미묘한의 여러 가지가 있습니다. 하기 전에 이러한 미묘한, 공급 업체를 나열 하는 GridView를 먼저 가져온 s가 있습니다.

열어 시작는 `RadioButtonField.aspx` 페이지에 `EnhancedGridView` 는 GridView 디자이너 도구 상자에서 끌어 폴더입니다. GridView s 설정 `ID` 를 `Suppliers` 하 고, 해당 스마트 태그에서 새 데이터 원본을 만들려면 선택 합니다. 특히, 라는 ObjectDataSource를 만들 `SuppliersDataSource` 에서 해당 데이터를 가져오고 하는 `SuppliersBLL` 개체입니다.


[![SuppliersDataSource 라는 새 ObjectDataSource 만들기](adding-a-gridview-column-of-radio-buttons-vb/_static/image4.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image3.png)

**그림 4**: 명명 된 새 ObjectDataSource 만드는 `SuppliersDataSource` ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image4.png))


[![ObjectDataSource SuppliersBLL 클래스를 사용 하도록 구성](adding-a-gridview-column-of-radio-buttons-vb/_static/image5.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image5.png)

**그림 5**: 구성에 사용 하 여 ObjectDataSource는 `SuppliersBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image6.png))


미국에 공급 업체에서 제공 목록 하고자 하므로 선택은 `GetSuppliersByCountry(country)` 선택 탭의 드롭다운 목록에서 메서드.


[![ObjectDataSource SuppliersBLL 클래스를 사용 하도록 구성](adding-a-gridview-column-of-radio-buttons-vb/_static/image6.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image7.png)

**그림 6**: 구성에 사용 하 여 ObjectDataSource는 `SuppliersBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image8.png))


업데이트 탭에서 선택 옵션 (없음) 한 다음을 클릭 합니다.


[![ObjectDataSource SuppliersBLL 클래스를 사용 하도록 구성](adding-a-gridview-column-of-radio-buttons-vb/_static/image7.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image9.png)

**그림 7**: 구성에 사용 하 여 ObjectDataSource는 `SuppliersBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image10.png))


이후는 `GetSuppliersByCountry(country)` 매개 변수를 허용 하는 메서드, 데이터 소스 구성 마법사에서 해당 매개 변수 원본에 대 한 우리 요구 합니다. 하드 코드 된 값 (이 예: 미국)를 지정 하려면 소스 드롭 다운 목록 None으로 설정 하 고 텍스트 상자에 기본값을 입력 매개 변수를 둡니다. 마법사를 완료 하려면 마침을 클릭 합니다.


[![USA를 사용 하 여 매개 변수 국가 대 한 기본 값으로](adding-a-gridview-column-of-radio-buttons-vb/_static/image8.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image11.png)

**그림 8**:에 대 한 기본 값으로 사용 하 여 미국은 `country` 매개 변수 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image12.png))


마법사를 완료 한 후 GridView 각 공급 업체 데이터 필드에 대 한 BoundField 포함 됩니다. 제거 제외한 모두 `CompanyName`, `City`, 및 `Country` BoundFields, 이름 바꾸기 및는 `CompanyName` BoundFields `HeaderText` 공급자에 게 속성입니다. 이렇게 한 다음, GridView 및 ObjectDataSource 선언적 구문 다음과 비슷해야 합니다.


[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample2.aspx)]

이 자습서에 대 한 s를 공급자 목록와 동일한 페이지에 또는 다른 페이지에서 선택한 공급자를 보려는 사용자의 제품 수 있습니다. 이 위해 페이지에 두 단추 웹 컨트롤을 추가 합니다. I 했습니다 집합은 `ID` 를 이러한 두 단추의 s `ListProducts` 및 `SendToProducts`, 이라는 개념으로 때 `ListProducts` 클릭할 포스트백이 발생 하 고 선택한 공급 업체의 제품 있지만 동일한 페이지에 나열 됩니다 `SendToProducts` 를 클릭 하면 사용자는 제품을 나열 하는 다른 페이지로 마을로 됩니다.

그림 9는 `Suppliers` GridView 및 두 개의 단추 웹 브라우저를 통해 볼 때를 제어 합니다.


[![미국에서 공급 업체에서 제공에 들어 있는 이름, 도시, 및 국가 정보 나열](adding-a-gridview-column-of-radio-buttons-vb/_static/image9.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image13.png)

**그림 9**: USA가 해당 이름, 도시, 및 국가 정보 나열에서 공급 하는 것 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image14.png))


## <a name="step-3-adding-a-column-of-radio-buttons"></a>3 단계: 라디오 단추의 열 추가

이 시점에서 `Suppliers` GridView에 3 개의 BoundFields 미국에 회사 이름, 도시, 및 각 공급 업체의 국가 표시 합니다. 그러나 라디오 단추의 열이 없는 여전히 것입니다. 그러나 GridView 대상이 t는 기본 제공 RadioButtonField, 그렇지 않으면 추가할 수 있는 표에 하 고 수행할 수를 포함 합니다. 대신, 우리를 TemplateField를 추가 하 고 구성할 수는 `ItemTemplate` 때문에 각 GridView 행에 대 한 라디오 단추, 라디오 단추를 렌더링 하 합니다.

RadioButton 웹 컨트롤을 추가 하 여 원하는 사용자 인터페이스를 구현할 수 있습니다 가정 수 처음에 `ItemTemplate` 를 TemplateField입니다. 이 실제로 단일 라디오 단추는 GridView의 각 행에에서는 추가 라디오 단추 그룹화 할 수 없습니다 및 상호 배타적인 하지 않습니다. 즉, 최종 사용자가을 GridView에서 동시에 여러 라디오 단추를 선택할 수 있습니다.

Let s 하므로이 접근 방식을 구현를 TemplateField RadioButton 웹 컨트롤을 사용 하 여 필요한 기능을 제공 하지 않습니다, 경우에 s 결과 라디오 단추 그룹화 되지 않은 이유를 확인 하는 것이 좋습니다. 먼저를 TemplateField 가장 왼쪽의 필드를 만드는 Suppliers GridView에 추가 합니다. 다음으로, GridView s 스마트 태그에서 템플릿 편집 링크를 클릭 하 고 TemplateField s에 도구 상자에서 RadioButton 웹 컨트롤을 끌어 `ItemTemplate` (그림 10 참조). RadioButton s 설정 `ID` 속성을 `RowSelector` 및 `GroupName` 속성을 `SuppliersGroup`합니다.


[![ItemTemplate에 RadioButton 웹 컨트롤 추가](adding-a-gridview-column-of-radio-buttons-vb/_static/image10.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image15.png)

**그림 10**: RadioButton 웹 컨트롤을 추가 `ItemTemplate` ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image16.png))


디자이너를 통해 추가 하는이 코드를 변경한 후 GridView의 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample3.aspx)]

RadioButton s [ `GroupName` 속성](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.radiobutton.groupname(VS.80).aspx) 일련의 라디오 단추 그룹화 데 사용 됩니다. 과 동일한 모든 RadioButton 컨트롤 `GroupName` 값 그룹화; 것으로 간주 됩니다 한 번에 하나의 라디오 단추 그룹에서 선택할 수 있습니다. `GroupName` s 렌더링 된 라디오 단추에 대 한 값을 지정 하는 속성 `name` 특성입니다. 브라우저의 라디오 단추를 검사 하 여 `name` 라디오 확인 하기 위해 특성 단추 그룹화 합니다.

RadioButton 웹 컨트롤에 추가 `ItemTemplate`브라우저를 통해이 페이지를 방문 하 고 s 그리드 행에 있는 라디오 단추를 클릭 합니다. 라디오 단추 그룹화 되지 않고 방법을 예 고 그림 11로의 모든 행을 선택 하 여 보여 줍니다.


[![그룹화 되지 않고 GridView의 라디오 단추를](adding-a-gridview-column-of-radio-buttons-vb/_static/image11.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image17.png)

**그림 11**: GridView의 라디오 단추 그룹화 되지 않고는 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image18.png))


라디오 단추 그룹화 되지 않은 이유 때문입니다의 렌더링 된 `name` 특성은 동일 하더라도 다른 `GroupName` 속성을 설정 합니다. 이러한 차이 보려면 브라우저에서 소스 보기/수행 하 고 라디오 단추 태그를 검사 합니다.


[!code-html[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample4.html)]

모두 통지는 `name` 및 `id` 특성 속성 창에서 지정 된 대로 정확한 값은 아니지만 여러 개의 다른 앞에 추가 됩니다 `ID` 값입니다. 추가 `ID` 는 렌더링 된 앞에 추가 값 `id` 및 `name` 특성은는 `ID` s 라디오 단추 부모 컨트롤의 `GridViewRow` s `ID` s, GridView의 `ID`, 콘텐츠 컨트롤 s `ID`, 및 Web Form의 `ID`합니다. 이러한 `ID` s 수 있도록 추가 각각 렌더링 GridView에서 웹 컨트롤에는 고유한 `id` 및 `name` 값입니다.

각각 렌더링 제어 요구 사항 다른 `name` 및 `id` 이 브라우저 클라이언트 쪽 방법을 식별 하는 웹 서버에 어떤 작업에 있는 각 컨트롤을 고유 하 게 식별 하는 방법을 또는 변경 포스트백에서 발생 했습니다. 예를 들어 상태가 변경 된 RadioButton s 확인할 때마다 일부 서버 쪽 코드를 실행 하 려 한다고 가정 합니다. RadioButton s를 설정 하 여이 위해 수 `AutoPostBack` 속성을 `True` 및에 대 한 이벤트 처리기 만들기는 `CheckChanged` 이벤트입니다. 그러나 경우 렌더링 된 `name` 및 `id` 값은 모든 라디오 단추의 같을에 포스트백 된 어떤 구체적인 확인할 수 없습니다 것 RadioButton이 클릭 되었습니다.

짧은 RadioButton 웹 컨트롤을 사용 하는 GridView에서 라디오 단추 열을 만들 수 없음을입니다. 대신, 태그를 적절 한 각 GridView 행에 삽입 됩니다 되도록 대신 낡은 기술을 사용 해야 했습니다.

> [!NOTE]
> RadioButton 웹 컨트롤을 라디오 단추는 서식 파일에 추가 될 때 HTML 컨트롤의 고유 포함 됩니다 처럼 `name` 특성을 그룹화 하지 않고 눈금에서 라디오 단추 만들기. HTML 컨트롤 모르는 경우 자유롭게이 주석은 무시 ASP.NET 2.0에 특히 HTML 컨트롤 사용은 거의 없습니다. 더 자세히 알고 싶은 경우 보지만 [K. Scott Allen](http://odetocode.com/blogs/scott/default.aspx) s 블로그 항목 [웹 컨트롤 및 HTML 컨트롤](http://www.odetocode.com/Articles/348.aspx)합니다.


## <a name="using-a-literal-control-to-inject-radio-button-markup"></a>리터럴 제어를 사용 하 여 라디오 단추 태그를 삽입 합니다.

모든 GridView 안에서 라디오 단추를 올바르게 그룹화 하려면 수동으로에 라디오 단추 태그를 삽입 해야는 `ItemTemplate`합니다. 각 라디오 단추를 필요한 동일한 `name` 특성은 고유한 필요 하지만 `id` (경우 클라이언트 쪽 스크립트를 통해 라디오 단추에 액세스 하려는) 특성입니다. 사용자가 라디오 단추를 선택 하 고 페이지를 다시 게시 후 브라우저 반환 되지 않음을 s 선택 된 라디오 단추의 값 `value` 특성입니다. 따라서 각 라디오 단추는 고유 해야 합니다 `value` 특성입니다. 마지막으로 다시 게시 될 필요를 추가 해야 하는 `checked` 특성을 선택 하지 않으면 사용자가 항목을 선택 하 고 다시 게시 하는 하나의 라디오 단추, 라디오 단추 돌아갑니다 기본 상태로 (모두 선택 되지 않음).

서식 파일에 낮은 수준의 태그를 삽입 하기 위해 수행할 수 있는 방법은 두 가지가 있습니다. 하나 태그와 코드 숨김 클래스에 정의 된 메서드를 서식 지정에 대 한 호출을 수행 하는 것입니다. 이 방법을 먼저 설명한는 [GridView 컨트롤에 사용 하 여 TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) 자습서입니다. 이 경우 것 다음과 같이 표시 될 수 있습니다.


[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample5.aspx)]

여기에서 `GetUniqueRadioButton` 및 `GetRadioButtonValue` 적절 한을 반환 하는 코드 숨김 클래스에 정의 된 메서드 것 `id` 및 `value` 특성 각 라디오 단추에 대 한 값입니다. 이 방법은 잘 할당는 `id` 및 `value` 특성 이지만 지정 해야 할 때는 짧은 대체는 `checked` 데이터 먼저 GridView에 바인딩될 때 구문이 실행 되므로 특성 값입니다. 따라서 GridView에 뷰 상태를 사용할 수 있는 경우 형식 지정 메서드는만 발생 시기는 페이지가 처음 로드 (또는 데이터 원본에 GridView 명시적으로 리바운드 되는 경우)을 설정 하는 함수가 따라서는 `checked` t 성공한 특성에 대해 호출할 수 다시 게시 합니다. 그 대신 미묘한 문제가 s 합니다 사용 하지 않으면이 있으므로이 문서에서는 다루지 않습니다 약간 합니다. 그러나 I, 보시기 위의 방식을 사용 하 여 작업과 말아야 통해 걸려 가져올 것 지점에 합니다. 이러한는 연습-이득 t에 액세스할 수 가까이 작업 버전, 하는 동안 GridView 및 데이터 바인딩 수명 주기에 대 한 깊은 이해가 식을 고 취합니다 데 도움이 됩니다.

추가 하는 다른 삽입 사용자 지정 방법 템플릿과이 자습서에 사용할 예정 접근 방식을 하위 수준 태그입니다는 [리터럴 제어](https://msdn.microsoft.com/en-us/library/sz4949ks(VS.80).aspx) 서식 파일에 있습니다. 그런 다음, GridView s `RowCreated` 또는 `RowDataBound` 이벤트 처리기를 Literal 컨트롤을 프로그래밍 방식으로 액세스할 수 있습니다 및 해당 `Text` 속성을 내보내려면 태그를 설정 합니다.

RadioButton TemplateField s에서 제거 하 여 시작 `ItemTemplate`, 리터럴 제어 바꿉니다. S 리터럴 제어 설정 `ID` 를 `RadioButtonMarkup`합니다.


[![ItemTemplate에 리터럴 컨트롤 추가](adding-a-gridview-column-of-radio-buttons-vb/_static/image12.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image19.png)

**그림 12**: 리터럴 컨트롤을 추가 `ItemTemplate` ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image20.png))


다음으로 GridView s에 대 한 이벤트 처리기를 만들고 `RowCreated` 이벤트입니다. `RowCreated` 이벤트가 추가 된 모든 행, 여부는 데이터는 되 고 다시 바인딩할 GridView에 한 번 발생 합니다. 즉 포스트백에도 데이터 뷰 상태에서 다시 로드 되는 `RowCreated` 이벤트 여전히 발생 하 고이 대신 사용 하는 이유는 `RowDataBound` (있는 발생만 때 데이터는 명시적으로 데이터에 바인딩된 웹 컨트롤).

이 이벤트 처리기에서만 포함 하려고 하는 경우 계속 하려면 다시 데이터 행을 처리 했습니다. 각 데이터 행에 대 한 프로그래밍 방식으로 참조 하려고는 `RadioButtonMarkup` 리터럴 제어 집합과 해당 `Text` 속성을 생성 하는 태그를 합니다. 내보낸 태그 라디오 만듭니다 다음 코드에서 볼 수 있듯이 갖는 단추 `name` 특성이로 설정 된 `SuppliersGroup`, 해당 `id` 특성이로 설정 된 `RowSelectorX`여기서 *X* 는 GridView 행의 인덱스 및 해당 `value` 특성은 GridView 행의 인덱스로 설정 합니다.


[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample6.vb)]

이 연습 GridView 행을 선택 하 고 포스트백이 발생할 때의 `SupplierID` 선택한 공급 업체의 합니다. 따라서 고 생각 각 라디오 단추의 값이 실제 되어야 함을 `SupplierID` (대신 GridView 행의 인덱스). 특정 상황에서 작동할 수는 있지만이 맹목적으로 수락 및 처리에 보안 위험이 됩니다는 `SupplierID`합니다. 예를 들어 우리의 GridView 미국에만 해당 공급자를 나열합니다. 그러나 경우는 `SupplierID` 유해 사용자 조작에서 중지 하려면 어떤 s 라디오 단추에서 직접 전달 되는 `SupplierID` 포스트백에 다시 전송 값? 로 행 인덱스를 사용 하 여는 `value`, 한 다음 가져와 `SupplierID` 에서 포스트백에는 `DataKeys` 컬렉션 수 인지 확인 하는 사용자만 사용 하는 `SupplierID` GridView 행 중 하나를 연관 된 값입니다.

이 이벤트 처리기 코드를 추가한 후 브라우저에서 페이지를 테스트 하는 데 1 분을 소요 됩니다. 먼저 해당 하나의 라디오 참고 눈금에서 단추를 한 번에 선택할 수 있습니다. 그러나 포스트백이 발생할 라디오 단추를 선택한 단추 중 하나를 클릭 하 여, 시점과 모든 라디오 단추를 초기 상태로 되돌리는 (즉, 다시 게시 될 선택 된 라디오 단추는 더 이상 선택). 이 문제를 해결 하려면 보강 해야는 `RowCreated` 포스트백에서 보낸 선택 된 라디오 단추 인덱스 검사 및 추가 있도록 이벤트 처리기는 `checked="checked"` 특성 내보낸된 태그를 일치 하는 행 인덱스 항목을 합니다.

포스트백 발생할 때 브라우저에서 다시 보내는 `name` 및 `value` 선택 된 라디오 단추의 합니다. 값 프로그래밍 방식으로 검색할 수를 사용 하 여 `Request.Form("name")`합니다. [ `Request.Form` 속성](https://msdn.microsoft.com/en-us/library/system.web.httprequest.form.aspx) 제공는 [ `NameValueCollection` ](https://msdn.microsoft.com/en-us/library/system.collections.specialized.namevaluecollection.aspx) 폼 변수를 나타내는입니다. 폼 변수 이름 및 웹 페이지에 있는 양식 필드의 값은 고 포스트백 계속 때마다 웹 브라우저에서 다시 전송 됩니다. 때문에 렌더링 된 `name` GridView에 있는 라디오 단추의 특성은 `SuppliersGroup`웹 페이지가 브라우저 송신할 다시 게시 될 때, `SuppliersGroup=valueOfSelectedRadioButton` (함께 다른 양식 필드) 웹 서버에 다시 합니다. 이 정보에서 액세스할 수 있습니다는 `Request.Form` 사용 하 여 속성: `Request.Form("SuppliersGroup")`합니다.

에서는 이후 합니다 필요 결정 선택한 라디오 단추의 인덱스를 에서만 하지는 `RowCreated` 의 이벤트 처리기는 `Click` Button 웹 컨트롤에 대 한 이벤트 처리기를 통해 s 추가 `SuppliersSelectedIndex` 속성 반환하는코드숨김클래스를`-1`없는 라디오 단추를 선택한 경우 및 선택한 인덱스의 라디오 단추 중 하나를 선택 하는 경우.


[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample7.vb)]

추가 된이 속성을 추가 하려면 알는 `checked="checked"` 태그에는 `RowCreated` 이벤트 처리기 때 `SuppliersSelectedIndex` 같음 `e.Row.RowIndex`합니다. 이 논리를 포함 하도록 이벤트 처리기를 업데이트 합니다.


[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample8.vb)]

이러한 변경으로 인해 선택 된 라디오 단추 선택 된 상태로 유지 하 여 포스트백 후 합니다. 페이지 먼저 방문 되는 경우 첫 번째 GridView 행의 라디오 단추가 선택 된 (되 하지 않고 기본적으로 선택 라디오 단추가 having, 현재 되도록 동작 지정 어떤 라디오 단추를 선택 하는 기능을 만들었으므로 이제 해당 변경 수 있습니다. 동작)입니다. 기본적으로 선택 하는 첫 번째 라디오 단추를 표시 하려면 단순히 변경는 `If SuppliersSelectedIndex = e.Row.RowIndex Then` 다음 문을: `If SuppliersSelectedIndex = e.Row.RowIndex OrElse (Not Page.IsPostBack AndAlso e.Row.RowIndex = 0) Then`합니다.

이 시점에서 선택할 수 있으며 다시 게시할 때마다 기억 하는 단일 GridView 행 수 있도록 허용 하는 GridView에 그룹화 된 라디오 단추의 열을 추가 했습니다. 우리의 다음 단계는 선택한 공급자가 제공 하는 제품을 표시 하는 합니다. 4 단계에서에서 보겠습니다 다른 페이지로 사용자를 리디렉션하는 방법을 따라 선택한 보내는 `SupplierID`합니다. 5 단계에서에서 동일한 페이지에 GridView에 선택한 공급 업체의 제품을 표시 하는 방법을 살펴보겠습니다.

> [!NOTE]
> 사용자 지정을 만들 수를 TemplateField (중점을 두고가 긴 3 단계)를 사용 하는 대신 `DataControlField` 적절 한 사용자 인터페이스와 기능을 렌더링 하는 클래스입니다. [ `DataControlField` 클래스](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.datacontrolfield.aspx) 파생 되는 BoundField, CheckBoxField, TemplateField, 및 다른 기본 제공 GridView 및 DetailsView 필드는 기본 클래스입니다. 사용자 지정 만들기 `DataControlField` 라디오 단추의 열만 선언 구문을 사용 하 여를 추가할 수 있으며 기능을 다른 웹 페이지 및 다른 웹 응용 프로그램을 훨씬 쉽게 복제 축소할 것을 의미 하므로 클래스입니다.


그러나 적, 사용자 지정을 만든 적 컴파일된 asp, 경우 파악 이렇게 하면 하므로 상당한 양의 legwork 필요 했으며 미묘한 및 가장자리 사례의 신중 하 게 처리 해야 하는 호스트를 함께 전달 합니다. 에서는 따라서를 구현 하는 사용자 지정 라디오 단추의 열 취소 됩니다 `DataControlField` 지금은 클래스 및 TemplateField 옵션으로 집중 합니다. 아마도 수 있는 기회를 만들기, 사용 및 사용자 지정 배포 탐색 되 겠 `DataControlField` 클래스는 이후 자습서에서!

## <a name="step-4-displaying-the-selected-supplier-s-products-in-a-separate-page"></a>4 단계: 별도 페이지에서 선택한 공급 업체의 제품 표시

사용자가 GridView 행을 선택 후 s 제품 선택한 공급자를 표시 해야 합니다. 일부 경우에 같은 페이지에서 작업을 수행할 수도 있고 다른 별도 페이지에서 이러한 제품을 전시 하기 원하는 수 있습니다. 먼저; 별도 페이지에는 제품을 표시 하는 방법을 검사 한 s 5 단계에서에서 추가 하는 GridView 살펴보겠습니다 `RadioButtonField.aspx` 선택된 협력 업체의 제품을 표시 합니다.

현재 페이지에 있는 단추 웹 컨트롤을 두는 `ListProducts` 및 `SendToProducts`합니다. 경우는 `SendToProducts` 단추를 클릭 하면, 사용자를 보냅니다 `~/Filtering/ProductsForSupplierDetails.aspx`합니다. 이 페이지에서 만든는 [마스터/세부 정보 필터링에서 두 페이지가](../masterdetail/master-detail-filtering-across-two-pages-vb.md) 자습서와 디스플레이 제품 공급 업체에 대 한 해당 `SupplierID` 라는 쿼리 문자열 필드를 통해 전달 되 `SupplierID`합니다.

이 기능을 제공 하려면에 대 한 이벤트 처리기를 만들고는 `SendToProducts` 단추의 `Click` 이벤트입니다. 3 단계에서에서 추가한 이유는 `SuppliersSelectedIndex` 해당 라디오 단추 행의 인덱스를 반환 하는 속성을 선택 합니다. 해당 `SupplierID` GridView s에서 검색할 수 `DataKeys` 컬렉션 및 사용자 수에 보낼 `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID` 를 사용 하 여 `Response.Redirect("url")`합니다.


[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample9.vb)]

이 코드는 아주 GridView에서 라디오 단추 중 하나를 선택으로 작동 합니다. 처음에 GridView에는 모든 라디오 단추를 선택 하 고 사용자가 클릭할 경우는 `SendToProducts` 단추를 `SuppliersSelectedIndex` 됩니다 `-1`, 예외가 이후 throw 하면 `-1` 는 의인덱스범위를벗어났습니다`DataKeys`컬렉션입니다. 그러나이 문제가 되지 업데이트 하도록 결정 한 경우는 `RowCreated` 처음에 선택한 GridView에 첫 번째 라디오 단추를 포함 하기 위해 3 단계에서에서 설명한 대로 이벤트 처리기입니다.

수용 하기 위해는 `SuppliersSelectedIndex` 값 `-1`, GridView 위에 있는 페이지에 레이블 웹 컨트롤을 추가 합니다. 설정의 `ID` 속성을 `ChooseSupplierMsg`, 해당 `CssClass` 속성을 `Warning`, 해당 `EnableViewState` 및 `Visible` 속성을 `False`, 및 해당 `Text` 속성 하십시오를 그리드에서 공급 업체를 선택 합니다. CSS 클래스 `Warning` 빨간색, 기울임꼴, 굵게, 큰 글꼴로 텍스트를 표시 하 고에 정의 된 `Styles.css`합니다. 설정 하 여는 `EnableViewState` 및 `Visible` 속성을 `False`, where 항목만 포스트백에 대 한 제외 하 고 레이블을 렌더링 되지 않습니다 컨트롤 s `Visible` 프로그래밍 방식으로 속성 `True`합니다.


[![GridView 위에 레이블 웹 컨트롤 추가](adding-a-gridview-column-of-radio-buttons-vb/_static/image13.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image21.png)

**그림 13**:는 레이블 웹 컨트롤 위에 GridView 추가 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image22.png))


그런 다음를 확장 하는 `Click` 를 표시 하는 이벤트 처리기는 `ChooseSupplierMsg` 레이블을 지정 하는 경우 `SuppliersSelectedIndex` 보다 작은 경우 0 이며 사용자를 리디렉션하 `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID` 그렇지 않은 경우.


[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample10.vb)]

클릭 하 여 브라우저에서 페이지를 방문 하는 `SendToProducts` GridView에서 공급 업체를 선택 하기 전에 단추입니다. 그림 14에서 볼 수 있듯이이 표시는 `ChooseSupplierMsg` 레이블. 그런 다음 공급 업체를 선택 하 고 클릭는 `SendToProducts` 단추입니다. 선택한 공급자가 제공 하는 제품을 나열 하는 페이지로 있습니다 whisk 됩니다이 있습니다. 그림 15는 `ProductsForSupplierDetails.aspx` Bigfoot Breweries 공급자 선택 될 때 페이지입니다.


[![No 공급자 선택 되어 있으면 ChooseSupplierMsg 레이블이 표시 됩니다.](adding-a-gridview-column-of-radio-buttons-vb/_static/image14.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image23.png)

**그림 14**:는 `ChooseSupplierMsg` 아니요 공급자 선택 되어 있으면 레이블이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image24.png))


[![선택한 공급 업체의 제품 ProductsForSupplierDetails.aspx에 표시 됩니다.](adding-a-gridview-column-of-radio-buttons-vb/_static/image15.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image25.png)

**그림 15**: 제품은 The 선택한 공급자에 표시 되는 `ProductsForSupplierDetails.aspx` ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image26.png))


## <a name="step-5-displaying-the-selected-supplier-s-products-on-the-same-page"></a>5 단계: 선택한 공급 업체의 제품을 같은 페이지에 표시

4 단계에서에서 s 제품 선택한 공급자를 표시 하려면 다른 웹 페이지로 사용자를 전송 하는 방법을 살펴보았습니다. 또는 선택한 공급 업체의 제품 동일한 페이지에 표시할 수 있습니다. 이 설명 하기에 다른 GridView 추가 하겠습니다 `RadioButtonField.aspx` 선택된 협력 업체의 제품을 표시 합니다.

제품의 공급 업체를 선택 하 고 나면 표시 하려면이 GridView를만 포함 하려고 하므로 추가 패널 웹 컨트롤 아래에 `Suppliers` 설정 GridView의 `ID` 를 `ProductsBySupplierPanel` 및 해당 `Visible` 속성을 `False`합니다. 명명 된 GridView 패널 내에서 선택한 공급자에 대 한 텍스트 제품 추가 뒤 `ProductsBySupplier`합니다. GridView s 스마트 태그에서 이라는 새 ObjectDataSource 바인딩할 선택 `ProductsBySupplierDataSource`합니다.


[![새 ObjectDataSource ProductsBySupplier GridView 바인딩합니다](adding-a-gridview-column-of-radio-buttons-vb/_static/image16.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image27.png)

**그림 16**: 바인딩하는 `ProductsBySupplier` GridView에 새 ObjectDataSource ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image28.png))


그런 다음, ObjectDataSource 사용 하도록 구성 된 `ProductsBLL` 클래스입니다. 선택한 공급자가 제공 된 제품 검색 하고자 이므로 지정는 ObjectDataSource 호출 해야 합니다는 `GetProductsBySupplierID(supplierID)` 메서드 데이터를 검색 하도록 합니다. (없음), 삽입, 업데이트에서 드롭 다운 목록에서 선택한 탭 삭제 합니다.


[![ObjectDataSource GetProductsBySupplierID(supplierID) 메서드를 사용 하도록 구성](adding-a-gridview-column-of-radio-buttons-vb/_static/image17.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image29.png)

**그림 17**: 구성에 사용 하 여 ObjectDataSource는 `GetProductsBySupplierID(supplierID)` 메서드 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image30.png))


[![UPDATE, INSERT에에서 드롭 다운 목록을 (없음)으로 설정 하 고 탭 삭제](adding-a-gridview-column-of-radio-buttons-vb/_static/image18.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image31.png)

**그림 18**: 업데이트, 삽입 및 삭제 탭에서을 (없음) 드롭 다운 목록 설정 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image32.png))


SELECT를 구성한 후 업데이트, 삽입 및 삭제 탭, 다음을 클릭 합니다. 이후는 `GetProductsBySupplierID(supplierID)` 메서드에서 예상 입력된 매개 변수, 데이터 원본 만들기 마법사의 매개 변수의 값에 대 한 원본을 지정 하 라는 메시지가 나타납니다.

두 가지 옵션이 여기에 매개 변수의 값의 소스를 지정 해야 합니다. 기본 매개 변수 개체를 사용 하 고 프로그래밍 방식으로의 값을 할당 수 우리는 `SuppliersSelectedIndex` 속성 매개 변수 s에 `DefaultValue` ObjectDataSource s에서 속성 `Selecting` 이벤트 처리기입니다. 다시 참조는 [ObjectDataSource의 매개 변수 값을 프로그래밍 방식으로 설정](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb.md) ObjectDataSource s 매개 변수 값에 프로그래밍 방식으로 할당 세부 정보에 대 한 자습서입니다.

또는에서는 사용 하 여는 ControlParameter 참조는 `Suppliers` GridView s [ `SelectedValue` 속성](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.gridview.selectedvalue.aspx) (그림 19 참조). GridView s `SelectedValue` 속성에서 반환 된 `DataKey` 값에 해당 하는 [ `SelectedIndex` 속성](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.gridview.selectedindex.aspx)합니다. GridView s 프로그래밍 방식으로 설정 해야이 옵션을 사용 하려면 순서로 `SelectedIndex` 속성을 선택한 경우 행은 `ListProducts` 단추를 클릭 합니다. 설정 하 여 추가 혜택으로는 `SelectedIndex`, 선택된 된 레코드에 대해 수행 된 `SelectedRowStyle` 에 정의 된는 `DataWebControls` 테마 (노란색 배경).


[![매개 변수 원본으로 지정 하는 GridView의 SelectedValue를는 ControlParameter를 사용 하 여](adding-a-gridview-column-of-radio-buttons-vb/_static/image19.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image33.png)

**그림 19**:는 ControlParameter를 사용 하 여 매개 변수 원본으로 지정 하는 GridView의 SelectedValue ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image34.png))


마법사를 완료 되 면 Visual Studio 제품의 데이터 필드에 대 한 필드를 자동으로 추가 됩니다. 제거 제외한 모두 `ProductName`, `CategoryName`, 및 `UnitPrice` BoundFields, 변경 하 고는 `HeaderText` 속성 제품, 범주 및 가격을 합니다. 구성의 `UnitPrice` BoundField 통화로 해당 값의 서식을 지정 되도록 합니다. 다음과 같이 변경한 후 GridView 패널과 ObjectDataSource s 선언 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample11.aspx)]

이 연습을 완료 하려면 GridView s를 설정 해야 `SelectedIndex` 속성을는 `SelectedSuppliersIndex` 및 `ProductsBySupplierPanel` 패널 s `Visible` 속성을 `True` 때는 `ListProducts` 단추를 클릭 합니다. 에 대 한 이벤트 처리기를 만들고이를 위해는 `ListProducts` 단추 웹 컨트롤의 `Click` 이벤트를 다음 코드를 추가:


[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample12.vb)]

GridView에서 공급 업체가 제공한 선택 되지 않은 경우에 `ChooseSupplierMsg` 레이블이 표시 됩니다 및 `ProductsBySupplierPanel` 숨겨진 패널입니다. 공급 업체를 선택 하는 경우는 `ProductsBySupplierPanel` 가 표시 및 GridView의 `SelectedIndex` 속성이 업데이트 됩니다.

그림 20 Bigfoot Breweries 공급자 선택 되 고 페이지 단추에 표시할 제품을 클릭 한 후 결과 보여줍니다.


[![같은 페이지에 나열 됩니다 Bigfoot Breweries에서 제품 제공](adding-a-gridview-column-of-radio-buttons-vb/_static/image20.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image35.png)

**그림 20**: Bigfoot Breweries에서 제공한 제품의 동일한 페이지에 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-vb/_static/image36.png))


## <a name="summary"></a>요약

에 설명 된 대로 [마스터/세부 정보 DetailView 선택 가능한 마스터 GridView 사용에 대해 자세히 설명](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md) 자습서는 CommandField를 사용 하 여 GridView에서 레코드를 선택할 수 인 `ShowSelectButton` 속성이로 설정 된 `True`합니다. 하지만 CommandField 일반 누름 단추, 링크, 또는 이미지 단추가 표시 됩니다. 다른 행 선택 사용자 인터페이스는 라디오 단추를 클릭 하거나 각 GridView 행의 확인란을 제공 합니다. 이 자습서에서는 라디오 단추의 열을 추가 하는 방법을 검사 했습니다.

아쉽게도 된다고 예상 대로 간단한으로 라디오 단추 되지 않으면의 열을 추가 합니다. 단추 클릭에 추가할 수 있는 기본 제공 RadioButtonField 되지 않으며를 TemplateField 내에서 RadioButton 웹 컨트롤을 사용 하 여 집합을 도입 자체의 문제입니다. 에 마지막으로 이러한 인터페이스를 제공 하거나는 사용자 지정 만들어 `DataControlField` 클래스나 중를 TemplateField로 적절 한 HTML을 삽입 하기 위한 수단은 `RowCreated` 이벤트입니다.

라디오 단추의 열을 추가 하는 방법을 탐색할 수 있으면 응 배웠으므로 확인란의 열을 추가 합니다. 확인란의 열이 있는 사용자 GridView 행을 하나 이상 선택 하 고 (예: 웹 기반 전자 메일 클라이언트에서 전자 메일의 집합을 선택 하면 선택한 다음 선택한 모든 전자 메일을 삭제 하려면) 선택 된 행의 모든 작업을 수행 합니다. 다음 자습서에서 이러한 열을 추가 하는 방법을 살펴보겠습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 David Suru 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](inserting-a-new-record-from-the-gridview-s-footer-cs.md)
[다음](adding-a-gridview-column-of-checkboxes-vb.md)
