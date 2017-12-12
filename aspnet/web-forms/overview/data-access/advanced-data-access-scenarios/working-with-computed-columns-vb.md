---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-vb
title: "계산된 열 (VB) 작업 | Microsoft Docs"
author: rick-anderson
description: "Microsoft SQL Server 계산된 열 값은 식에서 계산을 정의할 수 있습니다는 데이터베이스 테이블을 만들 때 일반적으로 referen..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/03/2007
ms.topic: article
ms.assetid: 5811b8ff-ed56-40fc-9397-6b69ae09a8f6
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-vb
msc.type: authoredcontent
ms.openlocfilehash: a6ff0df27e19d6feecde27a77d4b212d1e9bc45e
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="working-with-computed-columns-vb"></a>계산된 열 (VB) 작업
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_71_VB.zip) 또는 [PDF 다운로드](working-with-computed-columns-vb/_static/datatutorial71vb1.pdf)

> 데이터베이스 테이블을 만들 때 Microsoft SQL Server를 사용 하면 계산된 열 값은 일반적으로 동일한 데이터베이스 레코드의 다른 값을 참조 하는 식에서 계산을 정의할 수 있습니다. 이러한 값은 Tableadapter를 작업할 때 특별히 고려해 야 할 요구 하 여 데이터베이스에서 읽기 전용입니다. 이 자습서에서는 계산된 열에 의해 제기 되 과제를 충족 하는 방법에 설명 합니다.


## <a name="introduction"></a>소개

에 대 한 Microsoft SQL Server에서는  *[계산 열](https://msdn.microsoft.com/en-us/library/ms191250.aspx)*, 열 값이 동일한 테이블의 다른 열에서 값을 일반적으로 참조 하는 식에서 계산 되는 합니다. 예를 들어, 데이터 모델을 추적 하는 한 번 라는 테이블이 있을 수 `ServiceLog` 포함 하 여 열이 있는 `ServicePerformed`, `EmployeeID`, `Rate`, 및 `Duration`, 등입니다. 금액 하는 동안 서비스 당 항목 웹 페이지 또는 기타 프로그래밍 인터페이스를 통해 계산할 수 없습니다 (되는 기간을 곱한 속도)는 것이 편리 하 게 포함 된 열에는 `ServiceLog` 라는 테이블 `AmountDue` 이 보고 하는 정보입니다. 일반 열으로이 열을 만들 수 있지만 언제 든 지 업데이트 해야 합니다는 `Rate` 또는 `Duration` 열 값을 변경 합니다. 더 나은 방법은 만드는 것은 `AmountDue` 열 식을 사용 하는 계산된 열 `Rate * Duration`합니다. 이렇게 하면 SQL Server를 자동으로 계산 된 `AmountDue` 때마다 쿼리에서 참조 된 열 값입니다.

계산된 열의 값에 식에 의해 결정 됩니다, 이러한 열은 읽기 전용 없습니다가 값에 할당에서 `INSERT` 또는 `UPDATE` 문. 그러나 계산된 열에 임시 SQL 문을 사용 하는 TableAdapter에 대 한 기본 쿼리에 포함 된 경우 자동으로에서 다루지 않으므로 자동 생성 `INSERT` 및 `UPDATE` 문. Tableadapter 따라서 `INSERT` 및 `UPDATE` 쿼리 및 `InsertCommand` 및 `UpdateCommand` 계산된 열에 대 한 참조를 제거 하려면 속성을 업데이트 해야 합니다.

사용 하 여의 한 가지 문제 계산 임시 SQL 문을 사용 하는 TableAdapter가 포함 된 열은 TableAdapter s `INSERT` 및 `UPDATE` 쿼리 TableAdapter 구성 마법사가 완료 되는 언제 든 지 자동으로 다시 생성 됩니다. 계산된 열에서 수동으로 제거 따라서는 `INSERT` 및 `UPDATE` 마법사 다시 실행 되는 경우 쿼리 다시 나타납니다. 저장된 프로시저를 사용 하는 Tableadapter 인할이 오류를 발생를 3 단계에서에서 해결 하는 자체 quirks 되어지 않습니다.

이 자습서에서는 계산된 열을 추가 합니다는 `Suppliers` Northwind 데이터베이스의 테이블을 다음이 테이블의 계산된 열과 작동 하도록 해당 TableAdapter를 만듭니다. TableAdapter 구성 마법사를 사용 하는 경우이 사용자 지정 클라우드에 없는 t 손실 되도록 임시 SQL 문 대신 저장된 프로시저를 사용 하는 TableAdapter 있다고 합니다.

Let s가 시작 되었습니다.

## <a name="step-1-adding-a-computed-column-to-thesupplierstable"></a>1 단계: 계산된 열을 추가`Suppliers`테이블

Northwind 데이터베이스에 없으므로 계산된 열 하나 직접 추가 해야 합니다. 이 자습서에 계산된 열을 추가 하는 s 사용에 대 한는 `Suppliers` 라는 테이블 `FullContactName` 형식에서 s 연락처 이름, 제목 및에 대해 작동 하는 회사를 반환 하: `ContactName` (`ContactTitle`, `CompanyName`). 이 계산 열 공급자에 대 한 정보를 표시할 때 보고서에서 사용할 수 있습니다.

열어 시작는 `Suppliers` 마우스 오른쪽 단추로 클릭 하 여 테이블 정의 `Suppliers` 서버 탐색기에서 테이블 및 테이블 정의 열기 상황에 맞는 메뉴에서 선택 합니다. 허용 하는지 여부 및 해당 데이터 형식 등의 속성을 테이블의 열이 표시 됩니다 `NULL` s 및 붙습니다. 계산된 열을 추가 하려면 먼저 테이블 정의에 열 이름을 입력 합니다. 그런 다음 해당 식을 열 속성 창에서 계산 열 사양 섹션 (수식) 텍스트 상자에 입력 (그림 1 참조). 계산된 열의 이름을 `FullContactName` 다음 식을 사용 하 고 있습니다.


[!code-sql[Main](working-with-computed-columns-vb/samples/sample1.sql)]

SQL에서 문자열을 연결할 수 있는지 참고를 사용 하는 `+` 연산자입니다. `CASE` 기존의 프로그래밍 언어에는 조건부와 같은 문을 사용할 수 있습니다. 위 식에서는 `CASE` 문을로 읽을 수 있습니다: 경우 `ContactTitle` 않습니다 `NULL` 다음 출력 하는 `ContactTitle` 쉼표, 그렇지 않으면 연결 값을 내보낼 nothing입니다. 유용성에 대 한 자세한는 `CASE` 문을 참조 [SQL의 전원 `CASE` 문을](http://www.4guysfromrolla.com/webtech/102704-1.shtml)합니다.

> [!NOTE]
> 사용 하는 대신 한 `CASE` 여기 문, 또는 사용할 수도 `ISNULL(ContactTitle, '')`합니다. [`ISNULL(checkExpression, replacementValue)`](https://msdn.microsoft.com/en-us/library/ms184325.aspx)반환 *checkExpression* NULL이 아닌 경우, 그렇지 않으면 반환 *replacementValue*합니다. 하나는 동안 `ISNULL` 또는 `CASE` 작동이 경우에는 더 복잡 한 시나리오 여기서의 유연성은 `CASE` 문을 일치할 수 없는 `ISNULL`합니다.


이 계산된 열을 추가한 후 화면에 나오는 그림 1 스크린 샷의와 같아야 합니다.


[![FullContactName Suppliers 테이블에 명명 된 계산된 열 추가](working-with-computed-columns-vb/_static/image2.png)](working-with-computed-columns-vb/_static/image1.png)

**그림 1**: 계산 된 열 라는 추가 `FullContactName` 에 `Suppliers` 테이블 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image3.png))


계산된 된 열 이름을 지정 하 고 해당 식을 입력 한 후 변경 내용을 저장 테이블에는 도구 모음에 저장 아이콘을 클릭 하 여, Ctrl + S를 클릭 하 여 또는 파일 메뉴로 이동 하 고 저장을 선택 하 여 `Suppliers`합니다.

방금 추가 된 열을 포함 하는 서버 탐색기를 새로 고쳐야 테이블 저장 하는 `Suppliers`의 테이블 열 목록입니다. 열 이름을 대괄호로 둘러쌉니다, 불필요 한 공백을 제거 하는 해당 하는 식으로 자동으로 조정 하는 (수식) 텍스트 상자에 입력 된 식 또한 (`[]`)를 더 명시적으로 표시 하려면 괄호를 포함 합니다. 작업 순서:


[!code-sql[Main](working-with-computed-columns-vb/samples/sample2.sql)]

Microsoft SQL Server에서 계산된 열에 대 한 자세한 내용은 참조는 [기술 문서](https://msdn.microsoft.com/en-us/library/ms191250.aspx)합니다. 또한 체크 아웃의 [하는 방법: Specify Computed Columns](https://msdn.microsoft.com/en-us/library/ms188300.aspx) 계산된 열을 만드는 단계별 연습 과정에 대 한 합니다.

> [!NOTE]
> 기본적으로 계산된 열은 테이블에 물리적으로 저장 되지 않습니다 되지만 대신 쿼리에서 참조 될 때마다 다시 계산 합니다. 그러나이 확인란은 유지를 선택 하 여 테이블의 계산된 열을 물리적으로 저장 하도록 SQL Server 지시할 수 있습니다. 이렇게 인덱스에 계산된 열 값을 사용 하는 쿼리의 성능을 향상 시킬 수 있는 계산된 열에 만들 수 있습니다. 해당 `WHERE` 절. 참조 [Indexes on Computed Columns](https://msdn.microsoft.com/en-us/library/ms189292.aspx) 자세한 정보에 대 한 합니다.


## <a name="step-2-viewing-the-computed-column-s-values"></a>2 단계: 계산된 열의 값 보기

Let s를 보려면 잠시 데이터 액세스 계층에서 작업을 시작 하기 전에 `FullContactName` 값입니다. 서버 탐색기에서 마우스 오른쪽 단추로 클릭는 `Suppliers` 테이블 이름 하 고 상황에 맞는 메뉴에서 새 쿼리를 선택 합니다. 테이블의 정의와 쿼리에 포함 하도록 선택 하 라는 메시지가 나타납니다 쿼리 창이 나타납니다. 추가 `Suppliers` 테이블 한 닫기를 클릭 합니다. 그런 다음, 확인 된 `CompanyName`, `ContactName`, `ContactTitle`, 및 `FullContactName` Suppliers 테이블의 열입니다. 마지막으로 쿼리를 실행 하 고 결과 확인 하려면 도구 모음에서 빨강 느낌표 아이콘을 클릭 합니다.

결과 포함 하는 그림 2에서 볼 수 있듯이 `FullContactName`, 되는 목록을 `CompanyName`, `ContactName`, 및 `ContactTitle` 형식을 사용 하 여 열 `ContactName` (`ContactTitle`, `CompanyName`).


[![FullContactName 형식 ContactName (ContactTitle, CompanyName)를 사용 하 여](working-with-computed-columns-vb/_static/image5.png)](working-with-computed-columns-vb/_static/image4.png)

**그림 2**:는 `FullContactName` 형식을 사용 하 여 `ContactName` (`ContactTitle`, `CompanyName`) ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image6.png))


## <a name="step-3-adding-thesupplierstableadapterto-the-data-access-layer"></a>3 단계: 추가 된`SuppliersTableAdapter`데이터 액세스 계층

응용 프로그램의 공급 업체 정보를 사용 하려면 우선 우리의 DAL에서 TableAdapter와 DataTable을 생성 해야 합니다. 이상적으로 이렇게 이전 자습서에서 검토할 같은 간단한 단계를 사용 하 여 합니다. 그러나 계산된 열이 있는 작업 토론 대해서는 몇 가지 주름을 소개 합니다.

임시 SQL 문을 사용 하는 TableAdapter를 사용 하는 경우 TableAdapter s 주 쿼리에서 TableAdapter 구성 마법사를 통해 단순히 계산된 열을 포함할 수 있습니다. 그러나이를 자동으로 생성 `INSERT` 및 `UPDATE` 계산된 열을 포함 하는 문입니다. 다음이 방법 중 하나를 실행 하려고 하는 경우는 `SqlException` 열 메시지와 함께 *ColumnName* 은 계산된 열 이거나 UNION 연산자의 결과 throw 됩니다 이므로 수정할 수 없습니다. 반면는 `INSERT` 및 `UPDATE` 문은 TableAdapter s 통해 수동으로 조정할 수 있습니다 `InsertCommand` 및 `UpdateCommand` 속성, 이러한 사용자 지정 손실 됩니다 TableAdapter 구성 마법사를 다시 실행 될 때마다 합니다.

임시 SQL 문을 사용 하는 Tableadapter의 오류, 인해 것이 좋습니다 계산된 열을 작업할 때 저장된 프로시저를 사용 했습니다. 기존 저장된 프로시저를 사용 하는 경우 단순히 TableAdapter를 구성에 설명 된 대로 [를 사용 하 여 기존 저장 프로시저 형식화 된 데이터 집합의 Tableadapter에 대 한](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 자습서입니다. 그러나 저장된 프로시저 만들기 TableAdapter 마법사를 사용 하도록 설정한 경우 되기 처음에 주 쿼리에서 모든 계산된 열을 생략 하는 것이 중요 합니다. 주 쿼리에서 계산된 열을 포함 하는 경우 TableAdapter 구성 마법사는 알립니다, 완료 되 면 해당 저장된 프로시저를 만들 수 없습니다. 처음에 계산된 열 필요 없는 주 쿼리를 사용 하 여 TableAdapter를 구성 하 고 해당 저장된 프로시저 및 TableAdapter s 다음 수동으로 업데이트 해야 간단히 말해서 `SelectCommand` 계산된 열을 포함 하도록 합니다. 이 방법은 사용 되는 비슷합니다는 [TableAdapter를 사용 하 여 업데이트](updating-the-tableadapter-to-use-joins-vb.md)`JOIN`*s* 자습서입니다.

이 자습서에서는 새 TableAdapter를 추가 하 고 us에 대 한 저장된 프로시저를 자동으로 만들 하도록 s가 있습니다. 따라서 처음 생략 해야 합니다는 `FullContactName` 기본 쿼리에서 계산된 열입니다.

열어 시작는 `NorthwindWithSprocs` 에서 데이터 집합의 `~/App_Code/DAL` 폴더입니다. 디자이너에서 마우스, 상황에 맞는 메뉴에서 새 TableAdapter를 추가 하려면 선택 합니다. TableAdapter 구성 마법사를 시작 됩니다. 데이터베이스에서 데이터를 쿼리할 수 지정 (`NORTHWNDConnectionString` 에서 `Web.config`) 하 고을 클릭 합니다. 이후 쿼리 또는 수정에 대 한 모든 저장된 프로시저를 아직 만들지 않은 우리는 `Suppliers` 테이블을 새 저장된 프로시저 옵션을 마법사는 us에 하 고 다음 만들기를 선택 합니다.


[![새 저장된 프로시저 만들기 옵션을 선택 합니다.](working-with-computed-columns-vb/_static/image8.png)](working-with-computed-columns-vb/_static/image7.png)

**그림 3**:는 새 저장된 프로시저 만들기 옵션을 선택 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image9.png))


다음 단계는 기본 쿼리에 라는 메시지가 나타납니다. 반환 하는 다음 쿼리를 입력 하 고 `SupplierID`, `CompanyName`, `ContactName`, 및 `ContactTitle` 각 공급 업체에 대 한 열입니다. 이 쿼리는 계산된 열을 의도적으로 생략 하는 참고 (`FullContactName`); 4 단계에서에서이 열을 포함 하려면 해당 저장된 프로시저가 업데이트 됩니다.


[!code-sql[Main](working-with-computed-columns-vb/samples/sample3.sql)]

주 쿼리를 입력 하 고 다음을 클릭 한 후 마법사는 이름을 생성 하는 네 개의 저장된 프로시저 수 있습니다. 이러한 저장된 프로시저 이름을 `Suppliers_Select`, `Suppliers_Insert`, `Suppliers_Update`, 및 `Suppliers_Delete`그림 4와 같이 합니다.


[![자동 생성 저장된 프로시저의 이름을 사용자 지정](working-with-computed-columns-vb/_static/image11.png)](working-with-computed-columns-vb/_static/image10.png)

**그림 4**: Auto-Generated 저장 프로시저의 이름을 사용자 지정 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image12.png))


다음 마법사 단계에는 TableAdapter의 메서드 이름을 지정 하 고 데이터 액세스 및 업데이트에 사용 되는 패턴을 지정할 수 있습니다. 이 옵션을 선택 하는 모든 세 확인란 나 가지만 이름 바꾸기는 `GetData` 메서드를 `GetSuppliers`합니다. 마법사를 완료 하려면 마침을 클릭 합니다.


[![GetData 메서드 GetSuppliers를 이름을 바꿉니다.](working-with-computed-columns-vb/_static/image14.png)](working-with-computed-columns-vb/_static/image13.png)

**그림 5**: 이름 바꾸기는 `GetData` 메서드를 `GetSuppliers` ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image15.png))


마법사 완료 후를 클릭 하면 4 개의 저장된 프로시저 만들고이 형식화 된 데이터 집합에 TableAdapter 및 해당 DataTable을 추가 합니다.

## <a name="step-4-including-the-computed-column-in-the-tableadapter-s-main-query"></a>4 단계: 계산된 열을 포함 하 여 TableAdapter s 주 쿼리에서

이제 TableAdapter를 업데이트 해야 하 고 DataTable 포함 하려면 3 단계에서에서 만든는 `FullContactName` 계산된 열입니다. 이 두 단계로 이루어집니다.

1. 업데이트는 `Suppliers_Select` 저장 프로시저가 반환 하는 `FullContactName` 계산된 열 및
2. 업데이트는 해당 포함 하도록 DataTable `FullContactName` 열입니다.

서버 탐색기에 이동한 Stored Procedures 폴더에 드릴 다운 하 여 시작 합니다. 열기는 `Suppliers_Select` 저장 프로시저 및 업데이트는 `SELECT` 포함 하도록 쿼리는 `FullContactName` 계산된 열:


[!code-sql[Main](working-with-computed-columns-vb/samples/sample4.sql)]

도구 모음에 저장 아이콘을 클릭 하 여, Ctrl + S를 클릭 하 여 또는 저장 선택 하 여 저장된 프로시저의 변경 내용을 저장 `Suppliers_Select` 파일 메뉴에서 옵션입니다.

다음으로, 데이터 집합 디자이너를 반환 하 여 마우스 오른쪽 단추로 클릭는 `SuppliersTableAdapter`, 상황에 맞는 메뉴에서 구성 선택 합니다. `Suppliers_Select` 열에 포함 되어 이제는 `FullContactName` 해당 데이터 열 컬렉션에 있는 열입니다.


[![DataTable의 열을 업데이트할 TableAdapter의 구성 마법사 실행](working-with-computed-columns-vb/_static/image17.png)](working-with-computed-columns-vb/_static/image16.png)

**그림 6**: TableAdapter의 DataTable의 열을 업데이트 하려면 구성 마법사 실행 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image18.png))


마법사를 완료 하려면 마침을 클릭 합니다. 해당 하는 열을 자동으로 추가 됩니다이 `SuppliersDataTable`합니다. TableAdapter 마법사는 점을 감지할 수는 `FullContactName` 열은 계산된 열 및 읽기 전용입니다. 따라서 열 s 설정 `ReadOnly` 속성을 `true`합니다. 이 확인 하려면에서 열을 선택 된 `SuppliersDataTable` 하 고 속성 창으로 이동 합니다 (그림 7 참조). `FullContactName` 열 s `DataType` 및 `MaxLength` 속성 적절 하 게 설정 됩니다.


[![FullContactName 열이 읽기 전용으로 표시 되어 있습니다.](working-with-computed-columns-vb/_static/image20.png)](working-with-computed-columns-vb/_static/image19.png)

**그림 7**:는 `FullContactName` 열이 읽기 전용으로 표시 되어 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image21.png))


## <a name="step-5-adding-agetsupplierbysupplieridmethod-to-the-tableadapter"></a>5 단계: 추가 된`GetSupplierBySupplierID`TableAdapter에 메서드

이 자습서에 대 한 공급 업체는 업데이트 가능한 표로 표시 하는 ASP.NET 페이지를 만듭니다. 지난 자습서 업데이트 비즈니스 논리 계층에서 단일 레코드에 변경 내용을 전파 하는 dal과 해당 속성을 업데이트 하 고 업데이트 된 DataTable를 보내는 강력한 형식의 DataTable로 DAL에서 특정 레코드 백업는 검색 하 여 데이터베이스입니다. -DAL에서 업데이트 되는 레코드를 검색-이 첫 번째 단계를 수행 하려면 먼저 추가 해야는 `GetSupplierBySupplierID(supplierID)` 에 dal과 메서드.

마우스 오른쪽 단추로 클릭는 `SuppliersTableAdapter` 데이터 집합 디자인 하 고 상황에 맞는 메뉴에서 추가 쿼리 옵션을 선택 합니다. 3 단계에서에서 했던 것 처럼 새 저장된 프로시저 만들기 옵션을 선택 하 여 새 저장된 프로시저를 위해 생성 마법사를 통해 (참조 다시 그림 3 마법사의 스크린 샷에 대 한). 이 메서드는 여러 열이 있는 레코드를 반환 하 고는 선택 하는 행을 반환 하는 SQL 쿼리를 사용 하 고 다음을 클릭 하을 나타냅니다.


[![선택 옵션 행을 반환 합니다](working-with-computed-columns-vb/_static/image23.png)](working-with-computed-columns-vb/_static/image22.png)

**그림 8**: 선택 옵션 행을 반환 합니다 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image24.png))


이후 단계 쿼리에서이 메서드에 대 한 사용 하 라는 메시지가 나타납니다. 주 쿼리에서 동일 하지만 특정 공급 업체에 대 한 동일한 데이터 필드를 반환 하 고 다음을 입력 합니다.


[!code-sql[Main](working-with-computed-columns-vb/samples/sample5.sql)]

다음 화면에서 자동으로 생성 되는 저장된 프로시저 이름을 묻는 메시지가 나타납니다. 이 저장된 프로시저 이름을 `Suppliers_SelectBySupplierID` 고 다음을 클릭 합니다.


[![저장된 프로시저 Suppliers_SelectBySupplierID 이름](working-with-computed-columns-vb/_static/image26.png)](working-with-computed-columns-vb/_static/image25.png)

**그림 9**: 저장 프로시저 이름을 `Suppliers_SelectBySupplierID` ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image27.png))


마지막으로, 마법사에 나타나는 메시지 패턴 및 메서드 이름을 TableAdapter에 사용할 액세스 하는 데이터입니다. 이 옵션을 선택 확인란을 모두 유지 되지만 이름을 바꿀는 `FillBy` 및 `GetDataBy` 메서드를 `FillBySupplierID` 및 `GetSupplierBySupplierID`각각.


[![TableAdapter 메서드 FillBySupplierID 이름과 GetSupplierBySupplierID](working-with-computed-columns-vb/_static/image29.png)](working-with-computed-columns-vb/_static/image28.png)

**그림 10**: TableAdapter 메서드 이름을 `FillBySupplierID` 및 `GetSupplierBySupplierID` ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image30.png))


마법사를 완료 하려면 마침을 클릭 합니다.

## <a name="step-6-creating-the-business-logic-layer"></a>6 단계: 비즈니스 논리 계층 만들기

1 단계에서에서 만든 계산된 열을 사용 하는 ASP.NET 페이지를 만들기 전에 먼저 BLL에 해당 하는 메서드를 추가 해야 합니다. 7 단계에서에서 만들, 우리의 ASP.NET 페이지를 사용 하면 사용자가 보고 공급 업체를 편집할 수 있습니다. 따라서 최소한의 모든 공급 업체 및 다른 특정 공급 업체에 업데이트를 가져올 메서드를 제공 하 여 BLL 필요 합니다.

라는 새 클래스 파일을 만듭니다 `SuppliersBLLWithSprocs` 에 `~/App_Code/BLL` 폴더를 다음 코드를 추가 합니다.


[!code-vb[Main](working-with-computed-columns-vb/samples/sample6.vb)]

다른 BLL 클래스와 같은 `SuppliersBLLWithSprocs` 에 `Protected` `Adapter` 속성의 인스턴스를 반환 하는 `SuppliersTableAdapter` 함께 두 개의 클래스 `Public` 메서드: `GetSuppliers` 및 `UpdateSupplier`합니다. `GetSuppliers` 호출 하 고 반환 하는 메서드는 `SuppliersDataTable` 해당 반환한 `GetSupplier` 데이터 액세스 계층에서 메서드. `UpdateSupplier` 메서드 DAL s에 대 한 호출을 통해 업데이트 되 고 특정 공급 업체에 대 한 정보를 검색 `GetSupplierBySupplierID(supplierID)` 메서드. 그런 다음 업데이트는 `CategoryName`, `ContactName`, 및 `ContactTitle` 속성 데이터 액세스 계층 s 호출 하 여 데이터베이스에 이러한 변경 내용을 커밋합니다 `Update` 전달 수정 된 메서드를 `SuppliersRow` 개체입니다.

> [!NOTE]
> 제외 하 고 `SupplierID` 및 `CompanyName`, Suppliers 테이블의 모든 열 허용 `NULL` 값입니다. 따라서 경우에 전달 된 `contactName` 또는 `contactTitle` 매개 변수는 `Nothing` 해당 공간을 `ContactName` 및 `ContactTitle` 속성을는 `NULL` 사용 하 여 데이터베이스 값의 `SetContactNameNull` 및 `SetContactTitleNull`메서드를 각각.


## <a name="step-7-working-with-the-computed-column-from-the-presentation-layer"></a>계산 열이 프레젠테이션 계층에서 작업 하는 7 단계:

계산 열이 추가 `Suppliers` DAL 테이블 및 BLL 적절 하 게 업데이트, ASP.NET 페이지를 사용 하는 구성 준비가 `FullContactName` 계산된 열입니다. 열어 시작는 `ComputedColumns.aspx` 페이지에 `AdvancedDAL` 폴더와 디자이너 도구 상자에서 끌어서는 GridView입니다. GridView s 설정 `ID` 속성을 `Suppliers` 및 스마트 태그를 바인딩할 라는 새 ObjectDataSource `SuppliersDataSource`합니다. ObjectDataSource 사용 하도록 구성 된 `SuppliersBLLWithSprocs` 추가 클래스 6 단계에서에서 백업 하 고 다음을 클릭 합니다.


[![ObjectDataSource SuppliersBLLWithSprocs 클래스를 사용 하도록 구성](working-with-computed-columns-vb/_static/image32.png)](working-with-computed-columns-vb/_static/image31.png)

**그림 11**: 구성에 사용 하 여 ObjectDataSource는 `SuppliersBLLWithSprocs` 클래스 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image33.png))


에 정의 된 두 개의 메서드는는 `SuppliersBLLWithSprocs` 클래스: `GetSuppliers` 및 `UpdateSupplier`합니다. 이러한 두 가지 방법 선택에 지정 된 탭 각각 업데이트 및 확인는 ObjectDataSource의 구성을 완료 하려면 마침을 클릭 합니다.

데이터 소스 구성 마법사를 완료 하면 Visual Studio의 각 반환 된 데이터 필드에 대 한 BoundField를 추가 합니다. 제거는 `SupplierID` BoundField 변경는 `HeaderText` 의 속성은 `CompanyName`, `ContactName`, `ContactTitle`, 및 `FullContactName` BoundFields 회사, 연락처 이름, 제목 및 전체 연락처 이름에 각각. 스마트 태그에서 편집을 사용 하도록 설정 하려면 확인란 GridView s 기본 제공 편집 기능을 켭니다.

BoundFields GridView을 추가할 뿐 아니라 데이터 원본 마법사를 완료로 인해 Visual Studio를 설정 ObjectDataSource s `OldValuesParameterFormatString` 원래 속성\_{0}. 이 설정을 다시 기본값, {0}로 되돌립니다.

편집한 후 이러한 GridView 및 ObjectDataSource에 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](working-with-computed-columns-vb/samples/sample7.aspx)]

그런 다음 브라우저를 통해이 페이지를 참조 하세요. 각 공급 업체는 포함 하는 표에 나열 된 그림 12에서 볼 수 있듯이 `FullContactName` 값은 다른 3 개의 열 연결한 단순히 열 형식으로 지정 `ContactName` (`ContactTitle`, `CompanyName`).


[![각 공급 업체는 표에 나열 된](working-with-computed-columns-vb/_static/image35.png)](working-with-computed-columns-vb/_static/image34.png)

**그림 12**: 각 공급 업체는 표에 나열 된 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image36.png))


특정 공급 업체에서 포스트백이 발생 하 고 해당 행에서 렌더링 된에 대 한 편집 단추를 클릭 하면 (그림 13 참조) 인터페이스의 편집 합니다. 처음 3 개의 열 편집 인터페이스 기본에서 렌더링-TextBox 컨트롤 `Text` 속성 데이터 필드의 값으로 설정 됩니다. 그러나 `FullContactName` , 열을 텍스트로 유지 됩니다. BoundFields 데이터 소스 구성 마법사 완료 시 GridView에 추가 된 경우는 `FullContactName` BoundField s `ReadOnly` 속성이로 설정 된 `True` 때문에 해당 `FullContactName` 열에는 `SuppliersDataTable` 에 해당 `ReadOnly` 속성이로 설정 `True`합니다. 4 단계에서에서 설명한 것 처럼는 `FullContactName` s `ReadOnly` 속성이로 설정 된 `True` TableAdapter 열이 계산된 열을 검색 합니다.


[![FullContactName 열이 편집할 수 없습니다.](working-with-computed-columns-vb/_static/image38.png)](working-with-computed-columns-vb/_static/image37.png)

**그림 13**:는 `FullContactName` 열이 편집할 수 없습니다 ([전체 크기 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image39.png))


계속 하는 편집 가능한 열 중 하나 이상의 값으로 업데이트를 업데이트를 클릭 합니다. 참고 방법을 `FullContactName`의 값의 변경 내용을 반영 하도록 자동으로 업데이트 됩니다.

> [!NOTE]
> GridView 현재 사용 BoundFields 편집 가능한 필드에 대 한 기본 인터페이스 편집으로 인해 발생 합니다. 이후는 `CompanyName` 필드는 필수는 RequiredFieldValidator 포함 된를 TemplateField로 변환 해야 합니다. I이 그대로 실행으로 관심된 판독기에 대 한 합니다. 참조는 [편집 및 삽입 인터페이스에 유효성 검사 컨트롤 추가](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) 자습서에 대 한 단계별 지침은 BoundField를 TemplateField를 변환 및 유효성 검사 컨트롤을 추가 합니다.


## <a name="summary"></a>요약

Microsoft SQL Server 테이블에 대 한 스키마를 정의 하면 계산된 열을 포함 합니다. 이들은 일반적으로 동일한 레코드의 다른 열에서 값을 참조 하는 식에서 값이 계산 되는 열입니다. 값 이후 계산된 열은 식에 기반에 대 한 읽기 전용 이며 값을 할당할 수 없습니다는 `INSERT` 또는 `UPDATE` 문. 자동으로 해당를 생성 하려고 하는 TableAdapter의 주 쿼리에서 계산된 열을 사용 하는 경우 문제에 소개 `INSERT`, `UPDATE`, 및 `DELETE` 문.

이 자습서에서는 계산된 열에 의해 제기 되는 문제 해결에 대 한 기술에 설명 했습니다. 특히, 임시 SQL 문을 사용 하 여 Tableadapter에 내재 된 오류를 해결 하기 위해 우리의 TableAdapter에서 저장된 프로시저 사용. 저장 프로시저를 TableAdapter 마법사 새로 만들기, 것이 주 쿼리에서 현재 상태는 데이터 수정 저장 프로시저 생성 되지 않도록 하기 때문에 계산된 열을 처음 생략 된 것이 중요 합니다. TableAdapter 처음에 구성 된 후 해당 `SelectCommand` 저장된 프로시저는 모든 계산된 열을 포함 하도록 retooled 될 수 있습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Hilton Geisenow 및 Teresa 머피의 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](adding-additional-datatable-columns-vb.md)
[다음](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb.md)
