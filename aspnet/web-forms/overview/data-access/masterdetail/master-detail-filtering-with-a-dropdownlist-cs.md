---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
title: "마스터/세부 DropDownList (C#)를 사용 하 여 필터링 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에서는 DropDownList 컨트롤과 GridView에 선택한 목록 항목의 세부 정보에 마스터 레코드를 표시 하는 방법을 살펴보겠습니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/31/2010
ms.topic: article
ms.assetid: 53e659cc-eefb-40c1-a1dc-559481c99443
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-cs
msc.type: authoredcontent
ms.openlocfilehash: cf3058ac095bc2ed728a716e70f962e260eef5a2
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="masterdetail-filtering-with-a-dropdownlist-c"></a>마스터/세부 DropDownList (C#)를 사용 하 여 필터링
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_7_CS.exe) 또는 [PDF 다운로드](master-detail-filtering-with-a-dropdownlist-cs/_static/datatutorial07cs1.pdf)

> 이 자습서에서는 DropDownList 컨트롤과 GridView에 선택한 목록 항목의 세부 정보에 마스터 레코드를 표시 하는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

일반적인 유형의 보고서는 *마스터/세부 보고서*, 몇 가지 "마스터" 레코드 집합을 표시 하 여 시작 되는 보고서에 있습니다. 사용자는 다음으로 드릴 다운할 수 마스터 레코드 중 하나 함으로써 해당 마스터 레코드의 세부 정보를 "." 보기 마스터/세부 보고는 보고서와 같은 대 다 관계를 시각화에 적합 모든 범주를 보여 주는 다음 사용자를 특정 범주를 선택 하 고 관련된 제품을 표시할 수 있도록 합니다. 또한 마스터/세부 정보 보고서 (더 많은 열이 있는) 특히 "와이드" 테이블에서 자세한 정보를 표시 하는 데 유용 합니다. 예를 들어 "마스터" 수준의 마스터/세부 정보 보고서는 데이터베이스에 제품 이름과 단위 가격만 제품을 표시할 수 있습니다 및 특정 제품으로 드릴 다운 추가 제품 필드를 표시 합니다 (범주, 공급 업체, 단위당, 수량 및 에)입니다.

여러 가지 방법으로는 마스터/세부 정보 보고서를 구현할 수 있습니다. 이 고 다음 세 개의 자습서를 통해 다양 한 마스터/세부 보고서에서 살펴보겠습니다. 이 자습서에서는 마스터 레코드에 표시 하는 방법을 보겠습니다는 [DropDownList 컨트롤](https://msdn.microsoft.com/library/dtx91y0z.aspx) 는 GridView에 선택한 목록 항목의 세부 정보입니다. 특히,이 자습서의 마스터/세부 정보 보고서는 범주 및 제품 정보를 나열 됩니다.

## <a name="step-1-displaying-the-categories-in-a-dropdownlist"></a>1 단계: DropDownList에 범주를 표시합니다.

마스터/세부 정보 보고서는 선택한 목록 항목의 제품이 표시와 DropDownList에서 범주별 나열 됩니다는 GridView에 있는 페이지의 뒷부분 합니다. 그런 다음 미리 us, 첫 번째 작업 범주 DropDownList에 표시 되는 것입니다. 열기는 `FilterByDropDownList.aspx` 페이지에 `Filtering` 폴더 DropDownList에 페이지의 디자이너 도구 상자에서 끌어서 설정 해당 `ID` 속성을 `Categories`합니다. 다음으로 DropDownList의 스마트 태그에서 데이터 소스 선택 링크를 클릭 합니다. 데이터 소스 구성 마법사가 표시 됩니다.


[![DropDownList의 데이터 소스를 지정 합니다.](master-detail-filtering-with-a-dropdownlist-cs/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image1.png)

**그림 1**: DropDownList의 데이터 원본을 지정 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image3.png))


라는 새 ObjectDataSource를 추가 하도록 선택 `CategoriesDataSource` 를 호출 하는 `CategoriesBLL` 클래스의 `GetCategories()` 메서드.


[![CategoriesDataSource 라는 새 ObjectDataSource를 추가 합니다.](master-detail-filtering-with-a-dropdownlist-cs/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image4.png)

**그림 2**: 새 ObjectDataSource 라는 추가 `CategoriesDataSource` ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image6.png))


[![CategoriesBLL 클래스를 사용 하려면 선택 합니다.](master-detail-filtering-with-a-dropdownlist-cs/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image7.png)

**그림 3**: 사용 하도록 선택 된 `CategoriesBLL` 클래스 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image9.png))


[![ObjectDataSource GetCategories() 메서드를 사용 하도록 구성](master-detail-filtering-with-a-dropdownlist-cs/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image10.png)

**그림 4**: 구성에 사용 하 여 ObjectDataSource는 `GetCategories()` 메서드 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image12.png))


어떤 데이터 원본 필드 DropDownList에 표시 되 고 있는 지정 해야 ObjectDataSource를 구성한 후 목록 항목에 대 한 값으로 연결 해야 하나 합니다. 있어야는 `CategoryName` 디스플레이와 필드 및 `CategoryID` 각 목록 항목에 대 한 값으로.


[![DropDownList 표시 범주 필드와 사용 하 여 CategoryID는는 값으로](master-detail-filtering-with-a-dropdownlist-cs/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image13.png)

**그림 5**: DropDownList 디스플레이 `CategoryName` 필드 및 사용 `CategoryID` 값으로 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image15.png))


이 시점에서의 레코드와 채워지는 DropDownList 컨트롤이 `Categories` 테이블 (모두 약 6 초 후에 수행). 그림 6 브라우저를 통해 표시 될 때까지 진행률을 보여줍니다.


[![드롭 다운 현재 범주를 나열합니다.](master-detail-filtering-with-a-dropdownlist-cs/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image16.png)

**그림 6**: A 드롭다운 목록이 현재 범주 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image18.png))


## <a name="step-2-adding-the-products-gridview"></a>2 단계: 추가 제품 GridView

마스터/세부 정보 보고서의 마지막 단계는 선택한 범주와 관련 된 제품을 나열 하는 것입니다. 이를 위해 페이지에는 GridView를 추가 하 고 라는 새 ObjectDataSource 만들 `productsDataSource`합니다. 있어야는 `productsDataSource` 컨트롤의 데이터를 추려내는 `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드.


[![GetProductsByCategoryID(categoryID) 방법 선택](master-detail-filtering-with-a-dropdownlist-cs/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image19.png)

**그림 7**: 선택 된 `GetProductsByCategoryID(categoryID)` 메서드 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image21.png))


이 메서드를 선택한 후 ObjectDataSource 만들라는 우리는 메서드에 대 한 값에 대 한  *`categoryID`*  매개 변수입니다. 선택 된 값을 사용 하려면 `categories` DropDownList 항목 매개 변수 소스 제어 및에 ControlID를 설정 `Categories`합니다.


[![매개 변수 categoryID 범주 DropDownList의 값으로 설정](master-detail-filtering-with-a-dropdownlist-cs/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image22.png)

**그림 8**: 설정의  *`categoryID`*  의 값에 대 한 매개 변수는 `Categories` DropDownList ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image24.png))


브라우저에서 진행률을 확인해 보십시오. 해당 제품 선택한 범주에 속하는 페이지를 처음 방문 하는 경우 (음료) (그림 9에 표시)으로 표시 되지만 DropDownList 변경 데이터를 업데이트 하지는 않습니다. 즉, 업데이트 하는 GridView에 대 한 포스트백 있어야 합니다. 이를 위해 (둘 중 필요한 코드를 작성)는 두 가지 옵션이 있습니다.

- **범주 DropDownList의 설정**[AutoPostBack 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx)**True로 합니다.** (이 수행할 수 있습니다 DropDownList의 스마트 태그에서 AutoPostBack 사용 옵션을 선택 합니다.) DropDownList의 선택할 때마다 포스트백을 시도해 사용자 항목을 변경 합니다. 따라서 사용자가 드롭다운 목록에서 새 범주를 선택 하는 경우 계속 다시 게시 될 것 이라고 하 고 GridView 새로 선택한 범주에 대 한 제품으로 업데이트 됩니다. (이 자습서에서 사용한 접근 방식입니다.)
- **드롭다운 목록 옆에 있는 단추 웹 컨트롤을 추가 합니다.** 설정의 `Text` 속성 새로 고침을 또는 이와 비슷한 이름입니다. 이 방법을 사용 하면 새 범주를 선택 하 고 다음 단추를 클릭 해야 합니다. 단추를 클릭 하면 포스트백을 발생 하 고 선택한 범주의 해당 제품을 나열 하 여 GridView를 업데이트 합니다.

그림 9와 10 작업에서 마스터/세부 정보 보고서를 보여 줍니다.


[![처음 방문 하 여 페이지 음료 제품 표시 됩니다.](master-detail-filtering-with-a-dropdownlist-cs/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image25.png)

**그림 9**: 처음 방문 하 여 페이지 음료 제품 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image27.png))


[![새 제품 (생성)을 선택 하면 자동으로 포스트백을 업데이트 하는 GridView](master-detail-filtering-with-a-dropdownlist-cs/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image28.png)

**그림 10**: GridView 업데이트의 포스트백을 사용 하면 새 제품 (생성)을 선택 하면 자동으로 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image30.png))


## <a name="adding-a----choose-a-category----list-item"></a>"-범주 선택-" 목록 항목 추가

처음 방문할 때는 `FilterByDropDownList.aspx` DropDownList의 첫 번째 목록 항목 (음료) GridView에서 음료 제품을 표시 합니다. 기본적으로 선택 되어 범주 페이지입니다. 선택한 대신 DropDownList 항목을 포함 하는 것이 좋겠습니다 첫 번째 범주 제품을 표시 하지 않고 "-범주 선택-" 같은 내용이 표시 됩니다.

DropDownList를 새 목록 항목을 추가 하려면 속성 창으로 이동 하 고의 줄임표를 클릭 하 고 `Items` 속성입니다. 추가 된 새 목록 항목의 `Text` "-범주 선택-" 및 `Value` `-1`합니다.


[![추가--범주--목록 항목 선택](master-detail-filtering-with-a-dropdownlist-cs/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image31.png)

**그림 11**: 추가--범주--목록 항목 선택 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image33.png))


또는 드롭다운 목록에 다음 태그를 추가 하 여 목록 항목을 추가할 수 있습니다.

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample1.aspx)]

또한 DropDownList 제어를 설정 하려면 할 `AppendDataBoundItems` 경우 수동으로 추가 된 목록 항목 범주 들 여 ObjectDataSource에서 드롭다운 목록에 바인딩되어 덮어씁니다 때문에 True로 `AppendDataBoundItems` True 되지 않습니다.


![AppendDataBoundItems 속성이 True로 설정](master-detail-filtering-with-a-dropdownlist-cs/_static/image34.png)

**그림 12**: 설정의 `AppendDataBoundItems` 속성을 True로


이러한 변경 된 후 "-범주 선택-" 옵션을 선택 하는 경우 먼저 페이지를 방문 하 고 제품이 표시 됩니다.


[![초기 페이지 로드에 제품이 표시 됩니다.](master-detail-filtering-with-a-dropdownlist-cs/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image35.png)

**그림 13**:에서 초기 페이지 아니요 제품 로드 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image37.png))


값이 "-범주 선택-" 목록 항목을 선택 하기 때문에 제품이 때 표시 되는 이유는 `-1` 및 데이터베이스에 있는 제품은 `CategoryID` 의 `-1`합니다. 이 동작 수행 하려는 경우이 시점에서 끝난 다음! 그러나 표시 하려는 경우 *모든* 범주의 "-범주 선택-" 목록 항목을 선택 하면 반환 하는 `ProductsBLL` 클래스 및 사용자 지정의 `GetProductsByCategoryID(categoryID)` 메서드를 호출 하는 `GetProducts()` 메서드 경우 전달 된에서  *`categoryID`*  매개 변수는 0 보다 작은:

[!code-csharp[Main](master-detail-filtering-with-a-dropdownlist-cs/samples/sample2.cs)]

여기에서 사용 하는 방법의 모든 공급 업체를 표시 하는 방법은 비슷합니다 다시는 [선언적 매개 변수](../basic-reporting/declarative-parameters-cs.md) 자습서,이 예제에 대 한 값을 사용 하지만 `-1` 모든 레코드 해야 함을 나타내기 위해 과 반대 검색 `null`합니다. 때문에 이것이  *`categoryID`*  의 매개 변수는 `GetProductsByCategoryID(categoryID)` 메서드에서 예상 정수 값을 전달 된 반면 선언적 매개 변수 자습서에서 문자열 입력된 매개 변수에서 전달 된 것입니다.

그림 14의 스크린 샷을 나와 `FilterByDropDownList.aspx` "-범주 선택-" 옵션을 선택한 경우. 여기에서 기본적으로 표시 되는 모든 제품 하 고 사용자를 특정 범주를 선택 하 여 디스플레이 좁힐 수 있습니다.


[![이제 나열 기본적으로 모든 제품](master-detail-filtering-with-a-dropdownlist-cs/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-cs/_static/image38.png)

**그림 14**: 이제 나열 기본적으로 모든 제품 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-with-a-dropdownlist-cs/_static/image40.png))


## <a name="summary"></a>요약

계층적으로 관련 데이터를 표시할 때 종종 사용자 계층의 최상위에서 데이터를 읽는 데 시작 하 고 세부 정보로 드릴 다운는 마스터/세부 보고서를 사용 하 여 데이터를 제공할 수 있습니다. 이 자습서에서는 선택한 범주의 제품을 보여 주는 간단한 마스터/세부 보고서 작성을 검사 합니다. 이 범주에는 선택한 범주에 속한 제품에 대 한 GridView의 목록과 DropDownList를 사용 하 여 수행 되었습니다.

에 [다음 자습서](master-detail-filtering-with-two-dropdownlists-cs.md) 살펴보겠습니다 DropDownList 인터페이스 한 단계 더 두 dropdownlist 활용을 사용 하 여 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

>[!div class="step-by-step"]
[다음](master-detail-filtering-with-two-dropdownlists-cs.md)
