---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-cs
title: Join을 사용 하도록 TableAdapter 업데이트 (C#) | Microsoft Docs
author: rick-anderson
description: 데이터베이스를 사용 하 여 작업 하는 경우 여러 테이블에 걸쳐 요청 데이터에 공통적으로 적용 됩니다. 서로 다른 두 테이블에서 데이터를 검색 하거나 사용할 수 있습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/18/2007
ms.topic: article
ms.assetid: 675531a7-cb54-4dd6-89ac-2636e4c285a5
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/updating-the-tableadapter-to-use-joins-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ff63f1dc7c01f2be66dd99e1e00e2c2bb70058d
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37391003"
---
<a name="updating-the-tableadapter-to-use-joins-c"></a>Join을 사용 하도록 TableAdapter 업데이트 (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_69_CS.zip) 또는 [PDF 다운로드](updating-the-tableadapter-to-use-joins-cs/_static/datatutorial69cs1.pdf)

> 데이터베이스를 사용 하 여 작업 하는 경우 여러 테이블에 걸쳐 요청 데이터에 공통적으로 적용 됩니다. 서로 다른 두 테이블에서 데이터를 검색할 상관된 하위 쿼리 또는 조인 작업을 사용할 수 있습니다. 이 자습서에서는 해당 기본 쿼리에서 조인을 포함 하는 TableAdapter를 만드는 방법을 살펴보기 전에 상관된 하위 쿼리 및 조인 구문을 비교 했습니다.


## <a name="introduction"></a>소개

관계형 데이터베이스를 사용 하 여 사용에 관심이 데이터는 종종 여러 테이블 간에 분산 됩니다. 예를 들어 제품 정보를 표시할 때 가능성이 하려는 각 product s 해당 category 및 supplier s 이름 목록입니다. `Products` 테이블에 `CategoryID` 하 고 `SupplierID` 값 이지만 실제 category와 supplier 이름에는 `Categories` 및 `Suppliers` 테이블 각각.

사용할 수 있습니다 다른, 관련 테이블에서 정보를 검색할 *상관 하위 쿼리* 하거나 `JOIN` *s*입니다. 상관된 하위 쿼리 중첩 된 `SELECT` 외부 쿼리의 열을 참조 하는 쿼리. 예를 들어,를 [데이터 액세스 레이어 만들기](../introduction/creating-a-data-access-layer-cs.md) 자습서에서 두 개의 상관된 하위 쿼리를 사용 했습니다를 `ProductsTableAdapter` s 주 쿼리의 각 제품에 대 한 category와 supplier 이름을 반환할 합니다. `JOIN` 는 서로 다른 두 테이블의 관련된 행을 병합 하는 SQL 구문입니다. 사용을 `JOIN` 에 [SqlDataSource 컨트롤을 사용 하 여 데이터 쿼리](../accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-cs.md) 함께 각 제품 범주 정보를 표시 하는 자습서입니다.

우리가 사용 하 여 abstained 있는 이유 `JOIN` Tableadapter 사용 하 여가 해당 자동으로 생성할 TableAdapter가의 마법사에서 제한으로 인해 `INSERT`를 `UPDATE`, 및 `DELETE` 문입니다. 구체적으로 말하면, TableAdapter가 기본 쿼리 하나가 포함 된 경우 `JOIN` 개이면 TableAdapter 수 없습니다. 자동 생성 임시 SQL 문 또는 저장된 프로시저에 대 한 해당 `InsertCommand`를 `UpdateCommand`, 및 `DeleteCommand` 속성입니다.

이 자습서에서는 간단 하 게 비교 및 대비 상관 하위 쿼리 및 `JOIN` s를 포함 하는 TableAdapter를 만드는 방법을 살펴보기 전에 `JOIN` s의 기본 쿼리에서 합니다.

## <a name="comparing-and-contrasting-correlated-subqueries-andjoin-s"></a>비교 및 대조 상관 하위 쿼리 및`JOIN` s

이전에 설명한 대로 합니다 `ProductsTableAdapter` 의 첫 번째 자습서에서 만든는 `Northwind` 데이터 집합은 각 제품 s 해당 category와 supplier name을 제공 하도록 상관된 하위 쿼리를 사용 합니다. `ProductsTableAdapter` s 주 쿼리 아래에 표시 됩니다.


[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample1.sql)]

두 개의 상관 하위 쿼리- `(SELECT CategoryName FROM Categories WHERE Categories.CategoryID = Products.CategoryID)` 및 `(SELECT CompanyName FROM Suppliers WHERE Suppliers.SupplierID = Products.SupplierID)` -됩니다 `SELECT` 외부에서 추가 열으로 제품당 하나의 값을 반환 하는 쿼리 `SELECT`의 문 열 목록입니다.

또는 `JOIN` 각 s 제품 공급 업체와 범주 이름을 반환할 수 있습니다. 다음 쿼리는 위와 동일한 출력이 반환 하지만 사용 `JOIN` 하위 쿼리 대신 s:


[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample2.sql)]

`JOIN` 일부 조건에 따라 다른 테이블에서 레코드를 사용 하 여 한 테이블에서 레코드를 병합 합니다. 예를 들어, 위의 쿼리에서 `LEFT JOIN Categories ON Categories.CategoryID = Products.CategoryID` 사용 하면 병합 하는 각 SQL Server 해당 범주를 사용 하 여 제품 레코드 기록 `CategoryID` 값과 s 제품 일치 `CategoryID` 값입니다. 병합 된 결과 사용 하면 각 제품에 대해 해당 범주 필드를 사용 하려면 (같은 `CategoryName`).

> [!NOTE]
> `JOIN` s는 관계형 데이터베이스에서 데이터를 쿼리 하는 경우에 주로 사용 됩니다. 처음 접하는 경우 합니다 `JOIN` 구문, 사용법에 따라 약간 브러시 필요가 d 것이 좋습니다는 [자습서 SQL Join](http://www.w3schools.com/sql/sql_join.asp) 에서 [W3 학교](http://www.w3schools.com/)합니다. 또한 읽어 볼 가치가는 [ `JOIN` 기본 사항](https://msdn.microsoft.com/library/ms191517.aspx) 및 [하위 쿼리 기본 사항](https://msdn.microsoft.com/library/ms189575.aspx) 부분을 [SQL 온라인 설명서](https://msdn.microsoft.com/library/ms130214.aspx)합니다.


이후 `JOIN` 및 상관 관계가 지정 된 하위 쿼리 둘 다 수 다른 테이블의 관련된 데이터를 검색, 대부분의 개발자는 왼쪽 겨누는 사실일 뿐 및 사용 하는 방법을 궁금해 합니다. 모든 SQL 출력량이 있습니까 동일한 작업을 대략 있다고 이야기 ve 한다는 만들어지고 t 실제로 문제가 성능 관점에서 보면 SQL Server는 거의 동일한 실행 계획을 생성 합니다. 그런 다음 해당 조언 여러분과 팀 가장 익숙한 기술을 사용 하 여 방법은입니다. 부분 것에이 통지를 전달 하는 후 이러한 전문가 즉시 express의 기본 설정 주목할 `JOIN` 상관된 하위 쿼리 동안.

형식화 된 데이터 집합을 사용 하 여 데이터 액세스 계층을 빌드하는 경우 도구는 하위 쿼리를 사용 하는 경우에 더 잘 작동 합니다. 특히 TableAdapter가의 마법사에서 하지 자동 생성에 해당 `INSERT`, `UPDATE`, 및 `DELETE` 주 쿼리 하나가 포함 된 경우 문을 `JOIN` s, 하지만 생성 합니다. 자동-상관 관계가 지정 된 경우 이러한 문은 하위 쿼리 사용 됩니다.

이러한 단점을 탐색 하려면 임시 형식화 된 데이터 집합을 만드는 `~/App_Code/DAL` 폴더입니다. TableAdapter 구성 마법사를 하는 동안 임시 SQL 문을 사용 하 여 다음을 입력 하 선택 `SELECT` 쿼리 (그림 1 참조).


[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample3.sql)]


[![조인을 포함 하는 기본 쿼리를 입력 합니다.](updating-the-tableadapter-to-use-joins-cs/_static/image2.png)](updating-the-tableadapter-to-use-joins-cs/_static/image1.png)

**그림 1**: 포함 된 기본 쿼리를 입력 `JOIN` s ([클릭 하 여 큰 이미지 보기](updating-the-tableadapter-to-use-joins-cs/_static/image3.png))


TableAdapter 기본적으로 자동으로 만들어집니다 `INSERT`, `UPDATE`, 및 `DELETE` 주 쿼리를 기반으로 한 문입니다. 고급 단추를 클릭 하면이 기능을 사용할 수 있는지 확인할 수 있습니다. 이 설정에도 불구 하 고 TableAdapter 됩니다 만들 수는 `INSERT`, `UPDATE`, 및 `DELETE` 문 기본 쿼리에 포함 되어 있으므로 `JOIN`합니다.


![조인을 포함 하는 기본 쿼리를 입력 합니다.](updating-the-tableadapter-to-use-joins-cs/_static/image4.png)

**그림 2**: 포함 하는 기본 쿼리를 입력 `JOIN` s


마법사를 완료 하려면 마침을 클릭 합니다. 이 시점에 데이터 집합의 디자이너 포함 될 열이 포함 된 DataTable 사용 하 여 단일 TableAdapter에 반환 하는 필드의 각는 `SELECT`의 쿼리 열 목록입니다. 여기에 `CategoryName` 고 `SupplierName`그림 3과 같이, 합니다.


![DataTable 열 목록에 반환 된 각 필드에 대 한 열이 포함](updating-the-tableadapter-to-use-joins-cs/_static/image5.png)

**그림 3**: DataTable 열 목록에 반환 된 각 필드에 대 한 열이 포함


TableAdapter에 대 한 값이 부족 DataTable에는 적절 한 열에 있으면 해당 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성입니다. 이 확인 하려면 디자이너의 TableAdapter에 클릭 한 다음 속성 창으로 이동 합니다. 이 표시 됩니다는 합니다 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성 (없음)으로 설정 됩니다.


[![InsertCommand, UpdateCommand, 및 DeleteCommand 속성 (없음)으로 설정 됩니다.](updating-the-tableadapter-to-use-joins-cs/_static/image7.png)](updating-the-tableadapter-to-use-joins-cs/_static/image6.png)

**그림 4**: 합니다 `InsertCommand`를 `UpdateCommand`, 및 `DeleteCommand` 속성 (없음)으로 설정 됩니다 ([클릭 하 여 큰 이미지 보기](updating-the-tableadapter-to-use-joins-cs/_static/image8.png))


이러한 단점을 해결 하려면 수동으로 가능해 집니다 SQL 문 및 매개 변수를 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성 창을 통해 속성입니다. 또는 TableAdapter가 기본 쿼리를 구성 하 여 시작할 수 있을 것 *되지* 포함할 `JOIN` s입니다. 이렇게 하면 합니다 `INSERT`, `UPDATE`, 및 `DELETE` 문을 자동으로 생성 합니다. 마법사를 완료 한 후에서는 다음 수동으로 업데이트할 수는 tableadapter `SelectCommand` 을 포함 하도록 속성 창에서를 `JOIN` 구문입니다.

이 방법은 것이 매우 불안정 언제 든 지 TableAdapter가 기본 쿼리 때문에 임시 SQL 쿼리를 사용 하 여 자동으로 생성 하 여 마법사를 통해 다시 구성할 때 `INSERT`, `UPDATE`, 및 `DELETE` 문을 다시 작성 됩니다. 즉, 나중에 수행한 사용자 지정을 모두 손실 될 TableAdapter를 마우스 오른쪽 단추로 클릭, 상황에 맞는 메뉴에서 구성 선택 하 고 마법사를 다시 완료 합니다.

자동으로 생성 된 tableadapter의 때 `INSERT`, `UPDATE`, 및 `DELETE` 문을 인 다행 스럽게도 임시 SQL 문이 제한 합니다. 저장된 프로시저를 사용 하 여 TableAdapter 경우 사용자 지정할 수 있습니다 합니다 `SelectCommand`, `InsertCommand`를 `UpdateCommand`, 또는 `DeleteCommand` 저장 프로시저 및 저장된 프로시저 되도록 걱정 하지 않고 TableAdapter 구성 마법사를 다시 실행 합니다. 수정 합니다.

다음 통해 만들겠습니다 TableAdapter는 처음에 몇 가지 단계는 모든 생략 하는 기본 쿼리를 사용해 `JOIN` s 해당 삽입 되도록 업데이트 및 삭제 저장 프로시저를 자동으로 생성 됩니다. 업데이트 될 것을 `SelectCommand` 따라서를 사용 하는 `JOIN` 관련된 테이블에서 추가 열을 반환 하는 합니다. 마지막으로, 해당 비즈니스 논리 계층 클래스 만들어 ASP.NET 웹 페이지에서 TableAdapter를 사용 하 여 보여 줍니다.

## <a name="step-1-creating-the-tableadapter-using-a-simplified-main-query"></a>1 단계: 간소화 된 기본 쿼리를 사용 하 여 TableAdapter 만들기

이 자습서에 대 한 추가 대 한 강력한 형식의 DataTable을 TableAdapter 합니다 `Employees` 테이블에 `NorthwindWithSprocs` 데이터 집합입니다. `Employees` 표에서 `ReportsTo` 지정 된 필드는 `EmployeeID` 직원 s 관리자. 황 병 우에 직원 예를 들어를 `ReportTo` 인 값 5는 `EmployeeID` 정훈의 합니다. 따라서 Anne Steven, 관리자에 보고합니다. 각 직원 s 보고와 함께 `ReportsTo` 값 하고자 할 수 있습니다도 해당 관리자의 이름을 검색 합니다. 사용 하 여 수행할 수 있습니다는 `JOIN`합니다. 하지만 사용 하 여는 `JOIN` 때 마법사에서 자동으로 해당 하는 삽입을 생성 하므로 처음에 TableAdapter 만들기, 업데이트 및 삭제 기능입니다. 따라서 먼저 해당 주 쿼리에 포함 하지 않으면 TableAdapter 만들기 `JOIN` s입니다. 그런 다음 2 단계에서에서 업데이트할 것을 통해 관리자가의 이름을 검색 하는 기본 쿼리 저장 절차를 `JOIN`입니다.

열어서 시작 합니다 `NorthwindWithSprocs` 데이터 집합에는 `~/App_Code/DAL` 폴더. 디자이너에서 마우스 상황에 맞는 메뉴에서 추가 옵션을 선택 합니다. TableAdapter 메뉴 항목을 선택 합니다. TableAdapter 구성 마법사를 시작 됩니다. 그림 5 보여주고 처럼 새 저장된 프로시저를 만들고 다음을 클릭 하 여 마법사를 가집니다. 새로 만들기에 리프레셔가 저장 프로시저 TableAdapter가의 마법사에서에 대 한 참조를 [새 저장 프로시저 만들기 형식화 된 데이터 집합의 Tableadapter에 대 한](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 자습서입니다.


[![새 저장된 프로시저 만들기 옵션을 선택 합니다.](updating-the-tableadapter-to-use-joins-cs/_static/image10.png)](updating-the-tableadapter-to-use-joins-cs/_static/image9.png)

**그림 5**: 새 저장 프로시저 옵션 선택 만들기 ([큰 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-cs/_static/image11.png))


다음 사용 하 여 `SELECT` TableAdapter s 주 쿼리에 대 한 문:


[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample4.sql)]

이후이 쿼리에 포함 하지 않습니다 `JOIN` 개이면 TableAdapter 마법사가 자동으로 만듭니다. 저장된 프로시저 해당 `INSERT`, `UPDATE`, 및 `DELETE` 문 뿐만 아니라 주를 실행 하기 위한 저장된 프로시저 쿼리입니다.

다음 단계를 사용 하면 TableAdapter 저장 된 프로시저 이름 수 있습니다. 이름을 사용 하 여 `Employees_Select`, `Employees_Insert`를 `Employees_Update`, 및 `Employees_Delete`그림 6 에서처럼 합니다.


[![TableAdapter 저장 된 프로시저 이름](updating-the-tableadapter-to-use-joins-cs/_static/image13.png)](updating-the-tableadapter-to-use-joins-cs/_static/image12.png)

**그림 6**: TableAdapter가 저장 프로시저 이름 ([큰 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-cs/_static/image14.png))


마지막 단계 TableAdapter의 메서드 이름을 지정 하 라는 메시지가 나타납니다. 사용 하 여 `Fill` 고 `GetEmployees` 메서드 이름으로 합니다. 또한 업데이트 데이터베이스 (GenerateDBDirectMethods) 확인란이 선택 되어 직접 보내는 메서드 만들기를 유지 해야 합니다.


[![TableAdapter가의 메서드 채우기 이름과 GetEmployees](updating-the-tableadapter-to-use-joins-cs/_static/image16.png)](updating-the-tableadapter-to-use-joins-cs/_static/image15.png)

**그림 7**: tableadapter 메서드 이름을 `Fill` 하 고 `GetEmployees` ([클릭 하 여 큰 이미지 보기](updating-the-tableadapter-to-use-joins-cs/_static/image17.png))


마법사를 완료 한 후 시간을 내어 데이터베이스에서 저장된 프로시저를 검사 합니다. 4 개의 새로 표시 됩니다: `Employees_Select`, `Employees_Insert`를 `Employees_Update`, 및 `Employees_Delete`합니다. 다음으로 검사 합니다 `EmployeesDataTable` 및 `EmployeesTableAdapter` 방금 만든 합니다. DataTable 주 쿼리에서 반환 된 각 필드에 대 한 열을 포함 합니다. TableAdapter 클릭 하 고 속성 창으로 이동 합니다. 이 표시 됩니다는 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성 모두가 해당 저장된 프로시저를 호출 하도록 올바르게 구성 합니다.


[![TableAdapter 포함 삽입, 업데이트 및 삭제 기능](updating-the-tableadapter-to-use-joins-cs/_static/image19.png)](updating-the-tableadapter-to-use-joins-cs/_static/image18.png)

**그림 8**: TableAdapter 포함 Insert, Update 및 삭제 기능 ([큰 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-cs/_static/image20.png))


삽입, 업데이트 및 delete 저장된 프로시저를 자동으로 생성 하며 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 을 사용자 지정할 수는 올바르게 구성 하는 속성을는 `SelectCommand` s 저장 프로시저를 추가로 반환할 각 직원의 관리자에 대 한 정보입니다. 구체적으로 업데이트 해야 합니다 `Employees_Select` 저장 프로시저를 사용 하 여는 `JOIN` 관리자가 반환 하 고 `FirstName` 및 `LastName` 값입니다. 저장된 프로시저를 업데이트 후 이러한 추가 열이 포함 되어 있도록 DataTable을 업데이트 해야 합니다. 에서는 이러한 두 작업 단계 2에서 및 3 해결할 수 있습니다.

## <a name="step-2-customizing-the-stored-procedure-to-include-ajoin"></a>2 단계: 포함 하도록 저장된 프로시저를 사용자 지정을`JOIN`

서버 탐색기로 이동 하 고, Northwind 데이터베이스 s Stored Procedures 폴더로 드릴 다운, 열어 하 여 시작 된 `Employees_Select` 저장 프로시저입니다. 이 저장된 프로시저 표시 되지 않으면, Stored Procedures 폴더를 마우스 오른쪽 단추로 클릭 하 고 새로 고침을 선택 합니다. 사용 하도록 저장된 프로시저를 업데이트 한 `LEFT JOIN`의 관리자를 먼저 반환 하 여 성:


[!code-sql[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample5.sql)]

업데이트 한 후 합니다 `SELECT` 문을 파일 메뉴로 이동 하 고 저장을 선택 하 여 변경 내용 저장할 `Employees_Select`합니다. 또는 도구 모음에서 저장 아이콘을 클릭 하거나 Ctrl + S를 누르면 수 있습니다. 변경 내용을 저장 한 후 마우스 오른쪽 단추로 클릭는 `Employees_Select` 서버 탐색기에서 저장 프로시저 및 Execute를 선택 합니다. 이 저장된 프로시저를 실행 및 해당 결과 출력 창에 표시 됩니다 (그림 9 참조).


[![저장 프로시저 결과 출력 창에 표시 됩니다.](updating-the-tableadapter-to-use-joins-cs/_static/image22.png)](updating-the-tableadapter-to-use-joins-cs/_static/image21.png)

**그림 9**: 저장 프로시저 결과 출력 창에 표시 됩니다 ([큰 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-cs/_static/image23.png))


## <a name="step-3-updating-the-datatable-s-columns"></a>3 단계: DataTable의 열 업데이트

이 시점에서 합니다 `Employees_Select` 저장 프로시저 반환 `ManagerFirstName` 및 `ManagerLastName` 값 이지만 `EmployeesDataTable` 이러한 열이 누락 되었습니다. 이러한 누락 된 열을 두 가지 방법 중 하나에서 DataTable에 추가할 수 있습니다.

- **수동으로** -데이터 집합 디자이너에서 DataTable을 마우스 오른쪽 단추로 클릭 하 고, 추가 메뉴에서 열을 선택 합니다. 다음 열 이름을 지정 하 고 해당 속성을 적절 하 게 설정할 수 있습니다.
- **자동으로** -TableAdapter 구성 마법사가가 반환한 필드에 맞게 DataTable의 열 업데이트는 `SelectCommand` 저장 프로시저입니다. 임시 SQL 문을 사용 하는 경우 마법사가 제거도 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand` 속성을 `SelectCommand` 이제 포함을 `JOIN`. 하지만 저장된 프로시저를 사용 하는 경우 이러한 명령은 속성 그대로입니다.

이전 자습서에서는 포함 하 여 수동으로 추가 DataTable 열을 살펴보았습니다 있을 [마스터/세부 정보 DataList와 함께 a 글머리 기호 목록의 마스터 레코드를 사용 하 여 세부 정보](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) 하 고 [에 파일 업로드](../working-with-binary-files/uploading-files-cs.md), 드리겠습니다 다음 자습서에서이 프로세스를 다시 자세히 살펴봅니다. 그러나이 자습서에서는 s TableAdapter 구성 마법사를 통해 자동 방법을 사용 하도록 합니다.

마우스 오른쪽 단추로 클릭 하 여 시작 된 `EmployeesTableAdapter` 구성 상황에 맞는 메뉴에서 선택 합니다. 그러면 선택, 삽입, 업데이트 및 삭제와 반환 값 및 매개 변수 (있는 경우)에 사용 되는 저장된 프로시저를 나열 하는 TableAdapter 구성 마법사. 그림 10에서는이 마법사를 보여 줍니다. 여기서 볼 수 있는 하는 합니다 `Employees_Select` 저장 프로시저 반환 합니다 `ManagerFirstName` 및 `ManagerLastName` 필드입니다.


[![저장 프로시저는 마법사와 Employees_Select에 대 한 업데이트 된 열 목록](updating-the-tableadapter-to-use-joins-cs/_static/image25.png)](updating-the-tableadapter-to-use-joins-cs/_static/image24.png)

**그림 10**: 마법사에 대 한 업데이트 된 열 목록을 표시 합니다 `Employees_Select` 저장 프로시저 ([클릭 하 여 큰 이미지 보기](updating-the-tableadapter-to-use-joins-cs/_static/image26.png))


마침을 클릭 하 여 마법사를 완료 합니다. 데이터 집합 디자이너로 돌아가면 합니다 `EmployeesDataTable` 두 개의 추가 열이 포함 됩니다: `ManagerFirstName` 및 `ManagerLastName`합니다.


[![EmployeesDataTable 새 열 두 개를 포함합니다.](updating-the-tableadapter-to-use-joins-cs/_static/image28.png)](updating-the-tableadapter-to-use-joins-cs/_static/image27.png)

**그림 11**: 합니다 `EmployeesDataTable` 새 열 두 개 포함 되어 있습니다 ([클릭 하 여 큰 이미지 보기](updating-the-tableadapter-to-use-joins-cs/_static/image29.png))


설명 하기 위해 업데이트 된 `Employees_Select` s 보고 직원을 삭제 하는 사용자를 허용 하는 웹 페이지 만들기, 저장된 프로시저를 적용 하 고 삽입, 업데이트 하 고이 TableAdapter의 기능을 삭제 하는 문서가 계속 작동 합니다. 그러나 이러한 페이지를 만들기 전에 먼저 생성 해야 새 클래스 작업에서 직원을 위한 비즈니스 논리 계층에는 `NorthwindWithSprocs` 데이터 집합입니다. 4 단계에서에서 만듭니다는 `EmployeesBLLWithSprocs` 클래스입니다. 5 단계에서에서이 클래스는 ASP.NET 페이지에서 사용 합니다.

## <a name="step-4-implementing-the-business-logic-layer"></a>4 단계: 비즈니스 논리 레이어 구현

새 클래스 파일을 만듭니다는 `~/App_Code/BLL` 라는 폴더 `EmployeesBLLWithSprocs.cs`합니다. 이 클래스는 기존의 의미 체계를 모방 `EmployeesBLL` 클래스에만 새로운 하나 적은 메서드를 제공 하 고 사용 합니다 `NorthwindWithSprocs` 데이터 집합 (대신는 `Northwind` 데이터 집합). `EmployeesBLLWithSprocs` 클래스에 다음 코드를 추가합니다.


[!code-csharp[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample6.cs)]

`EmployeesBLLWithSprocs` s 클래스 `Adapter` 속성의 인스턴스를 반환 합니다 `NorthwindWithSprocs` dataset `EmployeesTableAdapter`합니다. S 클래스에 의해 사용 됩니다 `GetEmployees` 고 `DeleteEmployee` 메서드. `GetEmployees` 메서드 호출을 `EmployeesTableAdapter` s 해당 `GetEmployees` 메서드를 호출 하는 `Employees_Select` 저장 프로시저 및 그 결과 채웁니다는 `EmployeeDataTable`합니다. 합니다 `DeleteEmployee` 마찬가지로 메서드를 호출 합니다 `EmployeesTableAdapter` s `Delete` 메서드를 호출 하는 `Employees_Delete` 저장 프로시저.

## <a name="step-5-working-with-the-data-in-the-presentation-layer"></a>5 단계: 프레젠테이션 계층에서 데이터 작업

사용 하 여는 `EmployeesBLLWithSprocs` 클래스에서는 ASP.NET 페이지를 통해 직원 데이터를 사용할 준비가 완료 됩니다. 열기는 `JOINs.aspx` 페이지에 `AdvancedDAL` 폴더 및 설정 디자이너 도구 상자에서 GridView 끌어서 해당 `ID` 속성을 `Employees`합니다. 그런 다음 GridView가 스마트 태그를 모눈을 라는 새 ObjectDataSource 컨트롤을 바인딩할 `EmployeesDataSource`합니다.

ObjectDataSource를 사용 하 여 구성를 `EmployeesBLLWithSprocs` 클래스를 선택 하 고 삭제 탭에서 있는지를 확인 합니다 `GetEmployees` 및 `DeleteEmployee` 방법이 드롭 다운 목록에서 선택 됩니다. ObjectDataSource가의 구성을 완료 하려면 마침을 클릭 합니다.


[![EmployeesBLLWithSprocs 클래스를 사용 하는 ObjectDataSource 구성](updating-the-tableadapter-to-use-joins-cs/_static/image31.png)](updating-the-tableadapter-to-use-joins-cs/_static/image30.png)

**그림 12**: ObjectDataSource 사용 하도록 구성 된 `EmployeesBLLWithSprocs` 클래스 ([클릭 하 여 큰 이미지 보기](updating-the-tableadapter-to-use-joins-cs/_static/image32.png))


[![ObjectDataSource를 사용 하는 한 GetEmployees 및 종료 되 메서드](updating-the-tableadapter-to-use-joins-cs/_static/image34.png)](updating-the-tableadapter-to-use-joins-cs/_static/image33.png)

**그림 13**: ObjectDataSource 사용 합니다 `GetEmployees` 하 고 `DeleteEmployee` 메서드 ([클릭 하 여 큰 이미지 보기](updating-the-tableadapter-to-use-joins-cs/_static/image35.png))


Visual Studio의 각 GridView에는 BoundField에 추가 됩니다는 `EmployeesDataTable`의 열입니다. 모두 제외 하 고 이러한 BoundFields 제거 `Title`, `LastName`를 `FirstName`를 `ManagerFirstName`, 및 `ManagerLastName` 바꾸고는 `HeaderText` 성, 이름, 이름, 관리자가 마지막 4 BoundFields에 대 한 속성 및 관리자가 성, 각각.

사용자가 직원 들이이 페이지에서 삭제할 수 있도록 두 가지를 수행 해야 합니다. 먼저 스마트 태그에서 삭제 사용 옵션을 확인 하 여 삭제 기능을 제공 하는 GridView를 지시 합니다. 둘째, ObjectDataSource s를 변경 `OldValuesParameterFormatString` ObjectDataSource 마법사에서 속성 값을 설정 (`original_{0}`)을 기본값으로 (`{0}`). 다음과 같이 변경한 후 GridView 및 ObjectDataSource가 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](updating-the-tableadapter-to-use-joins-cs/samples/sample7.aspx)]

브라우저를 통해이 방문 하 여 페이지를 테스트 합니다. 그림 14에서 볼 수 있듯이 각 직원 및 (있는 경우)가 자신의 관리자의 이름 페이지 나열 됩니다.


[![Employees_Select 조인이 저장 프로시저 이름을 반환 합니다 Manager s](updating-the-tableadapter-to-use-joins-cs/_static/image37.png)](updating-the-tableadapter-to-use-joins-cs/_static/image36.png)

**그림 14**: 합니다 `JOIN` 에 `Employees_Select` 이름이 관리자를 반환 하는 저장 프로시저 ([전체 크기 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-cs/_static/image38.png))


실행에서 단계가 삭제 워크플로 시작 삭제 단추를 클릭 하 여 `Employees_Delete` 저장 프로시저. 그러나 시도가 `DELETE` 저장된 프로시저의 문이 foreign key 제약 조건 위반으로 인해 실패 (그림 15 참조). 특히, 각 직원에 하나 이상의 레코드를 `Orders` 테이블 삭제가 실패 합니다.


[![외래 키 제약 조건 위반을 해당 주문을 결과 있는 직원을 삭제 합니다.](updating-the-tableadapter-to-use-joins-cs/_static/image40.png)](updating-the-tableadapter-to-use-joins-cs/_static/image39.png)

**그림 15**: 외래 키 제약 조건 위반을 해당 주문을 결과 있는 직원을 삭제 ([큰 이미지를 보려면 클릭](updating-the-tableadapter-to-use-joins-cs/_static/image41.png))


직원이 사용할 수 있도록 하면 삭제 수:

- 하위 삭제를 적용 하도록 외래 키 제약 조건 업데이트
- 기록을 수동으로 삭제할는 `Orders` 삭제 하려는 직원에 대 한 테이블 또는
- 업데이트를 `Employees_Delete` 저장 프로시저를 먼저에서 관련된 레코드를 삭제 합니다 `Orders` 테이블을 삭제 하기 전에 `Employees` 레코드. 이 기법을 설명한 합니다 [를 사용 하 여 기존 저장 프로시저는 입력 데이터 집합의 Tableadapter에 대 한](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md) 자습서입니다.

필자는 판독기에 대 한 연습으로 둡니다.

## <a name="summary"></a>요약

관계형 데이터베이스에서 작업할 때 일반적으로 여러에서 해당 데이터를 가져오는 쿼리는 관련 테이블입니다. 상관 하위 쿼리 및 `JOIN` s 쿼리에서 관련된 테이블에서 데이터를 액세스 하기 위한 두 가지 기법을 제공 합니다. TableAdapter 생성할 수 없습니다. 자동 때문에 가장 일반적으로 수행 하는 이전 자습서 상관된 하위 쿼리 사용 `INSERT`, `UPDATE`, 및 `DELETE` 관련 쿼리에 대 한 문을 `JOIN` s입니다. 임시 SQL 문을 사용 하는 경우 이러한 값을 수동으로 제공할 수 있습니다 하는 동안에 TableAdapter 구성 마법사를 완료 되 면 모든 사용자 지정 덮어씁니다.

다행 스럽게도 Tableadapter 저장된 프로시저를 사용 하 여 만든 임시 SQL 문을 사용 하 여 만든 것과 동일한 때에서 발생 하지 않습니다. 해당 기본 쿼리에서 사용 하 여 TableAdapter를 만들 것 이므로 `JOIN` 저장된 프로시저를 사용 하는 경우. 이 자습서에서는 이러한 TableAdapter를 만드는 방법에 살펴보았습니다. 사용 하 여 시작을 `JOIN`-적은 `SELECT` 되도록 해당 되는 삽입, 업데이트 및 삭제 저장 프로시저는 자동 생성 TableAdapter s 주 쿼리에 대해 쿼리 합니다. TableAdapter가 초기 구성으로 완료 된 합니다 `SelectCommand` 저장 프로시저를 사용 하 여는 `JOIN` 업데이트 하려면 TableAdapter 구성 마법사를 다시 실행 하 고는 `EmployeesDataTable`의 열.

자동으로 업데이트 TableAdapter 구성 마법사를 다시 실행 합니다 `EmployeesDataTable` 열에서 반환 된 데이터 필드를 반영 하도록는 `Employees_Select` 저장 프로시저입니다. 또는 수에 추가 했습니다 이러한 열 수동으로 DataTable입니다. 다음 자습서에서 수동으로 추가 열을 DataTable에 학습 합니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Hilton Geisenow, David Suru 및 Teresa Murphy 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)
> [다음](adding-additional-datatable-columns-cs.md)
