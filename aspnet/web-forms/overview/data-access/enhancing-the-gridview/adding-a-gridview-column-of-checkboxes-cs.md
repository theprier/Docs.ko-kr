---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs
title: (C#) 확인란의 GridView 열 추가 | Microsoft Docs
author: rick-anderson
description: 이 자습서는 G의 여러 행을 선택 하는 직관적인 방법을 사용 하 여 사용자를 제공 하는 GridView 컨트롤에 확인란의 열을 추가 하는 방법을 살펴봅니다...
ms.author: aspnetcontent
ms.date: 03/06/2007
ms.assetid: f63a9443-2db0-4f80-8246-840d3e86c2a3
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: 481ae436ef644bcc4d5a13d060ed87671cfcb4dc
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37814796"
---
<a name="adding-a-gridview-column-of-checkboxes-c"></a>(C#) 확인란의 GridView 열 추가
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_52_CS.exe) 또는 [PDF 다운로드](adding-a-gridview-column-of-checkboxes-cs/_static/datatutorial52cs1.pdf)

> 이 자습서는 GridView의 여러 행을 선택 하는 직관적인 방법을 사용 하 여 사용자를 제공 하는 GridView 컨트롤에 확인란의 열을 추가 하는 방법을 살펴봅니다.


## <a name="introduction"></a>소개

이전 자습서에서 특정 레코드를 선택 하기 위해 GridView에는 열의 라디오 단추를 추가 하는 방법을 살펴보았습니다. 열의 라디오 단추는 그리드에서 항목 하나를 선택 하는 사용자가 제한 하는 경우 적합 한 사용자 인터페이스입니다. 그러나,에서는 수도 임의 개수의 그리드에서 항목을 선택할 수 있도록 합니다. 웹 기반 전자 메일 클라이언트, 예를 들어, 일반적으로 목록을 표시 확인란의 열을 사용 하 여 메시지입니다. 사용자는 임의 개수의 메시지를 선택 하 고 전자 메일을 다른 폴더로 이동 또는 삭제와 같은 몇 가지 작업을 수행할 수 있습니다.

이 자습서에서는 확인란의 열을 추가 하는 방법 및 어떤 확인란에 포스트백 될 때 체크 인 했던 확인 하는 방법을 살펴보겠습니다. 특히 밀접 하 게 웹 기반 전자 메일 클라이언트 사용자 인터페이스를 모방 하는 예제를 빌드 해 보겠습니다. 이 예제에서 제품을 나열 하는 페이징된 GridView 포함 됩니다는 `Products` 각 확인란을 사용 하 여 데이터베이스 테이블 행 (그림 1 참조). 선택 된 제품 삭제 단추를 클릭 하면 선택한 제품을 삭제 합니다.


[![각 제품 행 포함 확인란](adding-a-gridview-column-of-checkboxes-cs/_static/image1.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image1.png)

**그림 1**: 각 제품 행 포함 확인란 ([큰 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-cs/_static/image2.png))


## <a name="step-1-adding-a-paged-gridview-that-lists-product-information"></a>1 단계: 추가 제품 정보를 나열 하는 페이징된 GridView

확인란의 열을 추가 하는 방법에 대 한 걱정 했습니다 전에 페이징을 지원 되는 GridView의 제품 목록에서 첫 번째 포커스를 s 수 있습니다. 열어서 시작 합니다 `CheckBoxField.aspx` 페이지에서 `EnhancedGridView` 폴더 및 설정 디자이너 도구 상자에서 GridView 끌어서 해당 `ID` 에 `Products`. 그런 다음 GridView 라는 새로운 ObjectDataSource는 바인딩할 선택 `ProductsDataSource`합니다. ObjectDataSource를 사용 하 여 구성 합니다 `ProductsBLL` 클래스를 호출 합니다 `GetProducts()` 데이터를 반환 하는 방법. 되므로이 GridView 읽기 전용, UPDATE, INSERT에서에서 드롭 다운 목록을 설정 하 고 탭 (없음)를 삭제 합니다.


[![ProductsDataSource 라는 새로운 ObjectDataSource는 만들기](adding-a-gridview-column-of-checkboxes-cs/_static/image2.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image3.png)

**그림 2**: 명명 된 새 ObjectDataSource 만들려면 `ProductsDataSource` ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-checkboxes-cs/_static/image4.png))


[![GetProducts() 메서드를 사용 하 여 데이터를 검색할 ObjectDataSource 구성](adding-a-gridview-column-of-checkboxes-cs/_static/image3.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image5.png)

**그림 3**: 구성 데이터 사용을 검색 하는 ObjectDataSource 합니다 `GetProducts()` 메서드 ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-checkboxes-cs/_static/image6.png))


[![UPDATE, INSERT 드롭 다운 목록을 설정 하 고 탭 삭제 (없음)](adding-a-gridview-column-of-checkboxes-cs/_static/image4.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image7.png)

**그림 4**: 드롭다운 목록에서 업데이트, 삽입 및 삭제 탭 하도록 설정 (없음) ([큰 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-cs/_static/image8.png))


Visual Studio가 데이터 소스 구성 마법사를 완료 한 후 BoundColumns 및 제품 관련 데이터 필드에 대 한 CheckBoxColumn 자동으로 만들어집니다. 이전 자습서에서 수행한 것 처럼, 제거를 제외한 모든 `ProductName`, `CategoryName`, 및 `UnitPrice` BoundFields, 변경 및는 `HeaderText` Product, Category 및 Price 속성입니다. 구성 된 `UnitPrice` BoundField 해당 값을 통화로 형식이 되도록 합니다. 스마트 태그에서 페이징 사용 확인란을 선택 하 여 페이징을 지원 하기 위해 GridView를 구성할 수도 있습니다.

S를 선택한 제품을 삭제 하기 위한 사용자 인터페이스를 추가할 수도 있습니다. 아래 설정 GridView에 단추 웹 컨트롤을 추가 해당 `ID` 하 `DeleteSelectedProducts` 고 `Text` 선택한 제품을 삭제 하는 속성입니다. 제품 데이터베이스에서 실제로 삭제 하는 대신이 예제만 표시 됩니다 메시지가 삭제 되었을 수 있는 제품입니다. 이 위해 단추 아래에 레이블을 웹 컨트롤을 추가 합니다. 해당 ID를 설정 `DeleteResults`out의 선택을 취소 해당 `Text` 속성을 설정 하 고 해당 `Visible` 하 고 `EnableViewState` 속성을 `false`입니다.

다음과 같이 변경한 후 GridView, ObjectDataSource, 단추 및 레이블을 s 선언적 태그 해야 다음과 비슷합니다.


[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample1.aspx)]

브라우저에서 페이지를 보려면 잠시 (그림 5 참조). 이 시점에서 이름, 범주 및 처음 10 개 제품의 가격이 표시 됩니다.


[![이름, 범주 및 첫 번째 10 개 제품의 가격이 나와](adding-a-gridview-column-of-checkboxes-cs/_static/image5.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image9.png)

**그림 5**: Name, Category 및 첫 번째 10 개 제품의 가격 나열 됩니다 ([큰 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-cs/_static/image10.png))


## <a name="step-2-adding-a-column-of-checkboxes"></a>2 단계: 확인란의 열 추가

ASP.NET 2.0을 CheckBoxField를 포함 하므로 GridView에 확인란의 열을 추가를 사용할 수 있도록 고 생각 합니다. 그러나는 아닙니다 경우는 CheckBoxField 부울 데이터 필드와 작동 하도록 설계 되었습니다. 즉, CheckBoxField를 사용 하려면 렌더링 된 확인란을 검사할지 여부를 결정할 값을 참고 하는 기본 데이터 필드를 지정 해야 합니다. CheckBoxField unchecked 확인란의 열을 포함 하는 것을 사용할 수 없습니다.

대신 해야 templatefield로 추가 하 고 확인란을 웹 컨트롤을 추가 해당 `ItemTemplate`합니다. 계속 해 서를 templatefield로 추가 된 `Products` GridView 첫 번째 (맨 왼쪽) 필드를 확인 합니다. GridView가 스마트 태그에서 템플릿 편집 링크를 클릭 한 다음 도구 상자에서 확인란 웹 컨트롤을 끌어는 `ItemTemplate`합니다. 이 확인란을 s 설정할 `ID` 속성을 `ProductSelector`입니다.


[![TemplateField의 ItemTemplate에 ProductSelector 이라는 CheckBox 웹 컨트롤을 추가 합니다.](adding-a-gridview-column-of-checkboxes-cs/_static/image6.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image11.png)

**그림 6**: 명명 된 확인란 웹 컨트롤을 추가 `ProductSelector` TemplateField s `ItemTemplate` ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-checkboxes-cs/_static/image12.png))


추가한 TemplateField 및 CheckBox 웹 컨트롤을 사용 하 여 이제 각 행에는 확인란이 포함 됩니다. 그림 7 TemplateField 및 CheckBox를 추가한 후 브라우저를 통해 볼 때이 페이지를 보여 줍니다.


[![각 제품 행에는 이제 Checkbox](adding-a-gridview-column-of-checkboxes-cs/_static/image7.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image13.png)

**그림 7**: 각 제품 행에는 이제 확인란이 포함 됩니다 ([큰 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-cs/_static/image14.png))


## <a name="step-3-determining-what-checkboxes-were-checked-on-postback"></a>3 단계: 포스트백에서 확인 된 어떤 확인란을 확인

이 시점에서 어떤 확인란에 포스트백 될 때 체크 인 했던 확인할 방법은 없으며 확인란의 열이 있는 합니다. 선택한 제품 삭제 단추를 클릭할 때 그러나 알아야 어떤 확인란 해당 제품을 삭제 하려면 체크 합니다.

GridView s [ `Rows` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows.aspx) GridView 데이터 행에 대 한 액세스를 제공 합니다. CheckBox 컨트롤을 프로그래밍 방식으로 액세스 하 고 그런 다음 참조에서는 이러한 행을 반복할 수 해당 `Checked` 확인란을 선택 되었는지 여부를 결정 하는 속성입니다.

이벤트 처리기를 만들 합니다 `DeleteSelectedProducts` Button 웹 컨트롤의 `Click` 이벤트 다음 코드를 추가 하 고:


[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample2.cs)]

합니다 `Rows` 속성의 컬렉션을 반환 합니다. `GridViewRow` GridView의 데이터 행은 해당 구성을 인스턴스. `foreach` 루프 여기이 컬렉션을 열거 합니다. 각 `GridViewRow` 개체를 사용 하 여 행 s 확인란 프로그래밍 방식으로 액세스할 `row.FindControl("controlID")`합니다. 확인란을 선택한 경우 해당 행 s `ProductID` 값에서 검색 되는 `DataKeys` 컬렉션입니다. 이 연습에서는 단순히 표시의 정보 메시지를는 `DeleteResults` 레이블, 응용 프로그램에서 d에서는 대신 호출을 수행 하지만 합니다 `ProductsBLL` s 클래스 `DeleteProduct(productID)` 메서드.

이 이벤트 처리기를 추가 하 여 이제 선택 된 제품 삭제 단추를 클릭 하 여 표시 된 `ProductID` 선택한 제품의 합니다.


[![선택한 제품 Productid 나와 선택한 제품 삭제 단추를 클릭할 때](adding-a-gridview-column-of-checkboxes-cs/_static/image8.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image15.png)

**그림 8**: 때 the 삭제 선택한 제품 단추를 클릭 하면 선택한 제품 `ProductID` 가 나열 됩니다 ([클릭 하 여 큰 이미지 보기](adding-a-gridview-column-of-checkboxes-cs/_static/image16.png))


## <a name="step-4-adding-check-all-and-uncheck-all-buttons"></a>4 단계: 추가 모두 선택 하 고 모든 단추를 선택 취소

사용자를 현재 페이지의 모든 제품을 삭제 하려는 경우 이러한 각 10 확인란 확인 해야 합니다. 이 프로세스를 신속 하 게 모든 확인을 추가 하 여 도움을 줄 수를 클릭 하면 단추는 표의 모든 확인란을 선택 합니다. 모두 선택 취소 단추를 동일 하 게 유용한 것입니다.

GridView 위에 배치 하는 페이지에 두 개의 단추 웹 컨트롤을 추가 합니다. 첫 번째가 설정 `ID` 를 `CheckAll` 및 해당 `Text` 속성을 모두 선택, 두 번째 s 집합 `ID` 에 `UncheckAll` 고 `Text` 속성을 모두 선택 취소 합니다.


[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample3.aspx)]

다음으로 라는 코드 숨김 클래스에서 메서드를 만듭니다 `ToggleCheckState(checkState)` 는 호출 되 면 열거를 `Products` GridView s `Rows` 컬렉션 각 확인란 s를 가져오거나 설정 `Checked` 전달된 된 값으로 속성에서 *checkState*  매개 변수입니다.


[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample4.cs)]

다음을 만듭니다 `Click` 에 대 한 이벤트 처리기는 `CheckAll` 및 `UncheckAll` 단추입니다. `CheckAll` s 이벤트 처리기를 호출 하기만 `ToggleCheckState(true)`; `UncheckAll`를 호출 `ToggleCheckState(false)`합니다.


[!code-csharp[Main](adding-a-gridview-column-of-checkboxes-cs/samples/sample5.cs)]

이 코드를 사용 하 여 모든 확인 단추를 클릭 하 고 포스트백을 발생 시키는 고 모든 확인란의 GridView 확인 합니다. 마찬가지로, 모두 선택 취소를 클릭 하면 모든 확인란을 선택 취소 합니다. 그림 9에서는 모든 확인 단추를 확인 된 후에 화면을 보여 줍니다.


[![단추 모든 확인을 클릭 하 여 모든 확인란을 선택](adding-a-gridview-column-of-checkboxes-cs/_static/image9.gif)](adding-a-gridview-column-of-checkboxes-cs/_static/image17.png)

**그림 9**: 확인 모든 단추 선택 모든 확인란을 클릭 하면 ([큰 이미지를 보려면 클릭](adding-a-gridview-column-of-checkboxes-cs/_static/image18.png))


> [!NOTE]
> 때 열의 확인란을 선택 하거나 모든 확인란의 선택을 취소 하는 한 가지 방법 표시는 머리글 행의 확인란을 통해 이루어집니다. 또한 현재 모두 선택/모두 선택 취소 구현을 다시 게시 해야 합니다. 그러나 확인란 수 checked 또는 unchecked, snappier 사용자 경험을 제공 하는 클라이언트 쪽 스크립트를 통해 완전히 합니다. 모든 확인 하 고 모두 선택 취소에 대 한 머리글 행 확인란을 사용 하 여 클라이언트 쪽 기술을 사용 하 여 논의 함께 자세히 탐색 하려면 체크 아웃 [GridView를 사용 하 여 클라이언트 쪽 스크립트에는 모든 확인란 모든 확인란 확인](http://aspnet.4guysfromrolla.com/articles/053106-1.aspx)합니다.


## <a name="summary"></a>요약

사용자가 계속 하기 전에 GridView에서 임의 개수의 행을 선택할 수 있도록 해야 하는 경우 확인란의 열 추가 하나의 옵션입니다. 이 자습서에서 살펴본 것 처럼 확인란의 GridView 열 포함 확인란 웹 컨트롤을 사용 하 여 templatefield로 추가 수반 합니다. (이전 자습서에서 수행한 것 처럼 태그 템플릿에 직접 주입) 및 웹 컨트롤을 사용 하 여 ASP.NET 확인란 된 및 다시 게시를 통해 확인 되지 않은 자동으로 기억 합니다. 또한 프로그래밍 방식으로 지정 된 확인란을 검사할지 여부를 확인 하거나 선택된 상태를 변경 하려면 코드 확인란에 액세스할 수 있습니다.

이 자습서 및 마지막 GridView 행 선택기 열 추가 살펴보았습니다. 다음 자습서를 몇 가지 작업을 사용 하 여 추가할 수 있습니다 삽입 기능 GridView에 살펴보겠습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](adding-a-gridview-column-of-radio-buttons-cs.md)
> [다음](inserting-a-new-record-from-the-gridview-s-footer-cs.md)
