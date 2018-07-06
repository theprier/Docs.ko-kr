---
uid: web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs
title: 데이터베이스 수정 (C#) 트랜잭션 내에서 줄 바꿈 | Microsoft Docs
author: rick-anderson
description: 이 자습서는 4 개 업데이트, 삭제 및 데이터의 일괄 처리 삽입에 보이는 첫 번째입니다. 이 자습서에서는 데이터베이스 트랜잭션을 사용 하는 방법 알아보기...
ms.author: aspnetcontent
ms.date: 06/26/2007
ms.assetid: b45fede3-c53a-4ea1-824b-20200808dbae
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs
msc.type: authoredcontent
ms.openlocfilehash: a87ba758abd6b3e89be4f5aa64d658b734f99d9e
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37810931"
---
<a name="wrapping-database-modifications-within-a-transaction-c"></a>트랜잭션 (C#) 내에서 래핑된 데이터베이스 수정
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_63_CS.zip) 또는 [PDF 다운로드](wrapping-database-modifications-within-a-transaction-cs/_static/datatutorial63cs1.pdf)

> 이 자습서는 4 개 업데이트, 삭제 및 데이터의 일괄 처리 삽입에 보이는 첫 번째입니다. 이 자습서에서는 데이터베이스 트랜잭션을 모든 단계가 성공 하거나 모든 단계가 실패 하면 원자 단위 연산으로 수행 하도록 일괄 처리 수정이 허용 하는 방법을 알아봅니다.


## <a name="introduction"></a>소개

부터 살펴본 것 처럼 합니다 [An 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) 자습서에서는 GridView는 행 수준 편집 및 삭제에 대 한 기본 제공 지원의 제공 합니다. 몇 번의 마우스 클릭으로 콘텐츠를 편집 하 고 행 단위로에서 삭제 하는 코드 줄도 작성 하지 않고 다양 한 데이터 수정 인터페이스를 만들 가능성이 있습니다. 그러나 특정 시나리오에서이 부족 하 고 편집 하거나 삭제할 레코드의 일괄 처리 하는 기능을 사용 하 여 사용자에 게 제공 해야 합니다.

예를 들어, 대부분의 웹 기반 전자 메일 클라이언트 그리드를 사용 각 메시지를 나열 하려면 각 행 (제목, 보낸 사람 등) 전자 메일 s 정보와 확인란을 포함 하는 위치입니다. 이 인터페이스는 검사 하 고 선택한 메시지 삭제 단추를 클릭 하 여 여러 메시지를 삭제 하려면 사용자를 허용 합니다. 인터페이스를 편집 하는 일괄 처리를 여러 다른 레코드에 사용자가 일반적으로 편집 하는 경우에 적합 합니다. 사용자가 클릭을 요구 하는 대신 편집 해당 변경 및 수정 해야 하는 각 레코드에 대 한 업데이트를 클릭, 인터페이스를 편집 하는 일괄 처리의 편집 인터페이스를 사용 하 여 각 행을 렌더링 합니다. 사용자는 신속 하 게 변경 해야 하는 행 집합을 수정 하 고 업데이트 모든 단추를 클릭 하 여 이러한 변경 내용을 저장 수 있습니다. 이 자습서 집합 삽입, 편집 및 삭제 데이터의 일괄 처리에 대 한 인터페이스를 만드는 방법을 살펴보겠습니다.

일괄 처리 작업을 수행 하는 경우 해당 실패 해야 할지 가능 하지만 일부 성공 하려면 일괄 처리의 작업에 대 한 확인 해야 합니다. 인터페이스-실패 한 경우 첫 번째 선택한 레코드가 성공적으로 삭제 되는 두 번째, 예를 들어 외래 키 제약 조건 위반으로 인해 어떻게 삭제 일괄 처리를 것이 좋습니다. 첫 번째 레코드의 삭제 롤백해야 또는 첫 번째 레코드가 삭제 된 상태로 유지 하는 데 허용 되는?

일괄 처리 작업으로 처리 하려는 경우는 [원자 단위 연산](http://en.wikipedia.org/wiki/Atomic_operation), 여기서 중 하나 단계가 모두 성공 또는 실패의 모든 단계 다음 데이터 액세스 계층에 대 한 지원을 포함 하도록 확장할 수 해야 하나 [데이터베이스 트랜잭션](http://en.wikipedia.org/wiki/Database_transaction)합니다. 데이터베이스 트랜잭션 집합에 대 한 원자성을 보장 `INSERT`, `UPDATE`, 및 `DELETE` 문을 트랜잭션의 산하 실행 되며 대부분의 모든 최신 데이터베이스 시스템이 지 원하는 기능입니다.

이 자습서에서는 데이터베이스 트랜잭션을 사용 하는 DAL을 확장 하는 방법을 살펴보겠습니다. 후속 자습서에서는 삽입, 업데이트 및 인터페이스를 삭제 하는 일괄 처리에 대 한 구현 웹 페이지를 검사 합니다. Let s 시작!

> [!NOTE]
> 일괄 처리 트랜잭션에서 데이터를 수정할 때는 항상 원자성 필요 하지 않습니다. 일부 시나리오에서는 성공 하는 일부 데이터 수정이 있을 수 있으며 경우와 같이 실패 동일한 일괄 처리의 다른 웹 기반 전자 메일 클라이언트에서 전자 메일의 집합을 삭제 합니다. 있는 s를 삭제 하 여 데이터베이스 오류 중간 처리 하는 경우 해당 s 아마도 오류 없이 처리 되는 해당 레코드 삭제 된 상태로 유지 되도록 허용 합니다. 이러한 경우 DAL 데이터베이스 트랜잭션을 지원 하도록 수정할 필요가 없습니다. 그러나 다른 시나리오가 있습니다 일괄 처리 작업, 원자성이 중요 합니다. 두 작업을 수행 해야 자신의 자금 하나의 은행 계정에서 다른 위치로 이동 하는 고객을 하는 경우: 금액을 첫 번째 계정에서 공제 하 고 두 번째에 추가 해야 합니다. 은행 첫 번째 단계 성공 하지 개의치 수 있지만 두 번째 단계 실패 고객 작업 났을 것입니다. 이 자습서를 진행 하를 사용 하 여 일괄 처리 삽입, 업데이트 및에서는 다음 세 가지 자습서에서 작성 하는 인터페이스를 삭제 하지 않으려는 경우에 데이터베이스 트랜잭션을 지원 하기 위해 DAL의 향상 된 기능을 구현 하는 것이 바랍니다.


## <a name="an-overview-of-transactions"></a>트랜잭션 개요

대부분의 데이터베이스에 대 한 지원을 포함 *트랜잭션을*, 여러 데이터베이스 명령을 단일 작업의 논리 단위를 그룹화 할 수 있도록 합니다. 트랜잭션을 구성 하는 데이터베이스 명령은 개별적으로 모든 명령이 실패 하거나 성공할 모든 되도록 보장 됩니다.

일반적으로 트랜잭션 패턴을 사용 하 여 SQL 문을 통해 구현 됩니다.

1. 트랜잭션 시작을 표시 합니다.
2. 트랜잭션을 구성 하는 SQL 문을 실행 합니다.
3. 2 단계에서 트랜잭션 롤백하고에서에서 문 중 하나에 오류가 있으면입니다.
4. 오류 없이 완료 단계 2에서 문의 모든 경우에 트랜잭션을 커밋하십시오.

커밋 및 저장 프로시저를 만들거나 SQL 스크립트를 작성할 때 트랜잭션을 수동으로 입력할 수 있습니다 롤백 또는 프로그래밍을 통해 ADO.NET 또는의 클래스 중 하나를 사용 하 여 의미 SQL 문을 만드는 데 사용 합니다 [ `System.Transactions` 네임 스페이스](https://msdn.microsoft.com/library/system.transactions.aspx)합니다. 검토할 것만이 자습서에서는 ADO.NET을 사용 하 여 트랜잭션을 관리 합니다. 이후 자습서에서 만들기, 롤백, 및 트랜잭션 커밋에 대 한 SQL 문을 이때 살펴보겠습니다 데이터 액세스 계층에서 저장된 프로시저를 사용 하는 방법을 살펴보겠습니다. 참조 그동안 [SQL Server 저장 프로시저에서 트랜잭션을 관리](http://www.4guysfromrolla.com/webtech/080305-1.shtml) 자세한 내용은 합니다.

> [!NOTE]
> 합니다 [ `TransactionScope` 클래스](https://msdn.microsoft.com/library/system.transactions.transactionscope.aspx) 에 `System.Transactions` 네임 스페이스 트랜잭션의 범위 내에서 일련의 문을 프로그래밍 방식으로 래핑할 개발자 지원 하며 여러 관련 된 복잡 한 트랜잭션에 대 한 지원 두 개의 서로 다른 데이터베이스 또는 유형이 다른 Microsoft SQL Server 데이터베이스, Oracle 데이터베이스 및 웹 서비스와 같은 데이터 저장소와 같은 원본입니다. I ve 대신이 자습서에 대 한 ADO.NET 트랜잭션을 사용 하기로 합니다 `TransactionScope` 클래스 ADO.NET 데이터베이스 트랜잭션 및 대부분의 경우에서 보다 구체적인 이므로 훨씬 덜 리소스 집약적. 또한 특정 시나리오에서의 `TransactionScope` 클래스는 MSDTC Microsoft Distributed Transaction Coordinator ()를 사용 합니다. 구성, 구현 및 성능 문제 주변 MSDTC를 사용 하면 보다 특수 한 고급 항목 및이 자습서의 범위를 벗어납니다.


트랜잭션 호출을 통해 시작 되 고 ado.net에서 SqlClient 공급자를 사용할 때는 합니다 [ `SqlConnection` 클래스](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) s [ `BeginTransaction` 메서드](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.begintransaction.aspx)를 반환 하는 [ `SqlTransaction` 개체](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.aspx)합니다. 구성 된 트랜잭션 내에서 배치 되는 데이터 수정 문을 `try...catch` 블록입니다. 문에 오류가 발생 하는 경우는 `try` 블록에 대 한 전송을 실행 합니다 `catch` 블록은 트랜잭션을 통해 다시 롤백할 수 있습니다는 `SqlTransaction` s 개체 [ `Rollback` 메서드](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.rollback.aspx). 모든 문을 성공적으로 호출을 완료 하는 경우는 `SqlTransaction` s 개체 [ `Commit` 메서드](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.commit.aspx) 끝에 `try` 블록 트랜잭션을 커밋합니다. 다음 코드 조각에서는이 패턴을 보여 줍니다. 참조 [트랜잭션 사용 하 여 데이터베이스 일관성을 유지](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx) 추가 구문 및 ADO.NET을 사용 하 여 트랜잭션을 사용 하는 예제입니다.


[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample1.cs)]

기본적으로 형식화 된 데이터 집합의 Tableadapter에 트랜잭션을 사용 하지 마십시오. 트랜잭션을 지원 하기 위해 일련의 트랜잭션 범위 내에서 데이터 수정 문 수행 하려면 위의 패턴을 사용 하는 추가 메서드를 포함 하려면 TableAdapter 클래스를 보완 해야 합니다. 2 단계에서에서 partial 클래스를 사용 하 여 이러한 메서드를 추가 하는 방법을 살펴보겠습니다.

## <a name="step-1-creating-the-working-with-batched-data-web-pages"></a>1 단계: 일괄 처리 된 데이터 웹 페이지를 사용 하 여 작업 만들기

데이터베이스 트랜잭션을 지원 하기 위해 DAL을 추가 하는 방법 탐색을 시작 하기 전에 먼저 시간을 내어이 자습서에 필요한는 ASP.NET 웹 페이지를 만들고 다음 세 가지 s 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `BatchData` 폴더를 추가한 다음 ASP.NET 페이지와 각 페이지에 연결 된 `Site.master` 마스터 페이지입니다.

- `Default.aspx`
- `Transactions.aspx`
- `BatchUpdate.aspx`
- `BatchDelete.aspx`
- `BatchInsert.aspx`


![SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가](wrapping-database-modifications-within-a-transaction-cs/_static/image1.gif)

**그림 1**: SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더와 마찬가지로 `Default.aspx` 사용할지는 `SectionLevelTutorialListing.ascx` 사용자 컨트롤을 해당 섹션 내에서 자습서 목록입니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx`의 디자인 뷰에서 페이지의 솔루션 탐색기에서 끌어 합니다.


[![Default.aspx SectionLevelTutorialListing.ascx 사용자 컨트롤 추가](wrapping-database-modifications-within-a-transaction-cs/_static/image2.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image1.png)

**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 `Default.aspx` ([클릭 하 여 큰 이미지 보기](wrapping-database-modifications-within-a-transaction-cs/_static/image2.png))


마지막으로, 이러한 네 가지 페이지 항목을 추가 합니다 `Web.sitemap` 파일입니다. 특히 다음 태그는 사용자 지정 뒤에 추가 사이트 맵 `<siteMapNode>`:


[!code-xml[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample2.xml)]

업데이트 한 후 `Web.sitemap`, 잠시 브라우저를 통해 자습서 웹 사이트를 확인 합니다. 왼쪽 메뉴에는 이제 일괄 처리 된 데이터 자습서를 사용 하 여 작업에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 일괄 처리 된 데이터 자습서를 사용 하 여 작업 항목을 포함](wrapping-database-modifications-within-a-transaction-cs/_static/image3.gif)

**그림 3**: 이제 사이트 맵 일괄 처리 된 데이터 자습서를 사용 하 여 작업 항목을 포함


## <a name="step-2-updating-the-data-access-layer-to-support-database-transactions"></a>2 단계: 데이터베이스 트랜잭션을 지원 하도록 데이터 액세스 계층 업데이트

다시 첫 번째 자습서에서에서 설명한 대로 [데이터 액세스 레이어 만들기](../introduction/creating-a-data-access-layer-cs.md), Datatable 및 Tableadapter는 DAL에서 입력 데이터 집합으로 구성 되어 있습니다. TableAdapters를 데이터베이스에서 변경 Datatable 및 등을 사용 하 여 데이터베이스를 업데이트 하는 Datatable에 데이터를 읽는 기능을 제공 하지만 Datatable의 데이터를 보관 합니다. TableAdapters 일괄 업데이트와 DB 직접 참조 하는 데이터를 업데이트 하기 위한 두 가지 패턴을 제공 하는 것을 기억 하십시오. 일괄 처리 업데이트 패턴을 사용 하면 TableAdapter는 DataSet, DataTable 또는 Datarow의 컬렉션을 전달 됩니다. 이 데이터를 열거할 및 각각에 대 한 삽입, 수정 또는 행을 삭제 합니다 `InsertCommand`, `UpdateCommand`, 또는 `DeleteCommand` 실행 됩니다. DB 직접 패턴을 사용 하면 TableAdapter 삽입, 업데이트 또는 단일 레코드를 삭제 하는 데 필요한 열 값 대신 전달 합니다. DB 직접 패턴 메서드를 사용 하 여 전달 된 값을 적절 한 실행 `InsertCommand`, `UpdateCommand`, 또는 `DeleteCommand` 문입니다.

사용 되는 업데이트 패턴에 관계 없이 Tableadapter 자동으로 생성 된 메서드는 트랜잭션을 사용 하지 마세요. 기본적으로 각 insert, update 또는 delete TableAdapter 수행한 별도 단일 작업으로 처리 됩니다. 예를 들어 데이터베이스에 10 개의 레코드를 삽입할가 DB 직접 패턴이 BLL에 일부 코드에서 사용 되는 한다고 가정 합니다. 이 코드는 tableadapter 호출 `Insert` 메서드를 10 번입니다. 처음 5 개 삽입 성공 하지만 여섯 번째 하나는 예외가 발생 한 경우 데이터베이스에 삽입 된 처음 5 개 레코드 상태로 유지 됩니다. 마찬가지로, 일괄 처리 업데이트 패턴을 삽입 하는 데 사용 하는 경우 업데이트 및 삭제 하는 삽입 된 수정 및 삭제 된 행을 DataTable에 첫 번째 여러 수정 했지만 최신에는 이러한 이전 수정 오류가 발생 하는 경우는 완료 된 데이터베이스에 유지 됩니다.

특정 시나리오에서 수정 일련의 원자성을 유지 하려고 합니다. TableAdapter를 실행 하는 새 메서드를 추가 하 여 수동으로 확장 해야이 작업을 수행 하는 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 트랜잭션의 산하 s입니다. [데이터 액세스 레이어 만들기](../introduction/creating-a-data-access-layer-cs.md) 사용 하 여 살펴보았습니다 [partial 클래스](http://en.wikipedia.org/wiki/Partial_type) 형식화 된 데이터 집합에 Datatable의 기능을 확장 하 합니다. Tableadapter를 사용 하 여이 기법을 사용할 수도 있습니다.

입력 데이터 집합 `Northwind.xsd` 에 `App_Code` s 폴더 `DAL` 하위 폴더입니다. 하위 폴더를 만듭니다는 `DAL` 라는 폴더 `TransactionSupport` 라는 새 클래스 파일을 추가 하 고 `ProductsTableAdapter.TransactionSupport.cs` (그림 4 참조). 이 파일의 구현 일부를 보유할는 `ProductsTableAdapter` 트랜잭션을 사용 하는 데이터 수정 작업을 수행 하기 위한 메서드를 포함 하는 합니다.


![TransactionSupport 폴더 및 ProductsTableAdapter.TransactionSupport.cs 라는 클래스 파일을 추가 합니다.](wrapping-database-modifications-within-a-transaction-cs/_static/image4.gif)

**그림 4**: 라는 폴더를 추가 `TransactionSupport` 및 라는 클래스 파일을 `ProductsTableAdapter.TransactionSupport.cs`


다음 코드를 입력 합니다 `ProductsTableAdapter.TransactionSupport.cs` 파일:


[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample3.cs)]

`partial` 내에서 추가 된 멤버에 추가할 수 있는 컴파일러에 알리는 키워드를 클래스 선언에는 `ProductsTableAdapter` 클래스는 `NorthwindTableAdapters` 네임 스페이스. 참고는 `using System.Data.SqlClient` 파일의 맨 위에 있는 문. TableAdapter는 SqlClient 공급자를 사용 하도록 구성 된, 하므로 내부적으로 사용 하 여는 [ `SqlDataAdapter` ](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter.aspx) 데이터베이스로 해당 명령을 실행 하는 개체입니다. 따라서를 사용 해야는 `SqlTransaction` 트랜잭션을 시작 하는 클래스 커밋하거나 롤백하는 고 합니다. Microsoft SQL Server 이외의 데이터 저장소를 사용 하는 경우에 적절 한 공급자를 사용 해야 합니다.

이러한 메서드는 롤백을 시작 하는 데 필요한 구성 요소를 제공 하 고 트랜잭션 커밋. 표시 된 `public`, 내에서 사용할 수 있도록는 `ProductsTableAdapter`, DAL의 다른 클래스 또는 다른 계층 BLL 같은 아키텍처에 있습니다. `BeginTransaction` 내부 tableadapter를 엽니다 `SqlConnection` (필요한 경우), 트랜잭션을 시작 하 고 할당 합니다 `Transaction` 속성 내부에 트랜잭션 연결 `SqlDataAdapter` s `SqlCommand` 개체입니다. `CommitTransaction` 및 `RollbackTransaction` 호출을 `Transaction` s 개체 `Commit` 하 고 `Rollback` 메서드 내부를 닫기 전에 각각 `Connection` 개체.

## <a name="step-3-adding-methods-to-update-and-delete-data-under-the-umbrella-of-a-transaction"></a>3 단계: 트랜잭션 산하 데이터 업데이트 및 삭제 하는 메서드 추가

메서드를 추가 하려면 준비 다시에서는 전체이 메서드를 사용 하 여 `ProductsDataTable` 또는 일련의 트랜잭션 산하 명령 수행 하는 BLL 합니다. 다음 메서드는 일괄 처리 업데이트 패턴을 사용 하 여 업데이트를 `ProductsDataTable` 는 트랜잭션을 사용 하 여 인스턴스. 호출 하 여 트랜잭션을 시작 합니다 `BeginTransaction` 메서드를 사용 하 여를 `try...catch` 블록 데이터 수정 문을 실행 합니다. 경우에 대 한 호출을 `Adapter` s 개체 `Update` 예외가 메서드 결과 실행 하려면 전송는 `catch` 여기서 트랜잭션이 롤백되어 블록 및 예외 다시 throw 합니다. 이전에 설명한 대로 합니다 `Update` 제공 된 행을 열거 하 여 일괄 처리 업데이트 패턴을 구현 하는 메서드 `ProductsDataTable` 하 고 필요한 수행 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` s. 중 하나가 오류가이 명령 결과 트랜잭션이 롤백됩니다, 트랜잭션의 수명 동안 이전 수정 취소 합니다. 해야는 `Update` 문을 오류 없이 완료, 전체에서 트랜잭션이 커밋됩니다.


[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample4.cs)]

추가 합니다 `UpdateWithTransaction` 메서드를 합니다 `ProductsTableAdapter` 클래스의 partial 클래스를 통해 `ProductsTableAdapter.TransactionSupport.cs`합니다. 비즈니스 논리 레이어 s에이 메서드를 추가할 수 있습니다 또는 `ProductsBLL` 몇 가지만 구문 변경을 사용 하 여 클래스입니다. 즉, 키워드가 `this.BeginTransaction()`, `this.CommitTransaction()`, 및 `this.RollbackTransaction()` 사용 하 여 교체 해야 `Adapter` (이전에 설명한 대로 `Adapter` 의 속성 이름인 `ProductsBLL` 형식의 `ProductsTableAdapter`).

`UpdateWithTransaction` 메서드 일괄 처리 업데이트 패턴을 사용 하지만 메서드는 다음과 같이 트랜잭션 범위 내에서 일련의 DB 직접 호출을 사용할 수도 있습니다. `DeleteProductsWithTransaction` 메서드를 입력으로 받아들입니다를 `List<T>` 형식의 `int`는 `ProductID` 삭제 하도록 합니다. 메서드 호출을 통해 트랜잭션을 시작 `BeginTransaction` 차례로 합니다 `try` 차단, DB 직접 패턴을 호출 합니다. 제공 된 목록을 반복 `Delete` 각각에 대 한 메서드 `ProductID` 값. 호출 하는 경우 `Delete` 실패 하면 제어가 `catch` 트랜잭션이 롤백 여기서 블록 및 예외 다시 throw 합니다. 에 대 한 모든 호출은 경우 `Delete` 트랜잭션이 커밋될 때 다음 성공 합니다. 이 메서드를 추가 하 여 `ProductsBLL` 클래스입니다.


[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample5.cs)]

## <a name="applying-transactions-across-multiple-tableadapters"></a>여러 Tableadapter에 걸쳐 트랜잭션 적용

이 자습서에서 검사 하는 트랜잭션 관련 코드에 대 한 여러 문을 허용 된 `ProductsTableAdapter` 원자 단위 연산으로 처리 합니다. 하지만 다른 데이터베이스 테이블에 여러 가지 수정 사항이 원자 단위로 수행 해야 하는 경우에 어떻게? 예를 들어 범주를 삭제 하는 경우 일부 다른 범주에 현재 제품에 할당할 원하는 먼저 수 있습니다. 이러한 두 단계는 제품을 다시 할당 하 고 범주를 삭제 하는 원자성 작업으로 실행 되어야 합니다. 하지만 `ProductsTableAdapter` 수정 하기 위한 방법만 포함 합니다 `Products` 테이블 및 `CategoriesTableAdapter` 수정 하기 위한 방법만 포함는 `Categories` 테이블. 트랜잭션이 모두 Tableadapter를 어떻게 포함 될 수 있습니다?

메서드를 추가 하는 한 가지 방법은 합니다 `CategoriesTableAdapter` 라는 `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` 있고 모두 제품을 다시 할당 및 저장된 프로시저 내에 정의 된 트랜잭션 범위 내에서 범주를 삭제 하는 저장된 프로시저를 호출 하는 메서드. 이후 자습서에서 시작, 커밋, 방법 및 저장된 프로시저에서 트랜잭션을 롤백하고 살펴 보겠습니다 했습니다.

다른 옵션은 포함 하는 DAL에서 도우미 클래스를 만드는 것은 `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` 메서드. 이 메서드는의 인스턴스를 만듭니다는 `CategoriesTableAdapter` 하며 `ProductsTableAdapter` 로 설정한 다음 이러한 두 Tableadapter `Connection` 동일한 속성 `SqlConnection` 인스턴스. At 이때 두 Tableadapter 중 하나에 대 한 호출을 사용 하 여 트랜잭션을 시작 하는 `BeginTransaction`합니다. 제품을 다시 할당 하 고 범주를 삭제 하는 Tableadapter 메서드는 호출할 수는 `try...catch` 트랜잭션 커밋하거나 필요에 따라 다시 사용 하 여 블록입니다.

## <a name="step-4-adding-theupdatewithtransactionmethod-to-the-business-logic-layer"></a>4 단계: 추가 된`UpdateWithTransaction`비즈니스 논리 계층 방법

3 단계에서에서 추가한를 `UpdateWithTransaction` 메서드를는 `ProductsTableAdapter` DAL에서. BLL에 해당 하는 메서드를 추가 해야 합니다. 프레젠테이션 계층 DAL 호출까지 직접 호출할 수 있지만 `UpdateWithTransaction` 메서드를 이러한 자습서는 프레젠테이션 계층과에서 DAL을 분리 하는 계층화 된 아키텍처를 정의 하려면 strived 있어야 합니다. 따라서이 이렇게를 behooves입니다.

열기는 `ProductsBLL` 라는 메서드를 추가 하 고 클래스 파일 `UpdateWithTransaction` 까지 해당 하는 DAL 메서드는 단순히 호출 합니다. 두 개의 새 매서드 있어야 `ProductsBLL`: `UpdateWithTransaction`에서 방금 추가한는 및 `DeleteProductsWithTransaction`, 3 단계에서에서 추가 됨.


[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample6.cs)]

> [!NOTE]
> 이러한 메서드를 포함 하지 마십시오는 `DataObjectMethodAttribute` 특성의 다른 메서드에 대부분 할당할는 `ProductsBLL` ASP.NET 페이지 코드 숨김 클래스에서 직접 이러한 메서드를 호출 수 됩니다 것 때문에 클래스. 이전에 설명한 대로 `DataObjectMethodAttribute` 데 사용 하는 방법을 구성 데이터 원본 마법사 (SELECT, UPDATE, INSERT 또는 DELETE) 어떤 탭 ObjectDataSource에서 표시 됩니다. GridView에 편집 또는 삭제 일괄 처리에 대 한 기본 제공 지원, 없으므로 선언적 코드 없는 접근 방식을 사용 하는 대신 프로그래밍 방식으로 이러한 메서드를 호출 하는 것이 해야 합니다.


## <a name="step-5-atomically-updating-database-data-from-the-presentation-layer"></a>5 단계: 프레젠테이션 계층에서 데이터베이스 데이터를 자동으로 업데이트

트랜잭션 일괄 처리 레코드를 업데이트 하는 경우에 효과 보여 주기 위해 let s GridView의 모든 제품을 나열 하 고 단추 웹을 포함 하는 사용자 인터페이스를 만드는 컨트롤을 클릭 하면 제품 재할당 `CategoryID` 값입니다. 첫 번째 다양 한 제품 유효한 할당 된 있도록 범주 재할당 진행 되는 특히 `CategoryID` 이지만 나머지는 의도적으로 값 할당 존재 하지 않는 `CategoryID` 값입니다. 제품을 사용 하 여 데이터베이스를 업데이트 하려고 하는 경우 해당 `CategoryID` s 기존 범주와 일치 하지 않습니다 `CategoryID`, 외래 키 제약 조건 위반을 발생 하 고 예외가 발생 합니다. 이 예제에서 보이는 것는 경우 트랜잭션에서 외래 키 제약 조건 위반이 발생 하는 예외를 사용 하 여 이전 하면 유효한 `CategoryID` 변경 내용을 롤백할 수 있습니다. 그러나 트랜잭션을 사용 하지를 초기 범주 수정 유지 됩니다.

열어서 시작 합니다 `Transactions.aspx` 페이지에서 `BatchData` 폴더 및 디자이너 도구 상자에서 끌어서 GridView입니다. 설정 해당 `ID` 하 `Products` 및 스마트 태그를 바인딩할 라는 새로운 ObjectDataSource는 `ProductsDataSource`합니다. ObjectDataSource에서 해당 데이터를 가져오도록 구성 합니다 `ProductsBLL` s 클래스 `GetProducts` 메서드. 이 읽기 전용 GridView, 따라서 드롭 다운 목록에서 UPDATE, INSERT, 설정 및 탭 (없음)을 삭제 되며 마침을 클릭 합니다.


[![그림 5: ProductsBLL 클래스의 GetProducts 메서드를 사용 하는 ObjectDataSource 구성](wrapping-database-modifications-within-a-transaction-cs/_static/image5.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image3.png)

**그림 5**: 그림 5: ObjectDataSource를 사용 하 여 구성 합니다 `ProductsBLL` s 클래스 `GetProducts` 메서드 ([클릭 하 여 큰 이미지 보기](wrapping-database-modifications-within-a-transaction-cs/_static/image4.png))


[![UPDATE, INSERT 드롭 다운 목록을 설정 하 고 탭 삭제 (없음)](wrapping-database-modifications-within-a-transaction-cs/_static/image6.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image5.png)

**그림 6**: 드롭다운 목록에서 업데이트, 삽입 및 삭제 탭 하도록 설정 (없음) ([큰 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-cs/_static/image6.png))


데이터 소스 구성 마법사를 완료 한 후 Visual Studio BoundFields 및 제품 데이터 필드에 대 한 CheckBoxField 만들어집니다. 제외 하 고 이러한 필드를 모두 제거 `ProductID`, `ProductName`, `CategoryID`, 및 `CategoryName` 바꾸고 합니다 `ProductName` 및 `CategoryName` BoundFields `HeaderText` 속성 범주 및 제품을 각각. 스마트 태그에서 페이징 사용 옵션을 선택 합니다. 이러한 수정을 마치면 GridView 및 ObjectDataSource가 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample7.aspx)]

그런 다음 GridView 위의 세 가지 단추 웹 컨트롤을 추가 합니다. 새로 고침 표, 수정 범주 (사용 하 여 트랜잭션), 두 번째 s 및 세 번째 하나의 s 수정 범주 (트랜잭션 없이)를 첫 번째 단추의 텍스트 속성을 설정 합니다.


[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample8.aspx)]

이 시점에서 Visual Studio의 디자인 뷰에서 스크린샷과 그림 7 에서처럼 유사 합니다.


[![페이지에 GridView 및 3 개의 단추 웹 컨트롤](wrapping-database-modifications-within-a-transaction-cs/_static/image7.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image7.png)

**그림 7**: 세 개의 단추 웹 컨트롤을 GridView 페이지에 포함 되어 있습니다 ([큰 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-cs/_static/image8.png))


S 세 단추의 각 이벤트 처리기 만들기 `Click` 이벤트 및 다음 코드를 사용 합니다.


[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample9.cs)]

새로 고침 단추 s `Click` 를 호출 하 여 이벤트 처리기 단순히 다시 바인딩 횟수 GridView에 데이터를 `Products` GridView의 `DataBind` 메서드.

두 번째 이벤트 처리기 재할당 제품 `CategoryID` 및 사용 하 여 트랜잭션의 산하 데이터베이스를 수행 하는 BLL에서 새 트랜잭션 메서드를 업데이트 합니다. 각 제품 s `CategoryID` 임의로 동일한 값으로 설정 되어 해당 `ProductID`합니다. 정상적으로 작동 합니다 첫 번째에 대 한 몇 가지 제품을 제품 없으므로 `ProductID` 유효한 매핑할 발생 하는 값 `CategoryID` s입니다. 한 번 합니다 `ProductID` 너무 큼 먼저,이 우연의 일치 중복 `ProductID` s 및 `CategoryID` s 적용 되지 않습니다.

세 번째 `Click` 제품을 업데이트 하는 이벤트 처리기 `CategoryID` s 동일한 방식으로 사용 하 여 데이터베이스에 있지만 업데이트를 보냅니다는 `ProductsTableAdapter` 기본값 `Update` 메서드. 이 `Update` 메서드 일련의 트랜잭션 내에서 명령이 바뀌지 않으며, 첫 번째 발생 한 foreign key 제약 조건 위반 오류 전에 해당 변경 내용이 있으므로 유지 됩니다.

이 동작을 보여 주기 위해 브라우저를 통해이 페이지를 방문 합니다. 처음에 그림 8 에서처럼 데이터의 첫 페이지에 표시 됩니다. 다음으로 수정 범주 (사용 하 여 트랜잭션) 단추를 클릭 합니다. 포스트백을 발생 되 고 모든 제품을 업데이트 하려는 시도가 `CategoryID` 값 이지만 foreign key 제약 조건 위반 하 게 발생 됩니다 (그림 9 참조).


[![제품을 페이징할 수 있는 GridView에 표시 됩니다.](wrapping-database-modifications-within-a-transaction-cs/_static/image8.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image9.png)

**그림 8**: GridView를 페이징할 수 있는 제품 표시 됩니다 ([큰 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-cs/_static/image10.png))


[![Foreign Key 제약 조건 위반 하 게 범주 결과 다시 할당](wrapping-database-modifications-within-a-transaction-cs/_static/image9.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image11.png)

**그림 9**: 외래 키 제약 조건 위반을 범주 결과 다시 할당 ([큰 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-cs/_static/image12.png))


이제 사용자가 브라우저의 뒤로 단추를 누르면 및 그리드 새로 고침 단추를 클릭 합니다. 데이터 새로 고침 시 그림 8에 표시 된 대로 정확 하 게 동일한 출력이 표시 됩니다. 즉,도 있지만 일부 제품 `CategoryID` s 된 법률에 변경 된 값 및 데이터베이스에서 업데이트를 롤백 되었으므로 외래 키 제약 조건 위반이 발생 한 경우.

이제 수정 범주 (트랜잭션 없이) 단추를 클릭 해 보십시오. 동일한 foreign key 제약 조건 위반 오류가 발생 하면이 (그림 9 참조) 이러한 제품을 이번 하지만 해당 `CategoryID` 올바른 값이 변경 되었는지 값 없습니다 롤백됩니다. 사용자가 브라우저의 뒤로 단추 한 다음 새로 고침 눈금 단추를 누릅니다. 그림 10과 같이 `CategoryID` 처음 8 개 제품의 다시 할당 된 합니다. 예를 들어, 그림 8에서 변경 했습니다는 `CategoryID` 1의 그림 10 it s에서에 게 재할당 되었습니다 2 있지만.


[![일부 제품 CategoryID 값 없습니다. 업데이트 하는 동안 다른 되었습니다](wrapping-database-modifications-within-a-transaction-cs/_static/image10.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image13.png)

**그림 10**: 일부 제품 `CategoryID` 값 없습니다. 업데이트 하는 동안 다른 되었습니다 ([클릭 하 여 큰 이미지 보기](wrapping-database-modifications-within-a-transaction-cs/_static/image14.png))


## <a name="summary"></a>요약

기본적으로 TableAdapter가의 메서드를 사용 하는 트랜잭션의 범위 내에서 실행된 데이터베이스 문 줄 바꿈하지 않습니다 하지만 약간의 작업을 사용 하 여 추가할 수 있습니다를 만드는 방법, commit 및 rollback 트랜잭션. 이 자습서에서는 이러한 세 가지 방법 만들었습니다 합니다 `ProductsTableAdapter` 클래스: `BeginTransaction`를 `CommitTransaction`, 및 `RollbackTransaction`합니다. 와 함께 이러한 메서드를 사용 하는 방법에 살펴보았습니다를 `try...catch` 블록 일련의 데이터 수정 문 원자성을 보장 합니다. 만든 특히 합니다 `UpdateWithTransaction` 에서 메서드를 `ProductsTableAdapter`, 일괄 처리 업데이트 패턴의 제공 된 행에 필요한 수정 작업을 수행 하는를 사용 하 여 `ProductsDataTable`. 도 추가 합니다 `DeleteProductsWithTransaction` 메서드를 합니다 `ProductsBLL` 클래스 BLL은 허용 하는 `List` 의 `ProductID` 값을 해당 입력으로 직접 DB 패턴 메서드를 호출 하 `Delete` 각각에 대 한 `ProductID`. 두 방법 모두 먼저 트랜잭션을 만들고 다음 내에서 데이터 수정 문을 실행 하는 `try...catch` 블록입니다. 예외가 발생 하면 트랜잭션이 롤백됩니다 커밋된 것이 고, 그렇지입니다.

5 단계 들어오지 트랜잭션을 사용 하는 일괄 처리 업데이트와 트랜잭션 일괄 처리 업데이트의 효과를 보여 줍니다. 다음 세 개의 자습서에서이 자습서에서는 배치 foundation을 기반으로 하 고 일괄 처리 업데이트, 삭제 및 삽입을 수행 하기 위한 사용자 인터페이스를 만듭니다.

즐거운 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [트랜잭션 사용 하 여 데이터베이스 일관성을 유지 관리](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx)
- [저장 프로시저를 SQL Server에서 트랜잭션 관리](http://www.4guysfromrolla.com/webtech/080305-1.shtml)
- [간편해 진 트랜잭션: `System.Transactions`](https://blogs.msdn.com/florinlazar/archive/2004/07/23/192239.aspx)
- [TransactionScope 및 Dataadapter](http://andyclymer.blogspot.com/2007/01/transactionscope-and-dataadapters.html)
- [.NET의 Oracle 데이터베이스 트랜잭션 사용](http://www.oracle.com/technology/pub/articles/price_dbtrans_dotnet.html)

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Dave Gardner, Hilton giesenow와 함께 및 Teresa Murphy 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](batch-updating-cs.md)
