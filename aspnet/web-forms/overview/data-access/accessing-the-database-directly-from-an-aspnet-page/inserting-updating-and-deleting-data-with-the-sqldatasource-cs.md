---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-cs
title: 삽입, 업데이트 및 SqlDataSource (C#)를 사용 하 여 데이터를 삭제 합니다. | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서 삽입, 업데이트 및 데이터 삭제에 대 한 ObjectDataSource 컨트롤을 허용 하는 방법을 알게 되었습니다. SqlDataSource 컨트롤 지원 t...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2007
ms.topic: article
ms.assetid: a526f0ec-779e-4a2b-a476-6604090d25ce
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: b3037cfdc9a6b27b1f87e0b323b9ae59235cc27c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37385812"
---
<a name="inserting-updating-and-deleting-data-with-the-sqldatasource-c"></a>삽입, 업데이트 및 SqlDataSource (C#)를 사용 하 여 데이터를 삭제 합니다.
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_49_CS.exe) 또는 [PDF 다운로드](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/datatutorial49cs1.pdf)

> 이전 자습서에서 삽입, 업데이트 및 데이터 삭제에 대 한 ObjectDataSource 컨트롤을 허용 하는 방법을 알게 되었습니다. SqlDataSource 컨트롤 같은 연산을 지원 하지만 방법은 다른 및이 자습서에서는 삽입, 업데이트 및 데이터를 삭제 하려면 SqlDataSource를 구성 하는 방법을 보여 줍니다.


## <a name="introduction"></a>소개

에 설명 된 대로 [An 개요의 삽입, 업데이트 및 삭제](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)GridView 컨트롤 기본 제공 업데이트를 제공 하며 함께 삽입 FormView 및 DetailsView 컨트롤을 포함 하는 동안 삭제 기능을 지원 합니다. 편집 및 삭제 기능입니다. 이러한 데이터 수정 기능 쓸 필요 없이 코드 줄을 하지 않고 데이터 소스 컨트롤에 직접 연결할 수 있습니다. [개요의 삽입, 업데이트 및 삭제](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) ObjectDataSource를 사용 하 여 삽입, 업데이트 및 GridView, DetailsView 및 FormView 컨트롤을 사용 하 여 삭제를 용이 하 게 검사 합니다. 또는, SqlDataSource ObjectDataSource 대신 사용할 수 있습니다.

삽입, 업데이트 및 ObjectDataSource에서는 필요한 삽입을 수행 하기 위해 호출 하 여 개체 계층 메서드를 지정 하려면 업데이트 또는 삭제 작업을 사용 하 여 삭제를 지원 하려면을 기억 하십시오. SqlDataSource를 사용 하 여 제공 해야 `INSERT`, `UPDATE`, 및 `DELETE` SQL 문 또는 저장된 프로시저 실행 합니다. 이 자습서에서 살펴보겠지만 이러한 문을 수동으로 만들 수 있습니다 또는 SqlDataSource의 데이터 소스 구성 마법사에서 자동으로 생성할 수 있습니다.

> [!NOTE]
> 이후로 ve 설명한 삽입, 편집 및 삭제 DetailsView GridView의 기능 및 FormView 컨트롤,이 자습서는 이러한 작업을 지 원하는 SqlDataSource 컨트롤 구성 중점을 합니다. 사용 방법을 복습 GridView, DetailsView 및 FormView 돌아갑니다 편집, 삽입, 및 데이터 삭제 자습서에서 이러한 기능을 구현 해야 할 경우부터 [An 개요의 삽입, 업데이트 및 삭제](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)합니다.


## <a name="step-1-specifyinginsertupdate-anddeletestatements"></a>1 단계: 지정`INSERT`하십시오`UPDATE`, 및`DELETE`문

대로 ve 해야 SqlDataSource 컨트롤에서 데이터를 검색할 지난 두 자습서 에서처럼 두 속성을 설정 합니다.

1. `ConnectionString`무엇을 하는 쿼리를 보내는 데이터베이스를 지정 하 고
2. `SelectCommand`를 임시 SQL 문 또는 저장된 프로시저 결과를 반환할 실행 이름을 지정 합니다.

에 대 한 `SelectCommand` 매개 변수를 사용 하 여 값, 값 SqlDataSource s를 통해 지정 된 매개 변수 `SelectParameters` 컬렉션 하드 코드 된 값을 일반 매개 변수 원본 값을 포함할 수 있습니다 (쿼리 문자열 필드에 세션 변수를 웹 컨트롤 값 및 등등)에서 또는 프로그래밍 방식으로 할당할 수 있습니다. SqlDataSource s를 제어 하는 경우 `Select()` 메서드 프로그래밍 방식으로 또는 자동으로 데이터 웹 컨트롤에서에서 데이터베이스에 연결 되어, 매개 변수 값 쿼리에 할당 되 고 명령에 해제 shuttled 되는 데이터베이스입니다. S 컨트롤의 값에 따라 데이터 집합 또는 DataReader 결과 다음 반환 `DataSourceMode` 속성입니다.

데이터 선택, 함께 SqlDataSource 컨트롤 수를 삽입, 업데이트 및 제공 하 여 데이터를 삭제 `INSERT`, `UPDATE`, 및 `DELETE` 비슷하게에서 SQL 문입니다. 할당 하기만 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성을 `INSERT`를 `UPDATE`, 및 `DELETE` SQL 문을 실행 합니다. (로 항상 가장) 문을 매개 변수를 사용할 경우에 포함할 합니다 `InsertParameters`, `UpdateParameters`, 및 `DeleteParameters` 컬렉션입니다.

한 번을 `InsertCommand`, `UpdateCommand`, 또는 `DeleteCommand` 값 지정 된 경우, 해당 데이터 웹 컨트롤 s 스마트 태그의에서 삽입을 사용 하도록 설정, 사용 하도록 설정 편집 또는 삭제 사용 옵션을 사용할 수 있게 됩니다. Let s이 예의 예제를 수행 합니다 `Querying.aspx` 에서 만든 페이지를 [SqlDataSource 컨트롤을 사용 하 여 데이터 쿼리](querying-data-with-the-sqldatasource-control-cs.md) 자습서를 포함 하도록 삭제 기능 보강 하 여 합니다.

열어서 시작 합니다 `InsertUpdateDelete.aspx` 하 고 `Querying.aspx` 에서 페이지를 `SqlDataSource` 폴더. 디자이너에서 합니다 `Querying.aspx` 페이지에서 첫 번째 예제에서 SqlDataSource 및 GridView를 선택 (합니다 `ProductsDataSource` 및 `GridView1` 컨트롤). 두 컨트롤을 선택한 후 편집 메뉴 및 복사를 선택 (또는 Ctrl + C를 누르면 방금). 디자이너를 이동한 다음 `InsertUpdateDelete.aspx` 컨트롤에 붙여넣습니다. 두 개의 이동한 후 `InsertUpdateDelete.aspx`, 브라우저에서 페이지를 테스트 합니다. 값을 표시 합니다 `ProductID`, `ProductName`, 및 `UnitPrice` 열에 있는 레코드의 모든를 `Products` 데이터베이스 테이블.


[![모든 제품이 나열 된 ProductID에 따라 정렬](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image1.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image1.png)

**그림 1**: 모든 제품이 나열 된 정렬할 `ProductID` ([클릭 하 여 큰 이미지 보기](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image2.png))


## <a name="adding-the-sqldatasource-sdeletecommandanddeleteparametersproperties"></a>SqlDataSource s 추가`DeleteCommand`고`DeleteParameters`속성

SqlDataSource에서 레코드를 모두 반환 하는 것이 시점에서 `Products` 테이블 및이 데이터를 렌더링 하는 GridView입니다. 목표는 GridView 통해 제품을 삭제할 수 있도록이 예제를 확장 하는 것입니다. SqlDataSource 컨트롤 s에 대 한 값을 지정 해야이 위해 `DeleteCommand` 및 `DeleteParameters` 속성 한 다음 삭제를 지원 하려면 GridView를 구성 합니다.

합니다 `DeleteCommand` 및 `DeleteParameters` 속성 다양 한 방법으로 지정할 수 있습니다.

- 선언적 구문을 통해
- 디자이너에서 속성 창에서
- 지정 된 SQL 문이나 저장된 프로시저를 사용자 지정 화면에서 데이터 소스 구성 마법사
- 보기 화면에서 데이터 소스 구성 마법사의 테이블에서 열 지정에서에서 고급 단추를 통해는 실제로 자동으로 생성 됩니다는 `DELETE` 에서 사용 되는 SQL 문 및 매개 변수 컬렉션을 `DeleteCommand` 및 `DeleteParameters` 속성

자동으로 포함 하는 방법을 살펴보겠습니다는 `DELETE` 2 단계에서에서 만든 문입니다. 이제 데이터 소스 구성 마법사 또는 선언적 구문 옵션 작동할 것도 가능 하지만 디자이너에서 속성 창을 사용 하 여 s 수 있습니다.

디자이너에서 `InsertUpdateDelete.aspx`를 클릭 합니다 `ProductsDataSource` SqlDataSource 및 속성 창을 표시 한 다음 (보기 메뉴에서 속성 창을 선택 하거나 f4 키를 누르면 됩니다). 줄임표의 집합을 가져오는 DeleteQuery 속성을 선택 합니다.


![속성 창에서 DeleteQuery 속성을 선택 합니다.](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image2.gif)

**그림 2**: DeleteQuery 속성이 속성 창에서 선택


> [!NOTE]
> SqlDataSource 만들어지고 t DeleteQuery 속성을 가집니다. 아니라 DeleteQuery 결합 한 것을 `DeleteCommand` 및 `DeleteParameters` 속성 및 디자이너를 통해 창을 표시 하는 경우 속성 창에 나열만 됩니다. 소스 뷰에서 속성 창에서 찾으려는 경우 있습니다를 `DeleteCommand` 속성 대신 합니다.


명령 및 매개 변수 편집기 대화 상자를 표시 DeleteQuery 속성에서 줄임표 상자 (그림 3 참조)를 클릭 합니다. 이 대화 상자에서 지정할 수 있습니다는 `DELETE` SQL 문의 매개 변수를 지정 합니다. 다음 쿼리를 입력 합니다 `DELETE` 명령 텍스트 상자에 붙여넣습니다 (하거나 수동으로 또는 원하는 경우 쿼리 작성기를 사용 하 여):

[!code-sql[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/samples/sample1.sql)]

다음으로, 추가할 매개 변수 새로 고침 단추를 클릭 합니다 `@ProductID` 아래 매개 변수 목록에 매개 변수입니다.


[![속성 창에서 DeleteQuery 속성을 선택 합니다.](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image3.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image3.png)

**그림 3**: DeleteQuery 속성이 속성 창에서 선택 ([큰 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image4.png))


수행할 *되지* 이 매개 변수 (의 매개 변수는 원본 위치 없음 상태로 유지 함)에 대 한 값을 제공 합니다. GridView에 삭제 지원을 추가 하기 면 GridView는 자동으로 적용이 매개 변수 값의 값을 사용 하 여 해당 `DataKeys` 있는 삭제 단추를 클릭 한 행에 대 한 컬렉션입니다.

> [!NOTE]
> 사용 되는 매개 변수 이름 합니다 `DELETE` 쿼리 *해야 합니다* 의 이름이 같을 수는 `DataKeyNames` GridView, DetailsView 또는 FormView 값. 즉, 매개 변수를 `DELETE` 문을 의도적으로 이름이 `@ProductID` (대신 예를 들어, `@ID`) 이므로 Products 테이블 (및 따라서 GridView DataKeyNames 값)의 기본 키 열 이름이 `ProductID`합니다.


경우 매개 변수 이름 및 `DataKeyNames` 값 만들어지고 t 일치 하는 GridView 할당할 수 없습니다 자동으로 매개 변수에서 값을 `DataKeys` 컬렉션입니다.

명령 및 매개 변수 편집기 대화 상자에는 삭제 관련 정보를 입력 한 후 확인을 클릭 하 고 결과 선언적 태그를 검사 하 여 원본 뷰로 이동:

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/samples/sample2.aspx)]

추가 된 `DeleteCommand` 속성 뿐만 `<DeleteParameters>` 섹션과 명명 된 매개 변수 개체 `productID`합니다.

## <a name="configuring-the-gridview-for-deleting"></a>삭제 하기 위한 GridView 구성

사용 하 여는 `DeleteCommand` 속성이 추가 GridView가 스마트 태그는 이제 삭제 사용 옵션을 포함 합니다. 계속 해 서이 확인란을 선택 합니다. 에 설명 된 대로 [는 개요의 삽입, 업데이트 및 삭제](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)를 사용 하 여 CommandField 추가할 GridView이로 인해 해당 `ShowDeleteButton` 속성이로 설정 `true`합니다. 그림 4에서는, 브라우저를 통해 해당 페이지를 방문 하는 경우 처럼 삭제 단추가 포함 됩니다. 일부 제품을 삭제 하 여이 페이지 출력을 테스트 합니다.


[![각 GridView 행에는 이제 삭제 단추](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image4.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image5.png)

**그림 4**: 각 GridView 행에는 이제 삭제 단추가 포함 됩니다 ([큰 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image6.png))


삭제 단추를 클릭 하면 포스트백이 발생할 GridView 할당 합니다 `ProductID` 매개 변수 값의 합니다 `DataKeys` 해당 삭제 단추 클릭 되었는지 및 SqlDataSource s 호출 행의 컬렉션 값 `Delete()` 메서드. SqlDataSource 컨트롤에서 그런 다음 데이터베이스에 연결 하 고 실행 된 `DELETE` 문입니다. GridView는 SqlDataSource를 다시 시작 하 고 (포함 하는 더 이상만 삭제 된 레코드) 제품의 현재 집합을 표시 하려면 다음 다시 바인딩합니다.

> [!NOTE]
> GridView를 사용 하므로 해당 `DataKeys` SqlDataSource 매개 변수를 채울 컬렉션입니다이 중요 한 s는 GridView s `DataKeyNames` 하 고 기본 키를 구성 하는 열에 속성을 설정할 수 SqlDataSource의 `SelectCommand` 반환 이러한 열입니다. 또한 해당가 SqlDataSource에서 매개 변수 이름을 지정 하는 중요 `DeleteCommand` 로 설정 된 `@ProductID`합니다. 경우는 `DataKeyNames` 속성이 설정 되어 있지 않거나 매개 변수 이름이 지정 되지 않은 `@ProductsID`삭제 단추를 클릭 하면 포스트백을 되지만 획득된 t 실제로 모든 레코드를 삭제 합니다.


그림 5이 상호이 작용을 그래픽으로 보여 줍니다. 다시 참조를 [삽입, 업데이트 및 삭제와 관련 된 이벤트 검사](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md) 삽입, 업데이트 및 데이터 웹 컨트롤에서에서 삭제와 관련 된 이벤트 체인에 더 자세히 알아보려면 자습서입니다.


![SqlDataSource s delete () 메서드를 호출 하는 GridView에서 삭제 단추를 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image5.gif)

**그림 5**: SqlDataSource s를 호출 하는 GridView에서 삭제 단추를 클릭 `Delete()` 메서드


## <a name="step-2-automatically-generating-theinsertupdate-anddeletestatements"></a>2 단계: 자동으로 생성 합니다`INSERT`,`UPDATE`, 및`DELETE`문

검사 1 단계와 `INSERT`, `UPDATE`, 및 `DELETE` 속성 창이 나 컨트롤 s 선언적 구문을 통해 SQL 문을 지정할 수 있습니다. 그러나이 접근 방식에서는 수동으로 작성 SQL 문을 직접 단조로운 하 고 오류가 발생할 수 있습니다. 데이터 소스 구성 마법사가 하는 옵션을 제공 하는 다행 스럽게도 합니다 `INSERT`, `UPDATE`, 및 `DELETE` 보기 화면의 테이블에서 열 지정을 사용 하는 경우 자동으로 생성 하는 문입니다.

가이 자동 생성 옵션을 탐색할 수 있습니다. 디자이너는 DetailsView 추가할 `InsertUpdateDelete.aspx` 설정 및 해당 `ID` 속성을 `ManageProducts`입니다. 그런 다음 DetailsView가 스마트 태그에서 라는 SqlDataSource를 만들고 새 데이터 원본을 만들려면 선택 `ManageProductsDataSource`합니다.


[![ManageProductsDataSource 라는 새 SqlDataSource 만들기](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image6.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image7.png)

**그림 6**: 명명 된 새 SqlDataSource 만들려면 `ManageProductsDataSource` ([클릭 하 여 큰 이미지 보기](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image8.png))


데이터 소스 구성 마법사에서 사용 하도록 선택 된 `NORTHWINDConnectionString` 연결 문자열 하 고 다음을 클릭 합니다. Select 문 화면 구성에서 선택한 테이블 또는 뷰 라디오 단추에서 지정 열을 그대로 두고 및 선택은 `Products` 드롭 다운 목록에서 테이블입니다. 선택 된 `ProductID`, `ProductName`를 `UnitPrice`, 및 `Discontinued` 확인란 목록에서 열.


[![ProductID, ProductName, UnitPrice, 및 지원 되지 않는 열을 반환할 Products 테이블 사용](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image7.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image9.png)

**그림 7**:를 사용 하 여는 `Products` 테이블을 반환 합니다 `ProductID`, `ProductName`를 `UnitPrice`, 및 `Discontinued` 열 ([큰 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image10.png))


자동으로 생성 `INSERT`, `UPDATE`, 및 `DELETE` 선택한 테이블 및 열을 기반으로 하는 문을 고급 단추를 클릭 하 고 생성을 확인 `INSERT`를 `UPDATE`, 및 `DELETE` 문 확인란을 선택 합니다.


![확인란 삽입 생성, 업데이트 및 삭제 문을 확인 합니다.](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image8.gif)

**그림 8**: 생성 확인 `INSERT`를 `UPDATE`, 및 `DELETE` 문을 확인란


생성 `INSERT`, `UPDATE`, 및 `DELETE` 문을 확인란 수 들면 선택한 테이블에 기본 키 및 기본 키 열 (또는 열)은 반환 된 열 목록에 포함 됩니다. 사용 하 여 낙관적 동시성 확인란을 선택할 수 있게 하는 한 번 생성 `INSERT`, `UPDATE`, 및 `DELETE` 문을 확인란이 선택 되어 보강 됩니다 합니다 `WHERE` 결과 절 `UPDATE` 및 `DELETE` 낙관적 동시성 제어를 제공 하는 문입니다. 이제 둡니다이 확인란을 선택 취소 합니다. 다음 자습서에서 SqlDataSource 컨트롤을 사용 하 여 낙관적 동시성을 검사 합니다.

생성을 확인 한 후 `INSERT`, `UPDATE`, 및 `DELETE` 문 확인란을 Select 문 구성 화면으로 돌아간 후 다음을 클릭 확인 클릭 하 고 완료 한 후 데이터 소스 구성 마법사를 완료 합니다. 마법사를 완료 하면 Visual Studio 추가할 BoundFields에 대 한 DetailsView 합니다 `ProductID`, `ProductName`, 및 `UnitPrice` 열과에 대 한 CheckBoxField는 `Discontinued` 열입니다. 이 페이지를 방문 하는 사용자는 제품을 단계별로 실행할 수 있도록 DetailsView가 스마트 태그에서 페이징 사용 옵션을 확인 합니다. 또한 DetailsView s 지울 `Width` 고 `Height` 속성입니다.

스마트 태그에 삽입을 사용 하도록 설정, 사용 하도록 설정 편집 및 삭제 사용 옵션을 사용할 수 있는지 확인 합니다. SqlDataSource에 대 한 값을 포함 하기 때문에이 해당 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand`처럼 선언적 구문을 보여 줍니다.

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/samples/sample3.aspx)]

SqlDataSource 컨트롤에 자동으로 설정 된 값을 가진 하는 방법을 참고 해당 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성입니다. 참조 된 열 집합이 `InsertCommand` 하 고 `UpdateCommand` 속성에 기반한는 `SELECT` 문. 즉, 대신 *모든* 제품 열에는 `InsertCommand` 및 `UpdateCommand`에 지정 된 열만을 가지는 `SelectCommand` (적은 `ProductID`, 때문에 생략 되는 것 s는 [ `IDENTITY` 열](http://www.sqlteam.com/item.asp?ItemID=102), 편집 하는 경우 해당 값을 변경할 수 없습니다 및 삽입 하는 경우를 자동으로 할당 되는). 또한 각 매개 변수에 대해를 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 에서 해당 매개 변수는 속성을 `InsertParameters`, `UpdateParameters`, 및 `DeleteParameters` 컬렉션.

DetailsView의 데이터 수정 기능을 켜려면 삽입 사용, 편집 사용 및 삭제 사용 옵션에서 스마트 태그를 확인 합니다. 이 추가 사용 하 여 CommandField 해당 `ShowInsertButton`, `ShowEditButton`, 및 `ShowDeleteButton` 속성으로 설정 `true`합니다.

브라우저에서 페이지를 방문 하 고 편집, 삭제 및 DetailsView에 포함 된 새 단추입니다. DetailsView 각 BoundField 표시 하는 편집 모드로 설정 편집 단추를 클릭 하면 해당 `ReadOnly` 속성이 `false` (기본값) 텍스트 상자 및 확인란으로 CheckBoxField.


[![DetailsView s 기본 편집 인터페이스](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image9.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image11.png)

**그림 9**: The DetailsView s 편집 인터페이스 기본 ([큰 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image12.png))


마찬가지로, 현재 선택 된 제품 삭제 수도 있고 시스템에 새 제품을 추가할 수 있습니다. 때문를 `InsertCommand` 문을 에서만 작동 합니다 `ProductName`, `UnitPrice`, 및 `Discontinued` 열을 다른 열에도 하거나 `NULL` 또는 기본값으로 삽입 시 데이터베이스에서 할당. 와 마찬가지로 ObjectDataSource가 하는 경우는 `InsertCommand` 데이터베이스 테이블 t 있는 열 수 없습니다 `NULL` s 및 안 기본값이, SQL 오류가 발생 실행 하려고 할 때를 `INSERT` 문입니다.

> [!NOTE]
> DetailsView s 삽입 하 고 편집 인터페이스 사용자 지정 또는 유효성 검사의 부족 합니다. 유효성 검사 컨트롤을 추가 하거나 인터페이스를 사용자 지정 하는 BoundFields TemplateFields 변환 해야 합니다. 참조를 [편집 및 삽입 인터페이스에 유효성 검사 컨트롤 추가](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md) 하 고 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) 자세한 자습서입니다.


또한 염두에 업데이트 및 삭제, DetailsView는 현재 제품 s `DataKey` 만 값을 `DataKeyNames` 속성이 구성 되어 있습니다. 아무 효과도 없는 나타나면 편집 하거나 삭제 했는지를 `DataKeyNames` 속성을 설정 합니다.

## <a name="limitations-of-automatically-generating-sql-statements"></a>SQL 문을 자동으로 생성 하는 제한 사항

생성 이후에 `INSERT`, `UPDATE`, 및 `DELETE` 직접 작성 해야 하는 복잡 한 쿼리에 대 한 테이블에서 열을 선택 하는 경우에 문 옵션을 사용할 수만 `INSERT`를 `UPDATE`, 및 `DELETE` 1 단계에서에서 수행한 것과 같이 문입니다. 일반적으로 SQL `SELECT` 문을 사용 하 여 `JOIN` 표시에 하나 이상의 조회 테이블에서 데이터 다시 가져오기를 (다시 수행한 합니다 `Categories` s 테이블 `CategoryName` 제품 정보를 표시할 때 필드). 동시에, 하고자 할 수 있습니다 사용자 편집, 업데이트 또는 core 테이블로 데이터를 삽입 하도록 허용 (`Products`,이 경우).

동안 합니다 `INSERT`, `UPDATE`, 및 `DELETE` 문을 수동으로 입력할 수 있습니다,이 시간을 절약 하는 것이 좋습니다. 처음에 데이터를 방금 다시 가져오는 있도록 SqlDataSource를 설정 합니다 `Products` 테이블입니다. 자동으로 생성할 수 있도록 테이블 또는 뷰 화면에서 데이터 소스 구성 마법사가의 지정 열을 사용 합니다 `INSERT`, `UPDATE`, 및 `DELETE` 문입니다. 그런 다음 마법사를 완료 한 후 속성 창에서 SelectQuery 구성 하도록 선택 (하거나, 또는 돌아가서 데이터 소스 구성 마법사를 사용 하 여 지정 된 사용자 지정 SQL 문 또는 저장된 프로시저 옵션). 그런 다음 업데이트를 `SELECT` 포함 하도록 문을 `JOIN` 구문입니다. 이 기술은 자동으로 생성 된 SQL 문이 시간 절약 혜택을 제공 하 고 더 사용자 지정 허용 `SELECT` 문입니다.

자동으로 생성 하는 또 다른 제한은 `INSERT`, `UPDATE`, 및 `DELETE` 문을 열에는 `INSERT` 및 `UPDATE` 문을 기반으로 하 여 반환 되는 열을 `SELECT` 문. 그러나 더 많거나 적은 필드를 삽입 하거나 업데이트할 해야 합니다. 예를 들어, 2 단계에서에서 예제에서는 아마도 하고자 합니다 `UnitPrice` BoundField 읽기 전용으로 설정 합니다. 이런 경우 해당 해서는 t 나타나지는 `UpdateCommand`합니다. 또는 GridView에서 표시 되지 않는 테이블 필드의 값을 설정 하는 것이 좋겠습니다. 예를 들어, 새 추가 하는 경우 레코드 좋겠습니다는 `QuantityPerUnit` 값 TODO로 설정 합니다.

이러한 사용자 지정이 필요한 경우 속성 창, 사용자 지정 SQL 문 지정 또는 마법사에서 또는 선언적 구문을 통해 저장된 프로시저 옵션을 통해 이러한 수동으로 수행 해야 합니다.

> [!NOTE]
> 데이터의 해당 필드가 없는 매개 변수 추가 웹 컨트롤 때 이러한 매개 변수 값은 몇 가지 방식으로 값을 할당할 수 해야 하는 염두에 둡니다. 이러한 값은: 하드 코드에서 직접 합니다 `InsertCommand` 또는 `UpdateCommand`; (쿼리 문자열, 세션 상태, 페이지 및 등의 웹 컨트롤); 일부 미리 정의 된 소스에서 가져올 수 있습니다 또는 이전 자습서에서 살펴본 대로 프로그래밍 방식으로 할당할 수 있습니다.


## <a name="summary"></a>요약

순서 대로 데이터에 대 한 자신의 기본 삽입, 편집 및 삭제 기능을 활용 하려면 웹 컨트롤에 바인딩되어 있는 데이터 소스 컨트롤 이러한 기능을 제공 해야 합니다. SqlDataSource에 대 한 즉 `INSERT`, `UPDATE`, 및 `DELETE` SQL 문을에 할당 되어야 합니다는 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성입니다. 이러한 속성 및 해당 매개 변수 컬렉션 수동으로 추가 하거나 데이터 소스 구성 마법사를 통해 자동으로 생성 될 수 있습니다. 이 자습서에서는 두 가지 방법을 살펴보았습니다.

ObjectDataSource를 사용 하 여 낙관적 동시성을 사용 하 여 검사할 합니다 [낙관적 동시성 구현](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md) 자습서입니다. SqlDataSource 컨트롤 낙관적 동시성 지원도 제공 합니다. 자동으로 생성 하는 경우 2 단계에서에서 설명한 것 처럼 합니다 `INSERT`, `UPDATE`, 및 `DELETE` 문, 마법사를 사용 하 여 낙관적 동시성 옵션을 제공 합니다. 다음 자습서에서 살펴보겠지만 SqlDataSource를 사용 하 여 낙관적 동시성을 사용 하 여 수정 합니다 `WHERE` 절을 `UPDATE` 및 `DELETE` 문을 다른 열에 대 한 값을 t 데이터를 마지막으로 이후 변경 되지 않았고는 되도록 페이지에 표시 합니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](using-parameterized-queries-with-the-sqldatasource-cs.md)
> [다음](implementing-optimistic-concurrency-with-the-sqldatasource-cs.md)
