---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb
title: 일괄 업데이트 (VB)를 수행 합니다. | Microsoft Docs
author: rick-anderson
description: 완벽 하 게 편집할 만드는 방법 알아보기 DataList에 있는 모든 해당 항목의 편집 모드와 ' 모두 업데이트 ' 단추를 클릭 하 여 해당 값을 저장할 수 있습니다 합니다...
ms.author: aspnetcontent
ms.date: 10/30/2006
ms.assetid: 8dac22a7-91de-4e3b-888f-a4c438b03851
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb
msc.type: authoredcontent
ms.openlocfilehash: 6d6575e5f13441c38c5d7c74c8b5136a5206ffa9
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37803897"
---
<a name="performing-batch-updates-vb"></a>일괄 처리 업데이트 수행 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_37_VB.exe) 또는 [PDF 다운로드](performing-batch-updates-vb/_static/datatutorial37vb1.pdf)

> 완벽 하 게 편집할 만드는 방법 알아보기 DataList에 있는 모든 해당 항목의 편집 모드 및 페이지의 "모두 업데이트" 단추를 클릭 하 여 해당 값을 저장할 수 있습니다.


## <a name="introduction"></a>소개

에 [이전 자습서](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md) 는 항목 수준 DataList를 만드는 방법을 살펴보았습니다. 표준 편집 가능한 GridView DataList에서 각 항목에 포함 된 같은 편집 단추를 클릭 하면 항목 편집할 수 없게 합니다. 이 항목 수준만 가끔 업데이트 되는 데이터에 적합 합니다 편집 하는 동안 많은 레코드를 편집 하려면 사용자 특정 사용 사례 시나리오에 필요 합니다. 사용자 수십 개의 레코드를 편집 해야 하 고, 편집을 클릭 하 고, 해당 변경 하 고, 각각에 대 한 업데이트를 클릭 해야 하는 경우 자신의 생산성 클릭 양을 방해가 될 수 있습니다. 이러한 상황에서는 더 나은 옵션을 제공 하는 것을 완벽 하 게 편집할 DataList 곳 *모든* 해당 항목에 편집 모드와 페이지에서 모두 업데이트 단추를 클릭 하 여 해당 값을 편집할 수 있습니다 (그림 1 참조).


[![완벽 하 게 편집 가능한 DataList의 각 항목을 수정할 수 있습니다.](performing-batch-updates-vb/_static/image2.png)](performing-batch-updates-vb/_static/image1.png)

**그림 1**: 완벽 하 게 편집 가능한 DataList에서 각 항목을 수정할 수 있습니다 ([큰 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image3.png))


이 자습서에서는 사용자가 완벽 하 게 편집할 DataList를 사용 하 여 공급 업체 주소 정보를 업데이트할 수 있게 하는 방법을 살펴보겠습니다.

## <a name="step-1-create-the-editable-user-interface-in-the-datalist-s-itemtemplate"></a>1 단계: DataList의 ItemTemplate의 편집 가능한 사용자 인터페이스 만들기

이전 자습서에서는 표준, 항목 수준 편집 가능한 DataList를 만드는 것을 사용 했던 두 템플릿:

- `ItemTemplate` 읽기 전용 사용자 인터페이스 (각 제품 s 이름과 가격을 표시 하는 것에 대 한 레이블 웹 컨트롤)를 포함 합니다.
- `EditItemTemplate` 편집 모드 사용자 인터페이스 (두 개의 텍스트 웹 컨트롤)를 포함 합니다.

DataList s `EditItemIndex` 속성은 무엇을 나타냅니다 `DataListItem` (있는 경우)를 사용 하 여 렌더링 되는 `EditItemTemplate`합니다. 특히 합니다 `DataListItem` 해당 `ItemIndex` 값과 s DataList 일치 `EditItemIndex` 속성은 사용 하 여 렌더링 됩니다는 `EditItemTemplate`. 이 모델에는 완벽 하 게 편집할 DataList를 만들 때 시간만 폭포 간격에 하나의 항목을 편집할 수 있습니다 하는 경우에 작동 합니다.

완벽 하 게 편집할 DataList에 대 한 원하는 *모든* 의 `DataListItem` 를 편집할 수 있는 인터페이스를 사용 하 여 렌더링 합니다. 이 수행 하는 가장 간단한 방법에서 편집할 수 있는 인터페이스를 정의 하는 것은 `ItemTemplate`합니다. 공급 업체 주소 정보를 수정 하는 것에 대 한 편집 가능한 인터페이스 주소, 도시 및 국가 값에 대 한 텍스트 및 텍스트 상자와 공급 업체 이름을 포함 합니다.

열어서 시작 합니다 `BatchUpdate.aspx` 페이지에서 DataList 컨트롤을 추가 하 고 설정 해당 `ID` 속성을 `Suppliers`입니다. DataList s 스마트 태그에서 이라는 새 ObjectDataSource 컨트롤을 추가 하도록 선택할 `SuppliersDataSource`합니다.


[![SuppliersDataSource 라는 새로운 ObjectDataSource는 만들기](performing-batch-updates-vb/_static/image5.png)](performing-batch-updates-vb/_static/image4.png)

**그림 2**: 명명 된 새 ObjectDataSource 만들려면 `SuppliersDataSource` ([클릭 하 여 큰 이미지 보기](performing-batch-updates-vb/_static/image6.png))


ObjectDataSource를 사용 하 여 데이터를 검색할 구성 합니다 `SuppliersBLL` s 클래스 `GetSuppliers()` 메서드 (그림 3 참조). 이전 자습서에서가 아니라 ObjectDataSource 통해 공급 업체 정보를 업데이트와 마찬가지로 비즈니스 논리 계층와 직접 협업할 수 했습니다. 따라서 업데이트 탭에서 드롭 다운 목록 (없음)을 설정 (그림 4 참조).


[![GetSuppliers() 메서드를 사용 하 여 공급 업체 정보를 검색 합니다.](performing-batch-updates-vb/_static/image8.png)](performing-batch-updates-vb/_static/image7.png)

**그림 3**: 검색 공급자 사용 하 여 정보를 `GetSuppliers()` 메서드 ([클릭 하 여 큰 이미지 보기](performing-batch-updates-vb/_static/image9.png))


[![(없음) 드롭다운 목록에서 업데이트 탭 설정](performing-batch-updates-vb/_static/image11.png)](performing-batch-updates-vb/_static/image10.png)

**그림 4**: (None) 드롭 다운 목록 업데이트 탭에서 설정 ([큰 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image12.png))


마법사를 완료 한 후 Visual Studio를 자동으로 생성 DataList의 `ItemTemplate` Label 웹 컨트롤의 데이터 소스에서 반환 된 각 데이터 필드를 표시 합니다. 이 템플릿을 편집 인터페이스 대신 제공 하도록 수정 해야 합니다. `ItemTemplate` DataList s 스마트 태그에서 템플릿 편집 옵션을 사용 하 여 디자이너를 통해 또는 선언적 구문을 통해 직접 사용자 지정할 수 있습니다.

시간을 내어 공급자의 이름을 텍스트로 표시 되지만 공급자의의 주소, 도시 및 국가 값에 대 한 텍스트를 포함 하는 편집 인터페이스를 만듭니다. 다음과 같이 변경한 후 페이지 s 선언적 구문을 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](performing-batch-updates-vb/samples/sample1.aspx)]

> [!NOTE]
> 이전 자습서에서는이 자습서에서는 DataList 보기 상태로 사용할 수 있어야 합니다.


`ItemTemplate` 있나요 두 개의 새 CSS 클래스를 사용 하 여 m `SupplierPropertyLabel` 및 `SupplierPropertyValue`를 추가할를 `Styles.css` 클래스와 동일한 스타일 설정을 사용 하도록 구성 합니다 `ProductPropertyLabel` 및 `ProductPropertyValue` CSS 클래스.


[!code-css[Main](performing-batch-updates-vb/samples/sample2.css)]

다음과 같이 변경한 후 브라우저를 통해이 페이지를 방문 합니다. 그림 5에서 볼 수 있듯이 각 DataList 항목 공급자 이름을 텍스트로 표시 하 고 주소, 도시 및 국가 표시 하려면 텍스트 상자를 사용 합니다.


[![DataList에서 각 공급자는 편집 가능](performing-batch-updates-vb/_static/image14.png)](performing-batch-updates-vb/_static/image13.png)

**그림 5**: DataList에서 각 공급자는 편집 가능 ([큰 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image15.png))


## <a name="step-2-adding-an-update-all-button"></a>2 단계: 업데이트를 모든 단추 추가

그림 5에 각 공급 업체에 해당 주소, 도시 및 국가 필드 텍스트 상자에 표시 하는 동안 현재 업데이트 단추가 없는 사용할 수 있습니다. 항목당 업데이트 단추 대신 완벽 하 게 편집할 DataLists를 사용 하 여 일반적으로 단일 모두 업데이트 단추에 없는 페이지를 클릭 하면 업데이트 *모든* DataList의 레코드입니다. 이 자습서에 대 한 s를 (단추 중 하나를 클릭 하면 동일한 효과 갖습니다) 하지만 두 개의 단추-맨 아래에 여러 개 있는 페이지의 맨 위에 있는 한 모든 업데이트를 추가할 수 있습니다.

DataList 및 집합 위에 단추 웹 컨트롤을 추가 하 여 시작 해당 `ID` 속성을 `UpdateAll1`입니다. 다음으로, DataList, 아래에 두 번째 단추 웹 컨트롤을 추가 설정 해당 `ID` 에 `UpdateAll2`입니다. 설정 된 `Text` 모두 업데이트 하려면 두 개의 단추에 대 한 속성입니다. 마지막으로, 두 단추에 대 한 이벤트 처리기를 만들 `Click` 이벤트입니다. 각 이벤트 처리기에서 업데이트 논리를 복제 하는 대신 let s 세 번째 메서드에 논리를 리팩터링할 `UpdateAllSupplierAddresses`, 단순히이 세 번째 메서드를 호출 하는 이벤트 처리기를 필요 합니다.


[!code-vb[Main](performing-batch-updates-vb/samples/sample3.vb)]

그림 6에서는 모두 업데이트 단추를 추가한 후 페이지를 보여 줍니다.


[![두 업데이트 모두 단추가 페이지에 추가 되었습니다.](performing-batch-updates-vb/_static/image17.png)](performing-batch-updates-vb/_static/image16.png)

**그림 6**: 두 업데이트 모두 단추가 페이지에 추가 되었습니다 ([큰 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image18.png))


## <a name="step-3-updating-all-of-the-suppliers-address-information"></a>3 단계: 모든 공급 업체 주소 정보를 업데이트합니다.

모든 편집 인터페이스를 표시 하는 항목에 DataList s 및 모든 업데이트 단추를 추가 하 여 모든 유지는 코드를 작성 하려면 일괄 처리 업데이트를 수행 합니다. 특히, s DataList 항목 및 호출을 반복 해야 합니다 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드 각각에 대 한 합니다.

컬렉션인 `DataListItem` DataList의 DataList를 통해 액세스할 수는 구성 인스턴스 [ `Items` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.items.aspx)합니다. 에 대 한 참조를 사용 하 여는 `DataListItem`, 해당 것이 나옵니다 `SupplierID` 에서 합니다 `DataKeys` 컬렉션 및 프로그래밍 방식으로 텍스트 웹 컨트롤 내 참조는 `ItemTemplate` 다음 코드에서 볼 수 있듯이:


[!code-vb[Main](performing-batch-updates-vb/samples/sample4.vb)]

모두 업데이트 단추 중 하나를 클릭할 때를 `UpdateAllSupplierAddresses` 메서드는 각 반복 `DataListItem` 에 `Suppliers` DataList 및 호출 합니다 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 해당 값을 전달 하는 메서드. 주소, 도시 또는 국가 전달 되지 않은 입력 값의 값인 `Nothing` 하 `UpdateSupplierAddress` 데이터베이스의 결과입니다 (빈 문자열의 경우) 하는 대신 `NULL` 기본 s 레코드 필드에 대 한 합니다.

> [!NOTE]
> 향상 된 기능으로 일괄 처리 업데이트 수행 된 후 몇 가지 확인 메시지를 제공 하는 페이지에 상태 레이블 웹 컨트롤을 추가 하는 것이 좋습니다.


## <a name="updating-only-those-addresses-that-have-been-modified"></a>수정 된 주소에만 업데이트

이 자습서 호출에 사용 된 일괄 처리 업데이트 알고리즘 합니다 `UpdateSupplierAddress` 에 대 한 메서드 *모든* 공급자가 해당 주소 정보가 변경 되었는지 여부에 관계 없이 DataList, 합니다. 이러한 과제를 안겨 유효 하지 t 일반적으로 성능 문제를 업데이트 하는 동안 데이터베이스 테이블에 변경 내용을 다시 감사 하는 경우 불필요 한 레코드를 발생할 수 있습니다 이러한 합니다. 예를 들어 트리거를 사용 하 여 모든 기록 `UPDATE` s를 `Suppliers` 사용자 하나 수행 여부에 관계 없이 시스템에서 각 공급자에 대 한 새 감사 레코드를 만들 수는 모두 업데이트 단추를 클릭할 때마다 감사 테이블에 테이블 변경 내용입니다.

ADO.NET DataTable 및 DataAdapter 클래스를 데이터베이스 통신만 수정, 삭제 및 새 레코드를 결과 일괄 처리 업데이트를 지원 하도록 설계 되었습니다. DataTable의 각 행에는 [ `RowState` 속성](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx) 는 행에서 수정, 삭제 하는 DataTable에 추가 되었습니다 그대로 유지 하는지 여부를 나타냅니다. DataTable을 채울 처음 때 모든 행 변경 되지 않은 상태로 표시 됩니다. 수정 된 행을 표시 행 s 열의 모든 값을 변경 합니다.

에 `SuppliersBLL` 에 단일 공급 업체 레코드의 첫 번째 읽어 지정 된 공급자가의 주소 정보를 업데이트 하는 클래스를 `SuppliersDataTable` 설정한 후 합니다 `Address`를 `City`, 및 `Country` 다음 코드를 사용 하 여 열 값:


[!code-vb[Main](performing-batch-updates-vb/samples/sample5.vb)]

이 코드에서는 잡이 전달 된 주소, 도시 및 국가 값을 할당 합니다 `SuppliersRow` 에 `SuppliersDataTable` 값이 변경 되었는지 여부에 관계 없이 합니다. 이러한 수정으로 인해 합니다 `SuppliersRow` s `RowState` 속성을 수정 하는 것으로 표시 되어야 합니다. 때 데이터 액세스 계층 s `Update` 메서드를 호출 하는 발견 된 `SupplierRow` 수정 되었고 그 따라서 보냅니다는 `UPDATE` 명령을 데이터베이스에 합니다.

그러나 Imagine, 할당할만 전달 된 주소, 도시 및 국가 값에서 다를 경우이 메서드에 코드를 추가 했습니다는 `SuppliersRow` s 기존 값입니다. 주소, 도시 및 국가 있는 기존 데이터와 동일한 경우에는 변경 되지 하며 `SupplierRow` s `RowState` 왼쪽으로 표시 된 그대로입니다. 결과 경우 DAL s `Update` 메서드를 호출 하기 때문에 없는 데이터베이스 전화를 걸 수는 `SuppliersRow` 수정 되지 않았습니다.

이 변경은 적용 하려면 맹목적으로 전달 된 주소, 도시 및 다음 코드를 사용 하 여 국가 값을 할당 하는 문을 바꿉니다.


[!code-vb[Main](performing-batch-updates-vb/samples/sample6.vb)]

이 추가 코드를 DAL s `Update` 메서드 보냅니다는 `UPDATE` 주소와 관련 된 값이 변경 된 레코드만 데이터베이스에는 문입니다.

또는 데이터베이스 데이터와 전달 된 주소 필드 간에 차이점이 여부를 추적 하 고 수 있었습니다, 없는 경우 DAL s에 대 한 호출을 무시 하기만 `Update` 메서드. 이 방법은 DB를 사용 하 여 다시 있습니다 직접 메서드, DB 직접 메서드 되지 않으면 전달 된 경우는 `SuppliersRow` 인스턴스입니다 `RowState` 데이터베이스 호출에 실제로 필요한 지 여부를 확인 하려면 확인할 수 있습니다.

> [!NOTE]
> 각 시간을 `UpdateSupplierAddress` 메서드가 호출 되 면 업데이트 된 레코드에 대 한 정보를 검색할 데이터베이스에 호출 됩니다. 그런 다음 데이터에서 변경한 경우 다른 데이터베이스로 호출 테이블 행을 업데이트 합니다. 이 워크플로 만들어 최적화할 수 있습니다는 `UpdateSupplierAddress` 허용 하는 메서드 오버 로드는 `EmployeesDataTable` 인스턴스가 있다고 *모든* 의 변경 사항는 `BatchUpdate.aspx` 페이지. 그런 다음 모든 레코드를 가져오려면 데이터베이스를 한 번 호출 선택하실는 `Suppliers` 테이블입니다. 두 개의 결과 집합을 열거할 수 다음 하 고 변경 사항이 발생 하는 레코드만 업데이트할 수 없습니다.


## <a name="summary"></a>요약

이 자습서에서는 여러 공급 업체에 대 한 주소 정보를 신속 하 게 수정 하려면 사용자가 완벽 하 게 편집할 DataList를 만드는 방법에 살펴보았습니다. DataList s에서에서 공급자의의 주소, 도시 및 국가 값에 대 한 텍스트 웹 컨트롤의 편집 인터페이스를 정의 하 여 시작 `ItemTemplate`합니다. 다음으로, 위쪽 및 아래쪽 DataList 모두 업데이트 단추를 추가 했습니다. 사용자가 자신의 변경 하 고 업데이트 모든 단추 중 하나를 클릭 한 후는 `DataListItem` s 열거를 호출 하는 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Zack Jones와 박 단은 Pespisa 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)
> [다음](handling-bll-and-dal-level-exceptions-vb.md)
