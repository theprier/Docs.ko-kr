---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-vb
title: "(VB) 조인 TableAdapter를 사용 하 여 업데이트 | Microsoft Docs"
author: rick-anderson
description: "데이터베이스 작업을 수행 하는 경우에 데이터를 요청 하는 여러 테이블에 분산 되어 일반적입니다. 서로 다른 두 테이블에서 데이터를 검색 하려면 하나를 사용 하면..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/18/2007
ms.topic: article
ms.assetid: e624a3e0-061b-4efc-8b0e-5877f9ff6714
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-vb
msc.type: authoredcontent
ms.openlocfilehash: bb0b80f63ea69bb12a28f01193946f5689e70fb9
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="updating-the-tableadapter-to-use-joins-vb"></a>(VB) 조인 TableAdapter를 사용 하 여 업데이트
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_69_VB.zip) 또는 [PDF 다운로드](updating-the-tableadapter-to-use-joins-vb/_static/datatutorial69vb1.pdf)

> 데이터베이스 작업을 수행 하는 경우에 데이터를 요청 하는 여러 테이블에 분산 되어 일반적입니다. 두 개의 다른 테이블에서 데이터를 검색할 상관된 하위 쿼리 또는 조인 작업 중 하나를 사용할 수 있습니다. 이 자습서에서는 비교 상관된 하위 쿼리 및 조인 구문의 주 쿼리에서 조인을 포함 하는 TableAdapter를 만드는 방법을 살펴보기 전에 합니다.


## <a name="introduction"></a>소개

관계형 데이터베이스와 작업에 필요한 데이터는 종종 분산 여러 테이블. 예를 들어 제품 정보를 표시할 때 가능성이 하고자 각 제품 s 해당 범주와 공급 업체의 이름이 나열 합니다. `Products` 테이블에 `CategoryID` 및 `SupplierID` 값, 하지만 실제 범주와 공급 업체 이름에 있는 `Categories` 및 `Suppliers` 각각 테이블입니다.

사용 하거나 다른, 관련 테이블에서 정보를 검색 하려면 원하므로 *상관 하위 쿼리* 또는 `JOIN` *s*합니다. 상관된 하위 쿼리 중첩 된 `SELECT` 는 외부 쿼리의 열을 참조 하는 쿼리입니다. 예를 들어는 [데이터 액세스 계층을 만들려면](../introduction/creating-a-data-access-layer-vb.md) 자습서에서 두 개의 상관된 하위 쿼리 했었습니다는 `ProductsTableAdapter` 각 제품 범주 및 공급 업체 이름을 반환 하려면 s 주 쿼리 합니다. A `JOIN` 는 두 개의 서로 다른 테이블의 관련된 행을 병합 하는 SQL 구문입니다. 사용 하는 `JOIN` 에 [SqlDataSource 컨트롤을 사용 하 여 데이터를 쿼리](../accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-vb.md) 함께 각 제품 범주 정보를 표시 하는 자습서입니다.

사용 하 여 abstained가 म 이유 `JOIN` 자동 생성에 해당 하는 TableAdapter의 마법사의 제한 때문에 Tableadapter와 s는 `INSERT`, `UPDATE`, 및 `DELETE` 문. 보다 구체적으로, TableAdapter s 주 쿼리 하나가 포함 된 경우 `JOIN` s, TableAdapter 없습니다 자동 생성 임시 SQL 문 또는 저장된 프로시저에 대 한 해당 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성입니다.

이 자습서는 간단 하 게 비교 및 대비 상관 하위 쿼리 및 `JOIN` s를 포함 하는 TableAdapter를 만드는 방법을 살펴보기 전에 `JOIN` s의 주 쿼리에서 합니다.

## <a name="comparing-and-contrasting-correlated-subqueries-andjoin-s"></a>비교 및 대조 상관 하위 쿼리 및`JOIN` s

이전에 설명한 대로 `ProductsTableAdapter` 의 첫 번째 자습서에서 만든는 `Northwind` DataSet 상관된 하위 쿼리를 사용 하 여 각 제품 s 해당 범주와 공급 업체 이름 돌아가려고 합니다. `ProductsTableAdapter` s 주 쿼리 아래에 표시 됩니다.


[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample1.sql)]

두 개의 상관 하위 쿼리- `(SELECT CategoryName FROM Categories WHERE Categories.CategoryID = Products.CategoryID)` 및 `(SELECT CompanyName FROM Suppliers WHERE Suppliers.SupplierID = Products.SupplierID)` -는 `SELECT` 제품당 하나의 값을 외부에서 추가 열으로 반환 하는 쿼리 `SELECT`의 문 열 목록입니다.

또는 한 `JOIN` 는 각 제품 s 공급 업체와 범주 이름을 반환 하는 데 사용할 수 있습니다. 다음 쿼리는 위의 것과 동일한 출력을 반환 하지만 사용 하 여 `JOIN` 하위 쿼리 대신 s:


[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample2.sql)]

A `JOIN` 일부 조건에 따라 다른 테이블의 레코드와 한 테이블에서 레코드를 병합 합니다. 예를 들어 위의 쿼리에서 `LEFT JOIN Categories ON Categories.CategoryID = Products.CategoryID` 사용 하면 SQL Server 병합 각 범주와 제품 레코드를 기록 하는 `CategoryID` 값과 s 제품 일치 `CategoryID` 값입니다. 병합 된 결과 통해 각 제품에 대 한 해당 범주 필드를 사용 하 여 (예: `CategoryName`).

> [!NOTE]
> `JOIN`s 관계형 데이터베이스에서 데이터를 쿼리할 때 자주 사용 됩니다. 처음 사용 하는 경우는 `JOIN` 구문 또는 사용법에 대 약간 브러시를 사용 하는 필요성 d 것이 좋습니다.는 [SQL Join 자습서](http://www.w3schools.com/sql/sql_join.asp) 에서 [W3 학교](http://www.w3schools.com/)합니다. 또한 읽기 가치는 [ `JOIN` 기본 사항](https://msdn.microsoft.com/en-us/library/ms191517.aspx) 및 [하위 쿼리 기본 사항](https://msdn.microsoft.com/en-us/library/ms189575.aspx) 의 섹션은 [SQL 온라인 설명서](https://msdn.microsoft.com/en-us/library/ms130214.aspx)합니다.


이후 `JOIN` s와 상관된 하위 쿼리 둘 다 사용할 수 다른 테이블에서 관련된 데이터를 검색, 머리 보이지 않는 하 고 사용할 방법에 다음이 궁금할 많은 개발자에 게 남아 있습니다. 모든 SQL gurus I 간의 대화와 거의 동일한 작업에 설명 했습니다 한다는 대상이 t 중요 성능 관점에서 보면으로 SQL Server와 거의 동일한 실행 계획을 생성 합니다. 그런 다음 해당 조언을 팀과 가장 익숙한 기술을 사용 하 고 되려고 합니다. 이 충고를 전달 하는 후 이러한 전문가 즉시 express의 기본 설정의 데이터에 해당 `JOIN` 상관된 하위 쿼리를 통해 s입니다.

형식화 된 데이터 집합을 사용 하 여 데이터 액세스 계층을 만들 때 도구는 하위 쿼리를 사용 하는 경우에 더 잘 작동 합니다. 특히, s TableAdapter 마법사는 하지 자동 생성에 해당 `INSERT`, `UPDATE`, 및 `DELETE` 주 쿼리에서 하나가 포함 된 경우 문을 `JOIN` s, 하지만 생성 합니다. 자동-상관 관계가 지정 된 경우 이러한 문은 하위 쿼리 사용 됩니다.

이러한 단점을 탐색 하려면 임시 형식화 된 데이터 집합 만들기에 `~/App_Code/DAL` 폴더입니다. TableAdapter 구성 마법사는 동안 임시 SQL 문을 사용 하 고 다음을 입력 하도록 선택할 `SELECT` 쿼리 (그림 1 참조).


[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample3.sql)]


[![조인을 포함 하는 주 쿼리를 입력 합니다.](updating-the-tableadapter-to-use-joins-vb/_static/image2.png)](updating-the-tableadapter-to-use-joins-vb/_static/image1.png)

**그림 1**: 포함 된 주 쿼리를 입력 `JOIN` s ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image3.png))


TableAdapter 기본적으로 자동으로 만들어집니다 `INSERT`, `UPDATE`, 및 `DELETE` 문을 주 쿼리를 기반 합니다. 고급 단추를 클릭 하는 경우이 기능이 설정 되어 있음을 확인할 수 있습니다. 이 설정은 불구 하 고 TableAdapter 됩니다 만들 수는 `INSERT`, `UPDATE`, 및 `DELETE` 문 기본 쿼리에 포함 되어 있으므로 `JOIN`합니다.


![조인을 포함 하는 주 쿼리를 입력 합니다.](updating-the-tableadapter-to-use-joins-vb/_static/image4.png)

**그림 2**: 포함 하는 주 쿼리를 입력 `JOIN` s


마법사를 완료 하려면 마침을 클릭 합니다. 이 시점에서 사용자 데이터 집합 디자이너는 포함 되어 열이 있는 DataTable 사용 하 여 단일 TableAdapter에 반환 되는 필드의 각는 `SELECT`의 쿼리 열 목록입니다. 여기에 `CategoryName` 및 `SupplierName`그림 3과 같이, 합니다.


![DataTable의 열 목록에 반환 된 각 필드에 대 한 열이 포함 됩니다.](updating-the-tableadapter-to-use-joins-vb/_static/image5.png)

**그림 3**: DataTable에 열이 열 목록에 반환 된 각 필드에 대 한


TableAdapter에 대 한 값에 DataTable의 적절 한 열에 있으면 해당 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성입니다. 이 확인 하려면 디자이너의 TableAdapter에서 클릭 한 다음 속성 창으로 이동 합니다. 발생 했음을 알 수 있습니다는 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성 (없음)으로 설정 됩니다.


[![InsertCommand, UpdateCommand, 및 DeleteCommand 속성 (없음)로 설정 되어](updating-the-tableadapter-to-use-joins-vb/_static/image7.png)](updating-the-tableadapter-to-use-joins-vb/_static/image6.png)

**그림 4**:는 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성 (없음)으로 설정 됩니다 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image8.png))


이러한 단점을 해결 하려면 수동으로 가능해 집니다 SQL 문 및에 대 한 매개 변수는 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성은 속성 창. 또는 TableAdapter s 주 쿼리를 구성 하 여 시작할 수 있을 것 *하지* 포함 하는 `JOIN` s입니다. 이렇게 하면는 `INSERT`, `UPDATE`, 및 `DELETE` 문을에 자동으로 생성 해야 합니다. 마법사를 완료 한 후 업데이트할 수 있습니다 다음 수동으로 TableAdapter s `SelectCommand` 포함 하도록 속성 창에서는 `JOIN` 구문입니다.

이 접근 방식은 것은 매우 불안정 TableAdapter s 주 쿼리 언제 든 지 때문에 임시 SQL 쿼리를 사용 하는 것이 자동으로 생성 하는 마법사를 통해 다시 구성할 때 `INSERT`, `UPDATE`, 및 `DELETE` 문을 다시 작성 됩니다. TableAdapter를 마우스 오른쪽 단추로 클릭, 상황에 맞는 메뉴에서 구성 선택 하 고 마법사를 다시 완료 경우 손실 될를 나중에 수행 하는 사용자 지정 항목의 모든 것입니다.

자동 생성 된 tableadapter의 오류 `INSERT`, `UPDATE`, 및 `DELETE` 문을 이면 다행히 임시 SQL 문이로 제한 합니다. 저장된 프로시저를 사용 하 여 TableAdapter를 사용자 지정할 수 있습니다는 `SelectCommand`, `InsertCommand`, `UpdateCommand`, 또는 `DeleteCommand` 저장 프로시저와 저장된 프로시저 된다는 것을 걱정 하지 않고 TableAdapter 구성 마법사를 다시 실행 합니다. 수정 합니다.

다음을 통해 만듭니다 TableAdapter는 처음에 몇 가지 단계 사용 하 여 모든 생략 하는 기본 쿼리에서 `JOIN` s 삽입할 해당 업데이트 및 삭제 저장 프로시저를 자동으로 생성 됩니다. 그런 다음 업데이트 됩니다는 `SelectCommand` 있으므로 사용 하는 `JOIN` 관련된 테이블에서 추가 열을 반환 하 합니다. 마지막으로, 해당 비즈니스 논리 계층 클래스를 만든 알아보고 TableAdapter를 사용 하 여 ASP.NET 웹 페이지의 설명 하겠습니다.

## <a name="step-1-creating-the-tableadapter-using-a-simplified-main-query"></a>1 단계: 간소화 된 주 쿼리를 사용 하 여 TableAdapter 만들기

이 자습서는 TableAdapter 및 추가 대 한 강력한 형식의 DataTable의 `Employees` 테이블에 `NorthwindWithSprocs` 데이터 집합입니다. `Employees` 테이블에는 `ReportsTo` 지정 필드는 `EmployeeID`의 직원 관리자의 합니다. Anne 병 우에 직원 예를 들어는 `ReportTo` 가 5의 값은 `EmployeeID` 정훈의 합니다. 따라서 Anne 서, 관리자에 보고합니다. 각 직원 s 보고 함께 `ReportsTo` 값 하고자 할 수 있습니다도 해당 관리자의 이름을 검색 합니다. 이 사용 하 여 수행할 수는 `JOIN`합니다. 하지만 사용 하 여 한 `JOIN` 때 자동으로 생성 되는 해당 하는 삽입에서 마법사에 의해 처음에 TableAdapter 만들기, 업데이트 및 삭제 기능입니다. 따라서 먼저 해당 주 쿼리에 포함 하지 않으면 TableAdapter를 만든 `JOIN` s입니다. 그런 다음 2 단계에서에서 업데이트할 것 주 쿼리 저장 프로시저를 통해 관리자의 이름을 검색 하는 `JOIN`합니다.

열어 시작는 `NorthwindWithSprocs` 에서 데이터 집합의 `~/App_Code/DAL` 폴더입니다. 디자이너, 상황에 맞는 메뉴 추가 옵션을 선택 고 TableAdapter 메뉴 항목을 선택 합니다. TableAdapter 구성 마법사를 시작 됩니다. 그림 5 보여주고 처럼 새 저장된 프로시저를 만들고 다음을 클릭 하 여 마법사를 가집니다. 새로운 세부 정보 저장 프로시저를 TableAdapter의 마법사에 대 한 참조는 [새 저장 프로시저 만들기 형식의 DataSet s Tableadapter에 대 한](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 자습서입니다.


[![새 저장된 프로시저 만들기 옵션을 선택 합니다.](updating-the-tableadapter-to-use-joins-vb/_static/image10.png)](updating-the-tableadapter-to-use-joins-vb/_static/image9.png)

**그림 5**: 새 저장 프로시저 옵션 선택 만들기 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image11.png))


다음을 사용 하 여 `SELECT` TableAdapter s 주 쿼리에 대 한 문을:


[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample4.sql)]

이후이 쿼리에 포함 하지 않습니다 `JOIN` s, TableAdapter를 자동으로 만듭니다 저장된 프로시저에 해당 포함 된 `INSERT`, `UPDATE`, 및 `DELETE` 문, 뿐 아니라 주 실행 되도록 저장된 프로시저 쿼리입니다.

다음 단계에는 TableAdapter s 저장 프로시저 이름을 수 있습니다. 이름을 사용 하 여 `Employees_Select`, `Employees_Insert`, `Employees_Update`, 및 `Employees_Delete`그림 6에 나와 있는 것 처럼, 합니다.


[![TableAdapter s 저장 프로시저 이름](updating-the-tableadapter-to-use-joins-vb/_static/image13.png)](updating-the-tableadapter-to-use-joins-vb/_static/image12.png)

**그림 6**: TableAdapter s 저장 프로시저 이름을 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image14.png))


마지막 단계에서 TableAdapter의 메서드 이름을 지정 하 라는 메시지가 나타납니다. 사용 하 여 `Fill` 및 `GetEmployees` 메서드 이름으로 합니다. 또한 데이터베이스 (GenerateDBDirectMethods) checkbox 선택에 직접 업데이트를 보내는 메서드 만들기를 유지 해야 합니다.


[![TableAdapter의 메서드 채우기 이름과 GetEmployees](updating-the-tableadapter-to-use-joins-vb/_static/image16.png)](updating-the-tableadapter-to-use-joins-vb/_static/image15.png)

**그림 7**: tableadapter 메서드 이름을 `Fill` 및 `GetEmployees` ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image17.png))


마법사를 완료 한 후 데이터베이스의 저장된 프로시저를 검사 하려면 보십시오. 4 개의 새로 표시 됩니다: `Employees_Select`, `Employees_Insert`, `Employees_Update`, 및 `Employees_Delete`합니다. 다음으로 검사는 `EmployeesDataTable` 및 `EmployeesTableAdapter` 방금 만든 합니다. DataTable 주 쿼리에서 반환 된 각 필드에 대 한 열을 포함 합니다. TableAdapter 클릭 한 다음 속성 창으로 이동 합니다. 발생 했음을 알 수 있습니다는 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성이 해당 저장된 프로시저를 호출할 제대로 구성 되어 있습니다.


[![TableAdapter 포함 삽입, 업데이트 및 삭제 기능](updating-the-tableadapter-to-use-joins-vb/_static/image19.png)](updating-the-tableadapter-to-use-joins-vb/_static/image18.png)

**그림 8**: TableAdapter 포함 Insert, Update 및 Delete 기능 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image20.png))


삽입, 업데이트 및 delete 저장된 프로시저를 자동으로 생성 및 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 을 사용자 지정할 수는 올바르게 구성 속성는 `SelectCommand` s 저장 프로시저를 추가로 반환 각 직원의 관리자에 대 한 정보입니다. 특히, 업데이트 해야는 `Employees_Select` 저장 프로시저를 사용 하 여 한 `JOIN` s 관리자를 반환 하 고 `FirstName` 및 `LastName` 값입니다. 저장된 프로시저가 업데이트 된 후 이러한 추가 열 포함 되도록 DataTable을 업데이트 해야 합니다. 이 두 가지 작업 단계 2에서와 3 해결할 합니다.

## <a name="step-2-customizing-the-stored-procedure-to-include-ajoin"></a>2 단계: 사용자를 포함 하도록 저장된 프로시저 정의`JOIN`

시작 하 여 서버 탐색기로 이동, Northwind 데이터베이스 s 저장 프로시저 폴더를 차례로 드릴 다운을 열면는 `Employees_Select` 저장 프로시저입니다. 이 저장된 프로시저 표시 되지 않으면 저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 새로 고침을 선택 합니다. 사용 하도록 저장된 프로시저를 업데이트 한 `LEFT JOIN`의 관리자를 먼저 반환 하 고 이름을 마지막에:


[!code-sql[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample5.sql)]

업데이트 한 후의 `SELECT` 파일 메뉴로 이동 하 고 저장을 선택 하 여 변경 내용 저장할 문을 `Employees_Select`합니다. 또는 도구 모음에 저장 아이콘을 클릭 하거나 Ctrl + S를 적중 수 있습니다. 변경 내용을 저장 한 후 마우스 오른쪽 단추로 클릭는 `Employees_Select` 서버 탐색기에서 프로시저를 저장 하 고 실행을 선택 합니다. 이 저장된 프로시저를 실행 하 고 출력 창에 해당 결과 표시 됩니다 (그림 9 참조).


[![저장 프로시저 결과 출력 창에 표시 됩니다.](updating-the-tableadapter-to-use-joins-vb/_static/image22.png)](updating-the-tableadapter-to-use-joins-vb/_static/image21.png)

**그림 9**: 저장 프로시저 결과 출력 창에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image23.png))


## <a name="step-3-updating-the-datatable-s-columns"></a>DataTable의 열을 업데이트 하는 3 단계:

이 시점에서 `Employees_Select` 저장 프로시저 반환 `ManagerFirstName` 및 `ManagerLastName` 값 이지만 `EmployeesDataTable` 이러한 열이 없습니다. 누락 된 열이 두 가지 방법 중 하나에 DataTable에 추가할 수 있습니다.

- **수동으로** -데이터 집합 디자이너에서 DataTable을 마우스 오른쪽 단추로 클릭 하 고, 추가 메뉴에서 열을 선택 합니다. 다음 열의 이름을 하 고 그에 따라 해당 속성을 설정할 수입니다.
- **자동으로** -TableAdapter 구성 마법사가 DataTable의 열에서 반환 되는 필드를 반영 하도록 업데이트는 `SelectCommand` 저장 프로시저입니다. 임시 SQL 문이 사용할 때는 마법사도 제거 됩니다는 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 이후 속성은 `SelectCommand` 이제 포함 한 `JOIN`합니다. 하지만 이러한 명령 속성은 그대로 저장된 프로시저를 사용 하는 경우.

이전 자습서에서는 포함 하 여 수동으로 추가 DataTable 열을 탐색 했습니다 우리 [마스터/세부 레코드를 사용 하는 글머리 기호 목록의 마스터 세부 정보 사용](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md) 및 [파일 업로드](../working-with-binary-files/uploading-files-vb.md), 우리는 다음이 자습서에서이 과정을 자세히 다시 확인 합니다. 그러나이 자습서에 대 한 s TableAdapter 구성 마법사를 통해 자동 접근 방식을 사용을 사용 합니다.

마우스 오른쪽 단추로 클릭 하 여 시작 된 `EmployeesTableAdapter` 상황에 맞는 메뉴에서 구성을 선택 하 고 합니다. 이것은 선택, 삽입, 업데이트 및 반환 값 및 매개 변수 (있는 경우)와 함께 삭제에 사용 되는 저장된 프로시저를 나열 하는 TableAdapter 구성 마법사를 표시 합니다. 그림 10이이 마법사를 보여 줍니다. 것을 확인할 수 여기는 `Employees_Select` 저장 프로시저 반환은 `ManagerFirstName` 및 `ManagerLastName` 필드입니다.


[![저장 프로시저는 마법사에 나와 있는 Employees_Select에 대 한 업데이트 된 열 목록](updating-the-tableadapter-to-use-joins-vb/_static/image25.png)](updating-the-tableadapter-to-use-joins-vb/_static/image24.png)

**그림 10**: 마법사에 대 한 업데이트 된 열 목록에 표시 된 `Employees_Select` 저장 프로시저 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image26.png))


마침을 클릭 하 여 마법사를 완료 합니다. 데이터 집합 디자이너를 반환 하면는 `EmployeesDataTable` 두 개의 추가 열 포함: `ManagerFirstName` 및 `ManagerLastName`합니다.


[![EmployeesDataTable 새 열 두 개를 포함합니다.](updating-the-tableadapter-to-use-joins-vb/_static/image28.png)](updating-the-tableadapter-to-use-joins-vb/_static/image27.png)

**그림 11**:는 `EmployeesDataTable` 두 개의 새 열 포함 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image29.png))


설명 하기 위해 업데이트 된 `Employees_Select` s 사용자가 보고 하 고 직원을 삭제할 수 있는 웹 페이지 생성, 저장된 프로시저가 고 삽입, 업데이트 및 삭제 기능 TableAdapter의 문서가 계속 작동 합니다. 그러나 이러한 페이지를 만들기 전에 해야 작업에서 직원을 위한 비즈니스 논리 계층에 새 클래스를 먼저 만들어야 하는 `NorthwindWithSprocs` 데이터 집합입니다. 4 단계에서에서 만듭니다는 `EmployeesBLLWithSprocs` 클래스입니다. 5 단계에서에서 ASP.NET 페이지에서이 클래스를 사용 합니다.

## <a name="step-4-implementing-the-business-logic-layer"></a>4 단계: 비즈니스 논리 계층 구현

새 클래스 파일을 만듭니다는 `~/App_Code/BLL` 라는 폴더 `EmployeesBLLWithSprocs.vb`합니다. 이 클래스는 기존의 의미 체계를 그대로 모방 `EmployeesBLL` 클래스만 새로운 적은 메서드를 제공 및 사용 하 여 하나는 `NorthwindWithSprocs` 데이터 집합 (대신는 `Northwind` 데이터 집합). `EmployeesBLLWithSprocs` 클래스에 다음 코드를 추가합니다.


[!code-vb[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample6.vb)]

`EmployeesBLLWithSprocs` s 클래스 `Adapter` 속성의 인스턴스를 반환 합니다.는 `NorthwindWithSprocs` dataset `EmployeesTableAdapter`합니다. 이것은 s 클래스에서 사용 `GetEmployees` 및 `DeleteEmployee` 메서드. `GetEmployees` 메서드 호출의 `EmployeesTableAdapter` s 해당 `GetEmployees` 메서드를 호출 하는 `Employees_Select` 정보에서 결과 표시 하 고 저장 프로시저는 `EmployeeDataTable`합니다. `DeleteEmployee` 메서드를 호출 또한는 `EmployeesTableAdapter` s `Delete` 메서드를 호출 하는 `Employees_Delete` 저장 프로시저입니다.

## <a name="step-5-working-with-the-data-in-the-presentation-layer"></a>5 단계: 프레젠테이션 계층에서 데이터 작업

와 `EmployeesBLLWithSprocs` 클래스 완료 준비 된 ASP.NET 페이지를 통해 직원 데이터에 사용할 수 있습니다. 열기는 `JOINs.aspx` 페이지에 `AdvancedDAL` 폴더를 끌어서는 GridView 설정 디자이너 도구 상자에서 해당 `ID` 속성을 `Employees`합니다. 다음으로, GridView s 스마트 태그에서 표를 바인딩할 라는 새 ObjectDataSource 컨트롤 `EmployeesDataSource`합니다.

ObjectDataSource 사용 하도록 구성 된 `EmployeesBLLWithSprocs` 클래스, 선택 및 DELETE 탭에 및는 `GetEmployees` 및 `DeleteEmployee` 방법이 드롭 다운 목록에서 선택 됩니다. ObjectDataSource의 구성을 완료 하려면 마침을 클릭 합니다.


[![ObjectDataSource EmployeesBLLWithSprocs 클래스를 사용 하도록 구성](updating-the-tableadapter-to-use-joins-vb/_static/image31.png)](updating-the-tableadapter-to-use-joins-vb/_static/image30.png)

**그림 12**: 구성에 사용 하 여 ObjectDataSource는 `EmployeesBLLWithSprocs` 클래스 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image32.png))


[![ObjectDataSource 사용 하 여 한 GetEmployees 및 종료 되 메서드](updating-the-tableadapter-to-use-joins-vb/_static/image34.png)](updating-the-tableadapter-to-use-joins-vb/_static/image33.png)

**그림 13**: ObjectDataSource 사용는 `GetEmployees` 및 `DeleteEmployee` 메서드 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image35.png))


Visual Studio의 각 GridView BoundField 추가 됩니다는 `EmployeesDataTable`의 열입니다. 모두를 제외 하 고 이러한 BoundFields 제거 `Title`, `LastName`, `FirstName`, `ManagerFirstName`, 및 `ManagerLastName` 및 이름 바꾸기는 `HeaderText` 마지막 네 BoundFields 성, 이름, 관리자의 이름에 대 한 속성 및 관리자 s 성, 각각.

직원 들이이 페이지에서 삭제할 수 있도록 하려면 다음 두 가지를 수행 해야 합니다. 첫째, 스마트 태그에서는 삭제 사용 옵션을 선택 하 여 삭제 기능을 제공 하 여 GridView를 지시 합니다. 둘째, ObjectDataSource s 변경 `OldValuesParameterFormatString` ObjectDataSource 마법사에 의해 속성 값을 설정 (`original_{0}`) 기본값으로 (`{0}`). 다음과 같이 변경한 후 GridView 및 ObjectDataSource s 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](updating-the-tableadapter-to-use-joins-vb/samples/sample7.aspx)]

브라우저를 통해 방문 하 여 페이지를 테스트 합니다. 그림 14에서 볼 수 있듯이 각 직원 및 사용자가 관리자의 이름을 (가지고 있는 경우) 페이지에 나열 됩니다.


[![Employees_Select에서 조인을 저장 프로시저 반환 관리자의 이름](updating-the-tableadapter-to-use-joins-vb/_static/image37.png)](updating-the-tableadapter-to-use-joins-vb/_static/image36.png)

**그림 14**:는 `JOIN` 에 `Employees_Select` 이름의 관리자를 반환 하는 저장 프로시저 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image38.png))


삭제 단추를 클릭 하면 삭제 워크플로 실행의 완료는 시작 된 `Employees_Delete` 저장 프로시저입니다. 그러나 시도가 `DELETE` 외래 키 제약 조건 위반으로 인해 실패 하는 저장된 프로시저의 문이 (그림 15 참조). 특히 각 직원에, 하나 이상의 레코드는 `Orders` 테이블 삭제가 실패 합니다.


[![외래 키 제약 조건 위반 해당 주문을 결과 있는 직원 삭제](updating-the-tableadapter-to-use-joins-vb/_static/image40.png)](updating-the-tableadapter-to-use-joins-vb/_static/image39.png)

**그림 15**: 외래 키 제약 조건 위반 해당 주문을 결과 있는 직원 삭제 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-vb/_static/image41.png))


삭제 되도록 직원 수 있도록 수 없습니다.

- 업데이트를 삭제, 종속 외래 키 제약 조건
- 레코드를 수동으로 삭제는 `Orders` 삭제할 직원에 대 한 테이블 또는
- 업데이트는 `Employees_Delete` 저장 프로시저를 관련된 레코드를 먼저 삭제는 `Orders` 테이블을 삭제 하기 전에 `Employees` 레코드입니다. 이 기술을 논의 [를 사용 하 여 기존 저장 프로시저 형식화 된 데이터 집합의 Tableadapter에 대 한](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 자습서입니다.

I이 그대로 실행으로 판독기에 대 한 합니다.

## <a name="summary"></a>요약

관계형 데이터베이스를 사용할 때는 일반적으로 여러에서 해당 데이터를 가져오도록 쿼리 관련 테이블을 합니다. 상관 하위 쿼리 및 `JOIN` 쿼리에서 관련된 테이블의 데이터에 액세스 하기 위한 두 가지 방법을 제공 합니다. 가장 일반적으로 수행 하는 이전 자습서 TableAdapter 생성할 수 없습니다. 자동 때문에 상관된 하위 쿼리를 활용 `INSERT`, `UPDATE`, 및 `DELETE` 관련 쿼리에 대 한 문을 `JOIN` s입니다. 임시 SQL 문을 사용 하는 경우 이러한 값을 수동으로 제공 될 수 있습니다 하는 동안 TableAdapter 구성 마법사가 완료 되 면 사용자 지정 내용이 덮어쓰게 됩니다.

다행히 Tableadapter 저장된 프로시저를 사용 하 여 만든 임시 SQL 문을 사용 하 여 만든 것과 동일한 오류에서 저하 되지 않습니다. 따라서 주 해당 쿼리에서 사용 하 여 TableAdapter를 만들 수는 `JOIN` 저장된 프로시저를 사용 하는 경우. 이 자습서에서는 TableAdapter를 만드는 방법에 살펴보았습니다. 사용 하 여을 시작 했습니다. 한 `JOIN`-덜 `SELECT` 되도록 해당 되는 삽입, 업데이트 및 삭제 저장 프로시저는 자동 생성 TableAdapter s 주 쿼리를 쿼리 합니다. Augmented 우리는 TableAdapter s 초기 구성이 완료 된 `SelectCommand` 저장 프로시저를 사용 하 여는 `JOIN` 업데이트 하려면 TableAdapter 구성 마법사를 다시 실행 하 고는 `EmployeesDataTable`의 열입니다.

자동으로 업데이트 TableAdapter 구성 마법사를 다시 실행은 `EmployeesDataTable` 열에서 반환 된 데이터 필드에 맞게는 `Employees_Select` 저장 프로시저입니다. 또는 수 이러한 열 수동으로에 추가한 DataTable입니다. 다음 자습서의 열을 수동으로 추가 DataTable을 학습 합니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자가 Hilton Geisenow, David Suru 및 Teresa 머피의 합니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
[다음](adding-additional-datatable-columns-vb.md)
