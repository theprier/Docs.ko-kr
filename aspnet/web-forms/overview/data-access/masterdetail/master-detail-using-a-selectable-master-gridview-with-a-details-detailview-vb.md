---
uid: web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb
title: 선택 가능한 마스터 GridView 세부 정보 DetailView (VB)를 사용 하 여 마스터/세부 | Microsoft Docs
author: rick-anderson
description: 이 자습서는 GridView 행이 있는 이름과 선택 단추와 함께 각 제품의 가격을 포함 해야 합니다. particu에 대 한 선택 단추를 클릭 하면...
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 1d1a7c93-971d-4690-9c5e-dac0e5014a09
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb
msc.type: authoredcontent
ms.openlocfilehash: 80db1589de901f7364c05c5bb67829145579b6c0
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30881105"
---
<a name="masterdetail-using-a-selectable-master-gridview-with-a-details-detailview-vb"></a>마스터/세부 정보 DetailView (VB)는 선택 가능한 마스터 GridView 사용
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_10_VB.exe) 또는 [PDF 다운로드](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/datatutorial10vb1.pdf)

> 이 자습서는 GridView 행이 있는 이름과 선택 단추와 함께 각 제품의 가격을 포함 해야 합니다. 특정 제품에 대 한 선택 단추를 클릭 하면 같은 페이지에 DetailsView 컨트롤에 표시할 전체 세부 정보.


## <a name="introduction"></a>소개

에 [이전 자습서](master-detail-filtering-across-two-pages-vb.md) 두 개의 웹 페이지를 사용 하 여 마스터/세부 정보 보고서를 만드는 방법에 살펴보았습니다: 공급 업체; 목록을 표시 했습니다 되는 "마스터" 웹 페이지 및 선택한에서 제공 하는 해당 제품을 나열 하는 "details" 웹 페이지 공급 업체입니다. 이 두 페이지 보고서 형식은 한 페이지를 모두 나타낼 수 있습니다. 이 자습서는 GridView 행이 있는 이름과 선택 단추와 함께 각 제품의 가격을 포함 해야 합니다. 특정 제품에 대 한 선택 단추를 클릭 하면 같은 페이지에 DetailsView 컨트롤에 표시할 전체 세부 정보.


[![선택 단추를 클릭 하 여 제품의 세부 정보가 표시 됩니다.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image2.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image1.png)

**그림 1**: 제품의 세부 정보를 표시 하 고 선택 단추를 클릭 하면 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image3.png))


## <a name="step-1-creating-a-selectable-gridview"></a>1 단계: 선택 가능한 GridView 만들기

회수 마스터/세부 두 페이지에에서는 마스터 각 레코드는 하이퍼링크를 포함 하는 보고 하는 클릭 하면 클릭 한 행을 전달 하는 세부 정보 페이지에 사용자를 전송 `SupplierID` 쿼리 문자열의 값입니다. 이러한 하이퍼링크는 HyperLinkField를 사용 하 여 각 GridView 행에 추가 되었습니다. 필요한 단일 페이지 마스터/세부 정보 보고서에 대 한 단추를 클릭 하면 각 GridView 행는 대 한 세부 정보를 표시 합니다. GridView 컨트롤에서 포스트백이 발생 하 고 해당 행 GridView의으로 표시 되는 각 행에 대 한 선택 단추를 포함 하도록 구성할 수 있습니다 [SelectedRow](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedrow.aspx)합니다.

GridView 컨트롤을 추가 하 여 시작 된 `DetailsBySelecting.aspx` 페이지에 `Filtering` 폴더를 설정 해당 `ID` 속성을 `ProductsGrid`합니다. 다음으로 명명 된 새 ObjectDataSource 추가 `AllProductsDataSource` 를 호출 하는 `ProductsBLL` 클래스의 `GetProducts()` 메서드.


[![AllProductsDataSource 라는 ObjectDataSource 만들기](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image5.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image4.png)

**그림 2**: 명명 된 ObjectDataSource 만드는 `AllProductsDataSource` ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image6.png))


[![ProductsBLL 클래스를 사용 하 여](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image8.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image7.png)

**그림 3**: 사용 된 `ProductsBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image9.png))


[![구성 ObjectDataSource GetProducts() 메서드를 호출 하려면](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image11.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image10.png)

**그림 4**: 구성 invoke ObjectDataSource는 `GetProducts()` 메서드 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image12.png))


제거 하는 GridView의 필드 편집 제외한 모두 `ProductName` 및 `UnitPrice` BoundFields 합니다. 또한 서식 지정 하는 등 필요에 따라 이러한 BoundFields 사용자 지정을 자유롭게는 `UnitPrice` 통화로 BoundField 및 변경는 `HeaderText` 는 BoundFields의 속성입니다. GridView의 스마트 태그에서 열 편집 링크를 클릭 하 여 또는 선언적 구문을 수동으로 구성 하 여 다음이 단계를 그래픽으로 수행할 수 있습니다.


[![ProductName 및 UnitPrice BoundFields 남기고 모두 제거](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image14.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image13.png)

**그림 5**: 제거 제외 하 고 모두는 `ProductName` 및 `UnitPrice` BoundFields ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image15.png))


GridView에 대 한 최종 태그는입니다.


[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample1.aspx)]

다음으로, 각 행에 선택 단추를 추가 하는 GridView 선택 가능으로 표시 해야 합니다. 이렇게 하려면 단순히 확인란을 선택 가능 GridView의 스마트 태그입니다.


[![GridView의 행을 선택할 수 있는 만들기](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image17.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image16.png)

**그림 6**: GridView의 행 선택 가능한 확인 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image18.png))


에 CommandField 추가 선택 영역을 사용 하도록 설정 옵션을 선택는 `ProductsGrid` 이 있는 GridView의 `ShowSelectButton` 속성이 True로 설정 합니다. 따라서 선택 단추는 GridView의 각 행에 대 한 그림 6 있듯이 됩니다. 기본적으로 선택 단추 링크 단추가,으로 렌더링 하지만 단추 또는 ImageButtons CommandField의를 통해 대신 사용할 수 있습니다 `ButtonType` 속성입니다.


[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample2.aspx)]

포스트백 계속 GridView 행의 선택 단추를 클릭할 때 및 GridView의 `SelectedRow` 속성이 업데이트 됩니다. 이외에 `SelectedRow` 속성, GridView 제공는 [SelectedIndex](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex%28VS.80%29.aspx), [SelectedValue](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue%28VS.80%29.aspx), 및 [SelectedDataKey](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selecteddatakey%28VS.80%29.aspx) 속성입니다. `SelectedIndex` 속성이 선택된 된 행의 인덱스를 반환 하지만 `SelectedValue` 및 `SelectedDataKey` 속성 GridView의 기준 값을 반환 [DataKeyNames 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames%28VS.80%29.aspx)합니다.

`DataKeyNames` 하나 연결할 속성은 사용 또는 더 많은 데이터 필드 값 각 행을 포함 하는 특성 각 GridView 행은 데이터의 정보를 고유 하 게 식별 하는 데 주로 사용 합니다. `SelectedValue` 속성이 첫 번째 값을 반환 `DataKeyNames` 데이터 필드에 선택된 된 행으로 where는 `SelectedDataKey` 속성 선택된 된 행을 반환 `DataKey` 지정 된 데이터 키 필드에 대 한 값이 모두 들어 있는 개체를 해당 행입니다.

`DataKeyNames` GridView, DetailsView, 또는 디자이너를 통해 FormView에 데이터 소스에 바인딩하는 경우 고유 하 게 식별 하는 데이터 필드 속성이 자동 설정 됩니다. 없이 예제는 동작이 속성에 설정한 우리 자동으로 이전 자습서에서 동안는 `DataKeyNames` 지정 된 속성입니다. 그러나이 자습서에서는 선택 가능한 GridView에 대 한 것은 물론는 म 합니다 수 검사 삽입, 업데이트 및 삭제, 이후 자습서에서 `DataKeyNames` 속성을 올바르게 설정 해야 합니다. GridView의 확인을 `DataKeyNames` 속성이 `ProductID`합니다.

지금까지 브라우저를 통해 진행률을 보겠습니다. GridView의 이름 및 모든 선택 LinkButton 함께 제품에 대 한 가격 표시 되는지 확인 합니다. 선택 단추를 클릭 하면 다시 게시 합니다. 2 단계에서에서 선택한 제품에 대 한 세부 정보를 표시 하 여이 포스트백에 DetailsView 응답 하는 방법을 살펴보겠습니다.


[![각 제품 행 선택 LinkButton 포함](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image20.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image19.png)

**그림 7**: 선택 LinkButton을 포함 하는 각 제품 행 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image21.png))


## <a name="highlighting-the-selected-row"></a>선택한 행을 강조 표시

`ProductsGrid` GridView에는 `SelectedRowStyle` 속성을 선택된 된 행에 대 한 시각적 스타일을 나타내는 데 사용할 수입니다. 적절 하 게 사용이 향상 시킬 수는 사용자의 환경을 더 명확 하 게를 표시 하 여 현재 선택 된 GridView의 어떤 행. 이 자습서에서 노란색 배경으로 강조 표시 선택 된 행 죠.

이 이전 자습서에서와 마찬가지로 CSS 클래스로 정의 된 좋게 관련 설정을 사용 하려면 노력 하겠습니다 합니다. 따라서 새로운 CSS 클래스를 만들 `Styles.css` 라는 `SelectedRowStyle`합니다.


[!code-css[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample3.css)]

이 CSS 클래스를 적용 하려면는 `SelectedRowStyle` 의 속성 *모든* 는 자습서 시리즈의 Gridview 편집는 `GridView.skin` 에서 스킨는 `DataWebControls` 포함 하도록 테마는 `SelectedRowStyle` 아래와 같이 설정:


[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample4.aspx)]

이 추가 된 선택 된 GridView 행 노란색 배경색으로 강조 이제 표시 됩니다.


[![GridView의 SelectedRowStyle 속성을 사용 하 여 선택한 행의 모양을 사용자 지정](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image23.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image22.png)

**그림 8**: 사용자 지정 모양을 사용 하 여 선택한 행의 GridView의 `SelectedRowStyle` 속성 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image24.png))


## <a name="step-2-displaying-the-selected-products-details-in-a-detailsview"></a>2 단계: DetailsView에 선택된 된 제품 세부 정보 표시

와 `ProductsGrid` 남아 선택한 특정 제품에 대 한 정보를 나타내는 DetailsView를 추가 하는 모든 GridView 완료 합니다. GridView 위에 DetailsView 컨트롤을 추가 하 고 라는 새 ObjectDataSource 만들 `ProductDetailsDataSource`합니다. 선택한 제품에 대 한 특정 정보를 표시 하려면이 DetailsView 할 것 이므로 구성는 `ProductDetailsDataSource` 사용 하 여 `ProductsBLL` 클래스의 `GetProductByProductID(productID)` 메서드.


[![ProductsBLL 클래스 GetProductByProductID(productID) 메서드를 호출 합니다.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image26.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image25.png)

**그림 9**: 호출 된 `ProductsBLL` 클래스의 `GetProductByProductID(productID)` 메서드 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image27.png))


있어야는 *`productID`* GridView 컨트롤에서 가져온 매개 변수 값 `SelectedValue` 속성입니다. GridView의 앞에서 설명한 대로 `SelectedValue` 속성 첫 번째 데이터 키 선택된 된 행에 대 한 값을 반환 합니다. 따라서를 반드시 하는 GridView의 `DataKeyNames` 속성이 `ProductID`되도록 선택한 행의 `ProductID` 반환한 값 `SelectedValue`합니다.


[![GridView의 SelectedValue 속성에는 productID 매개 변수 설정](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image29.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image28.png)

**그림 10**: 설정의 *`productID`* 매개 변수를 GridView의 `SelectedValue` 속성 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image30.png))


한 번의 `productDetailsDataSource` 이 자습서를 완료, ObjectDataSource 올바르게 구성 되었으며 DetailsView에 바인딩된! 해당 페이지를 처음 방문 하는 경우 선택한 행, 하므로 GridView의 `SelectedValue` 속성에서 반환 `Nothing`합니다. 없는 제품을 되므로 `NULL` `ProductID` 값에서 반환 된 레코드가 없습니다는 `GetProductByProductID(productID)` DetailsView 표시 되지 않으면 의미 메서드 (11 그림 참조). GridView 행의 선택 단추를 클릭 하면 계속 다시 게시 하 고 DetailsView 새로 고쳐집니다. GridView의 이번 `SelectedValue` 속성에서 반환은 `ProductID` 선택한 행의는 `GetProductByProductID(productID)` 메서드가 반환 되는 `ProductsDataTable` 해당 특정 제품 및 DetailsView에 대 한 정보로 이러한 세부 정보를 표시 합니다 (그림 12 참조).


[![첫 번째 방문한 GridView만 표시 되 면](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image32.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image31.png)

**그림 11**: 먼저 방문 GridView만 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image33.png))


[![행을 선택 하면 제품의 세부 정보가 표시 됩니다.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image35.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image34.png)

**그림 12**: 행을 선택 하면 제품의 세부 정보가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image36.png))


## <a name="summary"></a>요약

이 예제와 이전 세 개의 자습서 마스터/세부 보고서를 표시 하는 여러를 살펴보았습니다. 검사 했습니다이 자습서에서는 선택 가능한 GridView를 사용 하 여 마스터 레코드와 동일한 페이지에 선택된 된 마스터 레코드에 대 한 정보를 표시 하려면 DetailsView을 수용 하도록 합니다. 이전 자습서에서 한 웹 페이지 및 다른 세부 레코드에서 마스터 레코드를 표시 하는 dropdownlist 활용을 사용 하 여 마스터/세부 정보 보고서를 표시 하는 방법을 찾았습니다.

이 자습서의 마스터/세부 보고서 우리의 검사도 마칩니다. 다음 자습서와 함께 시작 GridView, DetailsView, 및 FormView 사용자 지정 된 형식 지정의 탐색을 시작 합니다. 에 바인딩된 데이터를 기반으로 이러한 컨트롤의 모양을 사용자 지정 하는 방법, GridView의 바닥글에 데이터를 요약 하는 방법 및 높은 수준의 레이아웃에 대 한 제어를 가져오려면 서식 파일을 사용 하는 방법을 살펴보겠습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Hilton Giesenow 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-detail-filtering-across-two-pages-vb.md)
