---
uid: web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs
title: "데이터베이스 수정 (C#) 트랜잭션 내에서 줄 바꿈 | Microsoft Docs"
author: rick-anderson
description: "이 자습서에는 업데이트, 삭제 및 삽입 데이터의 일괄 처리에는 4 개의 중 첫 번째 숫자입니다. 이 자습서에서는 데이터베이스 트랜잭션을 허용 하는 방법 알아보기..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/26/2007
ms.topic: article
ms.assetid: b45fede3-c53a-4ea1-824b-20200808dbae
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs
msc.type: authoredcontent
ms.openlocfilehash: 3081a695230056aedce875dbbb750c6853a863b7
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="wrapping-database-modifications-within-a-transaction-c"></a>트랜잭션 (C#) 내에서 줄 바꿈 데이터베이스 수정
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_63_CS.zip) 또는 [PDF 다운로드](wrapping-database-modifications-within-a-transaction-cs/_static/datatutorial63cs1.pdf)

> 이 자습서에는 업데이트, 삭제 및 삽입 데이터의 일괄 처리에는 4 개의 중 첫 번째 숫자입니다. 이 자습서에서는 데이터베이스 트랜잭션 일괄 처리 수정을 모든 단계가 성공 되거나 모든 단계가 실패 원자성 작업으로 수행할 수를 허용 하는 방법을 알아봅니다.


## <a name="introduction"></a>소개

부터는 살펴본 것 처럼는 [는 개요의 삽입, 업데이트 및 삭제 데이터](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) 자습서에서는 GridView 기본적으로 제공 행 수준 편집 및 삭제에 대 한 합니다. 마우스 클릭 몇 번으로 콘텐츠를 편집 및 삭제 행 단위로에 코드 줄도 작성 하지 않고 다양 한 데이터 수정 인터페이스를 만들 수 있습니다. 그러나 특정 시나리오에서이 부족 및 편집 또는 일괄 처리 레코드를 삭제 하는 기능 사용자에 게 제공 해야 합니다.

예를 들어 대부분의 웹 기반 전자 메일 클라이언트 표를 사용는 각 메시지를 나열 하려면 각 행 (제목, 보낸 사람, 등) 전자 메일의 정보와 함께 확인란을 포함 하는 위치. 이 인터페이스는 확인과 선택한 메시지 삭제 단추를 클릭 하 여 여러 메시지를 삭제 하는 사용자를 허용 합니다. 일괄 처리 편집 인터페이스는 여러 다른 레코드에 사용자가 일반적으로 편집 하는 경우에 이상적입니다. 편집을 클릭 하 여 사용자를 요구 하는 대신, 해당 변경 작업을 수행 하 고 수정 해야 하는 각 레코드에 대 한 업데이트를 클릭 한 다음, 편집 인터페이스의 각 행을 렌더링 하는 일괄 처리 편집 인터페이스 사용자는 신속 하 게 변경 해야 하는 행 집합을 수정할 수 있으며 모두 업데이트 하는 단추를 클릭 하 여 이러한 변경 내용을 저장 합니다. 이 자습서에서는 삽입, 편집 및 데이터의 일괄 처리 삭제에 대 한 인터페이스를 만드는 방법을 검토 합니다.

일괄 처리 작업을 수행할 때 그 실패 s 여부 수 있어야 하지만 성공 하려면 일괄 처리의 작업 중 일부에 대 한 결정 하는 것이 중요 합니다. 인터페이스-실패 한 경우 선택한 첫 번째 레코드를 성공적으로 삭제 합니다. 두 번째, 예를 들어, 외래 키 제약 조건 위반 때문에 수행할 동작을 삭제 하는 일괄 처리를 것이 좋습니다. 첫 번째 레코드 s delete 롤백해야 하는지 아니면 삭제 된 상태를 유지 하는 첫 번째 레코드에 대해 허용 가능한 있습니까?

일괄 처리 작업으로 처리 하려는 경우는 [원자 단위 연산](http://en.wikipedia.org/wiki/Atomic_operation), 위치 중 하나 성공 모든 단계 또는 모든 단계에 실패 한 데이터 액세스 계층에 대 한 지원을 포함 하도록 확장할 수 있어야 하나 [데이터베이스 트랜잭션을](http://en.wikipedia.org/wiki/Database_transaction)합니다. 데이터베이스 트랜잭션 집합에 대 한 원자성을 보장 하기 `INSERT`, `UPDATE`, 및 `DELETE` 문은 트랜잭션의 포괄적인 아래에서 실행 되 고 대부분 모든 최신 데이터베이스 시스템에서 지원 되는 기능입니다.

이 자습서에서는 데이터베이스 트랜잭션을 사용 하는 DAL을 확장 하는 방법을 살펴보겠습니다. 이후 자습서 일괄 처리 삽입, 업데이트 및 삭제 인터페이스에 대 한 구현 웹 페이지를 검사 합니다. Let s가 시작 되었습니다.

> [!NOTE]
> 일괄 처리 트랜잭션의 데이터를 수정할 때 항상 원자성 필요 하지 않습니다. 일부 시나리오에서는 성공 하는 일부 데이터 수정 내용을 포함 하도록 허용 수 있으며 예를 들어 실패 동일한 일괄 처리의 다른 웹 기반 전자 메일 클라이언트에서 전자 메일의 집합을 삭제 합니다. 없어 s 삭제 데이터베이스 오류 중간 처리 하는 경우 그 s 허용 처리가 오류 없이 이러한 레코드 삭제 유지 하는 것입니다. 이러한 경우에는 DAL 하지 않아도 데이터베이스 트랜잭션을 지원 하도록 수정 합니다. 그러나 시나리오가 다른 일괄 처리 작업, 원자성이 중요 합니다. 두 작업을 수행 해야 자신의 자금 하나의 은행 계좌에서 다른 위치로 이동 하는 고객을 하는 경우: 자금을 첫 번째 계정에서 차감 하 고 두 번째 인스턴스에 추가 해야 합니다. 은행 성공 하는 첫 번째 단계 필요 상관 하지 않을 수 있습니다, 두 번째 단계가 실패 하는 동안 고객 당연히 화가 것입니다. 이 자습서를 진행 하 고 구현에 삽입 하는 일괄 처리에서 사용, 업데이트 및 인터페이스는 다음 세 개의 자습서에서 구축 म 삭제 하지 않을 경우에 데이터베이스 트랜잭션을 지원 하기 위해 DAL의 향상 된 기능을 확인해 합니다.


## <a name="an-overview-of-transactions"></a>트랜잭션 개요

대부분의 데이터베이스에 대 한 지원 포함 *트랜잭션을*, 여러 데이터베이스 명령을 작업의 단일 논리 단위로 그룹화 할 수 있도록 합니다. 모든 명령이 실패 합니다 중 하나 또는 모두에 성공할 원자성 트랜잭션을 구성 하는 데이터베이스 명령 보장 됩니다.

일반적으로 트랜잭션은 다음 패턴을 사용 하 여 SQL 문을 통해 구현 됩니다.

1. 트랜잭션의 시작을 표시 합니다.
2. 트랜잭션을 구성 하는 SQL 문을 실행 합니다.
3. 2 단계에서 트랜잭션 롤백하고에서에서 문 중 하나에 오류가 있는 경우.
4. 오류 없이 완료 모든 2 단계에서에서 문을 경우 트랜잭션을 커밋하십시오.

를 만들려면 사용 되는 SQL 문의 커밋, 및 저장 프로시저를 만들거나 SQL 스크립트를 작성할 때 트랜잭션을 수동으로 입력할 수 있습니다 롤백하거나 프로그래밍을 통해의 클래스 또는 ADO.NET을 사용 하 여 의미는 [ `System.Transactions` 네임 스페이스](https://msdn.microsoft.com/en-us/library/system.transactions.aspx)합니다. 만 살펴보겠습니다이 자습서에서는 ADO.NET을 사용 하 여 트랜잭션을 관리 합니다. 이후 자습서 될 때 SQL 문을 만들고, 롤백 하 고 트랜잭션을 커밋하기 위한 살펴볼 것 데이터 액세스 계층에서 저장된 프로시저를 사용 하는 방법을 살펴보겠습니다. 한편, 참조 [SQL Server 저장 프로시저에서 트랜잭션을 관리](http://www.4guysfromrolla.com/webtech/080305-1.shtml) 자세한 정보에 대 한 합니다.

> [!NOTE]
> [ `TransactionScope` 클래스](https://msdn.microsoft.com/en-us/library/system.transactions.transactionscope.aspx) 에서 `System.Transactions` 네임 스페이스 개발자가 프로그래밍 방식으로 트랜잭션 범위 내에서 일련의 문을 래핑할 수와 여러 관련 된 복잡 한 트랜잭션에 대 한 지원이 포함 됩니다. 두 개의 서로 다른 데이터베이스 또는 심지어 유형이 다른 Microsoft SQL Server 데이터베이스, Oracle 데이터베이스 및 웹 서비스 같은 데이터 저장소와 같은 원본입니다. I 대신이 자습서에 대 한 ADO.NET 트랜잭션을 사용 하기로 결정 했습니다는 `TransactionScope` 클래스 ADO.NET 데이터베이스 트랜잭션 및 대부분의 경우에서 특정 해야 하므로 훨씬 적은 리소스를 많이 사용 합니다. 또한 특정 시나리오에서의 `TransactionScope` 클래스는 Microsoft Distributed Transaction Coordinator (MSDTC)를 사용 합니다. 구성, 구현 및 성능 문제 주변 MSDTC를 사용 하면 보다 특수 한 고급 항목 및이 자습서의 범위를 벗어납니다.


호출을 통해 트랜잭션을 시작 ADO.NET에서 SqlClient 공급자를 사용할 때의 [ `SqlConnection` 클래스](https://msdn.microsoft.com/en-US/library/system.data.sqlclient.sqlconnection.aspx) s [ `BeginTransaction` 메서드](https://msdn.microsoft.com/en-us/library/system.data.sqlclient.sqlconnection.begintransaction.aspx)를 반환 하는 [ `SqlTransaction` 개체](https://msdn.microsoft.com/en-US/library/system.data.sqlclient.sqltransaction.aspx)합니다. 구성을 트랜잭션 내에 배치 됩니다 하는 데이터 수정 문을 `try...catch` 블록입니다. 문에 오류가 발생 하는 경우는 `try` 에 전송 하는 실행을 차단는 `catch` 블록은 트랜잭션을 통해 다시 롤백할 수 있습니다는 `SqlTransaction` 개체 s [ `Rollback` 메서드](https://msdn.microsoft.com/en-us/library/system.data.sqlclient.sqltransaction.rollback.aspx)합니다. 모든 문을 성공적으로 호출을 완료 하는 경우는 `SqlTransaction` 개체 s [ `Commit` 메서드](https://msdn.microsoft.com/en-us/library/system.data.sqlclient.sqltransaction.commit.aspx) 의 끝에는 `try` 블록에 트랜잭션을 커밋합니다. 다음 코드 조각에서는이 패턴을 보여 줍니다. 참조 [트랜잭션 사용 하 여 데이터베이스 일관성을 유지](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx) 추가 구문 및 트랜잭션을 사용 하 여 ado.net 예입니다.


[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample1.cs)]

기본적으로 형식화 된 데이터 집합에서 Tableadapter에는 트랜잭션을 사용 하지 마십시오. 트랜잭션에 대 한 지원을 제공 하려면 위의 패턴을 사용 하 여 일련의 트랜잭션 범위 내에서 데이터 수정 문 수행 하는 추가 메서드를 포함 하도록 TableAdapter 클래스를 확장 해야 합니다. 2 단계에서에서 이러한 메서드를 추가 하려면 partial 클래스를 사용 하는 방법을 살펴보겠습니다.

## <a name="step-1-creating-the-working-with-batched-data-web-pages"></a>1 단계: 웹 페이지를 일괄 처리 된 데이터와 작업 만들기

데이터베이스 트랜잭션을 지원 하기 위해 DAL 보강 하는 방법을 탐색을 시작 하기 전에 먼저이 자습서에 필요한 ASP.NET 웹 페이지를 만들고 다음에 나오는 세 보십시오 s가 있습니다. 라는 새 폴더를 추가 하 여 시작 `BatchData` 다음 연결 된 각 페이지는 다음 ASP.NET 페이지를 추가 하 고는 `Site.master` 마스터 페이지입니다.

- `Default.aspx`
- `Transactions.aspx`
- `BatchUpdate.aspx`
- `BatchDelete.aspx`
- `BatchInsert.aspx`


![SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가](wrapping-database-modifications-within-a-transaction-cs/_static/image1.gif)

**그림 1**: SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더와 마찬가지로 `Default.aspx` ´ ֲ는 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 섹션 내에서 자습서를 나열 합니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx`의 디자인 뷰에서 페이지 하려면 솔루션 탐색기에서 끌어서 합니다.


[![Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가](wrapping-database-modifications-within-a-transaction-cs/_static/image2.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image1.png)

**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-cs/_static/image2.png))


마지막으로, 이러한 4 개 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 구체적으로 사용자 지정 후 다음 태그를 추가 사이트 맵 `<siteMapNode>`:


[!code-xml[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample2.xml)]

업데이트 한 후 `Web.sitemap`, 브라우저를 통해 자습서 웹 사이트를 보려면 보십시오. 왼쪽 메뉴에는 이제 일괄 처리 된 데이터 자습서 사용에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 작업 일괄 처리 된 데이터 자습서에 대 한 항목을 포함](wrapping-database-modifications-within-a-transaction-cs/_static/image3.gif)

**그림 3**: 이제 사이트 맵 작업 일괄 처리 된 데이터 자습서에 대 한 항목을 포함


## <a name="step-2-updating-the-data-access-layer-to-support-database-transactions"></a>데이터베이스 트랜잭션을 지원 하도록 데이터 액세스 계층을 업데이트 하는 2 단계:

다시 첫 번째 자습서에서에서 설명한 것 처럼 [데이터 액세스 계층을 만들려면](../introduction/creating-a-data-access-layer-cs.md), Datatable와 Tableadapter 우리의 DAL에서 형식화 된 데이터 집합으로 구성 됩니다. Datatable 및 식에 적용 된 변경 내용과 데이터베이스를 업데이트 하는 Datatable에 데이터베이스에서 데이터를 읽는 기능을 제공 하는 Tableadapter의 Datatable 데이터를 보관 합니다. TableAdapters 일괄 업데이트 및 DB 직접 참조 하는 데이터를 업데이트 하기 위한 두 가지 패턴을 제공 하는 점에 유의 하세요. 일괄 처리 업데이트 패턴 TableAdapter DataSet, DataTable, 또는 Datarow의 컬렉션을 전달 됩니다. 이 데이터를 열거 하 고 각각에 대해 삽입, 수정 또는 행을 삭제는 `InsertCommand`, `UpdateCommand`, 또는 `DeleteCommand` 실행 됩니다. DB 부하 패턴으로 TableAdapter 삽입, 업데이트 또는 단일 레코드를 삭제 하는 데 필요한 열 값 대신 전달 합니다. DB 직접 패턴 메서드를 사용 하 여 전달 된 값의 적절 한 실행 `InsertCommand`, `UpdateCommand`, 또는 `DeleteCommand` 문.

사용 되는 업데이트 패턴에 관계 없이 자동으로 생성 된 Tableadapter 메서드는 트랜잭션을 사용 하지 마십시오. 기본적으로 각 insert, update 또는 delete TableAdapter 수행한 별도 단일 작업으로 처리 됩니다. 예를 들어, DB 부하 패턴 사용 되도록 BLL에 일부 코드를 데이터베이스에 10 개의 레코드를 삽입 하는 것으로 가정 합니다. 이 코드는 tableadapter 호출 `Insert` 메서드 10 배입니다. 처음 다섯 개의 삽입을 수행할 수 있지만 여섯 번째 한 결과가 예외, 경우에 데이터베이스에 삽입된 한 처음 5 개 레코드 남습니다. 마찬가지로, 일괄 처리 업데이트 패턴 삽입을 수행 하는를 사용 하는 경우 업데이트 및 삭제 하는 삽입 된 수정 및 삭제 된 행, DataTable의 첫 번째 여러 수정 했지만 최신 이전 이러한 수정 사항을 오류가 발생 하는 경우는 완료 된 데이터베이스에 남아 있는 것입니다.

특정 시나리오에서 일련의 수정 내용 걸쳐 원자성을 보장 하기 바랍니다. 실행 하는 새 메서드를 추가 하 여 TableAdapter를 수동으로 확장 해야에서는이를 위해는 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 트랜잭션의 포괄적인 아래 s입니다. [데이터 액세스 계층을 만들려면](../introduction/creating-a-data-access-layer-cs.md) 것을 사용 하 여 살펴 [partial 클래스](http://en.wikipedia.org/wiki/Partial_type) 형식화 된 데이터 집합 내에서 Datatable의 기능을 확장할 합니다. Tableadapter와이 방법을 사용할 수도 있습니다.

형식화 된 데이터 집합 `Northwind.xsd` 에 위치한는 `App_Code` s 폴더 `DAL` 하위 폴더입니다. 하위 폴더를 만들기는 `DAL` 라는 폴더 `TransactionSupport` 라는 새 클래스 파일을 추가 하 고 `ProductsTableAdapter.TransactionSupport.cs` (그림 4 참조). 이 파일을 부분적으로 구현 보유할는 `ProductsTableAdapter` 는 트랜잭션을 사용 하 여 데이터 수정 작업을 수행 하기 위한 메서드를 포함 하는 합니다.


![TransactionSupport 폴더 및 ProductsTableAdapter.TransactionSupport.cs 라는 클래스 파일 추가](wrapping-database-modifications-within-a-transaction-cs/_static/image4.gif)

**그림 4**: 라는 폴더를 추가 `TransactionSupport` 와 명명 된 클래스 파일`ProductsTableAdapter.TransactionSupport.cs`


입력에 다음 코드는 `ProductsTableAdapter.TransactionSupport.cs` 파일:


[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample3.cs)]

`partial` 내에서 추가 된 멤버에 추가 하는 컴파일러에 알리는 키워드를 클래스 선언에는 `ProductsTableAdapter` 클래스에 `NorthwindTableAdapters` 네임 스페이스입니다. 참고는 `using System.Data.SqlClient` 파일 맨 위에 있는 문. TableAdapter가 SqlClient 공급자를 사용 하도록 구성 된 이후 내부적으로 사용 하 여 한 [ `SqlDataAdapter` ](https://msdn.microsoft.com/en-us/library/system.data.sqlclient.sqldataadapter.aspx) 개체를 데이터베이스에 해당 명령을 실행 합니다. 사용 해야 결과적는 `SqlTransaction` 트랜잭션을 시작 하는 클래스 다음 커밋하거나 롤백합니다. Microsoft SQL Server 이외의 데이터 저장소를 사용 하는 경우 적절 한 공급자를 사용 하도록 해야 합니다.

이러한 메서드는 롤백를 시작 하는 데 필요한 구성 요소를 제공 하 고 트랜잭션을 커밋하는 합니다. 표시 된 `public`, 내에서 사용할 수 있도록는 `ProductsTableAdapter`, DAL에서 다른 클래스 또는 BLL 같은 아키텍처의 또 다른 계층입니다. `BeginTransaction`내부 tableadapter를 엽니다 `SqlConnection` (필요한 경우) 트랜잭션을 시작 하 고에 할당 된 `Transaction` 속성을 트랜잭션을 내부에 연결 하 고 `SqlDataAdapter` s `SqlCommand` 개체입니다. `CommitTransaction`및 `RollbackTransaction` 호출는 `Transaction` 개체 s `Commit` 및 `Rollback` 메서드 내부를 닫기 전에 각각 `Connection` 개체입니다.

## <a name="step-3-adding-methods-to-update-and-delete-data-under-the-umbrella-of-a-transaction"></a>3 단계: 업데이트 및 트랜잭션의 포괄적인 정리 된 데이터를 삭제 하는 메서드를 추가

완료 이러한 메서드를 통해 다시 우리 준비가 메서드를 추가 `ProductsDataTable` 또는 일련의 트랜잭션 포괄적인 아래 명령 수행 하는 BLL 합니다. 다음 메서드는 일괄 처리 업데이트 패턴 업데이트를 사용 하 여 한 `ProductsDataTable` 는 트랜잭션을 사용 하 여 인스턴스. 호출 하 여 트랜잭션을 시작는 `BeginTransaction` 메서드를 사용 하 여 한 `try...catch` 블록 데이터 수정 문을 실행 합니다. 경우에 대 한 호출에서 `Adapter` 개체 s `Update` 실행을 전송 하면 예외가 발생 메서드는 `catch` 여기서 트랜잭션이 롤백되어 블록 및 예외 다시 throw 합니다. 이전에 설명한 대로 `Update` 제공 된 행을 열거 하 여 일괄 처리 업데이트 패턴을 구현 하는 메서드 `ProductsDataTable` 수행 하는 데 필요한 및 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` s입니다. 중 하나가 없으면 오류가이 명령 결과 트랜잭션이 롤백하지 트랜잭션의 수명 동안 이전 수정 실행 취소 합니다. 해야는 `Update` 문을 오류 없이 완료, 전체에서 트랜잭션이 커밋됩니다.


[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample4.cs)]

추가 `UpdateWithTransaction` 메서드는 `ProductsTableAdapter` 클래스의 partial 클래스를 통해 `ProductsTableAdapter.TransactionSupport.cs`합니다. 비즈니스 논리 계층 s에이 메서드를 추가할 수 없습니다 또는 `ProductsBLL` 약간 구문상의 차이가 있는 클래스입니다. 즉, 키워드에이 `this.BeginTransaction()`, `this.CommitTransaction()`, 및 `this.RollbackTransaction()` 으로 대체 해야 `Adapter` (이전에 설명한 대로 `Adapter` 에서 속성의 이름 `ProductsBLL` 형식의 `ProductsTableAdapter`).

`UpdateWithTransaction` 메서드는 일괄 처리 업데이트 패턴을 사용 하지만 메서드는 다음과 같이 트랜잭션의 범위 내에서 일련의 DB 직접 호출 사용할 수도 있습니다. `DeleteProductsWithTransaction` 메서드 입력으로 받아들입니다는 `List<T>` 형식의 `int`는 `ProductID` s를 삭제 합니다. 메서드 호출을 통해 트랜잭션을 시작 `BeginTransaction` 를 선택한 후는 `try` 차단, DB 직접 패턴 호출 제공 된 목록에서 반복 `Delete` 메서드 각각에 대해 `ProductID` 값입니다. 경우에 대 한 호출 `Delete` 실패로 제어가 전달 되는 `catch` 트랜잭션이 롤백 여기서 블록 및 예외 다시 throw 합니다. 모든 호출 하는 경우 `Delete` 성공적으로 트랜잭션이 커밋됩니다. 이 메서드를 추가 `ProductsBLL` 클래스입니다.


[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample5.cs)]

## <a name="applying-transactions-across-multiple-tableadapters"></a>여러 Tableadapter에서 트랜잭션을 적용

이 자습서에서 검사 하는 트랜잭션 관련 코드에 대 한 여러 문을 허용 된 `ProductsTableAdapter` 원자 단위 연산으로 처리 됩니다. 하지만 다른 데이터베이스 테이블의 여러 수정을 원자 단위로 수행 해야 하는 경우에 어떻게? 예를 들어, 범주를 삭제할 때 수 먼저 하려고 다른 범주에 현재 제품을 다시 할당 합니다. 제품을 다시 할당 하 고는 범주를 삭제 하면 다음 두 단계는 원자성 작업으로 실행 되어야 합니다. 하지만 `ProductsTableAdapter` 수정 하기 위한 방법만 포함 됩니다는 `Products` 테이블 및 `CategoriesTableAdapter` 수정 하기 위한 방법만 포함 됩니다는 `Categories` 테이블입니다. 트랜잭션 수 모두 Tableadapter를 포함 하는 방식을 보여 주는

첫 번째 방법은 메서드를 추가 하는 `CategoriesTableAdapter` 라는 `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` 있고 해당 메서드는 제품을 다시 할당 하 고 저장된 프로시저 내에 정의 된 트랜잭션 범위 내에서 범주를 제거 하는 저장된 프로시저를 호출 합니다. 살펴보게 시작, 커밋, 하는 방법 및 저장된 프로시저에서 트랜잭션을 롤백하는 이후 자습서에서 합니다.

포함 하는 DAL에서 도우미 클래스를 만드는 또 다른 옵션은는 `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` 메서드. 인스턴스를 만들 것이 메서드는 `CategoriesTableAdapter` 및 `ProductsTableAdapter` 다음 이러한 두 Tableadapter를 설정 하 고 `Connection` 동일 하 게 속성 `SqlConnection` 인스턴스. At 두 Tableadapter 중 하나가 발생 지점에 대 한 호출을 사용 하 여 트랜잭션을 시작 하는 `BeginTransaction`합니다. 제품을 다시 할당 하 고 범주를 삭제 하기 위한 Tableadapter 메서드가 호출 되는 `try...catch` 필요에 따라 다시 트랜잭션이 커밋 또는 롤백됨 트랜잭션 사용 하 여 블록입니다.

## <a name="step-4-adding-theupdatewithtransactionmethod-to-the-business-logic-layer"></a>4 단계: 추가 된`UpdateWithTransaction`비즈니스 논리 계층 메서드

3 단계에서에서 추가한 이유는 `UpdateWithTransaction` 메서드를는 `ProductsTableAdapter` DAL에서 합니다. BLL에 해당 하는 메서드를 추가 해야 했습니다. 프레젠테이션 계층 DAL 호출 하려면 아래쪽으로 직접 호출 하 여는 동안는 `UpdateWithTransaction` 메서드를 이러한 자습서 프레젠테이션 계층에서 DAL을 분리 하는 계층화 된 아키텍처를 정의 하려면 strived 있어야 합니다. 따라서이 방법은 계속를 behooves 합니다.

열기는 `ProductsBLL` 라는 메서드를 추가 하 고 클래스 파일 `UpdateWithTransaction` 호출 하는 단순히 해당 DAL 메서드 다운 합니다. 에 두 가지 방법이 있어야 `ProductsBLL`: `UpdateWithTransaction`, 방금 추가한 있는 및 `DeleteProductsWithTransaction`, 3 단계에서에서 추가한 합니다.


[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample6.cs)]

> [!NOTE]
> 이러한 메서드를 포함 하지 않습니다는 `DataObjectMethodAttribute` 의 다른 메서드에 대부분에 할당 된 특성의 `ProductsBLL` 클래스에서는 ASP.NET 페이지 코드 숨김 클래스에서 직접 이러한 메서드를 호출 하 여야 합니다. 이전에 설명한 대로 `DataObjectMethodAttribute` 플래그 지정 하는 방법을 구성 데이터 원본 마법사 (SELECT, UPDATE, INSERT 또는 DELETE) 어떤 탭 아래에서 ObjectDataSource s에 표시 되어야 하는 데 사용 됩니다. GridView 편집 또는 삭제 일괄 처리에 대 한 모든 기본 제공 지원 없으므로 코드 없이 선언적 접근 방식을 사용 하는 대신 프로그래밍 방식으로 이러한 메서드를 호출 해야 합니다.


## <a name="step-5-atomically-updating-database-data-from-the-presentation-layer"></a>5 단계: 프레젠테이션 계층에서 데이터베이스 데이터를 자동으로 업데이트

일괄 처리 레코드를 업데이트할 때 있음을 효과 보여 주기 위해 let s는 GridView의 모든 제품을 나열 하 고 단추 웹을 포함 하는 사용자 인터페이스를 만들 컨트롤을 클릭 하면 제품 재할당 `CategoryID` 값입니다. 첫 번째 몇 가지 제품은 유효한 할당 되도록 범주 재할당 진행 되는 특히 `CategoryID` 이지만 나머지는 의도적으로 값이 존재 하지 할당 `CategoryID` 값입니다. 제품으로 데이터베이스를 업데이트 하려고 하는 경우 해당 `CategoryID` s 기존 범주와 일치 하지 않습니다 `CategoryID`외래 키 제약 조건 위반이 발생 하며, 및 예외가 발생 합니다. 이 예제에 맞게 살펴보겠습니다 않은 트랜잭션에서 외래 키 제약 조건 위반이 발생 한 예외를 사용 하 여 이전 하면 유효한 `CategoryID` 변경 내용을 롤백할 수 있습니다. 그러나 트랜잭션을 사용 하지 않을 때 수정 사항을 초기 범주에 유지 됩니다.

열어 시작는 `Transactions.aspx` 페이지에 `BatchData` 폴더와 디자이너 도구 상자에서 끌어서는 GridView입니다. 설정의 `ID` 를 `Products` 및 스마트 태그를 바인딩할 라는 새 ObjectDataSource `ProductsDataSource`합니다. 구성에서 해당 데이터를 가져오도록 ObjectDataSource는 `ProductsBLL` s 클래스 `GetProducts` 메서드. 이 읽기 전용 GridView, 하므로 UPDATE, INSERT에서에서 드롭 다운 목록을 설정 하 고 각 탭 (없음)을 삭제 되며 마침을 클릭 합니다.


[![그림 5: ObjectDataSource ProductsBLL 클래스의 GetProducts 메서드를 사용 하도록 구성](wrapping-database-modifications-within-a-transaction-cs/_static/image5.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image3.png)

**그림 5**: 그림 5: 구성에 사용 하 여 ObjectDataSource는 `ProductsBLL` s 클래스 `GetProducts` 메서드 ([전체 크기 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-cs/_static/image4.png))


[![삽입, 업데이트에서 드롭 다운 목록을 설정 하 고 탭 (없음)를 삭제](wrapping-database-modifications-within-a-transaction-cs/_static/image6.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image5.png)

**그림 6**: 드롭 다운 목록에서 업데이트, 삽입 및 삭제 탭 하도록 설정 (None) ([전체 크기 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-cs/_static/image6.png))


데이터 소스 구성 마법사를 완료 한 후 Visual Studio BoundFields 및 제품 데이터 필드에 대 한 CheckBoxField 만들어집니다. 이 필드를 제외 하 고 제거 `ProductID`, `ProductName`, `CategoryID`, 및 `CategoryName` 및 이름 바꾸기는 `ProductName` 및 `CategoryName` BoundFields `HeaderText` 속성 범주 및 제품을 각각. 스마트 태그에서 페이징 사용 옵션을 선택 합니다. 이러한 수정에 확인 한 후 GridView 및 ObjectDataSource s 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample7.aspx)]

다음으로 GridView 위에 세 개의 단추 웹 컨트롤을 추가 합니다. 새로 고침 그리드, 수정 범주 (된 트랜잭션), 두 번째 s 및 세 번째 하나 s 수정 범주 (없이 트랜잭션)를 첫 번째 단추의 Text 속성을 설정 합니다.


[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample8.aspx)]

이 시점에서 Visual Studio의 디자인 뷰에서 스크린샷과 그림 7에 표시 된 비슷해야 합니다.


[![페이지에는 GridView과 세 개의 단추 웹 컨트롤](wrapping-database-modifications-within-a-transaction-cs/_static/image7.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image7.png)

**그림 7**:는 페이지에 GridView과 세 개의 단추 웹 컨트롤 ([전체 크기 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-cs/_static/image8.png))


각 s 세 단추에 대 한 이벤트 처리기 만들기 `Click` 이벤트 및 다음 코드를 사용 하 여:


[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample9.cs)]

새로 고침 단추 s `Click` 호출 하 여 이벤트 처리기 단순히 다시 바인딩 횟수 GridView에 데이터는 `Products` GridView의 `DataBind` 메서드.

두 번째 이벤트 처리기는 제품 재할당 `CategoryID` s 및 사용 하 여 데이터베이스를 수행 하려면 BLL에서 새 트랜잭션 메서드 라는 큰 트랜잭션 업데이트 합니다. 각 제품 s `CategoryID` 임의로 동일한 값으로 설정 되어 해당 `ProductID`합니다. 정상적으로 작동 합니다 첫 번째에 대 한 몇 가지 제품 해당 제품에는 이후 `ProductID` 유효한에 매핑할 발생 하는 값 `CategoryID` s입니다. 하지만 한 번의 `ProductID` 너무 커지지 s 시작, 잠금의 겹쳐진 부분이 우연의 일치 `ProductID` s 및 `CategoryID` s 적용 되지 않습니다.

세 번째 `Click` 이벤트 처리기를 업데이트 하는 제품 `CategoryID` s 동일한 방식으로 사용 하 여 데이터베이스에 업데이트를 전송 하지만 `ProductsTableAdapter` s 기본 `Update` 메서드. 이 `Update` 메서드 일련의 트랜잭션 내에서 명령으로 바뀌지 않으며, 첫 번째 발생 한 외래 키 제약 조건 위반 오류 이전에 이러한 변경 내용이 있으므로 계속 유지 됩니다.

이 동작을 재현 하려면 브라우저를 통해이 페이지를 방문 합니다. 처음 그림 8에 나와 있는 것 처럼 데이터의 첫 번째 페이지를 표시 됩니다. 다음으로 수정 범주 (된 트랜잭션) 단추를 클릭 합니다. 포스트백을 발생 되 고 모든 제품을 업데이트 하려고 `CategoryID` 값 이지만 외래 키 제약 조건 위반 하 게 발생 됩니다 (그림 9 참조).


[![제품은 페이징 가능한 GridView에 표시 됩니다.](wrapping-database-modifications-within-a-transaction-cs/_static/image8.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image9.png)

**그림 8**: The 제품 페이징 가능한 GridView에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-cs/_static/image10.png))


[![외래 키 제약 조건 위반 하 게 범주 결과 다시 할당](wrapping-database-modifications-within-a-transaction-cs/_static/image9.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image11.png)

**그림 9**: 다시 할당 하는 외래 키 제약 조건 위반에 범주 결과 ([전체 크기 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-cs/_static/image12.png))


이제 s 브라우저 뒤로 단추를 모눈 새로 고침 단추 클릭 \ 0. 데이터 새로 고침 시 그림 8에 표시 된 대로 정확히 동일한 출력이 표시 됩니다. 즉,에 있지만 일부 제품 `CategoryID` s 법률에 변경 된 값을 되 고 데이터베이스에서 업데이트 롤백 되었으므로 외래 키 제약 조건 위반이 발생 한 경우.

이제 수정 범주 (트랜잭션 없이) 단추를 클릭 해 보십시오. 동일한 외래 키 제약 조건 위반 오류 이렇게 하면 (그림 9 참조) 집계 하고자 하지만 이러한 제품을 시간별이 인 `CategoryID` 법적 값이 변경 되었는지 값은 롤백되지 않습니다. S 브라우저 뒤로 단추 및 그리드 새로 고침 단추에 도달 했습니다. 그림 10과 같이 `CategoryID` 처음 8 개 제품의 s 다시 할당 된 합니다. 예를 들어 그림 8에서 파일과 변경에는 `CategoryID` 1의 그림 10 it s에 다시 할당 된 2로 하지만 합니다.


[![일부 제품 CategoryID 값 없습니다. 업데이트 하는 동안 다른 되었습니다](wrapping-database-modifications-within-a-transaction-cs/_static/image10.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image13.png)

**그림 10**: 일부 제품 `CategoryID` 값 없습니다. 업데이트 하는 동안 다른 않았습니다 ([전체 크기 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-cs/_static/image14.png))


## <a name="summary"></a>요약

기본적으로 TableAdapter의 메서드는 트랜잭션의 범위 내에서 실행 된 데이터베이스 문은 줄 바꿈하지 않습니다 되지만 약간의 작업으로 추가할 수 있습니다 메서드를 만들기, commit 및 rollback 트랜잭션. 이 자습서에서는 이러한 세 가지 방법 만든는 `ProductsTableAdapter` 클래스: `BeginTransaction`, `CommitTransaction`, 및 `RollbackTransaction`합니다. 와 함께 이러한 메서드를 사용 하는 방법에 살펴보았습니다는 `try...catch` 블록 원자성 일련의 데이터 수정 문 수 있도록 합니다. 만든 특히는 `UpdateWithTransaction` 에서 메서드는 `ProductsTableAdapter`, 일괄 처리 업데이트 패턴의 제공 된 행에 필요한 수정 작업을 수행 하는를 사용 하 여 `ProductsDataTable`합니다. 도 추가 `DeleteProductsWithTransaction` 메서드를는 `ProductsBLL` 허용 BLL에는 클래스는 `List` 의 `ProductID` 입력으로 값을 직접 DB 패턴 메서드를 호출 `Delete` 각 `ProductID`합니다. 두 방법 모두 트랜잭션을 만들고 다음 내에서 데이터 수정 문을 실행 하 여 시작 된 `try...catch` 블록입니다. 예외가 발생할 경우 트랜잭션이 롤백되면이 고 그렇지 않으면 커밋된 합니다.

5 단계는 트랜잭션을 사용 하 여 연락 하는 일괄 처리 업데이트와 업데이트 트랜잭션 일괄 처리의 효과를 보여 줍니다. 다음 세 개의 자습서에서이 자습서에 기초를 구축 하 고 일괄 처리 업데이트, 삭제 및 삽입을 수행 하기 위한 사용자 인터페이스를 작성 합니다.

만족도 매우 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [트랜잭션 사용 하 여 데이터베이스 일관성을 유지 관리](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx)
- [SQL Server에서 트랜잭션 관리 저장 프로시저](http://www.4guysfromrolla.com/webtech/080305-1.shtml)
- [간편해 진 트랜잭션의 경우:`System.Transactions`](https://blogs.msdn.com/florinlazar/archive/2004/07/23/192239.aspx)
- [TransactionScope 및 Dataadapter](http://andyclymer.blogspot.com/2007/01/transactionscope-and-dataadapters.html)
- [.NET에서 Oracle 데이터베이스 트랜잭션 사용](http://www.oracle.com/technology/pub/articles/price_dbtrans_dotnet.html)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자가 Dave Gardner, Hilton Giesenow 및 Teresa 머피의 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[다음](batch-updating-cs.md)
