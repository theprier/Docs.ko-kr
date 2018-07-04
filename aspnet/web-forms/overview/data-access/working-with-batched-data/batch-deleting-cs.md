---
uid: web-forms/overview/data-access/working-with-batched-data/batch-deleting-cs
title: 일괄 처리 삭제 (C#) | Microsoft Docs
author: rick-anderson
description: 단일 작업에서 여러 데이터베이스 레코드를 삭제 하는 방법에 알아봅니다. 사용자 인터페이스 계층에는 향상 된 GridView에서 만든 이전 tut 시 빌드...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2007
ms.topic: article
ms.assetid: ac6916d0-a5ab-4218-9760-7ba9e72d258c
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: c6d792519d4a9c30f8d28497a74bc45b00197169
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37365307"
---
<a name="batch-deleting-c"></a>일괄 삭제 (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_65_CS.zip) 또는 [PDF 다운로드](batch-deleting-cs/_static/datatutorial65cs1.pdf)

> 단일 작업에서 여러 데이터베이스 레코드를 삭제 하는 방법에 알아봅니다. 사용자 인터페이스 계층에서 이전 자습서에서 생성 하는 향상 된 GridView로 빌드합니다. 데이터 액세스 계층의 모든 삭제 성공 하거나 모든 삭제 롤백됩니다 않도록 트랜잭션 내에서 여러 개의 삭제 작업에서는 래핑합니다.


## <a name="introduction"></a>소개

합니다 [이전 자습서](batch-updating-cs.md) 완벽 하 게 편집할 GridView를 사용 하 여 인터페이스를 편집 하는 일괄 처리를 만드는 방법을 탐색 합니다. 인터페이스를 편집 하는 일괄 처리를 훨씬 적습니다 포스트백 및 키보드 / 마우스 상황에 맞는 경우 여기서 사용자는 일반적으로 여러 레코드 편집 한 번에 필요 하므로 최종 사용자가의 효율성을 개선 하는 스위치를 합니다. 이 기술은 다양 한 레코드를 삭제 하는 사용자에 대 한 일반적인 경우 페이지에 대 한 마찬가지로 유용 합니다.

친숙 한 인터페이스를 삭제 하는 가장 일반적인 일괄 처리 중 하나를 사용 하 여 이미 온라인 전자 메일 클라이언트를 사용 하는 사람:는 해당 모든 선택 항목 삭제를 사용 하 여 표의 각 행에 있는 확인란 단추 (그림 1 참조). 이 자습서는 대신 짧은 때문에 우리 ve 아직 모든 웹 기반 인터페이스와 단일 원자성 작업으로 일련의 레코드를 삭제 하는 메서드를 만드는 이전 자습서에서 어려운 작업을 수행 합니다. 에 [확인란의 GridView 열 추가](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) GridView 및 확인란의 열을 사용 하 여 만든 자습서는 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](wrapping-database-modifications-within-a-transaction-cs.md) 자습서에서 메서드를 만들었습니다 트랜잭션 삭제를 사용 하는 BLL을 `List<T>` 의 `ProductID` 값입니다. 이 자습서에서는 기반으로 하 고 예제를 삭제 하는 작업 일괄 처리를 만들려면 이전 경험을 병합 합니다.


[![각 행 포함 확인란](batch-deleting-cs/_static/image1.gif)](batch-deleting-cs/_static/image1.png)

**그림 1**: 각 행에 확인란이 포함 됩니다 ([큰 이미지를 보려면 클릭](batch-deleting-cs/_static/image2.png))


## <a name="step-1-creating-the-batch-deleting-interface"></a>1 단계: 인터페이스 삭제 일괄 처리 만들기

인터페이스를 삭제 하는 일괄 처리를 이미 만들었기 때문 합니다 [확인란의 GridView 열 추가](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) 자습서에서는 단순히 복사할 수를 `BatchDelete.aspx` 처음부터 새로 만드는 대신 합니다. 열어서 시작 합니다 `BatchDelete.aspx` 페이지를 `BatchData` 폴더 및 `CheckBoxField.aspx` 페이지에서 `EnhancedGridView` 폴더. `CheckBoxField.aspx` 페이지에서 소스 뷰로 이동 하 고 태그 간의 복사는 `<asp:Content>` 그림 2에 나와 있는 것 처럼 태그.


[![CheckBoxField.aspx의 선언적 태그를 클립보드에 복사](batch-deleting-cs/_static/image2.gif)](batch-deleting-cs/_static/image3.png)

**그림 2**:의 선언 태그 복사 `CheckBoxField.aspx` 클립보드로 ([클릭 하 여 큰 이미지 보기](batch-deleting-cs/_static/image4.png))


소스 뷰로 이동한 다음 `BatchDelete.aspx` 내에서 클립보드의 내용을 붙여를 `<asp:Content>` 태그입니다. 복사 하 고의 코드 숨김 클래스 내에서 코드를 붙여 넣을 수도 `CheckBoxField.aspx.cs` 를 코드 숨김 클래스 내에서 `BatchDelete.aspx.cs` (합니다 `DeleteSelectedProducts` s 단추 `Click` 이벤트 처리기를 `ToggleCheckState` 메서드를 및 `Click` 이벤트 처리기 에 대 한 합니다 `CheckAll` 및 `UncheckAll` 단추). 이 콘텐츠를 통해 복사한 후는 `BatchDelete.aspx`의 페이지 코드 숨김 클래스에 다음 코드를 포함 해야 합니다.


[!code-csharp[Main](batch-deleting-cs/samples/sample1.cs)]

선언적 태그 및 소스 코드를 복사한 후 잠시 테스트 `BatchDelete.aspx` 브라우저를 통해 확인 하 여 합니다. S 제품 이름, 범주 및 checkbox 함께 가격을 표시 하는 각 행을 사용 하 여 GridView에서 처음 10 개 제품을 나열 하는 GridView 표시 되어야 합니다. 다음 세 가지 단추가 있어야: 모든 확인, 모두 선택 취소 및 선택한 제품을 삭제 합니다. 모든 확인 단추를 클릭 하면 모든 확인란을 지웁니다 모두 선택 취소 하는 동안 모든 확인란을 선택 합니다. 나열 하는 메시지를 표시 선택 된 제품 삭제를 클릭 하 여 `ProductID` 선택한 제품에 대 한 값 하지만 제품을 실제로 삭제 하지 않습니다.


[![CheckBoxField.aspx에서 인터페이스 BatchDeleting.aspx로 이동 되었습니다.](batch-deleting-cs/_static/image3.gif)](batch-deleting-cs/_static/image5.png)

**그림 3**:에서 인터페이스 `CheckBoxField.aspx` 로 이동 되었습니다 `BatchDeleting.aspx` ([클릭 하 여 큰 이미지 보기](batch-deleting-cs/_static/image6.png))


## <a name="step-2-deleting-the-checked-products-using-transactions"></a>2 단계: 트랜잭션을 사용 하 여 확인 된 제품 삭제

성공적으로 복사 하는 인터페이스를 삭제 하는 일괄 처리 `BatchDeleting.aspx`계속 선택한 제품 삭제 단추를 사용 하 여 확인 된 제품 삭제 되도록 코드를 업데이트 하는 모든 합니다 `DeleteProductsWithTransaction` 에서 메서드를 `ProductsBLL` 클래스. 이 메서드를 추가 합니다 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](wrapping-database-modifications-within-a-transaction-cs.md) 자습서에서는 해당 입력으로 받아들입니다를 `List<T>` 의 `ProductID` 값 및 해당 삭제 `ProductID` 범위 내에서 트랜잭션입니다.

합니다 `DeleteSelectedProducts` s 단추 `Click` 이벤트 처리기는 다음에 현재 사용 하 여 `foreach` 각 GridView 행을 반복 하는 루프:


[!code-csharp[Main](batch-deleting-cs/samples/sample2.cs)]

각 행에 대해는 `ProductSelector` CheckBox 웹 컨트롤은 프로그래밍 방식으로 참조 합니다. 이 옵션을 선택 하는 경우 행 s `ProductID` 에서 검색 되는 `DataKeys` 컬렉션 및 `DeleteResults` 레이블의 `Text` 속성 행을 삭제 하도록 선택 했는지 나타내는 메시지를 포함 하도록 업데이트 됩니다.

위의 코드는 모든 레코드에 대 한 호출으로 실제로 삭제 되지 않습니다 합니다 `ProductsBLL` s 클래스 `Delete` 메서드 주석으로 처리 됩니다. 이 삭제 논리를 적용할 인 코드는 삭제할 제품 원자 단위 연산 내부가 아니라 합니다. 즉, 시퀀스의 첫 번째 몇 삭제 했지만, 최신 (아마도 foreign key 제약 조건 위반)로 인해 실패를 하는 경우 예외가 throw 됩니다 있지만 이미 삭제 된 제품 삭제 된 상태로 유지 됩니다.

원자성을 보장 하려면 대신 사용 해야 합니다 `ProductsBLL` s 클래스 `DeleteProductsWithTransaction` 메서드. 이 메서드는 목록이 있으므로 `ProductID` 값을 먼저 그리드에서이 목록은 컴파일 및 다음 매개 변수로 전달 해야 합니다. 인스턴스를 먼저 만듭니다는 `List<T>` 형식의 `int`합니다. 내 합니다 `foreach` 선택한 제품을 추가 해야 하는 루프 `ProductID` 값이 `List<T>`합니다. 루프 후이 `List<T>` 에 전달 해야 합니다 `ProductsBLL` s 클래스 `DeleteProductsWithTransaction` 메서드. 업데이트를 `DeleteSelectedProducts` s 단추 `Click` 이벤트 처리기를 다음 코드로 바꿉니다.


[!code-csharp[Main](batch-deleting-cs/samples/sample3.cs)]

업데이트 된 코드를 만듭니다는 `List<T>` 형식의 `int` (`productIDsToDelete`)을 사용 하 여 채웁니다는 `ProductID` 삭제 하는 값입니다. 후는 `foreach` 하나 이상의 제품을 선택한 경우 루프는 `ProductsBLL` s 클래스 `DeleteProductsWithTransaction` 메서드 호출 되 고이 목록에 전달 합니다. `DeleteResults` (새로 삭제 된 레코드를 더 이상 표시 되도록 표의 행으로) 데이터를 GridView에 차츰 및 레이블도 표시 됩니다.

그림 4에서는 삭제에 대 한 수의 행을 선택한 후 GridView를 보여 줍니다. 그림 5는 선택 된 제품 삭제 버튼을 클릭 한 후에 즉시 화면을 보여줍니다. 그림 5에서는 `ProductID` GridView 아래에 있는 레이블에서 삭제 된 레코드의 값 표시 되 고 해당 행은 GridView에서 더 이상.


[![선택 된 제품 삭제 됩니다.](batch-deleting-cs/_static/image4.gif)](batch-deleting-cs/_static/image7.png)

**그림 4**:은 선택한 제품 삭제 됩니다 ([큰 이미지를 보려면 클릭](batch-deleting-cs/_static/image8.png))


[![삭제할 제품 ProductID 값은 GridView 아래에 나열 된](batch-deleting-cs/_static/image5.gif)](batch-deleting-cs/_static/image9.png)

**그림 5**: The 삭제할 제품 `ProductID` 값은 GridView 아래에 나열 된 ([클릭 하 여 큰 이미지 보기](batch-deleting-cs/_static/image10.png))


> [!NOTE]
> 테스트할 합니다 `DeleteProductsWithTransaction` 메서드의 원자성에서 제품에 대 한 항목을 수동으로 추가 `Order Details` 테이블 및 기타) (및 해당 제품을 삭제 하려고 합니다. 연결 된 주문 인 제품을 삭제 하지만 어떻게 다른 선택 된 제품 삭제 롤백됩니다 하려고 할 때 foreign key 제약 조건 위반을 받습니다.


## <a name="summary"></a>요약

확인란의 열이 있는 GridView를 추가 하는 것 인터페이스 삭제 일괄 처리 만들기 및 단추 웹 컨트롤을 클릭할 경우 단일 원자성 작업으로 선택한 행의 모든 삭제 됩니다. 이 자습서에서 구축한 이러한 인터페이스에서 두 개의 이전 자습서에서 수행 하는 작업 하나로 결합 [확인란의 GridView 열 추가](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) 하 고 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](wrapping-database-modifications-within-a-transaction-cs.md)합니다. 첫 번째 자습서에서 확인란의 열을 사용 하 여 GridView 만든 및 BLL의 메서드를 구현 했습니다 후자에 전달 될 때를 `List<T>` 의 `ProductID` 값을 트랜잭션의 범위 내에서 모두 삭제 합니다.

다음 자습서에서 일괄 처리 삽입을 수행 하기 위한 인터페이스를 만들겠습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자는 Hilton Giesenow와 Teresa Murphy 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](batch-updating-cs.md)
> [다음](batch-inserting-cs.md)
