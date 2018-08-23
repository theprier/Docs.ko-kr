---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-vb
title: BLL 및 DAL 수준의 예외 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 요령껏는 편집 가능한 DataList의 업데이트 워크플로 중에 발생 하는 예외를 처리 하는 방법을 살펴보겠습니다.
ms.author: riande
ms.date: 10/30/2006
ms.assetid: ca665073-b379-4239-9404-f597663ca65e
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-vb
msc.type: authoredcontent
ms.openlocfilehash: e71ad365ecbfc1bb33117a6c93e7108a4b3866a6
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41837630"
---
<a name="handling-bll--and-dal-level-exceptions-vb"></a>BLL 및 DAL 수준의 예외 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_38_VB.exe) 또는 [PDF 다운로드](handling-bll-and-dal-level-exceptions-vb/_static/datatutorial38vb1.pdf)

> 이 자습서에서는 요령껏는 편집 가능한 DataList의 업데이트 워크플로 중에 발생 하는 예외를 처리 하는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

에 [DataList에서 데이터 삭제 및 편집 개요](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md) 자습서에서는 간단한 편집 및 삭제 기능을 제공 하는 DataList 만든 합니다. 완벽 하 게 작동 하는 동안 거의 사용자 친화적으로 편집 하는 동안 발생 한 모든 오류로 것 또는 처리 되지 않은 예외가 발생 한 프로세스를 삭제 합니다. 예를 들어 생략 s 제품 이름, 제품을 편집할 때 매우 가격 값을 입력 경제적인!, 예외를 throw 합니다. 이 예외는 코드에서 잡히지 않는, 이후 다음 웹 페이지에서 s 예외 세부 정보를 표시 하는 ASP.NET 런타임까지 전달 합니다.

설명한 것 처럼 합니다 [처리 BLL 및 DAL 수준의 예외 ASP.NET 페이지에서](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md) 자습서에서는 비즈니스 논리 또는 데이터 액세스 계층에 대 한 깊이 있는에서 예외가 발생 하는 경우 예외 세부 정보로 되돌아가며 ObjectDataSource 및 GridView 하 고. 정상적으로 만들어 이러한 예외를 처리 하는 방법에 살펴보았습니다 `Updated` 또는 `RowUpdated` ObjectDataSource에 GridView, 예외를 확인 하 고 다음 예외 처리 되었음을 나타내는 이벤트 처리기입니다.

그러나 우리의 DataList 자습서, ObjectDataSource를 사용 하 여 데이터 업데이트 및 삭제에 대 한 유효 하지 t입니다. 대신, BLL에 대해 직접 노력 합니다. BLL 또는 DAL에서 발생 한 예외를 감지 하려면 예외 처리는 ASP.NET 페이지의 코드 숨김 내의 코드를 구현 해야 합니다. 이 자습서에서는 더 요령껏 워크플로 업데이트 하는 편집 가능한 DataList s 하는 동안 발생 하는 예외를 처리 하는 방법을 살펴보겠습니다.

> [!NOTE]
> 에 *An 개요의 편집 및 DataList에서 데이터 삭제* ObjectDataSource를 사용 하 여 업데이트에 대 한 편집 및 DataList에서 데이터 삭제에 대 한 다양 한 기법을 설명한 자습서에서는 몇 가지 기술을 관련 및 삭제 중입니다. 이러한 기법을 사용 하는 경우, ObjectDataSource s 통한 BLL 또는 DAL에서 예외를 처리할 수 있습니다 `Updated` 또는 `Deleted` 이벤트 처리기입니다.


## <a name="step-1-creating-an-editable-datalist"></a>1 단계: 만들기는 편집 가능한 DataList

업데이트 워크플로 중에 발생 하는 예외를 처리 하는 방법에 대 한 걱정 했습니다 전에 편집 가능한 DataList를 먼저 만든 수 있습니다. 열기는 `ErrorHandling.aspx` 페이지에 `EditDeleteDataList` 폴더 집합 디자이너로 DataList를 추가 해당 `ID` 속성을 `Products`, 라는 새로운 ObjectDataSource는 추가 `ProductsDataSource`합니다. ObjectDataSource를 사용 하 여 구성 합니다 `ProductsBLL` s 클래스 `GetProducts()` 선택 하기 위한 메서드를 기록 하 고는 insert, UPDATE, 드롭 다운 목록을 설정 탭 (없음)을 삭제 합니다.


[![GetProducts() 메서드를 사용 하 여 제품 정보를 반환 합니다.](handling-bll-and-dal-level-exceptions-vb/_static/image2.png)](handling-bll-and-dal-level-exceptions-vb/_static/image1.png)

**그림 1**: 사용 하 여 제품 정보를 반환 합니다 `GetProducts()` 메서드 ([클릭 하 여 큰 이미지 보기](handling-bll-and-dal-level-exceptions-vb/_static/image3.png))


Visual Studio에서 자동으로 ObjectDataSource 마법사를 완료 한 후 만듭니다는 `ItemTemplate` DataList에 대 한 합니다. 사용 하 여 대체는 `ItemTemplate` 각 s 제품 이름과 가격을 표시 하 고 편집 단추를 포함 합니다. 다음으로 만듭니다는 `EditItemTemplate` 이름과 가격 업데이트 및 취소 단추에 대 한 텍스트 웹 컨트롤을 사용 합니다. 마지막으로 설정 하는 DataList의 `RepeatColumns` 속성을 2로 합니다.

이러한 변경 이후 페이지 s 선언적 태그 다음과 유사 합니다. 특정는 편집을 취소, 확인 하 고 [업데이트] 단추는 `CommandName` 속성 편집을 취소 하 고 각각 업데이트로 설정 합니다.


[!code-aspx[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample1.aspx)]

> [!NOTE]
> 이 자습서는 DataList의 뷰 상태가 활성화 되어야 합니다.


브라우저를 통해 진행 상황을 보려면 잠시 (그림 2 참조).


[![각 제품에 편집 단추가 포함 됩니다.](handling-bll-and-dal-level-exceptions-vb/_static/image5.png)](handling-bll-and-dal-level-exceptions-vb/_static/image4.png)

**그림 2**: 각 제품에 편집 단추를 포함 됩니다 ([큰 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-vb/_static/image6.png))


현재 편집 단추만 포스트백을 발생 시키는 해당 대상이 t 아직 제품 편집할 수 있도록 합니다. 편집을 사용 하려면 DataList s에 대 한 이벤트 처리기를 생성 해야 `EditCommand`하십시오 `CancelCommand`, 및 `UpdateCommand` 이벤트입니다. 합니다 `EditCommand` 하 고 `CancelCommand` 이벤트의 DataList를 간단 하 게 업데이트할 `EditItemIndex` 속성과 rebind DataList 데이터:


[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample2.vb)]

`UpdateCommand` 이벤트 처리기가 좀 더 복잡 합니다. 편집된 제품 s에서에서 읽는 데 필요한 `ProductID` 에서 `DataKeys` s 제품 이름 및 가격에 텍스트 상자에서 함께 컬렉션을 `EditItemTemplate`를 호출 합니다 `ProductsBLL` s 클래스 `UpdateProduct` DataList를 반환 하기 전에 메서드 미리 편집 상태로 합니다.

이제 let s 사용에서 동일한 코드를 `UpdateCommand` 이벤트 처리기는 *DataList에서 데이터 삭제 및 편집 개요* 자습서. 2 단계에서 예외를 매끄럽게 처리할 코드를 추가 합니다.


[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample3.vb)]

잘못 된 입력 발생 하는 경우는 부적절 하 게 서식이 지정 된 단위 가격, $5.00과 같은 잘못 된 단위 가격 값을 또는 예외가 발생 제품의 이름 생략 형식의 수 있습니다. 이후는 `UpdateCommand` 이벤트 처리기에서 예외 처리 코드를이 시점에서 다루지 않습니다, 예외는 버블링 ASP.NET 런타임 있는 최종 사용자에 게 표시 됩니다 (그림 3 참조).


![최종 사용자가 오류 페이지가 처리 되지 않은 예외가 발생 하는 경우](handling-bll-and-dal-level-exceptions-vb/_static/image7.png)

**그림 3**:의 최종 사용자가 오류 페이지가 처리 되지 않은 예외가 발생 하는 경우


## <a name="step-2-gracefully-handling-exceptions-in-the-updatecommand-event-handler"></a>2 단계: UpdateCommand 이벤트 처리기에서 예외를 정상적으로 처리

업데이트 워크플로 중에 예외가 발생할 수 있습니다는 `UpdateCommand` 이벤트 처리기, BLL은 DAL 합니다. 예를 들어, 사용자가 너무의 가격을 입력 하는 경우 비용이 많이 `Decimal.Parse` 문에서 `UpdateCommand` 이벤트 처리기를 발생 시킵니다를 `FormatException` 예외. 제품의 이름을 생략 된 경우 또는 가격에는 음수 값을 가진 경우 DAL 예외가 발생 합니다.

예외가 발생 하면 페이지 자체 내에서 정보 메시지를 표시 하려고 합니다. 레이블 웹 추가 페이지 컨트롤 `ID` 로 설정 된 `ExceptionDetails`합니다. 레이블 s 표시할 텍스트를 빨간색으로 매우 큰 할당 하 여 글꼴을 굵게 및 기울임꼴 구성 해당 `CssClass` 속성을 합니다 `Warning` 에 정의 된 CSS 클래스를 `Styles.css` 파일.

오류가 발생 하는 경우만 한 번에 표시할 레이블을 포함 하려고 합니다. 즉, 후속 포스트백에서 레이블에의 경고 메시지 사라져야 합니다. 레이블 s 아웃 하거나 선택을 취소 하 여이 작업을 수행할 수 있습니다 `Text` 속성이 나 설정을 해당 `Visible` 속성을 `False` 에 `Page_Load` 이벤트 처리기 (다시에서 수행한 것 처럼는 [처리 BLL 및 DAL 수준의 예외는 ASP에서 .NET 페이지](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md) 자습서) 또는 레이블의 보기 상태 지원을 사용 하지 않도록 설정 합니다. S를 후자의 옵션을 사용할 수 있습니다.


[!code-aspx[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample4.aspx)]

예외가 발생 하면 예외의 세부 정보를 할당 하겠습니다 합니다 `ExceptionDetails` 레이블 컨트롤의 `Text` 속성입니다. 후속 포스트백에서 해당 뷰 상태의 비활성화 되어 있으므로 `Text`의 속성 프로그래밍 방식으로 변경 내용이 손실, 복귀 하 여 경고 메시지를 숨기고 기본 텍스트 (빈 문자열), 됩니다.

페이지에서 유용한 메시지를 표시 하기 위해 오류가 발생 했습니다 시기를 확인 하려면 추가 해야는 `Try ... Catch` 블록을 `UpdateCommand` 이벤트 처리기입니다. `Try` 부분 예외를 발생 시킬 수 있는 코드를 포함 하는 동안는 `Catch` 블록에 예외가 발생 하는 경우 실행 되는 코드를 포함 합니다. 체크 아웃 합니다 [예외 처리 기본 사항](https://msdn.microsoft.com/library/2w8f0bss.aspx) 대 한 자세한 내용은.NET Framework 설명서 섹션의 `Try ... Catch` 블록입니다.


[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample5.vb)]

코드 내에서 모든 형식의 예외가 throw 됩니다는 경우는 `Try` 블록은 `Catch` 블록의 코드 실행을 시작 합니다. Throw 되는 예외의 유형을 `DbException`, `NoNullAllowedException`, `ArgumentException`, 및 오류를 처음부터 인해에 정확히 무엇을에 따라 달라 집니다. 하는 경우 데이터베이스 수준에서 s 문제가 여기는 `DbException` throw 됩니다. 잘못 된 값을 입력 하는 경우는 `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`, 또는 `ReorderLevel` 필드를 `ArgumentException` 에서 이러한 필드 값의 유효성을 검사 하는 코드를 추가 했습니다 throw 되는 `ProductsDataTable` 클래스 (참조는 [ 비즈니스 논리 레이어 만들기](../introduction/creating-a-business-logic-layer-vb.md) 자습서).

메시지 텍스트를 발견 하는 예외 유형을 기반으로 최종 사용자에 게 더 유용한 설명을 제공 수 있습니다. 거의 동일한 양식에서 사용 된 다음 코드를 다시는 [처리 BLL 및 DAL 수준의 예외 ASP.NET 페이지에서](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md) 자습서에서는이 수준의 세부 정보를 제공 합니다.


[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample6.vb)]

이 자습서를 완료 하려면 호출 하기만 하면 됩니다 합니다 `DisplayExceptionDetails` 메서드를 `Catch` 포착를 전달 하는 블록 `Exception` 인스턴스 (`ex`).

사용 하 여는 `Try ... Catch` 차단 되어에서, 사용자는 그림 4와 5 표시 자세한 오류 메시지와 함께 표시 됩니다. DataList 예외가 발생 하는 경우에 남아 있는 참고 편집 모드입니다. 제어 흐름으로 즉시 리디렉션되는 예외 발생 후 이므로이 `Catch` 블록, DataList 미리 편집 상태로 반환 하는 코드를 무시 합니다.


[![필요한 필드를 생략 하는 경우 오류 메시지가 표시 됩니다.](handling-bll-and-dal-level-exceptions-vb/_static/image9.png)](handling-bll-and-dal-level-exceptions-vb/_static/image8.png)

**그림 4**: 필수 필드를 생략 하는 경우는 오류 메시지가 표시 됩니다 ([큰 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-vb/_static/image10.png))


[![오류 메시지를 표시 하면 입력 된 음수 가격](handling-bll-and-dal-level-exceptions-vb/_static/image12.png)](handling-bll-and-dal-level-exceptions-vb/_static/image11.png)

**그림 5**:는 오류 메시지는 표시 되는 경우 입력 음수 가격 ([큰 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-vb/_static/image13.png))


## <a name="summary"></a>요약

GridView 및 ObjectDataSource 제공 예외 되었으면 여부를 나타내기 위해 설정할 수 있는 속성 뿐만 아니라 모든 업데이트 및 삭제 워크플로 중에 발생 하는 예외에 대 한 정보를 포함 하는 사후 수준 이벤트 처리기 처리 합니다. 하지만 이러한 기능을 사용할 수 없는 경우 DataList를 사용 하 여 작업 및 BLL을 직접 사용 합니다. 대신 우리는 예외 처리를 구현 하는 일을 담당 합니다.

이 자습서에서는 예외 처리를 추가 하 여 워크플로 업데이트 하는 편집 가능한 DataList s를 추가 하는 방법을 살펴보았습니다를 `Try ... Catch` 차단 된 `UpdateCommand` 이벤트 처리기입니다. 업데이트 워크플로 중에 예외가 발생 하는 경우는 `Catch` 블록의 코드 실행에서 유용한 정보를 표시 합니다 `ExceptionDetails` 레이블.

이 시점에서 DataList는 처음에 발생 한 예외를 방지 하기. 음수 가격 예외가 발생 합니다을 하지 않은 것을 알고 있는 경우에 t는 아직 이러한 잘못 된 입력을 입력에서 사용자를 사전에 방지 하기 위해 모든 기능을 추가 합니다. 유효성 검사 컨트롤에 추가 하 여 잘못 된 사용자 입력에 의해 발생 하는 예외를 완화 하는 방법 다음 자습서에서 살펴보겠습니다는 `EditItemTemplate`합니다.

즐거운 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [예외 디자인 지침](https://msdn.microsoft.com/library/ms298399.aspx)
- [오류 로깅 모듈 및 처리기 (ELMAH)](http://workspaces.gotdotnet.com/elmah) (로깅 오류에 대 한 오픈 소스 라이브러리)
- [.NET Framework 2.0 용 Enterprise Library](https://www.microsoft.com/downloads/details.aspx?familyid=5A14E870-406B-4F2A-B723-97BA84AE80B5&amp;displaylang=en) (예외 관리 응용 프로그램 블록을 포함 합니다.)

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 박 단은 Pespisa 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](performing-batch-updates-vb.md)
> [다음](adding-validation-controls-to-the-datalist-s-editing-interface-vb.md)
