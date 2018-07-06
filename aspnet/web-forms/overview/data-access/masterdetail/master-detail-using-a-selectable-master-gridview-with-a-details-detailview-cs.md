---
uid: web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs
title: 마스터/세부 정보는 선택 가능한 마스터 GridView를 사용 하 여 세부 정보 DetailView (C#)를 사용 하 여 | Microsoft Docs
author: rick-anderson
description: 이 자습서는 GridView 행이 있는 이름과 선택 단추와 함께 각 제품의 가격을 포함 해야 합니다. particu에 대 한 선택 단추를 클릭 하는 중...
ms.author: aspnetcontent
ms.date: 03/31/2010
ms.assetid: 0f982827-f8f9-420d-b36b-57b23f5aa519
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs
msc.type: authoredcontent
ms.openlocfilehash: ea1bb03e2ea39198b70cf71c1105b3e6134e3971
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37825758"
---
<a name="masterdetail-using-a-selectable-master-gridview-with-a-details-detailview-c"></a>마스터/세부 정보는 선택 가능한 마스터 GridView를 사용 하 여 세부 정보 DetailView (C#)를 사용 하 여
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_10_CS.exe) 또는 [PDF 다운로드](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/datatutorial10cs1.pdf)

> 이 자습서는 GridView 행이 있는 이름과 선택 단추와 함께 각 제품의 가격을 포함 해야 합니다. 특정 제품의 선택 단추를 클릭 하면 전체 세부 정보를 동일한 페이지의 DetailsView 컨트롤에 표시 합니다.


## <a name="introduction"></a>소개

에 [이전 자습서](master-detail-filtering-across-two-pages-cs.md) 두 개의 웹 페이지를 사용 하 여 마스터/세부 정보 보고서를 만드는 방법에 살펴보았습니다:에서는 suppliers; 목록을 표시 하는 "마스터" 웹 페이지 및 선택한 제공한 이러한 제품을 나열 하는 "세부 정보" 웹 페이지 공급 업체입니다. 한 페이지에이 두 페이지 보고서 형식을 요약할 수 있습니다. 이 자습서는 GridView 행이 있는 이름과 선택 단추와 함께 각 제품의 가격을 포함 해야 합니다. 특정 제품의 선택 단추를 클릭 하면 전체 세부 정보를 동일한 페이지의 DetailsView 컨트롤에 표시 합니다.


[![선택 단추를 클릭 하면 제품의 세부 정보가 표시 됩니다.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image2.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image1.png)

**그림 1**: 선택 단추를 클릭 하면 제품의 세부 정보가 표시 됩니다. ([큰 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image3.png))


## <a name="step-1-creating-a-selectable-gridview"></a>1 단계: 만들기를 선택할 수 있는 GridView

두 페이지 마스터/세부 정보에는 각 마스터 레코드 하이퍼링크를 포함 하는 보고 하는 재현 율,를 클릭 하면 클릭 한 행을 전달 하 여 세부 정보 페이지에 사용자를 전송 `SupplierID` 쿼리 문자열에서 값입니다. 이러한 하이퍼링크는 HyperLinkField를 사용 하 여 각 GridView 행에 추가 되었습니다. 단일 페이지 마스터/세부 정보 보고서에 대 한 필요 단추를 클릭 하면, 각 GridView 행에 대 한 세부 정보를 표시 합니다. GridView 컨트롤을 포스트백과 GridView의로 해당 행을 표시 하는 각 행의 선택 단추가 포함 하도록 구성할 수 있습니다 [SelectedRow](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedrow.aspx)합니다.

GridView 컨트롤을 추가 하 여 시작 합니다 `DetailsBySelecting.aspx` 페이지에 `Filtering` 폴더를 설정 해당 `ID` 속성을 `ProductsGrid`입니다. 라는 새 ObjectDataSource를 다음으로, 추가 `AllProductsDataSource` 를 호출 하는 `ProductsBLL` 클래스의 `GetProducts()` 메서드.


[![AllProductsDataSource 라는 ObjectDataSource 만들기](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image5.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image4.png)

**그림 2**: 명명 된 ObjectDataSource 만들려면 `AllProductsDataSource` ([클릭 하 여 큰 이미지 보기](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image6.png))


[![ProductsBLL 클래스 사용](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image8.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image7.png)

**그림 3**: 사용 된 `ProductsBLL` 클래스 ([클릭 하 여 큰 이미지 보기](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image9.png))


[![GetProducts() 메서드를 호출 하는 ObjectDataSource 구성](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image11.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image10.png)

**그림 4**: invoke ObjectDataSource를 구성 합니다 `GetProducts()` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image12.png))


제거 하는 GridView의 필드를 편집을 제외한 모든 `ProductName` 및 `UnitPrice` BoundFields 합니다. 또한 형식 지정과 같은 필요에 따라 이러한 BoundFields에 맞게 자유롭게 합니다 `UnitPrice` 통화로 BoundField 및 변경를 `HeaderText` 는 BoundFields의 속성입니다. GridView의 스마트 태그에서 열 편집 링크를 클릭 하 여 또는 선언적 구문을 수동으로 구성 하 여 이러한 단계를 그래픽으로 수행할 수 있습니다.


[![ProductName 및 UnitPrice BoundFields 남기고 모두 제거](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image14.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image13.png)

**그림 5**: 제거 제외한 모든 합니다 `ProductName` 하 고 `UnitPrice` BoundFields ([클릭 하 여 큰 이미지 보기](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image15.png))


GridView에 대 한 최종 태그 다음과 같습니다.


[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample1.aspx)]

다음으로, 각 행에 선택 단추를 추가 하는 GridView를 선택할 수 있는 것으로 표시 해야 합니다. 이렇게 하려면 단순히 GridView의 스마트 태그를 사용 하도록 설정 선택 확인란을 확인 합니다.


[![GridView의 행을 선택할 수 있는 확인](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image17.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image16.png)

**그림 6**: GridView의 행 선택 가능한 확인 ([큰 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image18.png))


CommandField 추가 설정 선택 옵션을 선택 합니다 `ProductsGrid` GridView를 사용 하 여 해당 `ShowSelectButton` 속성이 True로 설정 합니다. 이 인해 선택 단추의 GridView의 각 행에 대 한 그림 6에서 볼 수 있듯이 합니다. 기본적으로 선택 단추는 Linkbutton을으로 렌더링 됩니다 있지만 단추나 ImageButtons CommandField의를 통해 대신 사용할 수 있습니다 `ButtonType` 속성입니다.


[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample2.aspx)]

포스트백 근거가 GridView 행의 선택 단추를 클릭할 때 GridView의 및 `SelectedRow` 속성이 업데이트 됩니다. 외에 `SelectedRow` 속성인 GridView 제공 합니다 [SelectedIndex](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex%28VS.80%29.aspx), [SelectedValue](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue%28VS.80%29.aspx), 및 [SelectedDataKey](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selecteddatakey%28VS.80%29.aspx) 속성. `SelectedIndex` 반면 속성에서 선택한 행의 인덱스를 반환 합니다 `SelectedValue` 및 `SelectedDataKey` GridView의 기준 값을 반환 하는 속성 [DataKeyNames 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames%28VS.80%29.aspx)합니다.

`DataKeyNames` 속성 하나를 연결 하는 데 사용 됩니다 또는 데이터 필드를 더 각 행 값에 일반적으로 각 GridView 행을 사용 하 여 기본 데이터에서 고유 하 게 식별 정보 특성을 사용 합니다. `SelectedValue` 속성에는 첫 번째 값을 반환 합니다 `DataKeyNames` 선택한 행의 데이터 필드 여기서는 `SelectedDataKey` 선택된 된 행을 반환 하는 속성 `DataKey` 모든에 대해 지정 된 데이터 키 필드 값을 포함 하는 개체 해당 행입니다.

`DataKeyNames` GridView, DetailsView 또는 FormView 디자이너를 통해 데이터 소스를 바인딩하는 경우 고유 하 게 식별 하는 데이터 필드에 속성이 자동 설정 됩니다. 예제에서는 작동 하지 않고 했겠지만이 속성 설정한 우리 회사에 자동으로 이전 자습서에서 하는 동안는 `DataKeyNames` 지정 된 속성입니다. 그러나이 자습서에서는 선택할 수 있는 GridView 그리고는 우리가 됩니다 수 검사 삽입, 업데이트 및 삭제 하는 이후 자습서는 `DataKeyNames` 속성을 올바르게 설정 해야 합니다. GridView의 되도록 잠시 `DataKeyNames` 속성이 `ProductID`합니다.

브라우저를 통해 지금까지 진행 상황을 확인해 보겠습니다. GridView 이름 및 모든 선택 LinkButton 함께 제품에 대 한 가격을 나열 하는 참고 합니다. 포스트백을 발생 시키는 선택 단추를 클릭 합니다. 2 단계에서에서 선택한 제품에 대 한 세부 정보를 표시 하 여이 포스트백을 DetailsView 대응 하는 방법을 살펴보겠습니다.


[![각 제품 행 선택 LinkButton 포함](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image20.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image19.png)

**그림 7**: 각 제품 행을 선택 하는 LinkButton 포함 ([큰 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image21.png))


### <a name="highlighting-the-selected-row"></a>선택한 행을 강조 표시

합니다 `ProductsGrid` GridView에는 `SelectedRowStyle` 선택한 행에 대 한 비주얼 스타일을 나타내는 데 사용할 수 있는 속성입니다. 적절 하 게 사용이 성능을 향상 시킬 수 사용자의 자세한 명확 하 게를 표시 하 여 현재 선택 된 GridView의 어떤 행. 이 자습서에서는 노란색 배경으로 강조 표시 선택된 된 행을 보겠습니다.

이전 자습서에서와 마찬가지로 CSS 클래스로 정의 미학 관련 설정을 유지 하려면 노력 하겠습니다. 따라서 새 CSS 클래스를 만듭니다 `Styles.css` 라는 `SelectedRowStyle`합니다.


[!code-css[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample3.css)]

이 CSS 클래스를 적용 하는 `SelectedRowStyle` 의 속성 *모든* 자습서 시리즈에서 Gridview 편집를 `GridView.skin` 에서 스킨를 `DataWebControls` 포함 하는 테마를 `SelectedRowStyle` 설정을 아래와 같이:


[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample4.aspx)]

이 또한을 사용 하 여 선택한 GridView 행 배경색을 노란색으로 강조 이제 표시 됩니다.


[![GridView의 SelectedRowStyle 속성을 사용 하 여 선택된 된 행의 모양을 사용자 지정](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image23.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image22.png)

**그림 8**: 사용자 지정 선택한 행의 모양을 사용 하는 GridView `SelectedRowStyle` 속성 ([클릭 하 여 큰 이미지 보기](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image24.png))


## <a name="step-2-displaying-the-selected-products-details-in-a-detailsview"></a>DetailsView에서 선택한 제품의 세부 정보를 표시 하는 2 단계:

사용 하 여는 `ProductsGrid` 선택한 특정 제품에 대 한 정보를 표시 하는 DetailsView를 추가 하려면 유지 된 모든 GridView 완료 합니다. GridView 위에 DetailsView 컨트롤을 추가 라는 새로운 ObjectDataSource는 만들고 `ProductDetailsDataSource`합니다. 선택한 제품에 대 한 특정 정보를 표시 하려면이 DetailsView를 것 이므로 구성 합니다 `ProductDetailsDataSource` 사용 하는 `ProductsBLL` 클래스의 `GetProductByProductID(productID)` 메서드.


[![ProductsBLL 클래스의 GetProductByProductID(productID) 메서드를 호출 합니다.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image26.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image25.png)

**그림 9**: 호출 된 `ProductsBLL` 클래스의 `GetProductByProductID(productID)` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image27.png))


있어야 합니다 *`productID`* GridView 컨트롤에서 얻은 매개 변수의 값 `SelectedValue` 속성입니다. GridView의 앞에서 설명한 대로 `SelectedValue` 속성 첫 번째 데이터 키 선택한 행의 값을 반환 합니다. 따라서 반드시는 GridView의 `DataKeyNames` 속성이 `ProductID`되도록 선택한 행의 `ProductID` 반환한 값 `SelectedValue`합니다.


[![GridView의 SelectedValue 속성에는 productID 매개 변수 설정](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image29.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image28.png)

**그림 10**: 설정 된 *`productID`* GridView의 매개 변수 `SelectedValue` 속성 ([클릭 하 여 큰 이미지 보기](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image30.png))


한 번의 `productDetailsDataSource` ObjectDataSource 올바르게 구성 되었으며 DetailsView에 바인딩된,이 자습서를 완료! 해당 페이지를 처음으로 방문 하는 경우 행을 선택 하면 하므로 GridView의 `SelectedValue` 속성이 반환 `null`합니다. 사용 하 여 제품이 있으므로 `NULL` `ProductID` 값으로 반환 된 레코드가 없을 `GetProductByProductID(productID)` 메서드입니다. DetailsView 표시 되지 않으면 즉, (그림 11 참조). GridView 행의 선택 단추를 클릭 하면 포스트백 근거가 및 DetailsView 새로 고쳐집니다. GridView의 이번 `SelectedValue` 속성에서 반환 합니다 `ProductID` 선택한 행의는 `GetProductByProductID(productID)` 메서드가 반환 되는 `ProductsDataTable` 해당 특정 제품 및 DetailsView에 대 한 정보를 사용 하 여 이러한 세부 정보를 보여 줍니다. (그림 12 참조).


[![첫 번째 방문 GridView만 표시 되 면](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image32.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image31.png)

**그림 11**: 먼저 방문 GridView만 표시 됩니다 ([큰 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image33.png))


[![행을 선택 하면 제품의 세부 정보가 표시 됩니다.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image35.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image34.png)

**그림 12**: 행을 선택 하면 제품의 세부 정보가 표시 됩니다 ([큰 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image36.png))


## <a name="summary"></a>요약

이 단원과 이전 세 가지 자습서를 다양 한 마스터/세부 정보 보고서를 표시 하기 위한 기술 살펴보았습니다. 이 자습서를 살펴보았습니다 마스터 레코드와 동일한 페이지에 선택한 마스터 레코드에 대 한 세부 정보를 표시할 DetailsView를 보관 하 선택 가능한 GridView를 사용 합니다. 이전 자습서에서 하나의 웹 페이지 및 다른 세부 정보 레코드에서 마스터 레코드를 표시 하는 Dropdownlist를 사용 하 여 마스터/세부 정보 보고서를 표시 하는 방법에 살펴보았습니다.

이 자습서의 마스터/세부 정보 보고서는 검사를 완료 했습니다. 다음 tutorialwe부터 GridView, DetailsView 및 FormView 사용 하 여 사용자 지정 된 형식의 탐색을 시작 해 보겠습니다. 에 바인딩된 데이터를 기반으로 이러한 컨트롤의 모양을 사용자 지정 하는 방법, GridView의 바닥글에 데이터를 요약 하는 방법 및 뛰어난 레이아웃에 대 한 제어를 가져오려면 템플릿을 사용 하는 방법을 살펴보겠습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Hilton giesenow와 함께 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-detail-filtering-across-two-pages-cs.md)
> [다음](master-detail-filtering-with-a-dropdownlist-vb.md)
