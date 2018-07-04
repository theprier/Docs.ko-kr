---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-cs
title: (C#) 라디오 단추의 GridView 열 추가 | Microsoft Docs
author: rick-anderson
description: 이 자습서의 단일 행을 선택 하는 보다 직관적인 방법으로 사용자를 제공 하는 GridView 컨트롤이 라디오 단추의 열 추가 하는 방법을 살펴봅니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/06/2007
ms.topic: article
ms.assetid: 32377145-ec25-4715-8370-a1c590a331d5
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-cs
msc.type: authoredcontent
ms.openlocfilehash: 1e1691b3c0c5fb576f25b84e8f4d7125a8d0c698
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37366918"
---
<a name="adding-a-gridview-column-of-radio-buttons-c"></a>(C#) 라디오 단추의 GridView 열 추가
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_51_CS.exe) 또는 [PDF 다운로드](adding-a-gridview-column-of-radio-buttons-cs/_static/datatutorial51cs1.pdf)

> 이 자습서 GridView 컨트롤을 GridView의 단일 행을 선택 하는 보다 직관적인 방법으로 사용자를 제공 하는 열의 라디오 단추를 추가 하는 방법에 살펴봅니다.


## <a name="introduction"></a>소개

GridView 컨트롤은 많은 기본 제공 기능을 제공합니다. 텍스트, 이미지, 하이퍼링크 및 단추를 표시 하기 위한 다양 한 필드 수가 포함 됩니다. 추가 사용자 지정 템플릿을 지원합니다. 몇 번의 마우스 클릭을 사용 하 여이 단추를 통해 각 행을 선택할 수 있는 GridView 하거나 편집 또는 삭제 기능을 사용 하도록 설정 가능한 s입니다. 다양 한 제공 된 기능에 불구 하 고 종종 경우가 있습니다 추가는 지원 되지 않는 기능 추가 해야 합니다. 이 자습서에서 다음 두 개의 추가 기능을 포함 하는 GridView가의 기능을 개선 하는 방법을 살펴보겠습니다.

이 자습서와 다음 행 선택 프로세스 향상에 집중 합니다. 살펴본 대로 합니다 [마스터/세부 정보 DetailView와 함께 선택 가능한 마스터 GridView를 사용 하 여 세부 정보](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)는 CommandField 선택 단추를 포함 하는 GridView에 추가할 수 있습니다. 클릭 하면 포스트백 근거가 GridView의 `SelectedIndex` 속성은 선택 된 단추를 클릭 한 행의 인덱스를 업데이트 합니다. 에 [마스터/세부 정보 DetailView와 함께 선택 가능한 마스터 GridView를 사용 하 여 세부 정보](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) 자습서, 선택된 된 GridView 행에 대 한 정보를 표시 하려면이 기능을 사용 하는 방법에 살펴보았습니다.

대부분의 경우에서 선택 단추가 작동 하는 동안 다른 사용자도 작동 하지 않습니다. 단추를 사용 하는 대신 다른 두 사용자 인터페이스 요소는 일반적으로 사용 선택: 라디오 단추 및 확인란을 선택 합니다. 단추를 선택 하는 대신 각 행 라디오 단추나 확인란을 포함 되도록 GridView를 강화할 수 했습니다. 여기서 사용자만 선택할 수 GridView 레코드 중 하나의 경우 라디오 단추 선택 단추를 통해 기본 수 있습니다. 여러 메시지 삭제 확인란을 선택 하려면 사용자가 수도 있는 웹 기반 전자 메일 응용 프로그램에서와 같은 여러 레코드를 잠재적으로 선택할 수 있는 경우에 선택 단추 또는 라디오 단추에서 사용할 수 없는 기능을 제공 합니다. 사용자 인터페이스입니다.

이 자습서는 GridView에는 열의 라디오 단추를 추가 하는 방법을 살펴봅니다. 계속 자습서에서는 확인란을 사용 하 여 합니다.

## <a name="step-1-creating-the-enhancing-the-gridview-web-pages"></a>1 단계: 기능을 향상 하는 GridView 웹 페이지 만들기

라디오 단추의 열을 포함 하도록 GridView 향상 시작 하기 전에 s를 먼저 시간을 내어이 자습서에는 다음 두 해야 하는 웹 사이트 프로젝트에서 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `EnhancedGridView`합니다. 다음에 있는 각 페이지에 연결할 수 있도록 해당 폴더에 다음 ASP.NET 페이지를 추가 합니다 `Site.master` 마스터 페이지:

- `Default.aspx`
- `RadioButtonField.aspx`
- `CheckBoxField.aspx`
- `InsertThroughFooter.aspx`


![SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가](adding-a-gridview-column-of-radio-buttons-cs/_static/image1.gif)

**그림 1**: SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더와 같이 `Default.aspx` 에 `EnhancedGridView` 폴더 섹션의 자습서를 나열 됩니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 사용자 컨트롤은이 기능을 제공 합니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx`의 디자인 뷰에서 페이지의 솔루션 탐색기에서 끌어 합니다.


[![Default.aspx SectionLevelTutorialListing.ascx 사용자 컨트롤 추가](adding-a-gridview-column-of-radio-buttons-cs/_static/image2.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image1.png)

**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 `Default.aspx` ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-radio-buttons-cs/_static/image2.png))


마지막으로, 이러한 네 가지 페이지 항목을 추가 합니다 `Web.sitemap` 파일입니다. 특히 사용 후에 다음 태그를 추가 SqlDataSource 컨트롤 `<siteMapNode>`:


[!code-xml[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample1.xml)]

업데이트 한 후 `Web.sitemap`, 잠시 브라우저를 통해 자습서 웹 사이트를 확인 합니다. 왼쪽 메뉴에는 이제 편집, 삽입 및 삭제 자습서에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 기능을 향상 하는 GridView 자습서에 대 한 항목을 포함](adding-a-gridview-column-of-radio-buttons-cs/_static/image3.gif)

**그림 3**: 이제 사이트 맵 기능을 향상 하는 GridView 자습서에 대 한 항목을 포함


## <a name="step-2-displaying-the-suppliers-in-a-gridview"></a>2 단계: GridView에 공급자를 표시합니다.

이 자습서는 GridView 빌드 s 수에 대 한 라디오 단추를 제공 하는 각 GridView 행을 사용 하 여 미국에서 공급자를 나열 합니다. 라디오 단추를 통해 공급자를 선택한 후 사용자 단추를 클릭 하 여 공급자가의 제품을 볼 수 있습니다. 이 작업은 간단한 사운드 수, 하는 동안 특히 까다로운 부분이 미묘한 많은 있습니다. 사용 하기 전에 이러한 미묘한 측면이 들으로, s를 먼저 공급자를 나열 하는 GridView를 가져올 수 있습니다.

열어서 시작 합니다 `RadioButtonField.aspx` 페이지는 `EnhancedGridView` GridView 디자이너 도구 상자에서 끌어 폴더. 집합 GridView s `ID` 에 `Suppliers` 하 고 해당 스마트 태그에서 새 데이터 원본을 만들려면 선택 합니다. 특히 라는 ObjectDataSource를 만듭니다 `SuppliersDataSource` 에서 해당 데이터를 가져오고 있는 `SuppliersBLL` 개체입니다.


[![SuppliersDataSource 라는 새로운 ObjectDataSource는 만들기](adding-a-gridview-column-of-radio-buttons-cs/_static/image4.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image3.png)

**그림 4**: 명명 된 새 ObjectDataSource 만들려면 `SuppliersDataSource` ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-radio-buttons-cs/_static/image4.png))


[![SuppliersBLL 클래스를 사용 하는 ObjectDataSource 구성](adding-a-gridview-column-of-radio-buttons-cs/_static/image5.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image5.png)

**그림 5**: ObjectDataSource 사용 하도록 구성 된 `SuppliersBLL` 클래스 ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-radio-buttons-cs/_static/image6.png))


미국에 있는 해당 공급자를 나열 하고자 하므로 선택 된 `GetSuppliersByCountry(country)` 선택 탭의 드롭다운 목록에서 메서드.


[![SuppliersBLL 클래스를 사용 하는 ObjectDataSource 구성](adding-a-gridview-column-of-radio-buttons-cs/_static/image6.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image7.png)

**그림 6**: ObjectDataSource 사용 하도록 구성 된 `SuppliersBLL` 클래스 ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-radio-buttons-cs/_static/image8.png))


업데이트 탭에서 선택 옵션 (없음) 및 다음을 클릭 합니다.


[![SuppliersBLL 클래스를 사용 하는 ObjectDataSource 구성](adding-a-gridview-column-of-radio-buttons-cs/_static/image7.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image9.png)

**그림 7**: ObjectDataSource 사용 하도록 구성 된 `SuppliersBLL` 클래스 ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-radio-buttons-cs/_static/image10.png))


이후를 `GetSuppliersByCountry(country)` 매개 변수를 허용 하는 메서드, 데이터 소스 구성 마법사의 매개 변수 원본에 대 한 요청입니다. 지정 하는 하드 코드 된 값 (이 예제의: 미국), 원본 드롭 다운 목록 None으로 설정 하 고 텍스트 상자에 기본값을 입력 매개 변수를 둡니다. 마법사를 완료 하려면 마침을 클릭 합니다.


[![기본 값으로 USA를 사용 하 여 국가의 매개 변수](adding-a-gridview-column-of-radio-buttons-cs/_static/image8.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image11.png)

**그림 8**: 기본 값으로 사용 하 여 미국 합니다 `country` 매개 변수 ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-radio-buttons-cs/_static/image12.png))


마법사를 완료 한 후 GridView 각 공급 업체 데이터 필드에 대 한 BoundField 포함 됩니다. 제거를 제외한 모든 `CompanyName`, `City`, 및 `Country` BoundFields, 이름 바꾸기 및를 `CompanyName` BoundFields `HeaderText` 공급 업체에 대 한 속성입니다. 이렇게 한 다음, GridView 및 ObjectDataSource 선언 구문 다음과 유사 합니다.


[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample2.aspx)]

이 자습서에서는 s 다른 페이지 또는 공급 업체 목록과 같은 페이지에 선택한 공급자를 보려는 사용자가의 제품을 허용 하도록 합니다. 이 위해 페이지에 두 개의 단추 웹 컨트롤을 추가 합니다. I ve 집합 합니다 `ID` 이러한 두 단추의 s `ListProducts` 및 `SendToProducts`, 개념을 사용 하 여 때 `ListProducts` 클릭할 포스트백이 발생 하 고 선택한 공급자가의 제품 있지만 동일한 페이지에 나열 됩니다 `SendToProducts` 를 클릭 하면 사용자는 제품을 나열 하는 다른 페이지로 마을로 됩니다.

그림 9를 `Suppliers` GridView 및 두 개의 단추 웹 브라우저를 통해 볼 때를 제어 합니다.


[![미국에서 이러한 공급자가 해당 이름, 도시 및 국가 정보 나열](adding-a-gridview-column-of-radio-buttons-cs/_static/image9.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image13.png)

**그림 9**: USA가 해당 이름, 도시 및 국가가 정보에서 해당 공급자 ([큰 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image14.png))


## <a name="step-3-adding-a-column-of-radio-buttons"></a>3 단계: 열의 라디오 단추 추가

이 시점에서 `Suppliers` GridView에 세 가지 BoundFields 미국의 회사 이름, 도시 및 국가입니다. 각 공급 업체를 표시 합니다. 하지만이 여전히 부족 열의 라디오 단추, 합니다. 아쉽게도 GridView 만들어지고 t는 기본 제공 RadioButtonField,이 고 그렇지 추가할 수 있는 그리드로 하 고 수행할 수를 포함 합니다. 대신 수 templatefield로 추가 하 고 구성 해당 `ItemTemplate` 각 GridView 행에 대 한 라디오 단추에 라디오 단추를 렌더링 합니다.

RadioButton 웹 컨트롤에 추가 하 여 원하는 사용자 인터페이스를 구현할 수 있습니다 가정 수 처음에 `ItemTemplate` templatefield로입니다. 이 실제로 추가할 단일 라디오 단추를 GridView의 각 행을 하는 동안 라디오 단추 그룹화 할 수 없습니다 하 고 따라서 배타적이 지 않습니다. 즉, 최종 사용자가 GridView에서 동시에 여러 라디오 단추를 선택할 수 있게 합니다.

S 수 있으므로이 방법은 구현를 TemplateField RadioButton 웹 컨트롤을 사용 하 여 필요한 기능을 제공 하지 않습니다, 경우에 s 결과 라디오 단추 그룹화 되지 않은 이유를 검사 하는 것이 좋습니다. 가장 왼쪽의 필드를 만드는 공급자 GridView를 templatefield로 추가 하 여 시작 합니다. 다음으로 GridView가 스마트 태그에서 템플릿 편집 링크를 클릭 및 TemplateField s에 도구 상자에서 RadioButton 웹 컨트롤을 끌어 `ItemTemplate` (그림 10 참조). 집합 RadioButton s `ID` 속성을 `RowSelector` 하며 `GroupName` 속성을 `SuppliersGroup`입니다.


[![ItemTemplate에 RadioButton 웹 컨트롤 추가](adding-a-gridview-column-of-radio-buttons-cs/_static/image10.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image15.png)

**그림 10**: RadioButton 웹 컨트롤을 추가 합니다 `ItemTemplate` ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-radio-buttons-cs/_static/image16.png))


디자이너를 통해 이러한 추가 마치면 GridView의 태그 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample3.aspx)]

RadioButton s [ `GroupName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.radiobutton.groupname(VS.80).aspx) 는 일련의 라디오 단추 그룹에 사용 됩니다. 과 동일한 모든 RadioButton 컨트롤 `GroupName` 값 그룹화 라고 한 번에 하나의 라디오 단추 그룹에서 선택할 수 있습니다. 합니다 `GroupName` 렌더링 된 라디오 단추의 s 값을 지정 하는 속성 `name` 특성입니다. 라디오 단추를 검사 하는 브라우저 `name` 라디오를 확인 하기 위해 특성 단추 그룹화 합니다.

RadioButton 웹 컨트롤에 추가 된 `ItemTemplate`, 브라우저를 통해이 페이지를 방문 하 고 표의 행에서 라디오 단추를 클릭 합니다. 라디오 단추 그룹화 되지 않은 하는 방법을 예 고 그림 11의 모든 행을 선택 하 여 보여 줍니다.


[![GridView가의 라디오 단추 그룹화 되지 됩니다.](adding-a-gridview-column-of-radio-buttons-cs/_static/image11.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image17.png)

**그림 11**: GridView가의 라디오 단추 그룹화 되지 않은 됩니다 ([큰 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image18.png))


라디오 단추 그룹화 되지 않은 이유 때문입니다 해당 렌더링 `name` 특성은 동일한 불구 하 고 다른 `GroupName` 속성을 설정 합니다. 이러한 차이점을 확인 하려면 브라우저에서 소스 보기/작업을 수행 하 고 라디오 단추 태그 검사:


[!code-html[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample4.html)]

알림에서는 합니다 `name` 및 `id` 특성은 속성 창에서 지정 된 대로 정확한 값이 아닙니다 하지만 다른 많은 앞에 추가 되어 `ID` 값입니다. 추가 `ID` 는 렌더링 된 앞에 추가 하는 값 `id` 및 `name` 특성은 합니다 `ID` 라디오의 부모 컨트롤 단추를 `GridViewRow` s `ID` s, GridView의 `ID`, 콘텐츠 컨트롤 s `ID`, 및 Web Form의 `ID`입니다. 이러한 `ID` s 수 있도록 추가 각각 렌더링 gridview에서 웹 컨트롤에는 고유한 `id` 고 `name` 값입니다.

각 렌더링 제어 요구 사항 다른 `name` 및 `id` 각 컨트롤 클라이언트 쪽 및 식별 하는 방법 해당 웹 서버에 작업을 고유 하 게 식별 하는 브라우저 또는 변경 포스트백에서 발생 하는 방법 이기 때문에 있습니다. 예를 들어, RadioButton s 선택 상태가 변경 된 때마다 몇 가지 서버 쪽 코드를 실행 하 려 한다고 가정 합니다. RadioButton s를 설정 하 여이 작업을 수행할 수 없습니다 것 `AutoPostBack` 속성을 `true` 에 대 한 이벤트 처리기를 만들어는 `CheckChanged` 이벤트입니다. 그러나 경우 렌더링 된 `name` 및 `id` 모든 라디오 단추는 동일에서 포스트백 어떤 특정 확인할 수 없습니다 것에 대 한 값 라디오 단추를 클릭 합니다.

짧은 RadioButton 웹 컨트롤을 사용 하 여 GridView에서 라디오 단추 열을 만들 수 없음을입니다. 대신 적절 한 태그를 각 GridView 행 삽입 되어 있는지 확인 하려면 대신 구식 기술 사용 해야 합니다.

> [!NOTE]
> RadioButton 웹 컨트롤을 라디오 단추 컨트롤이 HTML 템플릿을 추가할 때 고유는 같은 `name` 특성도 라디오 단추 그룹화 되지 않은 표의 합니다. HTML 컨트롤을 사용 하 여 잘 모르는 경우 자유롭게이 메모를 무시 하려면 HTML 컨트롤은 거의에서 사용 되는, 특히 ASP.NET 2.0. 자세히 알아보는 데 관심이 있다면 볼 [K. Scott Allen](http://odetocode.com/blogs/scott/default.aspx) s 블로그 [웹 컨트롤과 HTML 컨트롤](http://www.odetocode.com/Articles/348.aspx)합니다.


## <a name="using-a-literal-control-to-inject-radio-button-markup"></a>리터럴 컨트롤을 사용 하 여 라디오 단추 태그를 삽입 하려면

모든 GridView 내에서 라디오 단추를 올바르게 그룹화 하기 위해 수동으로에 라디오 단추 태그를 삽입 해야 합니다 `ItemTemplate`합니다. 각 라디오 단추 동일 해야 `name` 특성을 하지만 고유한 있어야 `id` (하는 경우 클라이언트 쪽 스크립트를 통해 라디오 단추에 액세스 하고자) 특성입니다. 사용자가 라디오 단추를 선택 하 고 페이지를 다시 게시 한 후 브라우저에서 다시 전송 s 선택된 된 라디오 단추의 값 `value` 특성입니다. 따라서 각 라디오 단추는 고유 해야 `value` 특성입니다. 마지막으로 다시 게시 해야 추가 해야 합니다 `checked` 선택한, 그렇지 않으면 사용자가 선택 하 고 다시 게시 한 후 한 라디오 단추에 대 한 특성을 라디오 단추 돌아갑니다 기본 상태로 (모두 선택 되지 않음).

서식 파일에 하위 수준 태그를 삽입 하기 위해 수행할 수 있는 방법은 두 가지가 있습니다. 하나는 다양 한 태그 및 코드 숨김 클래스에 정의 된 메서드를 서식 지정에 대 한 호출을 수행 하는 것입니다. 이 기술은 설명 된 합니다 [GridView 컨트롤에서 TemplateFields 사용 하 여](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) 자습서입니다. 여기서 것 같이 보일 수 있습니다.


[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample5.aspx)]

이때 `GetUniqueRadioButton` 하 고 `GetRadioButtonValue` 적절 한 반환 하는 코드 숨김 클래스에 정의 된 메서드는 것 `id` 및 `value` 각 라디오 단추에 대 한 값을 특성입니다. 이 방법은 할당 하는 데는 `id` 및 `value` 특성 이지만 지정 해야 하는 경우 짧은 대체는 `checked` 데이터 먼저 GridView에 바인딩될 때 구문이 실행 되므로 특성 값입니다. 따라서 GridView에 뷰 상태를 사용 하는 경우 형식 지정 메서드와만 발생 시기는 페이지가 처음 로드 (또는 데이터 원본에 GridView 명시적으로 차츰 되는 경우) 및 설정 하는 함수의 따라서는 `checked` t-이득 특성에서 호출할 수 다시 게시 합니다. 이 s 보다 미묘한 문제를 및 잠시이 그대로 하므로이 문서의 범위를 벗어납니다. 그러나 수행, 위의 접근 방식을 사용해 보시기 바랍니다 했으며 막히면 수 있는 지점을 통해 작동 합니다. 이러한는 연습-이득 t 작업 버전으로 가까이 얻게, 깊이 있는 이해가 GridView 및 데이터 바인딩 수명 주기를 촉진 도움이 됩니다.

추가 하는 것을 다른 삽입 사용자 지정 방법 템플릿과이 자습서를 사용 하는 방법은에 하위 수준 태그를 [리터럴 컨트롤](https://msdn.microsoft.com/library/sz4949ks(VS.80).aspx) 템플릿에 합니다. GridView에서 다음 `RowCreated` 또는 `RowDataBound` 이벤트 처리기를 리터럴 컨트롤을 프로그래밍 방식으로 액세스할 수 있습니다 및 해당 `Text` 속성이를 내보내는 태그에 설정 합니다.

RadioButton TemplateField s에서 제거 하 여 시작 `ItemTemplate`, 리터럴 컨트롤을으로 바꿉니다. S 리터럴 컨트롤을 설정 `ID` 에 `RadioButtonMarkup`입니다.


[![ItemTemplate에 리터럴 컨트롤 추가](adding-a-gridview-column-of-radio-buttons-cs/_static/image12.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image19.png)

**그림 12**: 리터럴 컨트롤을 추가 합니다 `ItemTemplate` ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-radio-buttons-cs/_static/image20.png))


다음으로 GridView s에 대 한 이벤트 처리기를 만들고 `RowCreated` 이벤트입니다. `RowCreated` 이벤트가 추가 된 모든 행에 대해 여부 데이터는 중인 차츰 GridView에 한 번 발생 합니다. 즉, 다시 게시의 경우에 데이터 뷰 상태를 다시 로드 되 면 합니다 `RowCreated` 이벤트가 계속 발생 하 고이 대신 사용 하는 이유는 `RowDataBound` (발생 하는 경우 데이터는 명시적으로에 바인딩할 데이터 웹 컨트롤).

이 이벤트 처리기에서 하고자 하는 경우 계속 다시 데이터 행을 처리 했습니다. 각 데이터 행에 대해 프로그래밍 방식으로 참조 하려고 합니다 `RadioButtonMarkup` 리터럴 컨트롤 집합과 해당 `Text` 를 내보내는 태그 속성. 태그에 정해진 라디오를 만들고 다음 코드에서 볼 수 있듯이 해당 단추 `name` 특성이로 설정 된 `SuppliersGroup`해당 `id` 특성이로 설정 된 `RowSelectorX`여기서 *X* GridView 행의 인덱스 `value` 특성은 GridView 행의 인덱스로 설정 합니다.


[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample6.cs)]

GridView 행을 선택 하 고 포스트백이 발생할 때 관심이 `SupplierID` 선택한 공급자의입니다. 따라서 하나 생각할 각 라디오 단추의 값이 실제 되도록 `SupplierID` (대신 GridView 행의 인덱스). 특정 상황에서 작동할 수는 있지만이 것이 보안상의 위험을 무조건 수락 및 처리는 `SupplierID`합니다. 이 GridView에는 예를 들어 미국에 있는 해당 공급자만 나열합니다. 그러나 경우는 `SupplierID` 유해 사용자 조작에서 중지 하려면 새로운 라디오 단추에서 직접 전달 되는 `SupplierID` 포스트백에 다시 전송 하는 값? 행 인덱스를 사용 하 여는 `value`, 고를 가져오는 합니다 `SupplierID` 에서 포스트백에는 `DataKeys` 컬렉션을 확인할 수 있습니다는 사용자만 사용 하는 `SupplierID` GridView 행 중 하나를 사용 하 여 연결 된 값.

이 이벤트 처리기 코드를 추가한 후 브라우저에서 페이지를 테스트 하려면 몇 분을 걸립니다. 먼저 해당 하나만 라디오 참고 표에 단추 한 번에 선택할 수 있습니다. 그러나 포스트백이 발생할 라디오 단추를 선택 하면 단추 중 하나를 클릭 하 고 시간과 모든 라디오 단추를 초기 상태로 되돌리는 (즉, 포스트백에서 선택된 된 라디오 단추는 더 이상 선택). 이 문제를 해결 하려면 보강 해야 합니다 `RowCreated` 한다는 포스트백에서 전송 하는 선택된 된 라디오 단추 인덱스를 검사 하 고 추가 이벤트 처리기는 `checked="checked"` 행 인덱스 일치 하는 내보낸된 태그에 특성입니다.

포스트백을 발생 시기, 브라우저를 다시 전송 합니다 `name` 및 `value` 선택된 된 라디오 단추의 합니다. 값을 프로그래밍 방식으로 검색할 수를 사용 하 여 `Request.Form["name"]`입니다. 합니다 [ `Request.Form` 속성](https://msdn.microsoft.com/library/system.web.httprequest.form.aspx) 제공 된 [ `NameValueCollection` ](https://msdn.microsoft.com/library/system.collections.specialized.namevaluecollection.aspx) 폼 변수를 나타내는입니다. 폼 변수 이름 및 웹 페이지에 폼 필드의 값은 고 포스트백 근거가 될 때마다 웹 브라우저에서 다시 전송 됩니다. 때문에 렌더링 된 `name` 라디오 단추의 GridView에서 특성이 `SuppliersGroup`웹 페이지를 포스트백 브라우저 송신할 때 `SuppliersGroup=valueOfSelectedRadioButton` (다른 양식 필드)와 함께 웹 서버로 다시 합니다. 이 정보에서 액세스할 수 합니다 `Request.Form` 사용 하 여 속성: `Request.Form["SuppliersGroup"]`합니다.

이후로에서는 해야 결정할 선택된 된 라디오 단추를 인덱스에 하지는 `RowCreated` 이지만 이벤트 처리기는 `Click` Button 웹 컨트롤에 대 한 이벤트 처리기를 통해 s 추가 `SuppliersSelectedIndex` 를반환하는코드숨김클래스에속성`-1`없음 라디오 단추가 선택 된 라디오 단추 중 하나를 선택 하는 경우 선택한 인덱스입니다.


[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample7.cs)]

추가할 알게이 속성을 추가 합니다 `checked="checked"` 태그를 `RowCreated` 이벤트 처리기 때 `SuppliersSelectedIndex` equals `e.Row.RowIndex`. 이 논리를 포함 하도록 이벤트 처리기를 업데이트 합니다.


[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample8.cs)]

선택한 라디오 단추의이 변경으로 포스트백 후 선택한가 남아 있습니다. 먼저 페이지를 열어 보 았을 때 첫 번째 GridView 행의 라디오 단추를 선택 했습니다 (보다는 기본적으로 선택 라디오 단추가 없습니다, 하는 것이 현재 있도록 동작 지정할 어떤 라디오 단추를 선택 하는 기능을 만들었으므로 이제 해당 변경 수 있습니다. 동작)입니다. 첫 번째 라디오 단추를 기본적으로 선택 하도록 간단히 변경 합니다 `if (SuppliersSelectedIndex == e.Row.RowIndex)` 다음 문을: `if (SuppliersSelectedIndex == e.Row.RowIndex || (!Page.IsPostBack && e.Row.RowIndex == 0))`합니다.

이 시점에서 그룹화 된 라디오 단추의 열을 선택 하 고 다시 게시할 때마다 기억 하는 단일 GridView 행에 대 한 허용 하는 GridView에 추가 했습니다. 선택한 공급자가 제공 하는 제품을 전시 하기는 다음 단계가 있습니다. 4 단계에서에서 살펴보겠습니다 다른 페이지로 사용자를 리디렉션하는 방법 선택에 따라 전송 `SupplierID`합니다. 5 단계에서에서 선택한 공급자가의 제품을 같은 페이지에 GridView를 표시 하는 방법을 살펴보겠습니다.

> [!NOTE]
> TemplateField (이 긴 단계 3 포커스 내)를 사용 하는 대신 사용자 지정을 만들 수 것 `DataControlField` 적절 한 사용자 인터페이스와 기능을 렌더링 하는 클래스입니다. 합니다 [ `DataControlField` 클래스](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.aspx) 파생 되는 BoundField, CheckBoxField, TemplateField, 및 다른 기본 제공 GridView 및 DetailsView 필드는 기본 클래스입니다. 사용자 지정 만들기 `DataControlField` 클래스 의미는 라디오 단추에 있는 열의 선언적 구문을 사용 하 여 추가할 수 없으며 다른 웹 페이지에 다른 웹 응용 프로그램을 훨씬 쉽게 기능을 복제 합니다.


그러나 Ve 이전에 만든 사용자 지정 asp.net에서 컨트롤을 컴파일되지, 경우 있을 수행 되므로 상당한 양의 투자할 필요 미묘한 측면 들 및에 지 사례의 신중 하 게 처리 해야 하는 호스트를 함께 전달 합니다. 에서는 따라서에 구현 하는 사용자 지정 라디오 단추의 열은 됩니다 `DataControlField` 지금은 클래스 및 TemplateField 옵션을 사용 하 여 계속 합니다. 아마도 만들기, 사용 및 사용자 지정 배포를 탐색할 수 있는 기회를 마련 `DataControlField` 이후 자습서에서 클래스.

## <a name="step-4-displaying-the-selected-supplier-s-products-in-a-separate-page"></a>4 단계: 별도 페이지에서 선택한 공급자가의 제품 표시

사용자가 GridView 행을 선택한 후 선택한 공급자가의 제품을 표시 해야 합니다. 일부 경우에 동일한 페이지에서 수행할 수도 있고 다른 별도 페이지에서 이러한 제품을 전시 하기 원하는 수 있습니다. 먼저 별도 페이지에서 제품을 표시 하는 방법을 검사 한 s 5 단계에서에서 추가 하기 위한 GridView 살펴보겠습니다 `RadioButtonField.aspx` 선택한 공급자가의 제품을 전시 하기.

현재 페이지의 단추 웹 컨트롤을 두 가지 `ListProducts` 고 `SendToProducts`입니다. 경우는 `SendToProducts` 단추를 클릭 하면, 사용자가 보내려는 `~/Filtering/ProductsForSupplierDetails.aspx`합니다. 이 페이지를 생성 합니다 [마스터/세부 정보 필터링에서 두 페이지가](../masterdetail/master-detail-filtering-across-two-pages-cs.md) 자습서 및 공급자에 대 한 제품 표시입니다 `SupplierID` 명명 된 쿼리 문자열 필드를 통해 전달 됩니다 `SupplierID`.

이 기능을 제공 하려면 만들기에 대 한 이벤트 처리기를 `SendToProducts` s 단추 `Click` 이벤트입니다. 3 단계에서에서 추가한는 `SuppliersSelectedIndex` 해당 라디오 단추 행의 인덱스를 반환 하는 속성을 선택 합니다. 해당 `SupplierID` GridView s에서 검색할 수 있습니다 `DataKeys` 컬렉션과 사용자 다음 보낼 수 있습니다 `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID` 사용 하 여 `Response.Redirect("url")`입니다.


[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample9.cs)]

이 코드가 작동 쌓아가는 GridView에서 라디오 단추 중 하나를 선택 합니다. GridView에서 라디오 단추 선택 되지 않은 하 고 사용자가 처음에 `SendToProducts` 단추를 `SuppliersSelectedIndex` 됩니다 `-1`를 이후 throw 예외가 발생 하는 `-1` 합니다 의인덱스범위를벗어났습니다`DataKeys`컬렉션입니다. 하지만 이것이 문제가 되지 않습니다 업데이트 하기로 결정 하는 경우는 `RowCreated` 첫 번째 라디오 단추를 처음에 선택한 GridView에, 3 단계에서에서 설명한 대로 이벤트 처리기입니다.

에 맞게를 `SuppliersSelectedIndex` 의 값 `-1`를 GridView 위에 있는 페이지에 레이블 웹 컨트롤을 추가 합니다. 설정 해당 `ID` 속성을 `ChooseSupplierMsg`, 해당 `CssClass` 속성을 `Warning`, 해당 `EnableViewState` 하 고 `Visible` 속성을 `false`, 및 해당 `Text` 하세요 속성 그리드에서 공급자를 선택 합니다. CSS 클래스 `Warning` 빨간색, 기울임꼴, 굵게, 큰 글꼴로 텍스트를 표시 하 고에 정의 된 `Styles.css`합니다. 설정 하 여는 `EnableViewState` 하 고 `Visible` 속성을 `false`, where만 포스트백에 대 한 제외 하 고 레이블을 렌더링 되지 않습니다 s control `Visible` 속성을 프로그래밍 방식으로로 설정 됩니다 `true`.


[![GridView 위에 레이블 웹 컨트롤 추가](adding-a-gridview-column-of-radio-buttons-cs/_static/image13.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image21.png)

**그림 13**: 레이블 웹 컨트롤 위에 GridView 추가 ([큰 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image22.png))


다음으로 보강를 `Click` 표시할 이벤트 처리기는 `ChooseSupplierMsg` 레이블을 지정 하는 경우 `SuppliersSelectedIndex` 보다 작은 경우 0 이며 사용자를 리디렉션할 `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID` 이 고, 그렇지 합니다.


[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample10.cs)]

클릭을 브라우저의 페이지를 방문 합니다 `SendToProducts` GridView에서 공급자를 선택 하기 전에 단추입니다. 그림 14에서 볼 수 있듯이이 표시는 `ChooseSupplierMsg` 레이블. 그런 다음 공급자를 선택 하 고 클릭는 `SendToProducts` 단추입니다. 선택한 공급자가 제공 하는 제품을 나열 하는 페이지에 있습니다 whisk는이 합니다. 그림 15는 `ProductsForSupplierDetails.aspx` Bigfoot Breweries 공급자 선택 될 때 페이지입니다.


[![ChooseSupplierMsg 레이블 아니요 공급자 선택 되어 있으면 표시 됩니다.](adding-a-gridview-column-of-radio-buttons-cs/_static/image14.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image23.png)

**그림 14**: 합니다 `ChooseSupplierMsg` 레이블 아니요 공급자 선택 되어 있으면 표시 됩니다 ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-radio-buttons-cs/_static/image24.png))


[![선택한 공급자가의 제품 ProductsForSupplierDetails.aspx에 표시 됩니다.](adding-a-gridview-column-of-radio-buttons-cs/_static/image15.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image25.png)

**그림 15**: 선택한 공급자의 제품은에 표시 됩니다 `ProductsForSupplierDetails.aspx` ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-radio-buttons-cs/_static/image26.png))


## <a name="step-5-displaying-the-selected-supplier-s-products-on-the-same-page"></a>5 단계: 같은 페이지에서 선택한 공급자가의 제품 표시

4 단계에서에서 제품은 선택한 공급자에 표시할 다른 웹 페이지로 사용자를 보내는 방법에 살펴보았습니다. 또는 선택한 공급자가의 제품을 같은 페이지에 표시할 수 있습니다. 이 설명 하기에 다른 GridView 추가한 `RadioButtonField.aspx` 선택한 공급자가의 제품을 전시 하기.

공급자 선택 되 면 표시할 제품의이 GridView만 것 이므로 아래 패널 웹 컨트롤을 추가 합니다 `Suppliers` GridView, 설정 해당 `ID` 에 `ProductsBySupplierPanel` 고 `Visible` 속성을 `false`. 패널 내에서 선택한 공급자에 대 한 제품 텍스트를 추가 합니다. 뒤에 명명 된 GridView `ProductsBySupplier`합니다. GridView가 스마트 태그에서 이라는 새 ObjectDataSource를 바인딩할 선택 `ProductsBySupplierDataSource`합니다.


[![새 ObjectDataSource ProductsBySupplier GridView 바인딩합니다](adding-a-gridview-column-of-radio-buttons-cs/_static/image16.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image27.png)

**그림 16**: 바인딩하는 `ProductsBySupplier` 새 ObjectDataSource에 GridView ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-radio-buttons-cs/_static/image28.png))


ObjectDataSource를 사용 하 여 다음으로 구성 된 `ProductsBLL` 클래스입니다. ObjectDataSource를 호출 해야 하는 선택한 공급자가 제공 하는 이러한 제품을 검색 하려고 하므로 지정 된 `GetProductsBySupplierID(supplierID)` 해당 데이터를 검색 하는 방법입니다. UPDATE, INSERT에서에서 드롭 다운 목록에서 선택 (없음) 및 탭을 삭제 합니다.


[![GetProductsBySupplierID(supplierID) 메서드를 사용 하는 ObjectDataSource 구성](adding-a-gridview-column-of-radio-buttons-cs/_static/image17.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image29.png)

**그림 17**: ObjectDataSource 사용 하도록 구성 된 `GetProductsBySupplierID(supplierID)` 메서드 ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-radio-buttons-cs/_static/image30.png))


[![UPDATE, INSERT (없음) 드롭다운 목록을 설정 하 고 탭 삭제](adding-a-gridview-column-of-radio-buttons-cs/_static/image18.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image31.png)

**그림 18**: (없음)을 드롭다운 목록에서 업데이트, 삽입 및 삭제 탭 설정 ([큰 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image32.png))


SELECT를 구성한 후 업데이트, 삽입 및 삭제 탭, 다음을 클릭 합니다. 이후를 `GetProductsBySupplierID(supplierID)` 메서드는 입력된 매개 변수, 데이터 원본 만들기 마법사가 매개 변수 값에 대 한 원본을 지정 하 라는 메시지가 나타납니다.

두 가지 옵션이 여기에서 매개 변수의 값의 소스를 지정 해야 합니다. 기본 매개 변수 개체를 사용 하 고 프로그래밍 방식으로 값을 할당할 수 있었습니다 합니다 `SuppliersSelectedIndex` 매개 변수 s에 대 한 속성 `DefaultValue` ObjectDataSource에서 속성 `Selecting` 이벤트 처리기입니다. 다시 참조를 [프로그래밍 방식으로 ObjectDataSource의 매개 변수 값을 설정](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md) 프로그래밍 방식으로 ObjectDataSource s 매개 변수에 값을 할당 세부 정보에 대 한 자습서입니다.

또는 수를 ControlParameter를 사용 하 고 참조를 `Suppliers` GridView s [ `SelectedValue` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue.aspx) (그림 19 참조). GridView s `SelectedValue` 속성에서 반환 된 `DataKey` 값에 해당 하는 [ `SelectedIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex.aspx). GridView가 프로그래밍 방식으로 설정 해야 작동 하려면이 옵션에 대 한 순서로 `SelectedIndex` 속성을 선택한 경우 행을 `ListProducts` 단추를 클릭 합니다. 설정 하 여 추가 점으로 `SelectedIndex`를 선택한 레코드를 수행 합니다 `SelectedRowStyle` 에 정의 된를 `DataWebControls` 테마 (노란색 배경).


[![ControlParameter를 사용 하 여 GridView의 SelectedValue 매개 변수 원본으로 지정](adding-a-gridview-column-of-radio-buttons-cs/_static/image19.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image33.png)

**그림 19**:를 ControlParameter를 사용 하 여 GridView의 SelectedValue 매개 변수 원본으로 지정 ([큰 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image34.png))


마법사를 완료 하면 Visual Studio 제품의 데이터 필드에 대 한 필드를 자동으로 추가 됩니다. 제거를 제외한 모든 `ProductName`, `CategoryName`, 및 `UnitPrice` BoundFields, 변경 및는 `HeaderText` Product, Category 및 Price 속성입니다. 구성 된 `UnitPrice` BoundField 해당 값을 통화로 형식이 되도록 합니다. 다음과 같이 변경한 후 GridView 패널과 ObjectDataSource가 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample11.aspx)]

이 연습을 완료 하려면 GridView가 설정 해야 `SelectedIndex` 속성을를 `SelectedSuppliersIndex` 및 `ProductsBySupplierPanel` 패널 s `Visible` 속성을 `true` 경우는 `ListProducts` 단추를 클릭 합니다. 이를 위해 이벤트 처리기를 만듭니다는 `ListProducts` 단추 웹 컨트롤의 `Click` 이벤트 다음 코드를 추가 합니다.


[!code-csharp[Main](adding-a-gridview-column-of-radio-buttons-cs/samples/sample12.cs)]

GridView에서 공급자를 선택 하지 않은 경우는 `ChooseSupplierMsg` 레이블이 표시 되 고 `ProductsBySupplierPanel` 숨겨진 패널. 공급자를 선택한 경우 그러지 합니다 `ProductsBySupplierPanel` 표시 됩니다 및 GridView의 `SelectedIndex` 속성이 업데이트 됩니다.

그림 20 Bigfoot Breweries 공급자를 선택한 후 페이지 단추에 표시할 제품이 클릭 한 후 결과 보여 줍니다.


[![같은 페이지에 나열 됩니다 Bigfoot Breweries에서 제품 제공](adding-a-gridview-column-of-radio-buttons-cs/_static/image20.gif)](adding-a-gridview-column-of-radio-buttons-cs/_static/image35.png)

**그림 20**: 같은 페이지에 나열 됩니다 Bigfoot Breweries에서 제공 되는 제품 ([큰 이미지를 보려면 클릭](adding-a-gridview-column-of-radio-buttons-cs/_static/image36.png))


## <a name="summary"></a>요약

에 설명 된 대로 합니다 [마스터/세부 정보 DetailView와 함께 선택 가능한 마스터 GridView를 사용 하 여 세부 정보](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) 자습서를 CommandField를 사용 하 여 GridView에서 레코드를 선택할 수 있습니다입니다 `ShowSelectButton` 속성이 `true`합니다. 하지만 CommandField 일반 푸시 단추, 링크 또는 이미지 단추가 표시 됩니다. 대체 행 선택 사용자 인터페이스를 각 GridView 행에 있는 확인란 또는 라디오 단추를 제공 하는 것입니다. 이 자습서에서는 열의 라디오 단추를 추가 하는 방법을 살펴보았습니다.

그러나 예상할 수 있듯이 간단 또는 단순으로 열의 라디오 단추 되지 않으면 추가 합니다. 단추 클릭에 추가할 수 있는 기본 제공 RadioButtonField 없습니다 되며 자체 문제 집합이 소개를 TemplateField 내에서 RadioButton 웹 컨트롤 사용. 결국에서 이러한 인터페이스를 제공 하거나 해야 사용자 지정 만들기 `DataControlField` 클래스나 중를 TemplateField로 적절 한 HTML을 삽입 하는 수단을 `RowCreated` 이벤트입니다.

열의 라디오 단추를 추가 하는 방법을 탐색할 필요 확인란의 열 추가를 배웠으므로 수 있도록 합니다. 확인란의 열을 사용 하 여 사용자 GridView 행을 하나 이상 선택 하 고 (예: 웹 기반 전자 메일 클라이언트에서 전자 메일의 집합을 선택 하 고 모든 선택한 전자 메일을 삭제 하도록 선택)를 선택된 된 행의 모든에서 일부 작업을 수행할 수 있습니다. 다음 자습서에서 이러한 열을 추가 하는 방법에 살펴보겠습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 David Suru 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](adding-a-gridview-column-of-checkboxes-cs.md)
