---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-vb
title: SqlDataSource (VB)를 사용 하 여 낙관적 동시성 구현 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 낙관적 동시성 제어의 주요 정보를 검토 하 고 SqlDataSource 컨트롤을 사용 하 여 구현 하는 방법을 탐색 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2007
ms.topic: article
ms.assetid: a8fa72ee-8328-4854-a419-c1b271772303
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: a71e5ee06e4a970e7e6d6c3b5b0351ad218e0253
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37391049"
---
<a name="implementing-optimistic-concurrency-with-the-sqldatasource-vb"></a>SqlDataSource (VB)를 사용 하 여 낙관적 동시성 구현
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_50_VB.exe) 또는 [PDF 다운로드](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/datatutorial50vb1.pdf)

> 이 자습서에서는 낙관적 동시성 제어의 주요 정보를 검토 하 고 SqlDataSource 컨트롤을 사용 하 여 구현 하는 방법을 탐색 합니다.


## <a name="introduction"></a>소개

이전 자습서에서 삽입, 업데이트 및 삭제 기능 SqlDataSource 컨트롤을 추가 하는 방법을 살펴보았습니다. 즉, 이러한 기능을 제공 해야 해당 지정 `INSERT`, `UPDATE`, 또는 `DELETE` s control에서 SQL 문을 `InsertCommand`합니다 `UpdateCommand`, 또는 `DeleteCommand` 함께 적절 한 속성 매개 변수를 `InsertParameters`, `UpdateParameters`, 및 `DeleteParameters` 컬렉션입니다. 이러한 속성 및 컬렉션을 수동으로 지정할 수 있습니다, 데이터 소스 구성 마법사가 고급 단추는 생성을 제공 `INSERT`, `UPDATE`, 및 `DELETE` 문을 확인란을 통해 생성 되는 자동-이러한 문을 기반으로 `SELECT` 문입니다.

생성 함께 `INSERT`, `UPDATE`, 및 `DELETE` 문을 확인란을 고급 SQL 생성 옵션 대화 상자를 사용 하 여 낙관적 동시성 옵션 포함 (그림 1 참조). 옵션을 선택 하면 합니다 `WHERE` 자동으로 생성 된 절 `UPDATE` 및 `DELETE` 만 업데이트를 수행 하려면 문을 수정 되거나 삭제 기본 데이터베이스 데이터 영업일 기준 t 사용자 이후 수정 된 경우 마지막으로 로드 데이터 표입니다.


![고급에서 낙관적 동시성 지원을 추가할 수 있습니다 SQL 생성 옵션 대화 상자](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image1.gif)

**그림 1**: 고급에서 낙관적 동시성 지원을 추가할 수 있습니다 SQL 생성 옵션 대화 상자


다시 합니다 [낙관적 동시성 구현](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md) 자습서 ObjectDataSource에 추가 하는 방법과 낙관적 동시성 제어의 기본 개념을 살펴보았습니다. 이 자습서에서는 낙관적 동시성 제어의 essentials 재손질 하 고 SqlDataSource를 사용 하 여 구현 하는 방법을 탐색 합니다.

## <a name="a-recap-of-optimistic-concurrency"></a>낙관적 동시성의 요약

여러 허용 하는 웹 응용 프로그램에 대 한 동시 사용자가 편집 하거나 동일한 데이터를 삭제할 수 있을 가능성이 한 명의 사용자가 변경 내용을 다른를 실수로 덮어쓸 수 있습니다. 에 [낙관적 동시성 구현](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md) 자습서는 다음 예제를 제공 했습니다.

두 사용자 Jisun과 Sam, 된 모두 페이지를 방문 하는 업데이트 및 GridView 컨트롤을 통해 제품을 삭제 하는 방문자를 허용 하는 응용 프로그램에서 한다고 가정 합니다. 같은 시간대에 Chai에 대 한 편집 단추를 클릭 둘 다. Jisun은 Chai Tea 제품 이름을 변경 하 고 [업데이트] 단추를 클릭 합니다. 최종적인 결론은는 `UPDATE` 를 설정 하는 데이터베이스에 전송 되는 문 *모든* 제품 s 업데이트할 수 있는 필드 (Jisun 단일 필드를 업데이트 하는 경우에 `ProductName`). 이 시점에서, 데이터베이스에 Chai 차 음료, 범주 등이 특정 제품에 대 한 공급 업체 특이 한 액체 값. 그러나 Sam s 화면의 GridView 여전히 표시 제품 이름을 편집할 수 있는 GridView 행에서 Chai로 됩니다. 몇 초 후 Jisun의 변경 사항이 커밋되기 Sam 입력 하면 조미료에 범주를 업데이트 하 고 업데이트를 클릭 합니다. 이 인해를 `UPDATE` Chai에 제품 이름을 설정 하는 데이터베이스에 전송 하는 문을 `CategoryID` 해당 입력 하면 조미료 범주 ID 및 등입니다. 제품 이름 Jisun의 변경 덮어썼습니다.

그림 2에서는이 상호 작용을 보여 줍니다.


[![두 명의 사용자가 동시에 레코드를 업데이트 하는 경우 있습니다 s 잠재적인 사용자 s에 대 한 변경을 다른를 덮어쓰려면](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image2.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image1.png)

**그림 2**: 다른 덮어쓰기 때 두 사용자가 동시에 업데이트를 레코드 있습니다 s 잠재적 사용자 s에 대 한 변경 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image2.png))


이 시나리오의 형태를 펼치기 하지 못하도록 [동시성 제어](http://en.wikipedia.org/wiki/Concurrency_control) 구현 해야 합니다. [낙관적 동시성](http://en.wikipedia.org/wiki/Optimistic_concurrency_control) 이 자습서의 포커스는 있을 동시성 충돌 합니다, 대부분의 이러한 충돌-t 이득 시간 발생 가정 하에서 작동 합니다. 따라서는 충돌이 발생 하는 경우 낙관적 동시성 제어 하기만 하면 사용자에 게 알려을 다른 사용자가 동일한 데이터를 수정 하기 때문에 해당 변경 내용 수 t 저장 합니다.

> [!NOTE]
> 응용 프로그램의 많은 동시성 충돌 되도록 하거나 이러한 충돌은 허용 가능할 경우 가정 있는 경우 다음 비관적 동시성 제어 대신 사용할 수 있습니다. 다시 참조를 [낙관적 동시성 구현](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md) 자습서 비관적 동시성 제어에 대 한 더 상세히 논의 합니다.


낙관적 동시성 제어 업데이트나 삭제 프로세스를 시작 하는 경우와 마찬가지로 업데이트 되거나 삭제 된 레코드에 동일한 값 함으로써 작동 합니다. 예를 들어, 편집할 수는 GridView의 편집 단추를 클릭 하면 s 레코드 값을 데이터베이스에서 읽고 텍스트 상자 및 기타 웹 컨트롤에 표시 합니다. GridView에서 원래 값이 저장 됩니다. 사용자가 변경 하 고, [업데이트] 단추를 클릭 한 후에 이후를 `UPDATE` 문에 사용 되는 원래 값 및 새 값을 고려 하며 원래 값을 사용자가 편집을 시작 하는 경우 기본 데이터베이스 레코드에만 업데이트 데이터베이스에서 값으로 동일합니다. 그림 3에서는이 이벤트 시퀀스를 보여 줍니다.


[![성공 하려면 업데이트 또는 삭제, 원래 값을 현재 데이터베이스 값 이어야 합니다.](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image3.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image3.png)

**그림 3**:에 대 한 업데이트 또는 삭제 성공에는 원래 값 해야 수 값과 같은 현재 데이터베이스를 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image4.png))


낙관적 동시성을 구현 하는 방법은 여러 가지가 있습니다 (참조 [Peter A. Bromberg](http://peterbromberg.net/) s [Optmistic 동시성 업데이트 논리](http://www.eggheadcafe.com/articles/20050719.asp) 간략히 다양 한 옵션에 대 한). SqlDataSource에서 (뿐만 아니라 ADO.NET 입력 데이터 집합 데이터 액세스 계층에 사용 되는) 사용 방법을 보완 합니다 `WHERE` 모든 원래 값의 비교를 포함 하는 절. 다음 `UPDATE` 문을 현재 데이터베이스 값 GridView에서 레코드를 업데이트 하는 경우 원래 검색 된 값과 같은 경우에 해당 이름 및 제품의 가격을 예를 들어 업데이트 합니다. `@ProductName` 및 `@UnitPrice` 반면 매개 변수는 사용자가 입력 한 새 값이 포함 `@original_ProductName` 및 `@original_UnitPrice` 편집 단추를 클릭할 때 GridView에 원래 로드 된 값을 포함 합니다.


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample1.sql)]

이 자습서에서 살펴보겠지만 SqlDataSource 사용 하 여 낙관적 동시성 제어를 사용 하도록 설정 하면 간단 하 게는 확인란을 선택 합니다.

## <a name="step-1-creating-a-sqldatasource-that-supports-optimistic-concurrency"></a>1 단계: 낙관적 동시성을 지 원하는 SqlDataSource 만들기

열어서 시작 합니다 `OptimisticConcurrency.aspx` 에서 페이지를 `SqlDataSource` 폴더입니다. 설정 디자이너 도구 상자에서 SqlDataSource 컨트롤을 끌어 해당 `ID` 속성을 `ProductsDataSourceWithOptimisticConcurrency`입니다. 다음으로, 컨트롤 s 스마트 태그의 데이터 소스 구성 링크를 클릭 합니다. 마법사의 첫 번째 화면에서 사용 하 여 작업을 선택 합니다 `NORTHWINDConnectionString` 다음을 클릭 합니다.


[![위해 사용 하 여 작업을 선택 합니다.](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image4.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image5.png)

**그림 4**: 작업을 선택 합니다 `NORTHWINDConnectionString` ([클릭 하 여 큰 이미지 보기](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image6.png))


사용자가 편집할 수 있도록 하는 GridView를 추가할 예정이 예는 `Products` 테이블입니다. 따라서 Select 문 화면 구성에서 선택는 `Products` 드롭 다운 목록에서 테이블을 선택 합니다 `ProductID`, `ProductName`, `UnitPrice`, 및 `Discontinued` 그림 5에 표시 된 대로 열.


[![Products 테이블에서 ProductID, ProductName, UnitPrice, 및 지원 되지 않는 열 반환](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image5.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image7.png)

**그림 5**:에서 `Products` 테이블을 반환 합니다 `ProductID`, `ProductName`, `UnitPrice`, 및 `Discontinued` 열 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image8.png))


열을 선택한 후 고급 SQL 생성 옵션 대화 상자를 표시 하려면 고급 단추를 클릭 합니다. 생성을 확인 `INSERT`, `UPDATE`, 및 `DELETE` 문을 낙관적 동시성 확인란을 사용 하 고 확인을 클릭 (다시 그림 1 참조 스크린 샷에 대 한). 다음을 클릭 하 여 마법사를 완료 한 다음 완료 합니다.

데이터 소스 구성 마법사를 완료 한 후 결과 검사 하려면 잠시 시간이 소요 `DeleteCommand` 하 고 `UpdateCommand` 속성 및 `DeleteParameters` 및 `UpdateParameters` 컬렉션입니다. 이 작업을 수행 하는 가장 쉬운 방법은 소스 탭 페이지 s 선언적 구문을 보려면 왼쪽된 아래 모퉁이에서 클릭 하는 것입니다. 여기서 찾을 수 있습니다는 `UpdateCommand` 값:


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample2.sql)]

7 개의 매개 변수를 사용 하 여는 `UpdateParameters` 컬렉션:


[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample3.aspx)]

마찬가지로,는 `DeleteCommand` 속성 및 `DeleteParameters` 컬렉션 다음과 같이 표시 됩니다.


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample4.sql)]


[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample5.aspx)]

확대 하는 것 외에도 합니다 `WHERE` 절을 `UpdateCommand` 및 `DeleteCommand` 속성 (및 해당 매개 변수 컬렉션에 추가 매개 변수를 추가) 사용 하 여 낙관적 동시성 옵션 두 개의 다른 조정 선택 속성:

- 변경 된 [ `ConflictDetection` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.conflictdetection.aspx) 에서 `OverwriteChanges` (기본값)를 `CompareAllValues`
- 변경 된 [ `OldValuesParameterFormatString` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.oldvaluesparameterformatstring.aspx) 에서 {0} (기본값)에 원래\_ {0} 합니다.

데이터 웹 컨트롤 SqlDataSource s를 호출 하는 경우 `Update()` 또는 `Delete()` 원래 값을 메서드에 전달 합니다. 경우 SqlDataSource s `ConflictDetection` 속성이 `CompareAllValues`, 이러한 원래 값이 명령에 추가 됩니다. `OldValuesParameterFormatString` 속성은 이러한 원래 값 매개 변수에 대해 사용 되는 명명 패턴을 제공 합니다. 데이터 소스 구성 마법사를 사용 하 여 원래\_ {0} 각 원래 매개 변수 이름 및는 `UpdateCommand` 하 고 `DeleteCommand` 속성 및 `UpdateParameters` 및 `DeleteParameters` 컬렉션 적절 하 게 합니다.

> [!NOTE]
> SqlDataSource 컨트롤 s 삽입 기능을 사용 하지 다시 것에 자유롭게 삭제 되므로 합니다 `InsertCommand` 속성 및 해당 `InsertParameters` 컬렉션입니다.


## <a name="correctly-handlingnullvalues"></a>올바르게 처리`NULL`값

아쉽게도 증강 `UPDATE` 및 `DELETE` 문을 자동으로 생성 된 낙관적 동시성을 사용 하는 경우 데이터 소스 구성 마법사에서 수행 *되지* 포함 하는 레코드를 사용 하 여 회사 `NULL` 값. 이유를 확인 하려면이 SqlDataSource가 것이 좋습니다 `UpdateCommand`:


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample6.sql)]

`UnitPrice` 열에는 `Products` 테이블에 있을 수 `NULL` 값입니다. 특정 레코드가 있는 경우는 `NULL` 에 대 한 값 `UnitPrice`의 `WHERE` 절 부분 `[UnitPrice] = @original_UnitPrice` 됩니다 *항상* 때문에 False로 평가 `NULL = NULL` 항상 False를 반환 합니다. 따라서 레코드는 포함 `NULL` 값을 편집 하거나 삭제할 수로 `UPDATE` 및 `DELETE` 문을 `WHERE` 절 성공한 t 반환 행을 업데이트 하거나 삭제 합니다.

> [!NOTE]
> 이 버그의 2004 년 6 월에에서 Microsoft로 보고 먼저 되었습니다 [SqlDataSource 생성 된 잘못 된 SQL 문을](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=93937) 되었으며 나타내기 ASP.NET의 다음 버전에서 수정 될 예정입니다.


이 해결 하려면 수동으로 업데이트 해야 합니다 `WHERE` 절 모두를 `UpdateCommand` 및 `DeleteCommand` 속성에 대 한 **모든** 열 수 있는 `NULL` 값입니다. 일반적으로 변경할 `[ColumnName] = @original_ColumnName` 에:


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample7.sql)]

이 수정 속성 창에서 UpdateQuery 또는 DeleteQuery 옵션을 통해 선언적 태그를 통해 직접 또는 업데이트를 통해 구성할 수 있으며 사용자 지정 SQL 문 또는 저장된 프로시저 옵션의 구성 데이터를 지정에서 하는 탭 삭제 소스 마법사입니다. 이 수정에 대 한 다시 수 있어야 합니다 *모든* 열에는 `UpdateCommand` 하 고 `DeleteCommand` s `WHERE` 절을 포함할 수 있는 `NULL` 값입니다.

이 예제를 적용 하면 수정한 다음 결과 `UpdateCommand` 고 `DeleteCommand` 값:


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample8.sql)]

## <a name="step-2-adding-a-gridview-with-edit-and-delete-options"></a>2 단계: 추가 편집 및 삭제 옵션을 사용 하 여 GridView

낙관적 동시성을 지원 하도록 SqlDataSource를 사용 하 여에이 동시성 제어를 활용 하는 페이지 데이터 웹 컨트롤을 추가 합니다. 이 자습서에서는 편집을 제공 하는 GridView를 추가 및 삭제 기능을 사용 수 있습니다. 이렇게 하려면 GridView 집합과 디자이너 도구 상자에서 끌어 해당 `ID` 에 `Products`입니다. GridView가 스마트 태그에 바인딩하지는 `ProductsDataSourceWithOptimisticConcurrency` 1 단계에서에서 추가한 SqlDataSource 컨트롤입니다. 마지막으로, 스마트 태그에서 편집을 사용 하도록 설정 및 삭제 사용 옵션을 선택 합니다.


[![SqlDataSource를 GridView을 바인딩하고 편집 및 삭제를 사용 하도록 설정](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image6.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image9.png)

**그림 6**: GridView SqlDataSource 및 편집 사용 및 삭제 하는 중에 바인딩 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image10.png))


GridView를 추가한 후 제거 하 여 모양을 구성 합니다 `ProductID` BoundField 변경를 `ProductName` BoundField s `HeaderText` 속성을 업데이트 하 고 제품에는 `UnitPrice` BoundField 있도록 해당 `HeaderText` 속성은 단순히 가격입니다. 이상적으로 d 강화에 대 한 RequiredFieldValidator 포함 하도록 편집 인터페이스를 `ProductName` 값 및에 대해 CompareValidator의 `UnitPrice` 값 (s 올바른 형식의 숫자 값을 확인). 참조 된 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) GridView s 편집 인터페이스 사용자 지정에 대 한 자세한 설명에 대 한 자습서입니다.

> [!NOTE]
> SqlDataSource GridView에서 전달 된 원래 값은 s 뷰 상태를 사용 해야 하는 GridView 뷰 상태에 저장 합니다.


GridView에 다음과 같이이 수정에 확인 한 후 GridView, SqlDataSource 선언적 태그는 다음과 같아야 합니다.


[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample9.aspx)]

작업에서 낙관적 동시성 제어를 확인 하려면 두 개의 브라우저 창을 열고 로드는 `OptimisticConcurrency.aspx` 모두의 페이지입니다. 첫 번째 제품 두 브라우저에 대 한 편집 단추를 클릭 합니다. 하나의 브라우저에서 제품 이름을 변경 하 고 업데이트를 클릭 합니다. 브라우저에서 포스트백 됩니다 하 고 방금 편집한 레코드에 대 한 새 제품 이름을 보여 주는 GridView 해당 미리 편집 모드로 반환 됩니다.

두 번째 브라우저 창에서 제품 이름 원래 값으로 나감) (하지만 가격을 변경 하 고 업데이트를 클릭 합니다. 포스트백에서 표는 미리 편집 모드를 반환 하지만 가격 변경 기록 되지 않습니다. 두 번째 브라우저는 이전 가격으로 새 제품 이름 같은 첫 번째 값을 보여 줍니다. 두 번째 브라우저 창에서 변경한 내용을 손실 되었습니다. 또한 변경 내용이 손실 대신 자동으로 예외 없거나 동시성 위반을 방금 발생 했음을 나타내는 메시지가 발생 합니다.


[![두 번째 브라우저 창에서 변경 내용이 자동으로 손실](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image7.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image11.png)

**그림 7**:의 변경에는 두 번째 브라우저 창이 자동으로 손실 된 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image12.png))


두 번째 브라우저의 변경 내용이 커밋 이유 이유 이어서 합니다 `UPDATE` 문이의 `WHERE` 절 모든 레코드를 필터링 하 고 따라서 모든 행에 영향을 주지 않았습니다. 살펴볼 s는 `UPDATE` 문을 다시 합니다.


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample10.sql)]

원래 제품 이름에 지정 된 브라우저 창을 두 번째 레코드를 업데이트할 때의 `WHERE` (첫 번째 브라우저에 의해 변경 되었습니다) 이므로 기존 제품 이름과 함께 등록 되는 절 만들어지고 t 일치 합니다. 따라서 문을 `[ProductName] = @original_ProductName` False를 반환 하며 `UPDATE` 모든 레코드에는 영향을 주지 않습니다.

> [!NOTE]
> 동일한 방식으로 작동을 삭제 합니다. 두 개의 브라우저 창을 열고, 하나를 사용 하 여 특정된 제품을 편집한 다음 해당 변경 내용을 저장 하 여 시작 합니다. 변경 내용을 하나의 브라우저에서을 저장 한 후 다른 동일한 제품에 대 한 삭제 단추를 클릭 합니다. 원래 값 don t 일치 하므로 합니다 `DELETE` 문이의 `WHERE` 절 삭제 자동으로 실패 합니다.


두 번째 브라우저 창에서 최종 사용자가의 관점에서 [업데이트] 단추를 클릭 한 후 표 미리 편집 모드를 반환 하지만 해당 변경 내용이 손실 합니다. 그러나 여기서 s는 해당 변경 내용을 동작 t 시각적 피드백이 없습니다. 이상적으로 사용자가 변경 내용을 동시성 위반을 손실 되 면 d 알릴 수 하 고, 아마도, 표 편집 모드로 유지 합니다. 가이 작업을 수행 하는 방법을 살펴볼 수 있습니다.

## <a name="step-3-determining-when-a-concurrency-violation-has-occurred"></a>3 단계: 동시성 위반이 발생 했을 때 결정

동시성 위반을가 변경 하나에 거부 되므로 동시성 위반이 발생 했을 때 사용자에 게 경고할 좋을 것입니다. 사용자 경고를 통해의 컨트롤을 추가 레이블 웹 라는 페이지의 맨 위에 `ConcurrencyViolationMessage` 해당 `Text` 속성에 다음 메시지가 표시 됩니다: 업데이트 하거나 다른 사용자가 동시에 업데이트 된 레코드를 삭제 하려고 했습니다. 다른 사용자의 변경 내용을 검토 하 고 업데이트를 다시 실행 하거나 삭제 하십시오. 가 레이블 컨트롤을 설정 `CssClass` 에 정의 된 CSS 클래스에는 경고로 속성 `Styles.css` 빨간색, 기울임꼴, 굵게 및 큰 글꼴의 텍스트를 표시 하는 합니다. 마지막으로 s 레이블 설정 `Visible` 하 고 `EnableViewState` 속성을 `False`입니다. 명시적으로 설정한 포스트백에만 제외 하 고 레이블을 숨기는이 해당 `Visible` 속성을 `True`입니다.


[![경고를 표시 하려면 페이지에는 레이블 컨트롤 추가](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image8.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image13.png)

**그림 8**: 경고를 표시 하려면 페이지에 레이블 컨트롤을 추가 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image14.png))


업데이트 또는 삭제, GridView s를 수행할 때 `RowUpdated` 고 `RowDeleted` 이벤트 처리기는 요청 된 update 또는 delete 해당 데이터 소스 컨트롤을 수행한 후 발생 합니다. 행 개수 이러한 이벤트 처리기에서 작업에 의해 영향을 확인할 수 있습니다. 표시 하고자 하는 0 개의 행에 영향을 받은 경우는 `ConcurrencyViolationMessage` 레이블.

둘 다에 대 한 이벤트 처리기를 만듭니다는 `RowUpdated` 및 `RowDeleted` 이벤트 다음 코드를 추가 합니다.


[!code-vb[Main](implementing-optimistic-concurrency-with-the-sqldatasource-vb/samples/sample11.vb)]

두 이벤트 처리기에서 확인 합니다 `e.AffectedRows` 속성 0 이면 설정 및는 `ConcurrencyViolationMessage` 레이블 s `Visible` 속성을 `True`입니다. 에 `RowUpdated` 이벤트 처리기도 하도록 지시를 설정 하 여 편집 모드로 유지 GridView는 `KeepInEditMode` 속성을 true로 합니다. 이 과정에서 다른 사용자가의 데이터를 편집 인터페이스에 로드 되도록 데이터 표를 다시 바인딩할 필요 합니다. GridView가 호출 하 여 이렇게 `DataBind()` 메서드.

그림 9 있듯이 이러한 두 이벤트 처리기를 사용 하 여 동시성 위반이 발생할 때마다 확실 메시지가 표시 됩니다.


[![동시성 위반이 발생 하는 경우 메시지가 표시 됩니다.](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image9.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image15.png)

**그림 9**: 동시성 위반이 발생 하는 경우는 메시지가 표시 됩니다 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-vb/_static/image16.png))


## <a name="summary"></a>요약

웹 응용 프로그램을 만들 때 여기서 여러 동시 사용자가 편집 하 고 동일한 데이터에 동시성 제어 옵션을 고려해 야 할 중요 한 것입니다. 기본적으로 ASP.NET 데이터 웹 컨트롤 및 데이터 소스 제어를 사용 하지 않는 모든 동시성 제어 합니다. 이 자습서에서 보았듯이 SqlDataSource 사용 하 여 낙관적 동시성 제어를 구현는 비교적 빠르고 간단 합니다. SqlDataSource 처리를 투자할 대부분이 보강 사용자 추가 대 한 `WHERE` 절이 자동으로 생성 된 `UPDATE` 및 `DELETE` 제한이 없지만 문은 처리에 몇 가지 미묘한 `NULL` 에 설명 된 대로 열 값을 올바르게 처리 `NULL` 섹션 값입니다.

이 자습서는 SqlDataSource 검사도 마칩니다. 나머지 자습서는 ObjectDataSource, 계층화 된 아키텍처를 사용 하 여 데이터를 사용 하 여 작업 돌아갈 것입니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](inserting-updating-and-deleting-data-with-the-sqldatasource-vb.md)
