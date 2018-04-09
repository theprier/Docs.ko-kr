---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb
title: 확인란 (VB)의 GridView 열 추가 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 사용자에 게 G의 여러 행을 선택 하는 직관적인 방법을 제공 하는 GridView 컨트롤에 확인란의 열을 추가 하는 방법을 살펴봅니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 03/06/2007
ms.topic: article
ms.assetid: 39253d05-75c0-41c7-b9d4-a6c58ecf69ce
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: beb28de901805e07365f336192d20e914eeebb1e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="adding-a-gridview-column-of-checkboxes-vb"></a>확인란 (VB)의 GridView 열 추가
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_52_VB.exe) 또는 [PDF 다운로드](adding-a-gridview-column-of-checkboxes-vb/_static/datatutorial52vb1.pdf)

> 이 자습서에서는 사용자에 게는 GridView의 여러 행을 선택 하는 직관적인 방법을 제공 하는 GridView 컨트롤에 확인란의 열을 추가 하는 방법을 살펴봅니다.


## <a name="introduction"></a>소개

이전 자습서에서 특정 레코드를 선택 하는 용도 GridView에 라디오 단추의 열을 추가 하는 방법을 검사 했습니다. 라디오 단추의 열 그리드에서 항목 하나를 선택 하는 사용자가 제한 하는 경우 적절 한 사용자 인터페이스를입니다. 그러나 시간에 수 하려고 허용 사용자에 게는 임의 개수의 그리드에서 항목을 선택 합니다. 웹 기반 전자 메일 클라이언트 예를 들어 일반적으로 표시 확인란의 열이 있는 메시지 목록입니다. 사용자 임의 개수의 메시지를 선택 하 고 전자 메일을 다른 폴더로 이동 하거나 삭제 하는 것과 같은 작업을 수행할 수 있습니다.

이 자습서에서는 확인란의 열을 추가 하는 방법 및 다시 게시 될 때 어떤 확인란에 체크 인 했던 결정 하는 방법을 살펴봅니다. 특히, 밀접 하 게 웹 기반 전자 메일 클라이언트 사용자 인터페이스를 모방 하는 예제를 빌드합니다. 이 예제에 제품을 나열 하는 페이지 된 GridView 포함 됩니다는 `Products` 데이터베이스 테이블에서 각 확인란에 행 (그림 1 참조). 선택한 제품 삭제 단추를 클릭 하면 선택한 해당 제품을 삭제 합니다.


[![각 제품 행 포함 확인란](adding-a-gridview-column-of-checkboxes-vb/_static/image1.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image1.png)

**그림 1**: Checkbox를 포함 하는 각 제품 행 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-vb/_static/image2.png))


## <a name="step-1-adding-a-paged-gridview-that-lists-product-information"></a>1 단계: 추가 제품 정보를 나열 하는 페이지 된 GridView

확인란의 열을 추가 하는 방법에 대 한 걱정 म 전에 사용 s 먼저 포커스 페이징을 지원 되는 GridView에 제품을 나열 합니다. 열어 시작는 `CheckBoxField.aspx` 페이지에 `EnhancedGridView` 폴더를 끌어서는 GridView 설정 디자이너 도구 상자에서 해당 `ID` 를 `Products`합니다. 다음에 GridView를 명명 된 새 ObjectDataSource 바인딩할 선택 `ProductsDataSource`합니다. ObjectDataSource 사용 하도록 구성는 `ProductsBLL` 클래스를 호출 하는 `GetProducts()` 메서드 데이터를 반환할 수 있습니다. 있으므로이 GridView 읽기 전용, 삽입, 업데이트에서 드롭 다운 목록을 설정 하 고 각 탭 (없음)을 삭제 합니다.


[![ProductsDataSource 라는 새 ObjectDataSource 만들기](adding-a-gridview-column-of-checkboxes-vb/_static/image2.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image3.png)

**그림 2**: 명명 된 새 ObjectDataSource 만드는 `ProductsDataSource` ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-vb/_static/image4.png))


[![ObjectDataSource GetProducts() 메서드를 사용 하 여 데이터를 검색 구성](adding-a-gridview-column-of-checkboxes-vb/_static/image3.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image5.png)

**그림 3**: 구성 검색 사용 하 여 데이터를 ObjectDataSource는 `GetProducts()` 메서드 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-vb/_static/image6.png))


[![삽입, 업데이트에서 드롭 다운 목록을 설정 하 고 탭 (없음)를 삭제](adding-a-gridview-column-of-checkboxes-vb/_static/image4.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image7.png)

**그림 4**: 드롭 다운 목록에서 업데이트, 삽입 및 삭제 탭 하도록 설정 (None) ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-vb/_static/image8.png))


Visual Studio가 데이터 소스 구성 마법사를 완료 한 후 BoundColumns 및 제품 관련 데이터 필드에 대 한 CheckBoxColumn 자동으로 만들어집니다. 이전 자습서에서 수행한 것 같은, 제거 제외한 모두 `ProductName`, `CategoryName`, 및 `UnitPrice` BoundFields, 변경 하 고는 `HeaderText` 속성 제품, 범주 및 가격을 합니다. 구성의 `UnitPrice` BoundField 통화로 해당 값의 서식을 지정 되도록 합니다. 또한 스마트 태그에서 페이징 사용 확인란을 선택 하 여 페이징을 지원 하기 위해 GridView를 구성 합니다.

S 추가적으로 선택 된 제품을 삭제 하기 위한 사용자 인터페이스를 사용 합니다. 설정 하는 GridView 아래에 있는 단추 웹 컨트롤을 추가 해당 `ID` 를 `DeleteSelectedProducts` 및 해당 `Text` 속성을 선택한 제품 삭제 합니다. 제품을 데이터베이스에서 실제로 삭제 하지 않고이 예제에 대 한 합니다 방금 표시 삭제 된 제품 되었다는 메시지가 표시 됩니다. 이 위해 단추 아래에 레이블을 웹 컨트롤을 추가 합니다. ID를 설정 `DeleteResults`아웃 지우기, 해당 `Text` 속성과 집합 해당 `Visible` 및 `EnableViewState` 속성을 `False`합니다.

다음과 같이 변경한 후 GridView, ObjectDataSource, 단추 및 레이블에 s 선언 태그 해야 다음과 유사 합니다.


[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample1.aspx)]

브라우저에서 페이지를 볼 보십시오 (그림 5 참조). 이 시점에서 이름, 범주 및 처음 10 개 제품의 가격 나타납니다.


[![나열 된 이름, 범주 및 첫 번째는 10 개 제품의 가격](adding-a-gridview-column-of-checkboxes-vb/_static/image5.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image9.png)

**그림 5**: Name, 범주 및 첫 번째는 10 개 제품의 가격 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-vb/_static/image10.png))


## <a name="step-2-adding-a-column-of-checkboxes"></a>2 단계: 확인란 열 추가

ASP.NET 2.0에는 CheckBoxField, 이후는 GridView에 확인란 열 추가를 사용할 수 있도록 고 생각 합니다. 그러나 있는 아닙니다 경우 CheckBoxField 부울 데이터 필드와 작동 하도록 설계 되었습니다. 즉, CheckBoxField 사용 하려면 기본 데이터 필드 값을 갖는 렌더링된 확인란이 선택 되어 있는지 여부를 확인 하기 위해 참조은 지정 해야 합니다. CheckBoxField 방금 확인란 선택 되지 않은 열을 포함 하도록 사용할 수 없습니다.

대신, म를 TemplateField를 추가 하 고 추가 해야 CheckBox 웹 컨트롤을 해당 `ItemTemplate`합니다. 추가를 TemplateField는 `Products` GridView 첫 번째 (왼쪽 끝) 필드를 확인 합니다. GridView s 스마트 태그에서 템플릿 편집 링크를 클릭 한 다음 도구 상자에서 CheckBox 웹 컨트롤을 끌어는 `ItemTemplate`합니다. 이 확인란을 s 설정 `ID` 속성을 `ProductSelector`합니다.


[![TemplateField의 ItemTemplate에 ProductSelector 이라는 CheckBox 웹 컨트롤 추가](adding-a-gridview-column-of-checkboxes-vb/_static/image6.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image11.png)

**그림 6**: 명명 된 확인란 웹 컨트롤을 추가 `ProductSelector` TemplateField s에 `ItemTemplate` ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-vb/_static/image12.png))


추가 TemplateField 및 CheckBox 웹 컨트롤을 이제 각 행에는 확인란이 포함 됩니다. 그림 7 TemplateField 및 확인란 추가 된 후 브라우저를 통해 표시 될 경우이 페이지를 보여 줍니다.


[![각 제품 행에는 이제 Checkbox 포함](adding-a-gridview-column-of-checkboxes-vb/_static/image7.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image13.png)

**그림 7**: 각 제품 행에는 이제 Checkbox 포함 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-vb/_static/image14.png))


## <a name="step-3-determining-what-checkboxes-were-checked-on-postback"></a>3 단계: 포스트백에 체크 인 했던 어떤 확인란 결정

이 시점에서 우리는 열이 확인란을 선택 하지만 어떤 확인란 포스트백에 체크 인 했던 확인할 방법이 없습니다. 선택한 제품 삭제 단추를 클릭할 때 하지만 알아야 해당 제품을 삭제 하려면 체크 인 했던 어떤 확인란을 선택 합니다.

GridView s [ `Rows` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows.aspx) GridView의 데이터 행에 대 한 액세스를 제공 합니다. CheckBox 컨트롤을 프로그래밍 방식으로 액세스 하 고 그런 다음 참조에서는 이러한 행을 반복할 수 있는 해당 `Checked` 확인란 선택 되었는지 여부를 결정 하는 속성입니다.

에 대 한 이벤트 처리기를 만들고는 `DeleteSelectedProducts` 단추 웹 컨트롤의 `Click` 이벤트를 다음 코드를 추가:


[!code-vb[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample2.vb)]

`Rows` 속성의 컬렉션을 반환 `GridViewRow` GridView의 데이터 행은 해당 구성을 인스턴스. `For Each` 루프 여기이 컬렉션을 열거 합니다. 각 `GridViewRow` 개체를 사용 하 여 행 s 확인란 프로그래밍 방식으로 액세스할 `row.FindControl("controlID")`합니다. 확인란을 선택 하는 경우 해당 행 s `ProductID` 값에서 검색 되는 `DataKeys` 컬렉션입니다. 이 연습에서는 단순히 표시에 정보 메시지가 `DeleteResults` 에서는 응용 프로그램 d 대신 만들 것에 대 한 호출 되지만 레이블을 `ProductsBLL` s 클래스 `DeleteProduct(productID)` 메서드.

이 이벤트 처리기를 추가 하 여 이제 선택한 제품 삭제 단추를 클릭 하면 표시 됩니다는 `ProductID` 선택 된 제품의 s입니다.


[![선택한 제품 삭제 단추를 클릭 하면 선택한 제품 Productid와 같습니다.](adding-a-gridview-column-of-checkboxes-vb/_static/image8.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image15.png)

**그림 8**: 때 the 삭제 선택한 제품 단추를 클릭 하면 선택한 제품 `ProductID` 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-vb/_static/image16.png))


## <a name="step-4-adding-check-all-and-uncheck-all-buttons"></a>4 단계: 추가 모두 확인 하 고 모든 단추를 선택 취소

현재 페이지에서 모든 제품을 삭제 하려는 경우 각각 10 개 확인란 체크 해야 합니다. 이 프로세스를 신속 하 게 추가 모두 선택 하 여 드립니다 단추를 클릭 하면 눈금에서 모든 확인란의 선택 합니다. 모두 선택 취소 단추 것 동일 하 게 유용 합니다.

GridView 위에 배치 하는 페이지에 두 단추 웹 컨트롤을 추가 합니다. 첫 번째 s 설정 `ID` 를 `CheckAll` 및 해당 `Text` 속성을 모두 선택; 다른 하나는 s 집합 `ID` 를 `UncheckAll` 및 해당 `Text` 속성을 모두 선택 취소 합니다.


[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample3.aspx)]

다음으로 명명 된 코드 숨김 클래스에 메서드를 만듭니다 `ToggleCheckState(checkState)` 는 호출 되 면 열거는 `Products` GridView s `Rows` 컬렉션 하 고 각 확인란 s 설정 `Checked` 속성의 전달 된 값을에서 *checkState*  매개 변수입니다.


[!code-vb[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample4.vb)]

다음으로 만듭니다 `Click` 에 대 한 이벤트 처리기는 `CheckAll` 및 `UncheckAll` 단추입니다. `CheckAll` s 이벤트 처리기를 호출 하기만 하면 `ToggleCheckState(True)`, `UncheckAll`, 호출 `ToggleCheckState(False)`합니다.


[!code-vb[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample5.vb)]

이 코드를 통해 모든 확인 단추를 클릭 하 고 포스트백을 발생를 모든 GridView에서 확인란의 확인 합니다. 마찬가지로, 모두 선택 취소를 클릭 하면 모든 확인란 선택 취소 합니다. 그림 9 모두 확인 단추 확인 된 후에 화면을 보여 줍니다.


[![모든 단추 확인을 클릭 하 여 모든 확인란을 선택](adding-a-gridview-column-of-checkboxes-vb/_static/image9.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image17.png)

**그림 9**: 확인란을 클릭 하 고 확인 모든 단추 선택 하는 모든 ([전체 크기 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-vb/_static/image18.png))


> [!NOTE]
> 확인란을 선택 하거나 모든 확인란의 선택을 취소 하는 한 가지 방법의 열을 표시 합니다.이 경우 머리글 행의 확인란을 통해. 또한 현재 모든 확인/모두 선택 취소 구현을 다시 게시 해야 합니다. 그러나 확인란은 수 checked 또는 unchecked, snappier 사용자 환경을 제공 하는 클라이언트 쪽 스크립트를 통해 완전히 합니다. 체크 아웃을 모두 선택 하 고 모두 선택 취소에 대 한 머리글 행 확인란을 사용 하 여 클라이언트 쪽 기술을 사용 하 여에 대 한 설명 함께 자세히 탐색할 [GridView를 사용 하 여 클라이언트 쪽 스크립트 및 확인 모든 확인란의 모든 확인란 검사](http://aspnet.4guysfromrolla.com/articles/053106-1.aspx)합니다.


## <a name="summary"></a>요약

사용자가 계속 진행 하기 전에 GridView에서 임의 개수의 행을 선택할 수 있도록 해야 하는 경우에서 확인란 열 추가 한 옵션입니다. 이 자습서에서 살펴본 것 처럼 확인란 GridView에서 열을 포함 하 여 수반를 TemplateField CheckBox 웹 컨트롤을 추가 합니다. (이전 자습서에서와 같이 서식 파일에 직접 태그를 삽입)와 웹 컨트롤을 사용 하 여 ASP.NET 확인란을 선택 된 및 포스트백 전체에서 확인 되지 않은 자동으로 저장 합니다. 또한 프로그래밍 방식으로 주어진된 확인란이 선택 되었는지 여부를 결정 하거나 선택된 상태를 변경 하려면 코드에서 확인란에 액세스할 수 있습니다.

이 자습서와 마지막 GridView에 행 선택기 열 추가 살펴보았습니다. 다음이 자습서에서 어떻게, 약간의 작업을 추가할 수 있습니다 삽입 기능 GridView에 검토 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](adding-a-gridview-column-of-radio-buttons-vb.md)
> [다음](inserting-a-new-record-from-the-gridview-s-footer-vb.md)
