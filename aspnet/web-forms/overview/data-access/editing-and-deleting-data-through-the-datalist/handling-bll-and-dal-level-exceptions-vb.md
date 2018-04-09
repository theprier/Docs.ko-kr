---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-vb
title: 처리 BLL 및 DAL 수준의 예외 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 요령껏는 편집 가능한 DataList 업데이트 워크플로 중 발생 한 예외를 처리 하는 방법을 살펴보겠습니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/30/2006
ms.topic: article
ms.assetid: ca665073-b379-4239-9404-f597663ca65e
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-vb
msc.type: authoredcontent
ms.openlocfilehash: 0ee0eeff08b6ba490b401540de833eecd7122a17
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="handling-bll--and-dal-level-exceptions-vb"></a>(VB) BLL 및 DAL 수준의 예외 처리
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_38_VB.exe) 또는 [PDF 다운로드](handling-bll-and-dal-level-exceptions-vb/_static/datatutorial38vb1.pdf)

> 이 자습서에서는 요령껏는 편집 가능한 DataList 업데이트 워크플로 중 발생 한 예외를 처리 하는 방법을 살펴보겠습니다.


## <a name="introduction"></a>소개

에 [DataList에서 데이터 삭제 및 편집 개요](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md) 자습서에서는 간단한 편집 및 삭제 기능을 제공 하는 DataList 만든 합니다. 완벽 하 게 작동 하는 동안 편집 하는 동안 발생 한 모든 오류와 거의 편하게 사용 된 또는 처리 되지 않은 예외가 발생 한 프로세스를 삭제 합니다. 예를 들어 s 제품 이름을 생략 하거나, 제품을 편집할 때 매우 가격 값을 입력 합니다. 저렴 한!, 예외를 throw 합니다. 코드에서이 예외가 잡히지 않아, 이후 다음 웹 페이지의 s 예외 세부 정보를 표시 하는 ASP.NET 런타임에 버블링 됩니다.

설명한 것 처럼는 [처리 BLL-및 ASP.NET 페이지에서 DAL 수준 예외](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md) 자습서 깊이 비즈니스 논리 또는 데이터 액세스 계층의에서 예외가 발생 하는 경우 예외 세부 정보는 ObjectDataSource에 반환 됩니다 및 그런 다음 GridView에. 정상적으로 만들어 이러한 예외를 처리 하는 방법에 살펴보았습니다 `Updated` 또는 `RowUpdated` ObjectDataSource 또는 예외를 확인 한 다음 여 예외가 처리 되었는지 나타내는 GridView에 대 한 이벤트 처리기입니다.

그러나 우리의 DataList 자습서, 클라우드에 없는 t는 ObjectDataSource를 사용 하 여 업데이트 및 데이터를 삭제 합니다. 대신, BLL에 대해 직접 작업 합니다. BLL 또는 DAL에서 발생 한 예외를 검색 하기 위해 예외 처리 가격 ASP.NET 페이지의 관련 코드 내에서 코드를 구현 해야 합니다. 이 자습서에서는 요령껏 더는 편집 가능한 DataList의 워크플로 업데이트 하는 동안 발생 한 예외를 처리 하는 방법을 살펴보겠습니다.

> [!NOTE]
> 에 *는 개요의 편집 및 DataList의 데이터를 삭제* DataList에서 데이터 삭제 및 편집에 대 한 다양 한 기술을 설명한 자습서에서는 몇 가지 기법은 ObjectDataSource를 사용 하 여 업데이트 하기 위한 관련 및 삭제 중입니다. 이러한 기술을 사용 하는 경우 ObjectDataSource s 통해 BLL 또는 DAL에서 예외를 처리할 수 있습니다 `Updated` 또는 `Deleted` 이벤트 처리기입니다.


## <a name="step-1-creating-an-editable-datalist"></a>1 단계: 편집 가능한 DataList 만들기

업데이트 워크플로 중에 발생 하는 예외를 처리 하는 방법에 대 한 걱정 म 전에 먼저 편집 가능한 DataList 만든이 있습니다. 열기는 `ErrorHandling.aspx` 페이지에 `EditDeleteDataList` 폴더 설정 DataList 디자이너에 추가 해당 `ID` 속성을 `Products`, 라는 새 ObjectDataSource 추가 `ProductsDataSource`합니다. ObjectDataSource 사용 하도록 구성 된 `ProductsBLL` s 클래스 `GetProducts()` 선택 하기 위한 방법을 기록; INSERT, UPDATE에서 드롭 다운 목록을 설정 하 고 각 탭 (없음)을 삭제 합니다.


[![GetProducts() 메서드를 사용 하 여 제품 정보를 반환 합니다.](handling-bll-and-dal-level-exceptions-vb/_static/image2.png)](handling-bll-and-dal-level-exceptions-vb/_static/image1.png)

**그림 1**: 사용 하 여 제품 정보를 반환 된 `GetProducts()` 메서드 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-vb/_static/image3.png))


Visual Studio ObjectDataSource 마법사를 완료 한 후 자동으로 만들어집니다는 `ItemTemplate` DataList에 대 한 합니다. 이를 대체는 `ItemTemplate` 각 제품 s 이름과 가격을 표시 하 고 편집 단추를 포함 합니다. 다음으로 만듭니다는 `EditItemTemplate` 이름, 가격 및 업데이트 및 취소 단추에 대 한 TextBox 웹 제어 합니다. 마지막으로, s DataList 설정 `RepeatColumns` 속성을 2로 합니다.

이러한 변경 된 후 페이지 s 선언적 태그 다음과 비슷해야 합니다. 특정는 편집을 취소를 확인 하 고 [업데이트] 단추는 `CommandName` 속성 편집을 취소 하 고 업데이트를 각각로 설정 합니다.


[!code-aspx[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample1.aspx)]

> [!NOTE]
> DataList이이 자습서에 대 한 s 뷰 상태를 사용 해야 합니다.


브라우저를 통해 진행률을 보려면 잠시 (그림 2 참조).


[![편집 단추를 포함 하는 각 제품](handling-bll-and-dal-level-exceptions-vb/_static/image5.png)](handling-bll-and-dal-level-exceptions-vb/_static/image4.png)

**그림 2**: 편집 단추를 포함 하는 각 제품 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-vb/_static/image6.png))


현재 편집 단추만 포스트백이 대상이 t 아직 제품을 편집할 수 있도록 합니다. 편집을 사용 하려면 DataList s에 대 한 이벤트 처리기를 작성 해야 `EditCommand`, `CancelCommand`, 및 `UpdateCommand` 이벤트입니다. `EditCommand` 및 `CancelCommand` 이벤트의 DataList을 단순히 업데이트 `EditItemIndex` 속성과 rebind DataList 데이터:


[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample2.vb)]

`UpdateCommand` 이벤트 처리기가 약간 더 개입 됩니다. S 편집 된 제품에서 읽는 데 필요한 `ProductID` 에서 `DataKeys` s 제품 이름 및 가격에 텍스트 상자에서 함께 컬렉션의 `EditItemTemplate`, 한 다음 호출에서 `ProductsBLL` s 클래스 `UpdateProduct` DataList 반환 하기 전에 메서드 미리 편집 상태로 있습니다.

지금은 let s 방금 정확히 동일한 코드를 사용는 `UpdateCommand` 의 이벤트 처리기는 *DataList에서 데이터 삭제 및 편집 개요* 자습서입니다. 2 단계에서 예외를 정상적으로 처리 하는 코드를 추가 합니다.


[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample3.vb)]

잘못 된 입력 한 경우에도 서식이 잘못 지정 된 단위 가격, $5.00, 같은 잘못 된 단위 가격 값 또는 예외가 발생 합니다 제품의 이름 생략의 형태로 수 있습니다. 이후는 `UpdateCommand` 이벤트 처리기에는 모든 예외 처리 코드를이 시점에서, 최종 사용자에 게 표시 되므로 여기서 예외 ASP.NET 런타임에 버블링 됩니다 (그림 3 참조).


![오류 페이지 최종 사용자에 게 표시 되지 않은 예외가 발생 하는 경우](handling-bll-and-dal-level-exceptions-vb/_static/image7.png)

**그림 3**: 최종 사용자 오류 페이지에 게 표시 되지 않은 예외가 발생 하는 경우


## <a name="step-2-gracefully-handling-exceptions-in-the-updatecommand-event-handler"></a>UpdateCommand 이벤트 처리기에서 예외를 정상적으로 처리 하는 2 단계:

예외가 업데이트 워크플로 중에 발생할 수 있습니다는 `UpdateCommand` 이벤트 처리기, BLL, 또는 DAL 합니다. 예를 들어, 사용자가 너무의 가격을 입력 하는 경우 비용이 많이 들며는 `Decimal.Parse` 의 문에서 `UpdateCommand` 이벤트 처리기를 발생 시킵니다는 `FormatException` 예외입니다. 제품의 이름이 생략 됩니다. 사용자 또는 가격 음수 값을 가진 경우 DAL에서 예외가 발생 합니다.

예외가 발생 하면 페이지 자체 내에서 정보 메시지를 표시 하는 것이 좋습니다. 추가 레이블 웹 페이지에 컨트롤 `ID` 로 설정 된 `ExceptionDetails`합니다. S 레이블 텍스트를 할당 하 여 글꼴을 굵게 및 기울임꼴 특 대형 빨간색으로 표시 하려면 구성 해당 `CssClass` 속성을는 `Warning` 에 정의 된 CSS 클래스는 `Styles.css` 파일입니다.

오류가 발생할 때만 한 번에 표시할 레이블을 포함 하려고 합니다. 즉, 후속 포스트백에서 레이블의 경고 메시지가 사라집니다. 이 레이블을 s 하거나 선택을 취소 하 여 수행할 수 있습니다 `Text` 속성 또는 설정을 해당 `Visible` 속성을 `False` 에 `Page_Load` 이벤트 처리기 (다시에서 같이 [처리 BLL-및 ASP의 DAL 수준 예외 .NET 페이지](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md) 자습서) 레이블의 보기 상태 지원을 비활성화 합니다. S 후자 옵션을 사용 하도록 합니다.


[!code-aspx[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample4.aspx)]

예외가 발생 하는 경우는 예외에 대 한 세부 정보를 할당 합니다. 우리는 `ExceptionDetails` 레이블 컨트롤의 `Text` 속성입니다. 후속 포스트백에서 해당 뷰 상태가 해제 되어 있으므로 `Text`의 속성 프로그래밍 방식으로 변경 내용이 손실, 경고 메시지를 숨기 거 함으로써 기본 텍스트 (빈 문자열),으로 다시 전환 됩니다.

페이지에서 도움이 메시지를 표시 하도록 오류가 발생 했습니다 시기를 확인 하려면 추가 해야 한다고 한 `Try ... Catch` 블록을 `UpdateCommand` 이벤트 처리기입니다. `Try` 부분 예외를 야기할 수 있는 코드를 포함 하는 동안는 `Catch` 블록에서 예외가 발생할 때 실행 되는 코드를 포함 합니다. 체크 아웃의 [예외 처리 기본 사항](https://msdn.microsoft.com/library/2w8f0bss.aspx) 에 자세한 내용은.NET Framework 설명서 섹션의 `Try ... Catch` 블록입니다.


[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample5.vb)]

코드 내에서 모든 형식의 예외를 throw 하는 경우는 `Try` 블록의 `Catch` 블록의 코드 실행을 시작 합니다. Throw 되는 예외의 유형을 `DbException`, `NoNullAllowedException`, `ArgumentException`, 및 오류를 처음부터 인해에 정확 하 게 부분에 따라 달라 집니다. 하는 경우 데이터베이스 수준에서 s 문제가 여기는 `DbException` throw 됩니다. 잘못 된 값을 입력 하는 경우는 `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`, 또는 `ReorderLevel` 필드는 `ArgumentException` throw에서 이러한 필드 값의 유효성을 검사 하는 코드를 추가 하는 대로 `ProductsDataTable` 클래스 (참조는 [ 비즈니스 논리 계층을 만드는](../introduction/creating-a-business-logic-layer-vb.md) 자습서).

예외가 발생 함 유형의 메시지 텍스트를 기반으로 최종 사용자에 게 더 유용한 설명을 제공할 수 있습니다. 거의 동일한 폼에 사용 된 다음 코드에 다시는 [처리 BLL-및 ASP.NET 페이지에서 DAL 수준 예외](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md) 자습서에서는이 수준의 세부 정보를 제공 합니다.


[!code-vb[Main](handling-bll-and-dal-level-exceptions-vb/samples/sample6.vb)]

이 자습서를 완료 하려면 호출 하기만 하면는 `DisplayExceptionDetails` 에서 메서드는 `Catch` 블록에는 검색 되었습니다 전달 `Exception` 인스턴스 (`ex`).

와 `Try ... Catch` 위치에 블록을 사용자가 그림 4 및 5 쇼도 더 자세한 오류 메시지와 함께 표시 됩니다. DataList 예외가 발생할 때에 남아 있는 참고 편집 모드입니다. 제어 흐름으로 즉시 리디렉션됩니다 예외가 발생 한 후 때문에 이것이 `Catch` DataList 미리 편집 상태로 반환 하는 코드를 무시 블록입니다.


[![필수 필드를 생략 하는 경우 오류 메시지가 표시 됩니다.](handling-bll-and-dal-level-exceptions-vb/_static/image9.png)](handling-bll-and-dal-level-exceptions-vb/_static/image8.png)

**그림 4**: 필수 필드를 생략 하는 경우에 오류 메시지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-vb/_static/image10.png))


[![오류 메시지를 표시 되는 경우 입력 음수 가격](handling-bll-and-dal-level-exceptions-vb/_static/image12.png)](handling-bll-and-dal-level-exceptions-vb/_static/image11.png)

**그림 5**:는 오류 메시지는 표시 되는 경우 입력 음수 가격 ([전체 크기 이미지를 보려면 클릭](handling-bll-and-dal-level-exceptions-vb/_static/image13.png))


## <a name="summary"></a>요약

GridView 및 ObjectDataSource 제공 예외 되었으면 여부를 나타내기 위해 설정할 수 있는 속성 뿐만 아니라 모든 업데이트 및 삭제 워크플로 중에 발생 한 예외에 대 한 정보를 포함 하는 사후 수준의 이벤트 처리기 처리 됩니다. 하지만 이러한 기능을 사용할 수 없는 경우 DataList 작업 및 BLL을 직접 사용 합니다. 예외 처리를 구현 해야 하는 대신 합니다.

이 자습서에서는 예외 처리를 추가 하 여 워크플로 업데이트 하는 편집 가능한 DataList s를 추가 하는 방법을 살펴보았습니다는 `Try ... Catch` 블록은 `UpdateCommand` 이벤트 처리기입니다. 업데이트 워크플로 중 예외가 발생 하는 경우는 `Catch` 에서 유용한 정보를 표시 합니다. s 블록 코드가 실행 되는 `ExceptionDetails` 레이블.

이 시점에서 DataList 하면 처음에 발생 한 예외를 방지 하기 위해 작업 없이 있습니다. 음수 가격 예외가 발생 합니다, 않은 것을 알고 있는 경우에 t 아직 사전 이러한 잘못 된 입력을 입력에서 사용자를 방지 하기 위해 모든 기능을 추가 합니다. 다음이 자습서에서에서 유효성 검사 컨트롤을 추가 하 여 잘못 된 사용자 입력에 의해 발생 하는 예외를 줄이는 보겠습니다는 `EditItemTemplate`합니다.

만족도 매우 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [예외 디자인 지침](https://msdn.microsoft.com/library/ms298399.aspx)
- [오류 로깅 모듈 및 처리기 (ELMAH)](http://workspaces.gotdotnet.com/elmah) (오류 기록에 대 한 오픈 소스 라이브러리)
- [.NET Framework 2.0 용 Enterprise Library](https://www.microsoft.com/downloads/details.aspx?familyid=5A14E870-406B-4F2A-B723-97BA84AE80B5&amp;displaylang=en) (예외 관리 응용 프로그램 블록을 포함 합니다.)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 켄 Pespisa 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](performing-batch-updates-vb.md)
> [다음](adding-validation-controls-to-the-datalist-s-editing-interface-vb.md)
