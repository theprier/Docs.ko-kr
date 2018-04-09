---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-cs
title: SqlDataSource (C#)를 사용 하 여 낙관적 동시성 구현 | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 낙관적 동시성 제어에 대 한 필수 정보를 검토 한 다음 SqlDataSource 컨트롤을 사용 하 여 구현 하는 방법을 탐색 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2007
ms.topic: article
ms.assetid: df999966-ac48-460e-b82b-4877a57d6ab9
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: 246e8d0c2aee7358680fbca7229cc9b05ceca1cb
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="implementing-optimistic-concurrency-with-the-sqldatasource-c"></a>SqlDataSource (C#)를 사용 하 여 낙관적 동시성을 구현합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_50_CS.exe) 또는 [PDF 다운로드](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/datatutorial50cs1.pdf)

> 이 자습서에서는 낙관적 동시성 제어에 대 한 필수 정보를 검토 한 다음 SqlDataSource 컨트롤을 사용 하 여 구현 하는 방법을 탐색 합니다.


## <a name="introduction"></a>소개

이전 자습서에서 삽입, 업데이트 및 삭제 기능 SqlDataSource 컨트롤을 추가 하는 방법을 검사 했습니다. 즉, 이러한 기능을 제공 하려면 म 지정 하도록 필요한 해당 `INSERT`, `UPDATE`, 또는 `DELETE` s 컨트롤에서 SQL 문을 `InsertCommand`, `UpdateCommand`, 또는 `DeleteCommand` 속성을 적절 한 함께 매개 변수는 `InsertParameters`, `UpdateParameters`, 및 `DeleteParameters` 컬렉션입니다. 데이터 소스 구성 마법사 s 고급 단추는 생성을 제공 하는 동안 이러한 속성 및 컬렉션을 지정할 수 수동으로 `INSERT`, `UPDATE`, 및 `DELETE` 자동-만들어집니다 이러한 문은 문을 확인란에 따라는 `SELECT` 문.

생성 함께 `INSERT`, `UPDATE`, 및 `DELETE` 사용 하 여 낙관적 동시성 옵션을 포함 하는 문을 확인란, 고급 SQL 생성 옵션 대화 상자 (그림 1 참조). 옵션을 선택 하면는 `WHERE` 절에는 자동으로 생성 된 `UPDATE` 및 `DELETE` delete 기본 데이터베이스 데이터 않았음을 t 사용자 이후 수정 된 경우 마지막 데이터를 로드할 ड आ 또는 문은 업데이트를 수행 하도록 수정 되었습니다.


![지원을 추가 하는 낙관적 동시성에서 고급 SQL 생성 옵션 대화 상자](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image1.gif)

**그림 1**: 지원을 추가 하는 낙관적 동시성에서 고급 SQL 생성 옵션 대화 상자


에 [낙관적 동시성 구현](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md) 자습서는 ObjectDataSource에 추가 하는 방법과 낙관적 동시성 제어에 대 한 기본적인 검사 했습니다. 이 자습서에서는 낙관적 동시성 제어 essentials 재손질 알아보고 SqlDataSource를 사용 하 여 구현 하는 방법을 탐색 하겠습니다.

## <a name="a-recap-of-optimistic-concurrency"></a>낙관적 동시성에 대해 간략하게 설명

여러 명의 웹 응용 프로그램에 대 한 동시 사용자가 편집 하거나 동일한 데이터를 삭제할 수 있을 가능성이 사용자 다른 s 변경 내용을 실수로 덮어쓸 수 있습니다. 에 [낙관적 동시성 구현](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md) 다음 예제를 제공 하려면 자습서:

사용자 이영희, Jisun 및 Sam을 둘 다 방문 페이지를 업데이트 하는 GridView 컨트롤을 통해 제품 삭제 방문자를 허용 하는 응용 프로그램에 한다고 가정 합니다. Chai 편집 단추를 클릭 둘 다에서 같은 시간입니다. Jisun 제품 이름을 Chai 찻잔으로 변경 하 고 업데이트 단추를 클릭 합니다. 결과는 `UPDATE` 설정 하는 데이터베이스에 전송 되는 문을 *모든* 제품 s 업데이트할 수 있는 필드 (Jisun만 한 필드를 업데이트 하는 경우에 `ProductName`). 이 시점에서, 데이터베이스에는 공급 업체 삼 화 음료,이 특정 제품에 대해 Chai 차를 음료, 범주 값입니다. 그러나 Sam의 화면에 GridView 여전히 표시 제품 이름을 편집 가능한 GridView 행에서 Chai로 됩니다. 몇 초 후 Jisun의 변경 사항이 커밋되기 Sam 조미료 하는 범주를 업데이트 하 고 업데이트를 클릭 합니다. 이 인해는 `UPDATE` Chai을 제품 이름으로 설정 하는 데이터베이스에 보내는 문은 `CategoryID` 해당 입력 하면 조미료 범주 ID 및 등입니다. 제품 이름에 대 한 s 변경 Jisun 덮어썼습니다.

그림 2에서는이 상호 작용을 보여 줍니다.


[![두 명의 사용자가 동시에 레코드를 업데이트 하는 경우 있습니다 s 잠재적인 s 한 명의 사용자에 대 한 변경을 다른를 덮어쓰려면](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image2.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image1.png)

**그림 2**: 다른 s Overwrite로 때 두 사용자가 동시에 업데이트 된 레코드가 있습니다 s 가능성 s 한 명의 사용자에 대 한 변경 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image2.png))


이 시나리오의 형태를 펼치기 하지 않도록 하려면 [동시성 제어](http://en.wikipedia.org/wiki/Concurrency_control) 구현 해야 합니다. [낙관적 동시성](http://en.wikipedia.org/wiki/Optimistic_concurrency_control) 이 자습서의 포커스는 되어 있어도 동시성 충돌 합니다, 대부분의 이러한 충돌 t 성공한 시간 발생 가정 하에서 작동 합니다. 따라서 한 충돌이 발생 하는 경우 낙관적 동시성 제어 단순히 사용자에 게 알려 다른 사용자가 동일한 데이터를 수정 하기 때문에 해당 변경 내용 수 없습니다. 저장할 수 있습니다.

> [!NOTE]
> 응용 프로그램의 것 많은 동시성 충돌 하거나 이러한 충돌 지속할 수 없는 경우 가정 있는 경우 다음 비관적 동시성 제어 대신 사용할 수 있습니다. 다시 참조는 [낙관적 동시성 구현](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md) 비관적 동시성 제어에 보다 철저 한 토론에 대 한 자습서입니다.


낙관적 동시성 제어는 업데이트 또는 삭제 프로세스를 시작할 때 업데이트 되거나 삭제 되는 레코드에 동일한 값에서 작동 합니다. 예를 들어 편집 가능한 GridView에 있는 편집 단추를 클릭 하면 s 레코드 값은 데이터베이스에서 읽고 입력란 및 기타 웹 컨트롤에 표시 합니다. GridView에서 원래 값이 저장 됩니다. 나중에 사용자가 변경 하 고 업데이트 단추를 클릭 한 후의 `UPDATE` 사용 된 문을 원래 값과 새 값을 고려 하 고 원래 값을 사용자가 편집을 시작 하는 경우에 기본 데이터베이스 레코드를 업데이트 해야 데이터베이스에 여전히 값으로 동일합니다. 그림 3에서는이 이벤트 시퀀스를를 보여 줍니다.


[![성공 하려면 Update 또는 Delete에 대 한 원래 값을 현재 데이터베이스 값 이어야 합니다.](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image3.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image3.png)

**그림 3**: For Update 또는 Delete는 원래 값 해야 수와 같으면 현재 데이터베이스 값 Succeed로 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image4.png))


낙관적 동시성을 구현 하는 방법은 여러 가지가 (참조 [Peter A. Bromberg](http://www.eggheadcafe.com/articles/pbrombergresume.asp) s [Optmistic 동시성 업데이트 논리](http://www.eggheadcafe.com/articles/20050719.asp) 다양 한 옵션에 대 한 간단한 설명에 대 한). SqlDataSource (뿐만 아니라 ADO.NET 형식화 된 데이터 집합에서 데이터 액세스 계층에서 사용)를 사용 하는 방법 확대는 `WHERE` 절 모든 원래 값의 비교를 포함 하도록 합니다. 다음 `UPDATE` 문, 현재 데이터베이스 값을 GridView에서 레코드를 업데이트할 때 처음 검색 된 값은 경우에 해당 이름 및 제품의 가격을 예를 들어 업데이트 합니다. `@ProductName` 및 `@UnitPrice` 반면 매개 변수는 사용자가 입력 한 새 값이 들어 `@original_ProductName` 및 `@original_UnitPrice` 편집 단추 클릭 했을 때 GridView에 원래 로드 된 값이 포함:


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample1.sql)]

이 자습서에서는 볼 수 있겠지만, SqlDataSource로 낙관적 동시성 제어를 사용 하도록 설정 작업은을 확인란을 선택 합니다.

## <a name="step-1-creating-a-sqldatasource-that-supports-optimistic-concurrency"></a>1 단계: 낙관적 동시성을 지원 하는 SqlDataSource 만들기

열어 시작는 `OptimisticConcurrency.aspx` 에서 페이지는 `SqlDataSource` 폴더입니다. 설정 디자이너 도구 상자에서 SqlDataSource 컨트롤을 끌어 해당 `ID` 속성을 `ProductsDataSourceWithOptimisticConcurrency`합니다. 다음으로, 컨트롤 s 스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다. 마법사의 첫 번째 화면에서 사용 하도록 선택 된 `NORTHWINDConnectionString` 고 다음을 클릭 합니다.


[![위해 작업 선택](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image4.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image5.png)

**그림 4**: 사용 하도록 선택 된 `NORTHWINDConnectionString` ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image6.png))


사용자가을 편집할 수 있도록 하는 GridView 추가 되므로이 예는 `Products` 테이블입니다. 따라서 Select 문 화면 구성에서 선택 된 `Products` 드롭 다운 목록에서 테이블을 선택한는 `ProductID`, `ProductName`, `UnitPrice`, 및 `Discontinued` 그림 5에 표시 된 것 처럼 열.


[![Products 테이블에서 ProductID, ProductName, UnitPrice, 및 열에 지원 되지 않는 반환](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image5.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image7.png)

**그림 5**:에서 `Products` 테이블에서 반환 된 `ProductID`, `ProductName`, `UnitPrice`, 및 `Discontinued` 열 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image8.png))


열을 선택한 후 고급 SQL 생성 옵션 대화 상자를 표시 하는 고급 단추를 클릭 합니다. 생성 확인 `INSERT`, `UPDATE`, 및 `DELETE` 문을 낙관적 동시성 확인란 사용 하 여 한 확인을 클릭 하 고 (다시 그림 1 참조 스크린 샷을 대 한). 다음을 클릭 하 여 마법사를 완료 한 다음 완료 합니다.

데이터 소스 구성 마법사를 완료 한 후 결과 검사 하려면 잠시 시간이 걸릴 `DeleteCommand` 및 `UpdateCommand` 속성 및 `DeleteParameters` 및 `UpdateParameters` 컬렉션입니다. 이 작업을 수행 하는 가장 쉬운 방법은 소스 탭 페이지 s 선언적 구문 하단 왼쪽된 모서리 쪽에서 클릭 하는 것입니다. 있을 것는 `UpdateCommand` 값:


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample2.sql)]

7 개의 매개 변수를는 `UpdateParameters` 컬렉션:


[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample3.aspx)]

마찬가지로,는 `DeleteCommand` 속성 및 `DeleteParameters` 컬렉션은 다음과 같습니다.


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample4.sql)]


[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample5.aspx)]

보충 하며는 `WHERE` 절은 `UpdateCommand` 및 `DeleteCommand` 속성 (및 해당 매개 변수 컬렉션에 추가 매개 변수를 추가)을 사용 하 여 낙관적 동시성 옵션을 조정 두 개의 다른 선택 하면 속성:

- 변경 된 [ `ConflictDetection` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.conflictdetection.aspx) 에서 `OverwriteChanges` (기본값)를 `CompareAllValues`
- 변경 된 [ `OldValuesParameterFormatString` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.oldvaluesparameterformatstring.aspx) 원래 (기본값) {0}에서\_{0}.

웹 컨트롤 데이터 SqlDataSource s를 호출 하는 경우 `Update()` 또는 `Delete()` 원래 값 메서드를 전달 합니다. 경우 SqlDataSource s `ConflictDetection` 속성이 `CompareAllValues`, 원래 값이 명령에 추가 됩니다. `OldValuesParameterFormatString` 속성은 이러한 원래 값 매개 변수에 대해 사용 되는 명명 패턴을 제공 합니다. 데이터 소스 구성 마법사를 사용 하 여 원래\_{0} 각 원래 매개 변수 이름을 지정 하 고는 `UpdateCommand` 및 `DeleteCommand` 속성 및 `UpdateParameters` 및 `DeleteParameters` 컬렉션 적절 하 게 합니다.

> [!NOTE]
> SqlDataSource 컨트롤 s 삽입 기능을 사용 하지 다시 म 간편 하 게 제거 하므로 `InsertCommand` 속성 및 해당 `InsertParameters` 컬렉션입니다.


## <a name="correctly-handlingnullvalues"></a>올바르게 처리`NULL`값

안타깝게도, 보강 된 `UPDATE` 및 `DELETE` 낙관적 동시성을 사용 하는 경우 데이터 소스 구성 마법사에 의해 자동 생성 된 문을 수행 *하지* 포함 된 레코드는 관련 작업을 수행할 `NULL` 값입니다. 그 이유를 보려면 우리의 SqlDataSource s 고려 `UpdateCommand`:


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample6.sql)]

`UnitPrice` 열에는 `Products` 테이블 있을 수 있습니다 `NULL` 값입니다. 특정 레코드는 `NULL` 값 `UnitPrice`, `WHERE` 절 부분 `[UnitPrice] = @original_UnitPrice` 됩니다 *항상* 때문에 False로 평가 `NULL = NULL` 항상 False를 반환 합니다. 따라서 레코드 포함 하는 `NULL` 값 편집 또는 삭제 될 수 없습니다로 `UPDATE` 및 `DELETE` 문을 `WHERE` 절이 t 반환 행을 업데이트 하거나 삭제 합니다.

> [!NOTE]
> 이 버그에 처음 보고 되었지만 Microsoft의 2004 년 6 월에에 [SqlDataSource 생성 된 잘못 된 SQL 문을](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=93937) 않으며 나타내기 ASP.NET의 다음 버전에서 수정 될 예정입니다.


이 해결 하려면 수동으로 업데이트 해야는 `WHERE` 절 모두에 `UpdateCommand` 및 `DeleteCommand` 에 대 한 속성 **모든** 가질 수 있는 열 `NULL` 값입니다. 일반적으로 변경 `[ColumnName] = @original_ColumnName` 에:


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample7.sql)]

이 수정 업데이트 나 속성 창에서 UpdateQuery 또는 DeleteQuery 옵션을 통해 선언적 태그를 통해 직접 구성할 수 있으며 사용자 지정 SQL 문 또는 구성 데이터의 저장된 프로시저 옵션 지정에서 탭을 삭제 소스 마법사입니다. 이 수정 작업에 대 한 다시 이루어져야 합니다 *모든* 열에는 `UpdateCommand` 및 `DeleteCommand` s `WHERE` 포함 될 수 있는 절 `NULL` 값입니다.

수정 된 결과이 예제를 적용 `UpdateCommand` 및 `DeleteCommand` 값:


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample8.sql)]

## <a name="step-2-adding-a-gridview-with-edit-and-delete-options"></a>2 단계: 추가 편집 및 삭제 옵션을 사용 하는 GridView

낙관적 동시성을 지원 하도록 구성 된 SqlDataSource를 사용 했으므로 이제 남은 것 데이터 웹 컨트롤이 동시성 제어를 활용 하는 페이지를 추가 합니다. 이 자습서에 대 한 s 두 편집을 제공 하는 GridView 추가 및 삭제 기능을 사용 합니다. 이를 위해는 GridView 집합과 디자이너 도구 상자에서 끌어 해당 `ID` 를 `Products`합니다. GridView s 스마트 태그에서에 연결 하는 `ProductsDataSourceWithOptimisticConcurrency` 1 단계에서에서 추가한 SqlDataSource 컨트롤입니다. 마지막으로, 스마트 태그에서 사용 하도록 설정 편집 및 삭제 사용 옵션을 확인 합니다.


[![GridView SqlDataSource에 바인딩하고 편집 및 삭제를 사용 하도록 설정](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image6.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image9.png)

**그림 6**: SqlDataSource 및 편집 사용 및 삭제 하는 중에 GridView 바인딩 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image10.png))


GridView를 추가한 후의 모양을 제거 하 여 구성의 `ProductID` 변경 BoundField는 `ProductName` BoundField s `HeaderText` 속성을 제품 및 업데이트는 `UnitPrice` BoundField 되도록 해당 `HeaderText` 속성은 단순히 가격입니다. 편집 인터페이스에 대 한 RequiredFieldValidator 포함 하도록 향상 d 우리는 이상적으로 `ProductName` 값과에 대 한 CompareValidator는 `UnitPrice` 값 (s 올바른 형식의 숫자 값으로 확인)입니다. 참조는 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) GridView s 편집 인터페이스를 사용자 지정에 대 한 자세한 설명에 대 한 자습서입니다.

> [!NOTE]
> SqlDataSource GridView에서 전달 되는 원래 값은 s 뷰 상태를 사용 해야 하는 GridView 뷰 상태에 저장 합니다.


GridView에 이러한 수정에 확인 한 후 GridView 및 SqlDataSource 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample9.aspx)]

작업에서 낙관적 동시성 제어를 보려면 두 개의 브라우저 창을 열고 로드는 `OptimisticConcurrency.aspx` 모두의 페이지입니다. 두 브라우저에에서 첫 번째 제품에 대 한 편집 단추를 클릭 합니다. 하나의 브라우저에서 제품 이름을 변경 하 고 업데이트를 클릭 합니다. 브라우저에서 포스트백을 GridView 편집한 레코드에 대 한 새 제품 이름을 표시 하는 미리 편집 모드를 반환 합니다.

두 번째 브라우저 창에서 제품 이름 원래 값으로 나감) (않음 가격을 변경 하 고 업데이트를 클릭 합니다. 다시 게시 될 눈금의 미리 편집 모드를 반환 하지만 가격에 대 한 변경 기록 되지 않습니다. 두 번째 브라우저 이전 가격이 새 제품 이름 첫 번째 것과 동일한 값을 보여줍니다. 두 번째 브라우저 창에서 변경한 내용을 손실 되었습니다. 또한 변경 내용이 손실 자동 모드로 대신을 예외 또는 동시성 위반을 방금 발생 했음을 나타내는 메시지가 없습니다.


[![두 번째 브라우저 창에서 변경 내용을 자동으로 손실 되었습니다.](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image7.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image11.png)

**그림 7**: The 변경에는 두 번째 브라우저 창을 자동으로 손실 된 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image12.png))


두 번째 브라우저의 변경 내용이 커밋 이유 이유 때문에는 `UPDATE` 문이의 `WHERE` 절 모든 레코드를 필터링 및 따라서 모든 행에 영향을 주지 않습니다. 살펴보고 s는 `UPDATE` 문을 다시:


[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample10.sql)]

별도 브라우저 창이 레코드를 업데이트 하는 경우 원래 제품 이름에서 지정 된 `WHERE` (첫 번째 브라우저에서 변경 된) 이후 기존 제품 이름의 절 대상이 t 일치를 합니다. 따라서 문을 `[ProductName] = @original_ProductName` False를 반환 및 `UPDATE` 모든 레코드는 영향을 주지 않습니다.

> [!NOTE]
> 삭제 동일한 방식으로 작동 합니다. 두 개의 브라우저 창을 열고, 하나로, 특정된 제품을 편집 하 고 변경 내용을 저장 하 여 시작 합니다. 변경 내용을 하나의 브라우저에을 저장 한 후 다른 동일한 제품에 대 한 삭제 단추를 클릭 합니다. 원래 값 don t와 일치 하므로 `DELETE` 문이의 `WHERE` 절을 delete 자동으로 실패 합니다.


두 번째 브라우저 창에서 최종 사용자의 관점에서 업데이트 단추를 클릭 한 후 모눈 미리 편집 모드를 반환 하지만 해당 변경 내용이 손실 되었습니다. 그러나 여기서 s 자신의 변경 내용을 않았음에도 t 스티커 시각적 알 수 없습니다. 이상적으로 사용자 s 변경이 동시성 위반을 손실 했습니다 d 알려 서 and, 표 편집 모드에 유지 합니다. 이 수행 하는 방법에 대해 s를 사용 합니다.

## <a name="step-3-determining-when-a-concurrency-violation-has-occurred"></a>3 단계: 동시성 위반이 발생 했을 때 결정

변경 내용이 하나를 취소 하는 동시성 위반을, 때문에 동시성 위반이 발생 했을 때 사용자에 게 경고할 좋을 것입니다. 사용자에 게 경고할 let s 라는 페이지의 맨 위에 레이블을 웹 컨트롤을 추가 `ConcurrencyViolationMessage` 인 `Text` 속성에는 다음과 같은 메시지가 표시 됩니다: 업데이트 하거나 다른 사용자가 동시에 업데이트 된 레코드를 삭제 하려고 했습니다. 다른 사용자의 변경 내용을 검토 한 다음 업데이트를 다시 실행 하거나 삭제 하십시오. Label 컨트롤 s 설정 `CssClass` 에 정의 된 속성 경고는 CSS 클래스를을 `Styles.css` 빨간색, 기울임꼴, 굵은 글꼴, 및 큰 글꼴로 텍스트를 표시 하 합니다. 마지막으로, s 레이블 설정 `Visible` 및 `EnableViewState` 속성을 `false`합니다. 이렇게 하면 명시적으로 설정할 포스트백에만 제외 하 고 레이블이 숨겨집니다 해당 `Visible` 속성을 `true`합니다.


[![경고를 표시 하려면 페이지에 Label 컨트롤 추가](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image8.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image13.png)

**그림 8**: 경고를 표시 하려면 페이지에 Label 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image14.png))


업데이트 또는 삭제, GridView s 수행할 때 `RowUpdated` 및 `RowDeleted` 이벤트 처리기를 해당 데이터 소스 컨트롤이 요청 된 업데이트 또는 삭제를 수행한 후 발생 합니다. 행의 수가 이러한 이벤트 처리기에서 작업에 의해 영향을 확인할 수 있습니다. 0 개의 행을 영향을 표시 하려면 원하는 `ConcurrencyViolationMessage` 레이블.

모두에 대 한 이벤트 처리기를 만들고는 `RowUpdated` 및 `RowDeleted` 이벤트를 다음 코드를 추가 합니다.


[!code-csharp[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample11.cs)]

두 이벤트 처리기에서 확인는 `e.AffectedRows` 속성 및 0 이면 설정는 `ConcurrencyViolationMessage` 레이블 s `Visible` 속성을 `true`합니다. 에 `RowUpdated` 이벤트 처리기도 하도록 지시를 설정 하 여 편집 모드에 유지 GridView는 `KeepInEditMode` 속성을 true로 합니다. 이 과정에서 다른 s 사용자 데이터를 편집 하는 인터페이스에 로드 되도록 표에 데이터를 다시 바인딩할 필요 합니다. GridView s 호출 하 여 이렇게 `DataBind()` 메서드.

그림 9와 같이 이러한 두 개의 이벤트 처리기와 동시성 위반이 발생할 때마다 증가 메시지가 표시 됩니다.


[![동시성 위반을 한 경우에도 메시지가 표시 됩니다.](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image9.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image15.png)

**그림 9**: A 메시지가 동시성 위반이 발생 한 경우에도 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image16.png))


## <a name="summary"></a>요약

웹 응용 프로그램을 만들 때 위치, 여러 동시 사용자가 편집 하 고 동일한 데이터를 반드시 동시성 제어 옵션을 고려해 야 합니다. 기본적으로 웹을 제어 하는 ASP.NET 데이터 및 데이터 소스 제어를 사용 하지 않는 모든 동시성 제어 합니다. 이 자습서에서 살펴본 것 처럼 SqlDataSource로 낙관적 동시성 제어를 구현는 비교적 빠르고 간단 합니다. SqlDataSource augmented 사용자 추가 대 한는 legwork 대부분 처리 `WHERE` 는 자동으로 생성 하는 절 `UPDATE` 및 `DELETE` 했지만 문은 처리에 몇 가지 미묘한 `NULL` 에 설명 된 대로 열을 값의 올바르게 처리 `NULL` 섹션 값입니다.

SqlDataSource 검사 하 여으로이 자습서를 마칩니다. 나머지 자습서 우리의 ObjectDataSource 및 계층화 된 아키텍처를 사용 하 여 데이터 작업을 반환 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](inserting-updating-and-deleting-data-with-the-sqldatasource-cs.md)
> [다음](querying-data-with-the-sqldatasource-control-vb.md)
