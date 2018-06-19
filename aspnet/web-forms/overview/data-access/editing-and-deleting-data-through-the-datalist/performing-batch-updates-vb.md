---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb
title: 일괄 처리 업데이트 (VB)를 수행 합니다. | Microsoft Docs
author: rick-anderson
description: 완벽 하 게 편집할 만드는 방법을 설명에 해당 항목이 모두 있는 DataList 편집 모드와 해당 값에서 ' 모두 업데이트 ' 단추를 클릭 하 여 저장할 수 있습니다는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/30/2006
ms.topic: article
ms.assetid: 8dac22a7-91de-4e3b-888f-a4c438b03851
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb
msc.type: authoredcontent
ms.openlocfilehash: 4d28a431c2b09de8c46079e888aa191017de4e30
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/10/2018
ms.locfileid: "30892389"
---
<a name="performing-batch-updates-vb"></a>일괄 처리 업데이트 (VB)를 수행합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_37_VB.exe) 또는 [PDF 다운로드](performing-batch-updates-vb/_static/datatutorial37vb1.pdf)

> 완벽 하 게 편집할 만드는 방법을 설명에 해당 항목이 모두 있는 DataList 편집 모드와 페이지에는 "업데이트 모두" 단추를 클릭 하 여 해당 값을 저장할 수 있습니다.


## <a name="introduction"></a>소개

에 [이전 자습서](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md) 항목 수준 DataList를 만드는 방법을 검사 했습니다. 표준 편집 가능한 GridView DataList의 각 항목에 포함 된 같은 편집 단추를 클릭 하면 항목 편집할 수 있도록 합니다. 특정 사용 사례 시나리오가 필요한 반면이 항목 수준의 편집에서 잘 작동 가끔 업데이트 되는 데이터를 많은 레코드를 편집 하려면 사용자가 필요 합니다. 수십 개의 레코드를 편집 해야 하 고 편집을 클릭 하 고 해당 대로 변경한 각 하나에 대 한 업데이트를 클릭 하는 강제 적용 하는 사용자, 클릭 하면 양을 그녀의 생산성 방해가 될 수 있습니다. 이러한 경우에는 편이 더 나은지 제공 하는 것을 완벽 하 게 편집할 DataList 곳 *모든* 해당 항목은 편집 모드 및 페이지에서 모두 업데이트 단추를 클릭 하 여 해당 값을 편집할 수 있습니다 (그림 1 참조).


[![완벽 하 게 편집 가능한 DataList의 각 항목을 수정할 수 있습니다.](performing-batch-updates-vb/_static/image2.png)](performing-batch-updates-vb/_static/image1.png)

**그림 1**: 완벽 하 게 편집 가능한 DataList의 각 항목을 수정할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image3.png))


이 자습서에서는 사용자가 완벽 하 게 편집할 DataList를 사용 하 여 공급 업체 주소 정보를 업데이트할 수 있도록 하는 방법을 검토 합니다.

## <a name="step-1-create-the-editable-user-interface-in-the-datalist-s-itemtemplate"></a>1 단계: s DataList의 ItemTemplate에 편집 가능한 사용자 인터페이스 만들기

여기서 만드는 표준, 항목 수준 편집 가능한 DataList म 사용 두 템플릿이 이전 자습서:

- `ItemTemplate` 읽기 전용 사용자 인터페이스 (각 제품 s 이름과 가격을 표시 하기 위한 레이블 웹 컨트롤)를 포함 합니다.
- `EditItemTemplate` 편집 모드 사용자 인터페이스 (두 개의 TextBox 웹 컨트롤)를 포함 합니다.

DataList s `EditItemIndex` 속성은 어떤 나타냅니다 `DataListItem` (있는 경우)를 사용 하 여 렌더링 되는 `EditItemTemplate`합니다. 특히는 `DataListItem` 인 `ItemIndex` 값과 s DataList 일치 `EditItemIndex` 속성은 사용 하 여 렌더링는 `EditItemTemplate`합니다. 이 모델에는 완벽 하 게 편집할 DataList를 만들 때 시간만 떨어져 있는 폭포에 하나의 항목을 편집할 수 있습니다 하는 경우에 작동 합니다.

원하는 완벽 하 게 편집할 DataList에 대 한 *모든* 의 `DataListItem` 편집 가능한 인터페이스를 사용 하 여 렌더링 하도록 합니다. 편집 가능한 인터페이스를 정의 하는이 수행 하는 가장 간단한 방법은 `ItemTemplate`합니다. 공급 업체 주소 정보를 수정 하는 것에 대 한 편집 가능한 인터페이스에는 주소, 도시와 국가 값에 대 한 텍스트와 텍스트 상자와 공급 업체 이름을 포함 합니다.

열어 시작는 `BatchUpdate.aspx` 페이지 DataList 컨트롤을 추가 하 고 설정의 `ID` 속성을 `Suppliers`합니다. DataList s 스마트 태그에서 이라는 새 ObjectDataSource 컨트롤을 추가 하도록 선택할 `SuppliersDataSource`합니다.


[![SuppliersDataSource 라는 새 ObjectDataSource 만들기](performing-batch-updates-vb/_static/image5.png)](performing-batch-updates-vb/_static/image4.png)

**그림 2**: 명명 된 새 ObjectDataSource 만드는 `SuppliersDataSource` ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image6.png))


구성 ObjectDataSource를 사용 하 여 데이터를 검색 하는 `SuppliersBLL` s 클래스 `GetSuppliers()` 메서드 (그림 3 참조). 이전 자습서는 ObjectDataSource 통해 공급 업체 정보 업데이트를 대신와 마찬가지로 비즈니스 논리 계층와 직접 협업할 수 있습니다. 따라서 업데이트 탭에서 드롭 다운 목록을 (없음)을 설정 (그림 4 참조).


[![GetSuppliers() 메서드를 사용 하 여 공급 업체 정보를 검색 합니다.](performing-batch-updates-vb/_static/image8.png)](performing-batch-updates-vb/_static/image7.png)

**그림 3**: 검색 공급자 정보를 사용 하 여 `GetSuppliers()` 메서드 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image9.png))


[![(없음) 드롭 다운 목록을 업데이트 탭에서 설정](performing-batch-updates-vb/_static/image11.png)](performing-batch-updates-vb/_static/image10.png)

**그림 4**: (None) 드롭 다운 목록을 업데이트 탭에서 설정 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image12.png))


마법사를 완료 한 후 Visual Studio를 자동으로 생성 s DataList `ItemTemplate` 레이블 웹 컨트롤에 데이터 소스에서 반환 된 각 데이터 필드를 표시 합니다. 편집 인터페이스를 대신 제공 하도록이 서식 파일을 수정 해야 합니다. `ItemTemplate` DataList s 스마트 태그에서 템플릿 편집 옵션을 사용 하 여 디자이너를 통해 또는 직접 선언 구문을 통해 사용자 지정할 수 있습니다.

잠시 시간을 텍스트로 제공 업체의 이름을 표시 하지만 공급 업체의 주소, 도시, 및 국가 값에 대 한 입력란을 포함 하는 편집 인터페이스를 만들려면. 다음과 같이 변경한 후 페이지 s 선언적 구문 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](performing-batch-updates-vb/samples/sample1.aspx)]

> [!NOTE]
> 이전 자습서와 함께이 자습서에서는 DataList 사용에서 뷰 상태를가지고 있어야 합니다.


에 `ItemTemplate` I 두 가지 새 CSS 클래스를 사용 하 여 m `SupplierPropertyLabel` 및 `SupplierPropertyValue`에 추가 된는 `Styles.css` 클래스와 같은 스타일 설정을 사용 하도록 구성 된는 `ProductPropertyLabel` 및 `ProductPropertyValue` CSS 클래스입니다.


[!code-css[Main](performing-batch-updates-vb/samples/sample2.css)]

다음과 같이 변경한 후 브라우저를 통해이 페이지를 방문 합니다. 그림 5에서 볼 수 있듯이 각 DataList 항목은 텍스트로 공급 업체 이름을 표시 하 고 텍스트 상자를 사용 하 여 주소, 도시와 국가 표시 합니다.


[![DataList에 각 공급 업체는 편집 가능](performing-batch-updates-vb/_static/image14.png)](performing-batch-updates-vb/_static/image13.png)

**그림 5**: DataList에 각 공급 업체는 편집 가능 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image15.png))


## <a name="step-2-adding-an-update-all-button"></a>2 단계: 업데이트를 모두 단추 추가

그림 5에 각 공급 업체에 해당 주소, 도시, 및 텍스트 상자에 표시 되는 국가 필드에, 현재 업데이트 단추가 없는 사용할 수 있습니다. 항목당 업데이트 단추를 대신 완벽 하 게 편집할 DataLists 생깁니다 일반적으로 단일 모두 업데이트 단추 페이지는 클릭 하면 업데이트 *모든* DataList의 레코드입니다. 이 자습서에 대 한 s (단추 중 하나를 클릭 하는 동일한 효과가) 하지만 두 개의 모두 업데이트 단추-맨 아래에 여러 개 있는 페이지의 위쪽에 한 추가 사용 수 있습니다.

DataList 창과 집합 위로 단추 웹 컨트롤을 추가 하 여 시작 해당 `ID` 속성을 `UpdateAll1`합니다. 다음으로 설정 DataList, 아래에 두 번째 단추 웹 컨트롤 추가 해당 `ID` 를 `UpdateAll2`합니다. 설정의 `Text` 모두 업데이트 하는 두 개의 단추에 대 한 속성. 마지막으로, 두 단추에 대 한 이벤트 처리기를 만들 `Click` 이벤트입니다. 각 이벤트 처리기에서 업데이트 논리를 복제 하는 대신 let s 리팩터링 논리는 세 번째 메서드에 `UpdateAllSupplierAddresses`,이 세 번째 메서드를 단순히 호출할 이벤트 처리기에 필요 합니다.


[!code-vb[Main](performing-batch-updates-vb/samples/sample3.vb)]

그림 6 모두 업데이트 단추를 추가한 후에 페이지를 보여줍니다.


[![페이지에 추가 된 두 업데이트 모두 단추](performing-batch-updates-vb/_static/image17.png)](performing-batch-updates-vb/_static/image16.png)

**그림 6**: 페이지에 두 업데이트 모두 단추가 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image18.png))


## <a name="step-3-updating-all-of-the-suppliers-address-information"></a>3 단계: 모든 공급 업체 주소 정보를 업데이트합니다.

모든 DataList의 항목 편집 인터페이스를 표시 하 고 모든 업데이트 단추를 추가 하 여 계속이 일괄 처리 업데이트를 수행 하는 코드를 기록 하는 모든 있습니다. 특히, 해야 DataList의 항목 및 호출을 반복 하는 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드 각각에 대 한 합니다.

컬렉션 `DataListItem` DataList의 DataList를 통해 액세스할 수는 해당 구성을 인스턴스 [ `Items` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.items.aspx)합니다. 에 대 한 참조는 `DataListItem`, 해당을 잡고 수 `SupplierID` 에서 `DataKeys` 컬렉션 및 프로그래밍 방식으로 텍스트 웹 컨트롤 내 참조는 `ItemTemplate` 다음 코드와 같이:


[!code-vb[Main](performing-batch-updates-vb/samples/sample4.vb)]

사용자가 모두 업데이트 단추 중 하나를 클릭는 `UpdateAllSupplierAddresses` 메서드는 각 반복 `DataListItem` 에 `Suppliers` DataList 및 호출은 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드를 해당 값에서을 전달 합니다. 주소, 도시 또는 표준 국가 전달에 대 한 입력이 아닌 값의 값은 `Nothing` 를 `UpdateSupplierAddress` 는 데이터베이스의 결과입니다 (빈 문자열의 경우) 하는 대신 `NULL` 기본 s 레코드 필드에 대 한 합니다.

> [!NOTE]
> 향상 된 기능으로 일괄 처리 업데이트가 수행 된 후 몇 가지 확인 메시지가 제공 하는 페이지에 상태 Label 웹 컨트롤을 추가 하는 것이 좋습니다.


## <a name="updating-only-those-addresses-that-have-been-modified"></a>수정 된 주소에만 업데이트

이 자습서 호출에 사용 되는 일괄 처리 업데이트 알고리즘은 `UpdateSupplierAddress` 방법을 *모든* 자신의 주소 정보가 변경 되었는지 여부에 관계 없이 DataList의 공급 업체. 이러한 blind 클라우드에 없는 t 일반적으로 성능 문제를 업데이트 하는 동안 감사 된 데이터베이스 테이블에 변경 되 면 불필요 한 레코드를 발생할 수 있습니다. 예를 들어, 트리거를 사용 하 여 모든 기록 `UPDATE` s는 `Suppliers` 사용자 모든 했는지 여부에 관계 없이 시스템의 각 공급 업체에 대 한 새 감사 레코드를 만들 수는 모두 업데이트 단추를 클릭할 때마다 감사 테이블에 변경합니다.

ADO.NET DataTable 및 데이터 어댑터 클래스는 여기서만 수정, 삭제 및 새 레코드 데이터베이스 통신으로 인해 일괄 처리 업데이트를 지원 하도록 설계 되었습니다. DataTable의 각 행에는 [ `RowState` 속성](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx) 하는 행에서 수정, 삭제 하는 DataTable에 추가 되었습니다 그대로 유지 하는지 여부를 나타냅니다. 처음 DataTable 채워지면, 모든 행 변경 되지 않은 상태로 표시 됩니다. 수정 된 행을 표시 행 s 열의 모든 값을 변경 합니다.

에 `SuppliersBLL` 클래스에 단일 공급 업체 레코드에 대 한 첫 번째 읽기 하 여 지정 된 공급자의 주소 정보 업데이트는 `SuppliersDataTable` 로 설정한는 `Address`, `City`, 및 `Country` 다음 코드를 사용 하 여 열 값:


[!code-vb[Main](performing-batch-updates-vb/samples/sample5.vb)]

이 코드에서는 아무렇게나 전달 된 주소, 도시와 국가 값을 할당는 `SuppliersRow` 에 `SuppliersDataTable` 값이 변경 되었는지 여부에 관계 없이 합니다. 이러한 수정 된 `SuppliersRow` s `RowState` 속성을 수정 하는 것으로 표시 되어야 합니다. 때 데이터 액세스 계층 s `Update` 메서드를 호출 하 게 표시는 `SupplierRow` 수정 된 하 고 따라서 보냅니다는 `UPDATE` 명령을 데이터베이스에 있습니다.

그러나 가정,만에서 다를 경우 전달 된 주소, 도시, 및 국가 값을 할당 하려면이 메서드를 코드를 추가 했습니다는 `SuppliersRow` s 기존 값입니다. 주소, 도시와 국가 동일한 있는 기존 데이터와의 경우 변경 되지 것입니다 수 및 `SupplierRow` s `RowState` 왼쪽으로 표시 된 그대로 있습니다. 결과 하는 경우 DAL s `Update` 메서드가 호출 되 면 없는 데이터베이스 전화 걸 수 때문에 `SuppliersRow` 수정 되지 않았습니다.

이 변경을 적용할 맹목적으로 전달 된 주소, 도시, 및 다음 코드를 사용 하 여 국가 값을 할당 하는 문을 바꿉니다.


[!code-vb[Main](performing-batch-updates-vb/samples/sample6.vb)]

이 코드에서는 DAL s 추가 `Update` 메서드 보냅니다는 `UPDATE` 주소와 관련 된 값이 변경 된 레코드에 대 한 데이터베이스에 문의 합니다.

또는 우리 수 추적 데이터베이스 데이터 및 전달 된 주소 필드 사이 차이가 있는지 여부를 확인 하 고, none, 없는 경우 DAL s에 대 한 호출을 무시 하기만 하면 `Update` 메서드. 이 방법을 사용 하면 DB를 사용 하 여 다시 직접적인 방법, DB 직접적인 방법 되지 않으면 전달 된 경우에 적합 한 `SuppliersRow` 인스턴스입니다 `RowState` 데이터베이스 호출에 실제로 필요한 지 여부를 확인 하려면 확인할 수 있습니다.

> [!NOTE]
> 될 때마다는 `UpdateSupplierAddress` 메서드가 호출 되 면 업데이트 된 레코드에 대 한 정보를 검색할 데이터베이스에 대 한 호출 이루어집니다. 그런 다음 데이터의 변경 사항이 데이터베이스에 대 한 호출이 테이블 행을 업데이트 하기 이루어집니다. 이 워크플로 만들어 최적화할 수 있습니다는 `UpdateSupplierAddress` 허용 하는 메서드 오버 로드는 `EmployeesDataTable` 있는 인스턴스에 *모든* 로부터 변경 내용는 `BatchUpdate.aspx` 페이지. 그런 다음 레코드를 모두 가져오려면 데이터베이스에 한 번의 호출을 만들 수는 것은 `Suppliers` 테이블입니다. 두 개의 결과 집합을 열거할 수 다음 하 고 변경 레코드에만 업데이트할 수 없습니다.


## <a name="summary"></a>요약

이 자습서에서는 사용자가 신속 하 게 여러 공급자에 대 한 주소 정보를 수정 하는 완벽 하 게 편집할 DataList를 만드는 방법에 살펴보았습니다. DataList s에서에서 공급 업체의 주소, 도시, 및 국가 값에 대 한 TextBox 웹 컨트롤 편집 인터페이스를 정의 하 여을 시작 했습니다. `ItemTemplate`합니다. 다음으로, 위쪽 및 아래쪽 DataList 모두 업데이트 단추를 추가 했습니다. 사용자가 자신의 변경 작업을 수행 하 고 모두 업데이트 단추 중 하나를 클릭 한 후는 `DataListItem` s 열거를 호출 하는 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드 구성 됩니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Zack Jones 및 켄 Pespisa 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)
> [다음](handling-bll-and-dal-level-exceptions-vb.md)
