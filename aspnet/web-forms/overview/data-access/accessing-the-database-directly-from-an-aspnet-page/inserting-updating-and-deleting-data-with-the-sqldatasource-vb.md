---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-vb
title: 삽입, 업데이트 및 삭제 (VB) SqlDataSource 사용 하 여 데이터 | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서 삽입, 업데이트 및 데이터의 삭제에 대 한 ObjectDataSource 컨트롤을 허용 하는 방법을 배웠습니다. SqlDataSource 컨트롤 지원 t을 합니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2007
ms.topic: article
ms.assetid: 9673bef3-892c-45ba-a7d8-0da3d6f48ec5
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 92d195c3e1e349cd82e0625cf9a6c5a82644b5db
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="inserting-updating-and-deleting-data-with-the-sqldatasource-vb"></a>삽입, 업데이트 및 SqlDataSource (VB)를 사용 하 여 데이터를 삭제 합니다.
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_49_VB.exe) 또는 [PDF 다운로드](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/datatutorial49vb1.pdf)

> 이전 자습서에서 삽입, 업데이트 및 데이터의 삭제에 대 한 ObjectDataSource 컨트롤을 허용 하는 방법을 배웠습니다. SqlDataSource 컨트롤 같은 연산을 지원 하지만 방법은 다른 및이 자습서에서는 삽입, 업데이트 및 데이터를 삭제 하려면 SqlDataSource를 구성 하는 방법을 보여 줍니다.


## <a name="introduction"></a>소개

에 설명 된 대로 [는 개요의 삽입, 업데이트 및 삭제](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)GridView 컨트롤은 기본 제공 업데이트를 제공 하 고와 함께 DetailsView 및 FormView 제어 삽입을 포함 하는 동안 삭제 기능을 지원 합니다. 편집 및 삭제 기능입니다. 이러한 데이터 수정 기능을 기록 하는 코드의 줄이 없는 데이터 소스 제어로 직접 연결할 수 있습니다. [개요의 삽입, 업데이트 및 삭제](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) 는 ObjectDataSource를 사용 하 여 삽입, 업데이트 및 GridView, DetailsView, FormView 컨트롤을 사용 하 여 삭제를 용이 하 게 검사 합니다. 또는 SqlDataSource는 ObjectDataSource 대신 사용할 수 있습니다.

삽입, 업데이트 및 삭제, ObjectDataSource म 필요한 따라 삽입을 수행 하기 위해 호출할 개체 계층 메서드를 지정 하려면 업데이트 또는 삭제 작업을 지원 하도록 하는 점에 유의 하세요. SqlDataSource,으로 제공 해야 할 `INSERT`, `UPDATE`, 및 `DELETE` SQL 문 (또는 저장된 프로시저)를 실행 합니다. 이 자습서에서는 볼 수 있겠지만, 이러한 문을 수동으로 만들 수 있습니다 또는 SqlDataSource의 데이터 소스 구성 마법사에서 자동으로 생성 될 수 있습니다.

> [!NOTE]
> 에서는 이후 했습니다 앞에서 설명한 삽입, 편집 및 삭제는 GridView DetailsView의 기능 및 FormView 제어,이 자습서는 이러한 작업을 지 원하는 SqlDataSource 컨트롤 구성 중점을 합니다. 로 시작 하는 기술에 GridView, DetailsView, 및 FormView, 편집, 삽입, 및 데이터 삭제 자습서 돌아가기 내에서 이러한 기능을 구현 해야 할 경우 [는 개요의 삽입, 업데이트 및 삭제](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)합니다.


## <a name="step-1-specifyinginsertupdate-anddeletestatements"></a>1 단계: 지정`INSERT`,`UPDATE`, 및`DELETE`문

म으로 했습니다 해야 SqlDataSource 컨트롤에서 데이터를 검색 하려면 지난 두 자습서에서 볼 두 속성을 설정 합니다.

1. `ConnectionString`쿼리를 보낼 데이터베이스 기능을 지정 하 고
2. `SelectCommand`임시 SQL 문 또는 저장된 프로시저 실행 결과를 반환 하는 이름을 지정 합니다.

에 대 한 `SelectCommand` SqlDataSource s 통해 값이 지정 된 매개 변수, 매개 변수를 사용 하 여 값 `SelectParameters` 컬렉션 하드 코드 된 값을 일반 매개 변수 소스 값을 포함할 수 있습니다 (querystring 필드, 세션 변수 웹 컨트롤 값 및 이런 식으로) 또는 프로그래밍 방식으로 할당할 수 있습니다. SqlDataSource s를 제어 하는 경우 `Select()` 메서드 프로그래밍 방식으로 또는 자동으로 데이터 웹 컨트롤에서에서 데이터베이스에 연결 된, 매개 변수 값 쿼리에 할당 되 고 명령에 해제 shuttled는 데이터베이스입니다. 데이터 집합 또는 DataReader로 다음 결과 반환 s 컨트롤의 값에 따라 `DataSourceMode` 속성입니다.

데이터 선택, 함께 SqlDataSource 컨트롤 데 사용할 수 삽입, 업데이트 및 데이터를 제공 하 여 삭제 `INSERT`, `UPDATE`, 및 `DELETE` 거의 동일한 방법으로 SQL 문입니다. 할당 하기만 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성은 `INSERT`, `UPDATE`, 및 `DELETE` SQL 문을 실행 합니다. (항상 가장은 될 때와) 문은 매개 변수를 사용할 경우에 포함할는 `InsertParameters`, `UpdateParameters`, 및 `DeleteParameters` 컬렉션입니다.

한 번는 `InsertCommand`, `UpdateCommand`, 또는 `DeleteCommand` 값 지정 된 경우, 해당 데이터 웹 컨트롤 s 스마트 태그 삽입 사용, 사용 하도록 설정 편집 또는 삭제 사용 옵션을 사용할 수 있게 됩니다. 이 설명 하기 let s 라인의 한 예는 `Querying.aspx` 에서 만든 페이지는 [SqlDataSource 컨트롤을 사용 하 여 데이터를 쿼리](querying-data-with-the-sqldatasource-control-vb.md) 자습서 및 삭제 기능 포함 되도록 업그레이드 합니다.

열어 시작는 `InsertUpdateDelete.aspx` 및 `Querying.aspx` 에서 페이지는 `SqlDataSource` 폴더입니다. 에 디자이너에서는 `Querying.aspx` 페이지에서 첫 번째 예제에서 SqlDataSource 및 GridView 선택 (의 `ProductsDataSource` 및 `GridView1` 컨트롤). 두 컨트롤을 선택한 후 편집 메뉴로 이동 및 복사를 선택 (또는 Ctrl + C를 적중만). 다음으로 디자이너로 이동 하 여의 `InsertUpdateDelete.aspx` 컨트롤에 붙여 넣습니다. 두 개의 이동한 후 `InsertUpdateDelete.aspx`, 브라우저에서 페이지를 테스트 합니다. 값이 표시 됩니다는 `ProductID`, `ProductName`, 및 `UnitPrice` 에 있는 레코드의 모든 열은 `Products` 데이터베이스 테이블입니다.


[![모든 제품이 나열 된 제품 Id로 정렬](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image1.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image1.png)

**그림 1**: 모든 제품이 나열 된 순서로 `ProductID` ([전체 크기 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image2.png))


## <a name="adding-the-sqldatasource-sdeletecommandanddeleteparametersproperties"></a>SqlDataSource s 추가`DeleteCommand`및`DeleteParameters`속성

이 시점에서 레코드를 모두 반환 하는 SqlDataSource 했으므로 `Products` 테이블 및이 데이터를 렌더링 하는 GridView입니다. 이러한 목표 GridView 통해 제품을 삭제할 수 있도록이 예제를 연장 하는 것입니다. SqlDataSource 컨트롤 s에 대 한 값을 지정 해야이를 위해 `DeleteCommand` 및 `DeleteParameters` 속성 삭제를 지원 하 여 GridView를 구성 합니다.

`DeleteCommand` 및 `DeleteParameters` 여러 가지 방법으로 속성을 지정할 수 있습니다.

- 선언적 구문
- 디자이너에서 속성 창에서
- 지정 된 사용자 지정 SQL 문 또는 저장된 프로시저 화면에서 데이터 소스 구성 마법사
- 보기 화면에서 데이터 소스 구성 마법사의 테이블에서 열 지정에에서 대 한 고급 단추를 통해는 실제로 자동으로 생성 됩니다는 `DELETE` SQL 문 및 매개 변수 컬렉션에 사용 되는 `DeleteCommand` 및 `DeleteParameters` 속성

자동으로 포함 하는 방법을 검토는 `DELETE` 2 단계에서에서 만든 문입니다. 지금은 데이터 소스 구성 마법사 또는 선언적 구문 옵션와 마찬가지로 작동 하지만 디자이너에서 속성 창을 사용 하 여 s를 사용 합니다.

디자이너에서 `InsertUpdateDelete.aspx`, 클릭는 `ProductsDataSource` SqlDataSource 한 다음 속성 창 (보기 메뉴에서 속성 창을 선택 하거나 단순히 F4). 타원 집합이 표시 됩니다는 DeleteQuery 속성을 선택 합니다.


![속성 창에서 DeleteQuery 속성을 선택 합니다.](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image2.gif)

**그림 2**: DeleteQuery 속성은 속성 창에서 선택


> [!NOTE]
> SqlDataSource 대상이 t DeleteQuery 속성을 가집니다. DeleteQuery 결합 한 것 보다는 `DeleteCommand` 및 `DeleteParameters` 속성 디자이너를 통해 창을 볼 때 속성 창에만 나열 됩니다. 소스 뷰에서 속성 창에서 찾으려는 경우 있습니다는 `DeleteCommand` 속성 대신 합니다.


명령 및 매개 변수 편집기 대화 상자를 표시 DeleteQuery 속성에서 줄임표 상자 (그림 3 참조)를 클릭 합니다. 이 대화 상자에서 지정할 수 있습니다는 `DELETE` SQL 문의 매개 변수를 지정 하 고 있습니다. 다음 쿼리를 입력 하는 `DELETE` 명령 텍스트 상자에 붙여넣습니다 (중 하나 수동으로 또는 원하는 경우 쿼리 작성기를 사용 하 여):

[!code-sql[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample1.sql)]

다음 매개 변수 새로 고침 단추를 추가 하려면 클릭는 `@ProductID` 아래 매개 변수 목록에 매개 변수입니다.


[![속성 창에서 DeleteQuery 속성을 선택 합니다.](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image3.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image3.png)

**그림 3**: DeleteQuery 속성은 속성 창에서 선택 ([전체 크기 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image4.png))


수행 *하지* 이 매개 변수 (none 매개 변수 원본 나감)에 대 한 값을 제공 합니다. 지원을 추가 하 여 삭제 GridView에, 일단 GridView는 자동으로 적용이 매개 변수 값의 값을 사용 하 여 해당 `DataKeys` 인 삭제 단추를 클릭 한 행에 대 한 컬렉션입니다.

> [!NOTE]
> 에 사용 된 매개 변수 이름을 `DELETE` 쿼리 *해야* 의 이름과 같을 수는 `DataKeyNames` GridView, DetailsView, 또는 FormView의 값입니다. 즉, 매개 변수는 `DELETE` 문을 라는 특정 목적 `@ProductID` (대신, 예를 들어, `@ID`) Products 테이블 (및 따라서 GridView에서 DataKeyNames 값)의 기본 키 열 이름이 없으므로, `ProductID`합니다.


경우 매개 변수 이름 및 `DataKeyNames` 값 대상이 t 일치 하는 GridView 할당할 수 없습니다 자동으로 매개 변수에서 값의 `DataKeys` 컬렉션입니다.

명령 및 매개 변수 편집기 대화 상자에는 delete 관련 정보를 입력 한 후 확인을 클릭 하 고 결과 선언적 태그를 검사 하 여 원본 뷰로 이동 합니다.

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample2.aspx)]

추가 `DeleteCommand` 속성으로 `<DeleteParameters>` 섹션 및 명명 된 매개 변수 개체 `productID`합니다.

## <a name="configuring-the-gridview-for-deleting"></a>GridView를 삭제 하기 위한 구성

와 `DeleteCommand` 속성이 추가 GridView s 스마트 태그는 이제 삭제 사용 옵션을 포함 합니다. 계속 해이 확인란을 선택 합니다. 에 설명 된 대로 [는 개요의 삽입, 업데이트 및 삭제](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md),이 인해와 CommandField를 추가 하는 GridView의 `ShowDeleteButton` 속성이로 설정 `True`합니다. 그림 4에서는, 브라우저를 통해 해당 페이지를 방문 하는 경우 처럼 삭제 단추가 포함 됩니다. 일부 제품을 삭제 하 여 아웃이 페이지를 테스트 합니다.


[![각 GridView 행에는 이제 삭제 단추 포함](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image4.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image5.png)

**그림 4**: 각 GridView 행에는 이제 삭제 단추가 포함 됩니다 ([전체 크기 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image6.png))


삭제 단추를 클릭 하면 포스트백이 발생할 GridView 할당는 `ProductID` 매개 변수 값의는 `DataKeys` 행 인 삭제 단추가 클릭 되었습니다 및 SqlDataSource s 호출에 대 한 컬렉션 값 `Delete()` 메서드. SqlDataSource 컨트롤에서 그런 다음 데이터베이스에 연결 하 고 실행 된 `DELETE` 문. GridView에 SqlDataSource를 다시 시작 하 고 (포함 하는 더 이상 just 삭제 된 레코드) 제품의 현재 집합을 표시 한 다음 다시 바인딩합니다.

> [!NOTE]
> GridView 사용 하므로 해당 `DataKeys` SqlDataSource 매개 변수를 구성할 컬렉션 것 s 중요 하는 GridView s `DataKeyNames` 하 고 기본 키를 구성 하는 열에 속성을 설정할 수 SqlDataSource의 `SelectCommand` 반환 이러한 열입니다. 또한이 s SqlDataSource s에서 매개 변수 이름을 지정 하 고 중요 한 `DeleteCommand` 로 설정 된 `@ProductID`합니다. 경우는 `DataKeyNames` 속성을 설정 하지 않거나 매개 변수 이름이 지정 되지 않은 `@ProductsID`, 포스트백 삭제 단추를 클릭 하면 하지만 획득된 t 실제로 모든 레코드를 삭제 합니다.


그림 5에서는이 상호 작용을 그래픽으로 설명합니다. 다시 참조는 [삽입, 업데이트 및 삭제와 관련 된 이벤트를 검사](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb.md) 자습서에 대 한 자세한 내용은 삽입, 업데이트 및 웹 컨트롤 데이터에서 삭제와 관련 된 이벤트 체인을 합니다.


![SqlDataSource s delete () 메서드를 호출 하는 GridView에 삭제 단추를 클릭 하면](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image5.gif)

**그림 5**: SqlDataSource의 GridView에서 삭제 단추를 클릭 하면 호출 `Delete()` 메서드


## <a name="step-2-automatically-generating-theinsertupdate-anddeletestatements"></a>2 단계: 자동으로 생성 되는`INSERT`,`UPDATE`, 및`DELETE`문

검사, 단계 1로 `INSERT`, `UPDATE`, 및 `DELETE` 속성 창 또는 컨트롤 s 선언 구문을 통해 SQL 문을 지정할 수 있습니다. 그러나이 방법을 사용 해야는 수동으로 작성 SQL 문을 직접 되풀이 되 고 오류가 쉽게 발생할 수 있습니다. 데이터 소스 구성 마법사는 옵션을 제공 하는 다행히는 `INSERT`, `UPDATE`, 및 `DELETE` 문을 보기 화면의 테이블에서 열 지정을 사용 하는 경우 자동으로 생성 됩니다.

S 탐색이 자동 생성 옵션을 사용 합니다. DetailsView의 디자이너에 추가 `InsertUpdateDelete.aspx` 설정 하 고 해당 `ID` 속성을 `ManageProducts`합니다. 다음으로, DetailsView s 스마트 태그에서 새 데이터 원본을 만들고 라는 SqlDataSource 선택 `ManageProductsDataSource`합니다.


[![ManageProductsDataSource 라는 새 SqlDataSource 만들기](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image6.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image7.png)

**그림 6**: 명명 된 새 SqlDataSource 만드는 `ManageProductsDataSource` ([전체 크기 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image8.png))


데이터 소스 구성 마법사에서 사용 하기로 `NORTHWINDConnectionString` 연결 문자열을 다음을 클릭 합니다. Select 문 화면 구성에서 열 지정 선택한 테이블 또는 뷰 라디오 단추에서 그대로 두고 pick에서 `Products` 드롭 다운 목록에서 테이블입니다. 선택 된 `ProductID`, `ProductName`, `UnitPrice`, 및 `Discontinued` 확인란 목록에서 열.


[![Products 테이블을 사용 하 여, ProductID, ProductName, UnitPrice, 및 열에 지원 되지 않는 반환](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image7.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image9.png)

**그림 7**:를 사용 하 여는 `Products` 테이블에서 반환 된 `ProductID`, `ProductName`, `UnitPrice`, 및 `Discontinued` 열 ([전체 크기 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image10.png))


자동으로 생성 하려면 `INSERT`, `UPDATE`, 및 `DELETE` 고급 단추를 클릭 하 고 생성을 확인 하는 선택한 테이블 및 열을 기반으로 문을 `INSERT`, `UPDATE`, 및 `DELETE` 문 확인란을 선택 합니다.


![확인 확인란 생성 INSERT, UPDATE 및 DELETE 문](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image8.gif)

**그림 8**: 생성 확인 `INSERT`, `UPDATE`, 및 `DELETE` 문을 확인란


생성 `INSERT`, `UPDATE`, 및 `DELETE` 문을 확인란 수 선택 가능 선택한 테이블에 기본 키와 기본 키 열 (또는 열)의 반환 된 열 목록에 포함 됩니다. 선택할 수 있게 하는 사용 하 여 낙관적 동시성 확인란을 생성 한 번 `INSERT`, `UPDATE`, 및 `DELETE` 문을 확인란이 표시 되었으므로, 보강 됩니다는 `WHERE` 열리면 절 `UPDATE` 및 `DELETE` 문을 낙관적 동시성 제어를 제공 합니다. 지금은 선택이 확인란을이 선택 합니다. 다음 자습서의 SqlDataSource 컨트롤을 사용 하 여 낙관적 동시성을 검토 합니다.

생성을 확인 한 후 `INSERT`, `UPDATE`, 및 `DELETE` 문 확인란을 다음을 클릭 한 다음 Select 문 구성 화면으로 돌아가 확인 클릭 하 고 데이터 소스 구성 마법사를 완료 하려면 다음 완료 합니다. 마법사를 완료 되 면 Visual Studio에 추가 합니다 BoundFields DetailsView에 대 한는 `ProductID`, `ProductName`, 및 `UnitPrice` 열과에 대 한 CheckBoxField는 `Discontinued` 열입니다. 이 페이지를 방문 하는 사용자는 제품을 단계별로 실행할 수 있도록 DetailsView s 스마트 태그에서 페이징 사용 옵션을 선택 합니다. 또한 DetailsView s 지울 `Width` 및 `Height` 속성입니다.

스마트 태그에 삽입 사용, 사용 하도록 설정 편집 및 삭제 사용 옵션을 사용할 수 있는지 확인 합니다. SqlDataSource에 대 한 값을 포함 하기 때문에이 해당 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand`다음과 같은 선언 구문을 볼 수 있듯이,:

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/samples/sample3.aspx)]

SqlDataSource 컨트롤에 대 한 자동으로 설정 된 값을 가진 어떻게 참고 해당 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성입니다. 참조 된 열 집합이 `InsertCommand` 및 `UpdateCommand` 기반 속성이는 `SELECT` 문. 즉, 설치 하는 대신 *모든* 제품 열에는 `InsertCommand` 및 `UpdateCommand`에 지정 된 열에만는 `SelectCommand` (덜 `ProductID`, 때문에 생략 되는 것 s는 [ `IDENTITY` 열](http://www.sqlteam.com/item.asp?ItemID=102), 편집 하는 경우 값을 변경할 수 없습니다 및 삽입할 때 자동으로 할당 됨). 또한 각 매개 변수에 대해는 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성에 해당 매개 변수는 `InsertParameters`, `UpdateParameters`, 및 `DeleteParameters` 컬렉션입니다.

DetailsView의 데이터 수정 기능을 활성화 하려면 삽입 사용, 편집 사용 및 스마트 태그에서 삭제 사용 옵션을 확인 합니다. 이렇게 하면 추가와 CommandField 해당 `ShowInsertButton`, `ShowEditButton`, 및 `ShowDeleteButton` 속성으로 설정 `True`합니다.

브라우저에서 페이지를 방문 하 고 편집, 삭제 및 DetailsView에 포함 된 새 단추를 기록해 둡니다. 편집 단추를 클릭 하면 각 BoundField를 표시 하는 편집 모드로 DetailsView 설정 인 `ReadOnly` 속성이 `False` (기본값)는 텍스트 상자 및 확인란으로 CheckBoxField 합니다.


[![DetailsView s 기본 편집 인터페이스](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image9.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image11.png)

**그림 9**: The DetailsView s 기본 편집 인터페이스 ([전체 크기 이미지를 보려면 클릭](inserting-updating-and-deleting-data-with-the-sqldatasource-vb/_static/image12.png))


마찬가지로, 현재 선택 된 제품 하거나 새 제품 시스템에 추가할 수 있습니다. 이후는 `InsertCommand` 문을 에서만 작동는 `ProductName`, `UnitPrice`, 및 `Discontinued` 열을 다른 열 들어 하거나 `NULL` 또는 삽입 시 데이터베이스에 의해 할당 된 기본값입니다. 동일 하 게 ObjectDataSource를 사용 하는 경우는 `InsertCommand` 인할 열을 사용 하는 데이터베이스 테이블이 없습니다 `NULL` s 및 안은 기본값을 지정할 SQL 오류가 발생 합니다 실행 하려고 할 때는 `INSERT` 문.

> [!NOTE]
> DetailsView s 삽입 및 편집 인터페이스는 모든 종류의 사용자 지정 또는 유효성 검사 부족 합니다. 유효성 검사 컨트롤을 추가 하거나 인터페이스를 사용자 지정 하는 BoundFields TemplateFields를 변환 해야 합니다. 참조는 [편집 및 삽입 인터페이스에 유효성 검사 컨트롤 추가](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) 및 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) 자세한 정보에 대 한 자습서입니다.


또한 염두에 업데이트 및 삭제, DetailsView 사용 현재 제품 s `DataKey` 값은만 `DataKeyNames` 속성이 구성 되어 있습니다. 편집 또는 삭제에 아무런 영향을 주지으로 나타나지만, 하는 경우를 확인 하는 `DataKeyNames` 속성을 설정 합니다.

## <a name="limitations-of-automatically-generating-sql-statements"></a>자동으로 생성 되는 SQL 문의 제한 사항

생성 이후 `INSERT`, `UPDATE`, 및 `DELETE` 문 옵션은 직접 작성 해야 합니다 하면 보다 복잡 한 쿼리에 테이블에서 열을 선택 하는 경우에 사용할 수만 `INSERT`, `UPDATE`, 및 `DELETE` 1 단계에서에서 수행한 것 처럼 문입니다. 일반적으로 SQL `SELECT` 문을 사용 하 여 `JOIN` 표시 목적으로에 하나 이상의 조회 테이블에서 데이터 다시 가져오기 하려면 s (다시 가져오는 등의 `Categories` 테이블의 `CategoryName` 제품 정보를 표시할 때 필드). 같은 시간에 하고자 할 수 있습니다 사용자 편집, 업데이트 또는 핵심 테이블에 데이터를 삽입 하도록 허용 (`Products`,이 경우).

반면는 `INSERT`, `UPDATE`, 및 `DELETE` 문을 직접 입력, 다음 시간 절약 팁을 고려 합니다. 바로 데이터를 끌어와 다시 있도록 SqlDataSource를 처음 설치는 `Products` 테이블입니다. 자동으로 생성할 수 있도록 테이블 또는 뷰 화면에서 데이터 소스 구성 마법사의 지정 열을 사용 하 여는 `INSERT`, `UPDATE`, 및 `DELETE` 문. 그런 다음 마법사를 완료 한 후 속성 창에서 SelectQuery 구성 하도록 선택 하거나, 또는 데이터 소스 구성 마법사를 사용 하 여 지정 된 사용자 지정 SQL 문 또는 저장된 프로시저 옵션으로 다시 돌아가십시오. 그런 다음 업데이트는 `SELECT` 포함 하도록 문을 `JOIN` 구문입니다. 이 기술은 자동으로 생성 된 SQL 문 시간 절약 같은 이점을 제공 하 고 추가 사용자 지정 된 허용 `SELECT` 문.

자동으로 생성의 또 다른 제한은 `INSERT`, `UPDATE`, 및 `DELETE` 문에 열에는 `INSERT` 및 `UPDATE` 문을 기반으로 하 여 반환 되는 열은 `SELECT` 문. 그러나 더 많거나 적은 필드를 삽입 하거나 업데이트할 해야 할 수 있습니다. 예를 들어 2 단계에서에서 예에서 필요할 수 있어야는 `UnitPrice` BoundField 읽기 전용 이어야 합니다. 이 경우 그 이내에 사용 해야 t에 표시는 `UpdateCommand`합니다. 또는 GridView에 표시 되지 않는 테이블 필드의 값을 설정할 수 있습니다. 예를 들어, 새 추가 하는 경우 레코드 좋겠습니다는 `QuantityPerUnit` 값 TODO로 설정 합니다.

이러한 사용자 지정이 필요한 경우 속성 창, 지정 된 사용자 지정 SQL 문 또는 저장된 프로시저 옵션 마법사에서 또는 선언적 구문을 통해을 수동으로 수행 해야 합니다.

> [!NOTE]
> 데이터의 해당 필드를 갖지 않는 매개 변수 추가 웹 컨트롤을 하는 경우 이러한 매개 변수 값에서 특정 방식으로 값이 할당 되어야 할 염두에서에 둬야 합니다. 이러한 값은 가능: 하드 코드에서 직접는 `InsertCommand` 또는 `UpdateCommand`; (쿼리 문자열, 세션 상태, 페이지, 및 등 웹 컨트롤); 미리 정의 된 일부 소스에서 가져올 수 있습니다 또는 이전 자습서에서 살펴본 것 처럼 프로그래밍 방식으로 할당할 수 있습니다.


## <a name="summary"></a>요약

데이터의 기본 제공 삽입, 편집 및 삭제 기능을 활용 하 여 웹 컨트롤을 위해 데이터 소스 제어에 바인딩되어 있는 해당 기능을 제공 해야 합니다. SqlDataSource에 대 한 즉 `INSERT`, `UPDATE`, 및 `DELETE` SQL 문을에 할당 되어야 합니다는 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성입니다. 이러한 속성과 해당 매개 변수 컬렉션을 수동으로 추가 하거나 데이터 소스 구성 마법사를 통해 자동으로 생성 수 있습니다. 이 자습서에서는 두 가지 방법을 모두 검사 했습니다.

ObjectDataSource에서 낙관적 동시성 사용을 검사 했습니다는 [낙관적 동시성 구현](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md) 자습서입니다. SqlDataSource 컨트롤에는 또한 낙관적 동시성 지원을 제공합니다. 자동으로 생성 하는 경우 2 단계에서에서 설명한 것 처럼는 `INSERT`, `UPDATE`, 및 `DELETE` 문, 마법사 사용 하 여 낙관적 동시성 옵션을 제공 합니다. 다음 자습서에서 볼 수 있겠지만, SqlDataSource로 낙관적 동시성을 사용 하 여 수정는 `WHERE` 절에는 `UPDATE` 및 `DELETE` 문을 다른 열에 대 한 값 데이터를 마지막 이후 변경 t 않은 있는지 확인 하십시오. 페이지에 표시 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](using-parameterized-queries-with-the-sqldatasource-vb.md)
> [다음](implementing-optimistic-concurrency-with-the-sqldatasource-vb.md)
