---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
title: 마스터/세부 정보 필터링 (C#) DropDownList 한 개로 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 마스터 레코드 DropDownList 컨트롤과 GridView에서 선택한 목록 항목의 세부 정보를 표시 하는 방법을 살펴보겠습니다.
ms.author: aspnetcontent
ms.date: 03/31/2010
ms.assetid: 53e659cc-eefb-40c1-a1dc-559481c99443
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
msc.type: authoredcontent
ms.openlocfilehash: c2bf3156840c378e554eef3a0629705c059f2777
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37833344"
---
<a name="masterdetail-filtering-with-a-dropdownlist-c"></a>마스터/세부 정보 (C#) DropDownList 한 개로 필터링
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_7_CS.exe) 또는 [PDF 다운로드](master-detail-filtering-with-a-dropdownlist-cs/_static/datatutorial07cs1.pdf)

> 이 자습서에서는 마스터 레코드 DropDownList 컨트롤과 GridView에서 선택한 목록 항목의 세부 정보를 표시 하는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

보고서의 일반적인 형식은 합니다 *마스터/세부 정보 보고서*, 일부 "마스터" 레코드 집합을 표시 하 여 시작 하는 보고서에서. 사용자를 살펴볼 수 아래로 마스터 레코드 중 하나 있으므로 해당 마스터 레코드의 세부 정보를 "." 보기 마스터/세부 정보는 보고서와 같은 1 대 다 관계를 시각화에 대 한 이상적인 모든 범주를 표시 및 다음 사용자를 특정 범주를 선택 하 고 연결 된 제품을 표시할 수 있도록 보고 합니다. 또한 마스터/세부 정보 보고서 (많은 열 임) 특히 "와이드" 테이블에서 자세한 정보를 표시 하는 데 유용 합니다. 예를 들어 마스터/세부 정보 보고서의 "마스터" 수준 데이터베이스에서 제품 이름과 단위 가격만 제품을 표시할 수 있습니다 하 고 특정 제품에 드릴 다운 하면 추가 제품 필드를 표시 됩니다 (범주, 공급자, 단위, quantity 및 등등)입니다.

여러 가지 방법으로는 마스터/세부 정보 보고서를 구현할 수 있습니다. 이 고 다음 세 개의 자습서를 통해 다양 한 마스터/세부 정보 보고서에 살펴보겠습니다. 이 자습서에서 마스터 레코드를 표시 하는 방법을 알아봅니다를 [DropDownList 컨트롤](https://msdn.microsoft.com/library/dtx91y0z.aspx) 와 GridView에서 선택한 목록 항목의 세부 정보입니다. 특히이 자습서의 마스터/세부 정보 보고서는 범주 및 제품 정보를 나열 됩니다.

## <a name="step-1-displaying-the-categories-in-a-dropdownlist"></a>1 단계: DropDownList에 범주를 표시합니다.

마스터/세부 정보 보고서는 선택한 목록 항목의 제품이 표시를 사용 하 여 DropDownList, 범주 표시 페이지는 GridView에서 더 아래쪽 합니다. 첫 번째 작업을 미리 한는 DropDownList에 표시 되는 범주를 것입니다. 열기는 `FilterByDropDownList.aspx` 페이지에 `Filtering` 폴더, DropDownList에 페이지의 디자이너 도구 상자에서 끌어서 설정 해당 `ID` 속성을 `Categories`입니다. 다음으로, DropDownList의 스마트 태그의 데이터 소스 선택 링크를 클릭 합니다. 데이터 소스 구성 마법사가 표시 됩니다.


[![DropDownList의 데이터 소스를 지정 합니다.](master-detail-filtering-with-a-dropdownlist-cs/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image1.png)

**그림 1**: DropDownList의 데이터 원본을 지정 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image3.png))


라는 새 ObjectDataSource를 추가 하도록 선택할 `CategoriesDataSource` 를 호출 하는 `CategoriesBLL` 클래스의 `GetCategories()` 메서드.


[![CategoriesDataSource 라는 새 ObjectDataSource를 추가 합니다.](master-detail-filtering-with-a-dropdownlist-cs/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image4.png)

**그림 2**: 새 ObjectDataSource 라는 추가 `CategoriesDataSource` ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-cs/_static/image6.png))


[![CategoriesBLL 클래스를 사용 하려면 선택 합니다.](master-detail-filtering-with-a-dropdownlist-cs/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image7.png)

**그림 3**: 사용 하도록 선택 합니다 `CategoriesBLL` 클래스 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-cs/_static/image9.png))


[![GetCategories() 메서드를 사용 하는 ObjectDataSource 구성](master-detail-filtering-with-a-dropdownlist-cs/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image10.png)

**그림 4**: ObjectDataSource 사용 하도록 구성 된 `GetCategories()` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-cs/_static/image12.png))


DropDownList에 어떤 데이터 원본 필드를 표시 해야 하 고는 지정 해야 하는 ObjectDataSource를 구성한 후 목록 항목에 대 한 값으로 연결 해야 하나입니다. 있어야 합니다 `CategoryName` 필드를 표시 및 `CategoryID` 각 목록 항목에 대 한 값으로.


[![가 DropDownList 표시를 사용 하 여 CategoryID와 CategoryName 필드 값](master-detail-filtering-with-a-dropdownlist-cs/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image13.png)

**그림 5**: DropDownList을 표시 합니다 `CategoryName` 필드 및 사용 `CategoryID` 값으로 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-cs/_static/image15.png))


이 시점에서 레코드를 사용 하 여 채워지는 DropDownList 컨트롤이 있습니다를 `Categories` 테이블 (모두 약 6 초 후에 수행). 그림 6 브라우저를 통해 볼 때 지금 진행 상황을 보여줍니다.


[![현재 범주를 나열 하는 드롭다운](master-detail-filtering-with-a-dropdownlist-cs/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image16.png)

**그림 6**:는 드롭다운 목록이 현재 범주 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image18.png))


## <a name="step-2-adding-the-products-gridview"></a>2 단계: 추가 제품 GridView

마스터/세부 정보 보고서의 마지막 단계는 선택한 범주와 관련 된 제품을 나열 하는 것입니다. 이렇게 하려면 페이지에 GridView를 추가 하 고 라는 새로운 ObjectDataSource는 만들 `productsDataSource`합니다. 가 합니다 `productsDataSource` 컨트롤이 해당 데이터를 가져올 합니다 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드.


[![GetProductsByCategoryID(categoryID) 메서드를 선택 합니다.](master-detail-filtering-with-a-dropdownlist-cs/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image19.png)

**그림 7**: 선택 된 `GetProductsByCategoryID(categoryID)` 메서드 ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-cs/_static/image21.png))


이 메서드를 선택한 후 ObjectDataSource 마법사 묻는 메서드의 값 *`categoryID`* 매개 변수입니다. 선택한 값을 사용 하도록 `categories` DropDownList 항목으로 매개 변수 원본 컨트롤과를 ControlID `Categories`합니다.


[![CategoryID 매개 변수 범주 DropDownList의 값으로 설정](master-detail-filtering-with-a-dropdownlist-cs/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image22.png)

**그림 8**: 설정 합니다 *`categoryID`* 매개 변수 값으로는 `Categories` DropDownList ([클릭 하 여 큰 이미지 보기](master-detail-filtering-with-a-dropdownlist-cs/_static/image24.png))


시간을 내어 브라우저에서 진행 상황을 확인 합니다. 이러한 제품 선택한 범주에 속하는 페이지를 처음 방문 하는 경우 (음료) (그림 9에 표시 됨)으로 표시 되지만 DropDownList 변경 데이터를 업데이트 하지 않습니다. 업데이트를 GridView에 대 한 포스트백을 발생 해야 하는 때문입니다. 이렇게 하려면에서는 두 가지 옵션이 (둘 중 필요한 코드를 작성).

- **범주 DropDownList의 설정**[AutoPostBack 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)**True로 합니다.** (이렇게 하려면 DropDownList의 스마트 태그에 AutoPostBack을 사용 하도록 설정 옵션을 선택 합니다.) DropDownList의 선택할 때마다 포스트백을 트리거하는이 항목은 사용자가 변경 됩니다. 따라서 사용자가 드롭다운 목록에서 새 범주를 선택 하면 포스트백 계속 될 것 이라고 및 GridView 새로 선택한 범주에 대 한 제품을 사용 하 여 업데이트 됩니다. (이 자습서에서 사용한 접근 방식입니다.)
- **드롭다운 목록 옆에 있는 단추 웹 컨트롤을 추가 합니다.** 설정의 `Text` 속성 새로 고침을 또는 유사 합니다. 이 방법을 사용 하면 새 범주를 선택 하 고 다음 단추를 클릭 해야 합니다. 단추를 클릭 하면 포스트백을 발생 되며 선택한 범주의 제품을 나열 하려면 GridView를 업데이트 합니다.

그림 9와 10 중인 마스터/세부 정보 보고서를 보여 줍니다.


[![먼저 페이지를 방문 하 고, 음료 제품 표시 됩니다.](master-detail-filtering-with-a-dropdownlist-cs/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image25.png)

**그림 9**: 먼저 페이지를 방문 하 고, 음료 제품 표시 됩니다 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image27.png))


[![새 제품 (생성)을 선택 하면 자동으로 포스트백을 GridView를 업데이트 하는 중](master-detail-filtering-with-a-dropdownlist-cs/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image28.png)

**그림 10**: 새 제품 (생성)을 선택 하면 자동으로 포스트백을 GridView를 업데이트 하는 중 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image30.png))


## <a name="adding-a----choose-a-category----list-item"></a>"-범주-" 선택 목록 항목 추가

먼저 방문할 때는 `FilterByDropDownList.aspx` DropDownList의 첫 번째 목록 항목 (음료)는 선택, 기본적으로 GridView의 음료 제품을 보여 주는 범주 페이지입니다. 선택한 대신 DropDownList 항목이 하려는 경우 첫 번째 범주의 제품을 보여 주는 것이 아니라 "-범주 선택-" 같은 말입니다.

DropDownList에 새 목록 항목을 추가 하려면 속성 창으로 이동 하 고에서 줄임표를 클릭 합니다 `Items` 속성입니다. 사용 하 여 새 목록 항목을 추가 합니다 `Text` "-범주 선택-" 및 `Value` `-1`합니다.


[![추가--범주--목록 항목 선택](master-detail-filtering-with-a-dropdownlist-cs/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image31.png)

**그림 11**: 추가--범주--목록 항목 선택 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image33.png))


또는 드롭다운 목록에 다음 태그를 추가 하 여 목록 항목을 추가할 수 있습니다.

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample1.aspx)]

DropDownList 컨트롤을 설정 해야 뿐만 `AppendDataBoundItems` 범주는 ObjectDataSource의 DropDownList 바인딩할 때 덮어씁니다 수동으로 추가 된 목록 항목 경우 때문에 True로 `AppendDataBoundItems` True 되지 않습니다.


![AppendDataBoundItems 속성도 True로 설정](master-detail-filtering-with-a-dropdownlist-cs/_static/image34.png)

**그림 12**: 설정의 `AppendDataBoundItems` 속성을 true로


이러한 변경 이후 먼저 페이지를 방문할 때 "-범주 선택-" 옵션을 선택 하 고 제품이 표시 됩니다.


[![초기 페이지 로드에 제품이 표시 됩니다.](master-detail-filtering-with-a-dropdownlist-cs/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image35.png)

**그림 13**:에서 초기 페이지 로드 아니요 제품 표시 됩니다 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image37.png))


해당 값은 "-범주-" 선택 목록 항목이 선택 되어 있으므로 제품이 없습니다. 때 표시 되는 이유 이므로 `-1` 데이터베이스에 있는 제품이 및는 `CategoryID` 의 `-1`. 이 동작은 하려는 경우이 시점에서 완료 한 다음! 그러나 표시 하려는 경우 *모든* 범주의 목록 "-"선택 범주-항목을 선택 하면 반환 하는 `ProductsBLL` 클래스 및 사용자 지정 합니다 `GetProductsByCategoryID(categoryID)` 메서드를 호출는 `GetProducts()` 메서드 경우 전달 된에서 *`categoryID`* 매개 변수가 0 보다 작습니다.

[!code-csharp[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample2.cs)]

여기에 사용 되는 방법은 모든 공급 업체 표시를 사용 하는 방법과 비슷한 방법으로 다시 합니다 [선언적 매개 변수](../basic-reporting/declarative-parameters-cs.md) 자습서,이 예제에 대 한 값을 사용 하는 것 이지만 `-1` 모든 레코드를 해야 함을 나타내려면 아닌 사이트별로 검색 `null`합니다. 왜냐하면를 *`categoryID`* 의 매개 변수는 `GetProductsByCategoryID(categoryID)` 반면 선언적 매개 변수 자습서에서 문자열 입력 매개 변수에 전달 된 것에서 전달 된 정수 값으로 메서드에 필요 합니다.

그림 14의 스크린 샷을 보여 줍니다 `FilterByDropDownList.aspx` "-범주 선택-" 옵션을 선택한 경우. 여기에서 기본적으로 표시 되는 모든 제품 및 특정 범주를 선택 하면 사용자 표시를 좁힐 수 있습니다.


[![이제 나열 기본적으로 모든 제품](master-detail-filtering-with-a-dropdownlist-cs/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image38.png)

**그림 14**: 이제 나열 기본적으로 모든 제품 ([큰 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image40.png))


## <a name="summary"></a>요약

계층적으로 관련 데이터를 표시할 때 종종 사용자 계층의 최상위에서 데이터를 읽는 데 시작 하 고 세부 정보로 드릴 다운 하는 마스터/세부 정보 보고서를 사용 하 여 데이터를 제공할 수 있습니다. 이 자습서에서는 선택한 범주의 제품을 표시 하는 간단한 마스터/세부 정보 보고서 작성을 검사 합니다. 이 작업은 DropDownList 범주 목록과 선택한 범주에 속하는 제품 GridView를 사용 하 여 수행 되었습니다.

에 [다음 자습서](master-detail-filtering-with-two-dropdownlists-cs.md) 알아보겠습니다 DropDownList 인터페이스 한 단계 더 Dropdownlist 두를 사용 하 여 합니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [다음](master-detail-filtering-with-two-dropdownlists-cs.md)
