---
uid: web-forms/overview/data-access/working-with-batched-data/batch-deleting-cs
title: "일괄 처리 삭제 (C#) | Microsoft Docs"
author: rick-anderson
description: "한 번에 여러 데이터베이스 레코드를 삭제 하는 방법을 알아봅니다. 사용자 인터페이스 계층에는 향상 된 GridView에서 만든 이전 tut 시 빌드..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2007
ms.topic: article
ms.assetid: ac6916d0-a5ab-4218-9760-7ba9e72d258c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: 71c4b323c2604d9e775f75272bb9565505580522
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="batch-deleting-c"></a>일괄 처리 삭제 (C#)
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_65_CS.zip) 또는 [PDF 다운로드](batch-deleting-cs/_static/datatutorial65cs1.pdf)

> 한 번에 여러 데이터베이스 레코드를 삭제 하는 방법을 알아봅니다. 사용자 인터페이스 계층에서 이전 자습서에서 만든는 향상 된 GridView에 빌드합니다. 데이터 액세스 계층으로 모든 삭제 성공 하거나 모든 삭제 롤백되는 트랜잭션 내에서 여러 삭제 작업을 래핑할 합니다.


## <a name="introduction"></a>소개

[이전 자습서](batch-updating-cs.md) 편집 인터페이스는 완벽 하 게 편집할 GridView를 사용 하 여 일괄 처리를 만드는 방법을 설명 합니다. 여기서 사용자가 일반적으로 편집 하는 여러 레코드가 한 번에 경우에 편집 인터페이스는 일괄 처리 및가 필요 훨씬 적은 포스트백 키보드와 마우스-컨텍스트 스위치, 최종 사용자의 효율성을 향상 합니다. 이 기술은 한꺼번에 많은 레코드를 삭제 하는 사용자에 대 한 일반적인 경우 페이지에 대 한 마찬가지로 유용 합니다.

가 온라인 메일 클라이언트를 사용 하는 사람은 이미 익숙한가 인터페이스를 삭제 하는 가장 일반적인 일괄 처리 중 하나:는 해당 모든 선택 항목 삭제 된 눈금의 각 행에 확인란 단추 (그림 1 참조). 이 자습서는 보다 짧은 때문에에서는 모든 웹 기반 인터페이스와 단일 원자 단위 연산으로 일련의 레코드를 삭제 하는 메서드를 만드는 이전 자습서에서 복잡 한 작업을 이미 수행 했습니다. 에 [확인란 GridView 열 추가](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) 확인란의 및에서 열이 있는 GridView 만든 자습서는 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](wrapping-database-modifications-within-a-transaction-cs.md) 자습서에서 메서드를 만들었습니다 트랜잭션을 삭제를 사용 하 여 BLL는 `List<T>` 의 `ProductID` 값입니다. 이 자습서를 기반으로 작성 하 고 예제 삭제 작업 일괄 처리를 만들려는 이전 경험을 병합 합니다.


[![각 행에 Checkbox 포함 됩니다.](batch-deleting-cs/_static/image1.gif)](batch-deleting-cs/_static/image1.png)

**그림 1**: 각 행에 확인란이 포함 됩니다 ([전체 크기 이미지를 보려면 클릭](batch-deleting-cs/_static/image2.png))


## <a name="step-1-creating-the-batch-deleting-interface"></a>1 단계: 인터페이스 삭제 일괄 처리 만들기

인터페이스에 삭제 일괄 처리를 이미 만들었습니다 있으므로 [확인란 GridView 열 추가](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) 자습서에서는 복사 하기만 하면 되 게 `BatchDelete.aspx` 처음부터 새로 만드는 대신 합니다. 열어 시작는 `BatchDelete.aspx` 페이지에 `BatchData` 폴더 및 `CheckBoxField.aspx` 페이지에 `EnhancedGridView` 폴더입니다. `CheckBoxField.aspx` 페이지 소스 보기로 이동 하 고 태그 사이의 복사는 `<asp:Content>` 그림 2에 나와 있는 것 처럼 태그를 삽입 합니다.


[![CheckBoxField.aspx의 선언적 태그를 클립보드에 복사 합니다.](batch-deleting-cs/_static/image2.gif)](batch-deleting-cs/_static/image3.png)

**그림 2**:의 선언 태그 복사 `CheckBoxField.aspx` 클립보드로 ([전체 크기 이미지를 보려면 클릭](batch-deleting-cs/_static/image4.png))


다음에 보기로 이동 하 여 원본에서 `BatchDelete.aspx` 내에서 클립보드의 내용을 붙여넣습니다는 `<asp:Content>` 태그입니다. 복사 하에서 코드 숨김 클래스 내에서 코드 `CheckBoxField.aspx.cs` 를 코드 숨김 클래스 내에서 `BatchDelete.aspx.cs` (의 `DeleteSelectedProducts` 단추 s `Click` 이벤트 처리기는 `ToggleCheckState` 메서드, 및 `Click` 이벤트 처리기 에 대 한는 `CheckAll` 및 `UncheckAll` 단추). 이 콘텐츠를 통해 복사한 후의 `BatchDelete.aspx`의 페이지 코드 숨김 클래스는 다음 코드를 포함 해야 합니다.


[!code-csharp[Main](batch-deleting-cs/samples/sample1.cs)]

선언적 태그 및 소스 코드를 복사한 후 보십시오 테스트 `BatchDelete.aspx` 브라우저를 통해 보고 합니다. 각 행은 s 제품 이름, 범주 및 가격 checkbox 함께 나열 하는 GridView에 처음 10 개 제품을 나열 하는 GridView 표시 되어야 합니다. 세 개의 단추가 있어야: 모든 확인, 모두 선택 취소 및 선택한 제품 삭제 합니다. 모든 확인 단추를 클릭 하면 모든 확인란을 지웁니다 모두 선택 취소 하는 동안 모든 확인란을 선택 합니다. 선택 된 제품 삭제를 클릭 하면 나열 하는 메시지가 표시 됩니다.는 `ProductID` 값 선택 된 제품의 제품을 실제로 삭제 하지 않습니다.


[![인터페이스를 CheckBoxField.aspx BatchDeleting.aspx로 이동 되었습니다.](batch-deleting-cs/_static/image3.gif)](batch-deleting-cs/_static/image5.png)

**그림 3**:에서 인터페이스 `CheckBoxField.aspx` 로 이동 되었습니다 `BatchDeleting.aspx` ([전체 크기 이미지를 보려면 클릭](batch-deleting-cs/_static/image6.png))


## <a name="step-2-deleting-the-checked-products-using-transactions"></a>2 단계: 트랜잭션을 사용 하 여 선택 된 제품 삭제

인터페이스를 통해 성공적으로 복사 삭제 일괄 처리와 `BatchDeleting.aspx`, 선택한 제품 삭제 단추를 사용 하 여 선택 된 제품을 삭제 하는 코드를 업데이트 하려면 남았습니다는 모두는 `DeleteProductsWithTransaction` 에서 메서드는 `ProductsBLL` 클래스입니다. 에 추가 된이 메서드는 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](wrapping-database-modifications-within-a-transaction-cs.md) 자습서에서는 입력으로 수락는 `List<T>` 의 `ProductID` 값 및 각 해당 삭제 `ProductID` 범위 내에서 트랜잭션입니다.

`DeleteSelectedProducts` 단추 s `Click` 이벤트 처리기는 다음에 현재 사용 하 여 `foreach` 각 GridView 행에서 반복 하는 루프:


[!code-csharp[Main](batch-deleting-cs/samples/sample2.cs)]

각 행에 대해는 `ProductSelector` CheckBox 웹 컨트롤은 프로그래밍 방식으로 참조 합니다. 이 옵션을 선택 하는 경우 s 행 `ProductID` 에서 검색 되는 `DataKeys` 컬렉션 및 `DeleteResults` 레이블의 `Text` 속성 행 삭제 하도록 선택 된 나타내는 메시지를 포함 하도록 업데이트 됩니다.

위의 코드는 모든 레코드에 대 한 호출으로 실제로 삭제 되지 않습니다는 `ProductsBLL` s 클래스 `Delete` 메서드 주석으로 처리 됩니다. 이 삭제 논리를 적용할 인 코드는 제품도 삭제 하지만 원자성 작업 내에 없습니다. 즉, 시퀀스에서 첫 번째 몇 삭제 했지만, 최신 실패 (으로 인해 foreign key 제약 조건 위반),이 예외가 throw 됩니다 있지만 이러한 제품이 이미 삭제은 삭제 된 상태로 유지 합니다.

원자성을 보장 하려면 대신 사용 하 여 해야는 `ProductsBLL` s 클래스 `DeleteProductsWithTransaction` 메서드. 이 방법의 목록을 허용 하기 때문에 `ProductID` 값, 해야 먼저 그리드에서이 목록을 컴파일하고 매개 변수로 전달 합니다. 인스턴스를 처음 만들면는 `List<T>` 형식의 `int`합니다. 내에서 `foreach` 선택 된 제품을 추가 해야 하는 루프 `ProductID` 값이 `List<T>`합니다. 루프 후이 `List<T>` 에 전달 되어야 합니다는 `ProductsBLL` s 클래스 `DeleteProductsWithTransaction` 메서드. 업데이트는 `DeleteSelectedProducts` 단추의 `Click` 이벤트 처리기를 다음 코드로:


[!code-csharp[Main](batch-deleting-cs/samples/sample3.cs)]

업데이트 된 코드를 만듭니다는 `List<T>` 형식의 `int` (`productIDsToDelete`) 사용 하 여 정보를 표시 하 고는 `ProductID` 값을 삭제 합니다. 후의 `foreach` 하나 이상의 제품을 선택 하는 경우 루프는 `ProductsBLL` s 클래스 `DeleteProductsWithTransaction` 메서드가 호출 되 고이 목록에 전달 합니다. `DeleteResults` (새로 삭제할 레코드가 더 이상 표시 되도록 표에서 행으로) 데이터가 GridView에 리바운드 및 레이블도 표시 됩니다.

그림 4에서는 삭제에 대 한 행의 수를 선택한 후 GridView를 보여 줍니다. 그림 5는 선택한 제품 삭제 단추를 클릭 한 후에 즉시는 화면을 보여 줍니다. 그림 5에서는 `ProductID` GridView 아래에 있는 레이블에 표시 되는 삭제 된 레코드의 값이 고 해당 행 GridView에서 더 이상이 없습니다.


[![선택 된 제품 삭제](batch-deleting-cs/_static/image4.gif)](batch-deleting-cs/_static/image7.png)

**그림 4**:은 선택한 제품 삭제 됩니다 ([전체 크기 이미지를 보려면 클릭](batch-deleting-cs/_static/image8.png))


[![제품 ProductID 삭제 값은 GridView 아래에 나열 된](batch-deleting-cs/_static/image5.gif)](batch-deleting-cs/_static/image9.png)

**그림 5**: The 삭제 제품 `ProductID` 값은 GridView 아래에 나열 된 ([전체 크기 이미지를 보려면 클릭](batch-deleting-cs/_static/image10.png))


> [!NOTE]
> 테스트 하는 `DeleteProductsWithTransaction` 메서드의 원자성의 제품에 대 한 항목을 수동으로 추가 `Order Details` 테이블 및 기타) (함께 해당 제품을 삭제 하려고 합니다. 관련된 된 주문 인 제품을 삭제 하려면 어떻게 다른 선택 된 제품 삭제 롤백되는 동안 foreign key 제약 조건 위반을 받습니다.


## <a name="summary"></a>요약

확인란의 열이 있는 GridView를 추가 하는 것 인터페이스 삭제 일괄 처리를 만들지 및 Button 웹 컨트롤을 클릭 하면 선택 된 행의 모든 단일 원자 단위 작업으로 삭제 됩니다. 이러한 인터페이스 정보를 결합 두 이전 자습서에서 작업을 수행 하 여 빌드된에서는이 자습서에서는 [확인란 GridView 열 추가](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-cs.md) 및 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](wrapping-database-modifications-within-a-transaction-cs.md)합니다. 첫 번째 자습서에서 확인란의 열이 있는 GridView 만든 및 BLL에 메서드를 구현한 후자의 전달 될 때는 `List<T>` 의 `ProductID` 값을 트랜잭션의 범위 내에서 삭제 합니다.

다음 자습서에서 일괄 처리 삽입을 수행 하기 위한 인터페이스를 만들어 보겠습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Hilton Giesenow 및 Teresa 머피의 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](batch-updating-cs.md)
[다음](batch-inserting-cs.md)
