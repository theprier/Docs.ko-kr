---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-vb
title: 계산된 열 (VB)를 사용 하 여 작업 | Microsoft Docs
author: rick-anderson
description: Microsoft SQL Server 계산된 열 값은 식에서 계산을 정의할 수 있습니다 데이터베이스 테이블을 만들 때 일반적으로 referen...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 5811b8ff-ed56-40fc-9397-6b69ae09a8f6
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-vb
msc.type: authoredcontent
ms.openlocfilehash: 81254408252c5e786c938d4eb8beb1c7a2b65218
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41835460"
---
<a name="working-with-computed-columns-vb"></a>계산된 열 (VB)를 사용 하 여 작업
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_71_VB.zip) 또는 [PDF 다운로드](working-with-computed-columns-vb/_static/datatutorial71vb1.pdf)

> 데이터베이스 테이블을 만들 때 Microsoft SQL Server를 사용 하면 계산된 열 값은 일반적으로 같은 데이터베이스 레코드의 다른 값을 참조 하는 식에서 계산을 정의할 수 있습니다. 이러한 값은 Tableadapter를 사용 하 여 작업 하는 경우 특별 한 고려를 해야 하는 데이터베이스에서 읽기 전용입니다. 이 자습서에서는 계산된 열을 기준으로 인 한 과제를 충족 하는 방법에 알아봅니다.


## <a name="introduction"></a>소개

Microsoft SQL Server에 대 한 허용  *[계산 열](https://msdn.microsoft.com/library/ms191250.aspx)* 는 열 값은 일반적으로 동일한 테이블의 다른 열에서 값을 참조 하는 식에서 계산 됩니다. 예를 들어, 데이터 모델을 추적 하는 한 번 라는 테이블이 있을 수 있습니다 `ServiceLog` 포함 하 여 열을 사용 하 여 `ServicePerformed`를 `EmployeeID`를 `Rate`, 및 `Duration`, 특히 합니다. 금액을 하는 동안 서비스 당 항목 웹 페이지 또는 기타 프로그래밍 인터페이스를 통해 계산할 수 없습니다 (되는 기간을 곱한 속도)에서 열을 포함 하려면 유용할 수 있습니다 합니다 `ServiceLog` 라는 테이블 `AmountDue` 이 보고 하는 정보입니다. 일반 열으로이 열을 만들 수 있지만 언제 든 지 업데이트 해야 합니다 `Rate` 또는 `Duration` 열 값을 변경 합니다. 더 나은 방법을 확인 하는 것은 `AmountDue` 식을 사용 하는 열이 계산된 열 `Rate * Duration`합니다. 이렇게 하면 SQL Server를 자동으로 계산 된 `AmountDue` 때마다 쿼리에서 참조 된 열 값입니다.

이러한 열은 읽기 전용 및 따라서 수 없는 값에 할당 된에 s 계산된 열 값은 식에 의해 결정 됩니다, 하므로 `INSERT` 또는 `UPDATE` 문입니다. 그러나 계산된 열에는 임시 SQL 문을 사용 하 여 TableAdapter에 대 한 기본 쿼리는 포함 된 경우 자동으로에서 다루지 않으므로 자동 생성 `INSERT` 고 `UPDATE` 문입니다. Tableadapter 따라서 `INSERT` 하 고 `UPDATE` 쿼리 및 `InsertCommand` 및 `UpdateCommand` 계산된 열에 대 한 참조를 제거 하려면 속성을 업데이트 해야 합니다.

계산 임시 SQL 문을 사용 하 여 TableAdapter 사용 하 여 열을 사용 하는 한 가지 문제는 TableAdapter s `INSERT` 및 `UPDATE` 쿼리 TableAdapter 구성 마법사를 완료할 때마다 자동으로 다시 생성 됩니다. 계산된 열에서 수동으로 제거 되므로 합니다 `INSERT` 및 `UPDATE` 쿼리 마법사를 다시 실행 하는 경우에 나타납니다. Tableadapter는 저장된 프로시저를 사용 하지 않습니다 하지만이 오류에서 저하, 3 단계에서에서 제기 하는 자체 쿼크를 갖지 합니다.

이 자습서에서는 계산된 열을 추가 합니다 `Suppliers` Northwind 데이터베이스의 테이블을 만든 다음이 테이블의 계산된 열과 작동 하도록 해당 TableAdapter. TableAdapter 구성 마법사를 사용 하는 경우이 사용자 지정 유효 하지 t 손실 되도록 하는 대신 임시 SQL 문이 저장된 프로시저를 사용 하 여 TableAdapter를 얻게 됩니다.

Let s 시작!

## <a name="step-1-adding-a-computed-column-to-thesupplierstable"></a>1 단계: 계산된 열을 추가 합니다`Suppliers`테이블

Northwind 데이터베이스에 없으므로 계산된 열 하나 직접 추가 해야 합니다. 이 자습서에 계산된 열을 추가 하는 수에 대 한 합니다 `Suppliers` 라는 테이블 `FullContactName` s 연락처 이름, 제목 및에 회사는 다음 형식으로 반환: `ContactName` (`ContactTitle`, `CompanyName`). 이 계산 열 공급자에 대 한 정보를 표시할 때 보고서에 사용 될 수 있습니다.

열어서 시작 합니다 `Suppliers` 마우스 오른쪽 단추로 클릭 하 여 테이블 정의 `Suppliers` 서버 탐색기에서 테이블 및 상황에 맞는 메뉴에서 테이블 정의 열기를 선택 합니다. 테이블과 같은 데이터 형식에 해당 속성을 열 수 있는지 여부를 표시 됩니다 `NULL` 및 등입니다. 계산된 열을 추가 하려면 테이블 정의에 열 이름을 입력 하 여 시작 합니다. 그런 다음 해당 식을 열 속성 창에서 계산 열 사양 섹션 (수식) 텍스트 상자에 입력 (그림 1 참조). 계산된 열의 이름을 `FullContactName` 하 고 다음 식을 사용 합니다.


[!code-sql[Main](working-with-computed-columns-vb/samples/sample1.sql)]

SQL에서 문자열을 연결 수는 참고를 사용 하 여는 `+` 연산자입니다. `CASE` 문은 기존의 프로그래밍 언어의 조건부와 같은 사용할 수 있습니다. 위 식에서 합니다 `CASE` 로 문을 읽을 수 있습니다: 경우 `ContactTitle` 아닙니다 `NULL` 출력 한 다음를 `ContactTitle` 그렇지 쉼표를 사용 하 여 연결 하는 값 emit 아무 작업도 수행 합니다. 유용성에 대 한 자세한 내용은 합니다 `CASE` 문을 참조 [SQL의 Power `CASE` 문을](http://www.4guysfromrolla.com/webtech/102704-1.shtml)합니다.

> [!NOTE]
> 사용 하는 대신 한 `CASE` 방침, 또는 사용 했 `ISNULL(ContactTitle, '')`합니다. [`ISNULL(checkExpression, replacementValue)`](https://msdn.microsoft.com/library/ms184325.aspx) 반환 *checkExpression* NULL이 아닌 경우, 그렇지 않으면 반환 *replacementValue*합니다. 중 하나를 하는 동안 `ISNULL` 또는 `CASE` 작동이 인스턴스에서 더 복잡 한 시나리오 여기서의 유연성을 `CASE` 문이 일치할 수 없는 `ISNULL`.


이 계산된 열을 추가한 후 그림 1의 스크린샷 같은 화면이 표시 됩니다.


[![FullContactName Suppliers 테이블에 명명 된 계산된 열 추가](working-with-computed-columns-vb/_static/image2.png)](working-with-computed-columns-vb/_static/image1.png)

**그림 1**: 계산 된 열 이름이 추가 `FullContactName` 에 `Suppliers` 테이블 ([클릭 하 여 큰 이미지 보기](working-with-computed-columns-vb/_static/image3.png))


계산된 열을 명명 하 고 해당 식 입력을 변경 테이블에 저장 도구 모음 저장 아이콘을 클릭 하 여, Ctrl + S를 눌러 또는 파일 메뉴로 이동 하 고 저장을 선택 하 여 `Suppliers`입니다.

서버 탐색기에서 방금 추가 된 열을 포함 하 여 새로 고쳐야 테이블을 저장 합니다 `Suppliers`의 테이블 열 목록입니다. (수식) 텍스트 상자에 입력 한 식이 대괄호를 사용 하 여 열 이름을 둘러싸는 것, 불필요 한 공백을 제거 하는 해당 하는 식으로 자동으로 조정 되며 또한 (`[]`)를 보다 분명 하 게 표시 하려면 괄호를 포함 합니다. 작업 순서:


[!code-sql[Main](working-with-computed-columns-vb/samples/sample2.sql)]

Microsoft SQL Server의 계산된 열에 대 한 자세한 내용은 참조는 [기술 문서](https://msdn.microsoft.com/library/ms191250.aspx)합니다. 체크 아웃할 수도 합니다 [방법: Specify Computed Columns](https://msdn.microsoft.com/library/ms188300.aspx) 계산된 열 만들기의 단계별 연습에 대 한 합니다.

> [!NOTE]
> 기본적으로 계산된 열 테이블에 물리적으로 저장 되지 않습니다 하지만 대신 쿼리에서 참조 하는 때마다 다시 계산 합니다. 그러나 유지 하는 확인란을 선택 테이블의 계산된 열을 물리적으로 저장 하도록 SQL Server 지시할 수 있습니다. 이렇게 하면 인덱스에서 계산된 열 값을 사용 하는 쿼리의 성능을 향상 시킬 수 있는 계산 열을 만들 수를 해당 `WHERE` 절. 참조 [계산 열에 인덱스 만들기](https://msdn.microsoft.com/library/ms189292.aspx) 자세한 내용은 합니다.


## <a name="step-2-viewing-the-computed-column-s-values"></a>2 단계: 계산된 열의 값 보기

Let s 보려면 잠시 데이터 액세스 계층에서 작업을 시작 하기 전에 `FullContactName` 값입니다. 서버 탐색기에서 마우스 오른쪽 단추로 클릭는 `Suppliers` 테이블 이름 및 상황에 맞는 메뉴에서 새 쿼리를 선택 합니다. 사용 하는 쿼리에 포함할 테이블을 선택 하도록 요청 하는 쿼리 창을 표시 됩니다. 추가 된 `Suppliers` 테이블 및 닫기를 클릭 합니다. 다음으로 확인 합니다 `CompanyName`, `ContactName`, `ContactTitle`, 및 `FullContactName` Suppliers 테이블의 열입니다. 마지막으로 쿼리를 실행 하 고 결과 보려면 도구 모음에서 빨강 느낌표 아이콘을 클릭 합니다.

결과 포함 하는 그림 2에서 볼 수 있듯이 `FullContactName`, 나열 하는 합니다 `CompanyName`, `ContactName`, 및 `ContactTitle` 형식을 사용 하 여 열 `ContactName` (`ContactTitle`, `CompanyName`).


[![FullContactName 형식 ContactName (ContactTitle, CompanyName) 사용](working-with-computed-columns-vb/_static/image5.png)](working-with-computed-columns-vb/_static/image4.png)

**그림 2**: 합니다 `FullContactName` 형식을 사용 `ContactName` (`ContactTitle`에 `CompanyName`) ([클릭 하 여 큰 이미지 보기](working-with-computed-columns-vb/_static/image6.png))


## <a name="step-3-adding-thesupplierstableadapterto-the-data-access-layer"></a>3 단계: 추가 된`SuppliersTableAdapter`데이터 액세스 계층

응용 프로그램의 공급 업체 정보를 사용 하려면 먼저는 DAL에서 TableAdapter를 DataTable을 만들고 해야 합니다. 이상적으로 이렇게 이전 자습서에서 검사 같은 간단한 단계를 사용 하 여 합니다. 그러나 계산된 열을 사용 하 여 작업 토론을 활용 하는 몇 가지 주름을 소개 합니다.

임시 SQL 문을 사용 하 여 TableAdapter를 사용 하는 경우 TableAdapter가 기본 쿼리에 TableAdapter 구성 마법사를 통해 간단히 계산된 열을 포함할 수 있습니다. 그러나 따라서에서 자동 생성 `INSERT` 및 `UPDATE` 계산된 열을 포함 하는 문입니다. 다음이 방법 중 하나를 실행 하려는 경우는 `SqlException` 메시지 열을 사용 하 여 *ColumnName* 계산된 열 이거나 UNION 연산자의 결과 예외가 이므로 수정할 수 없습니다. 하는 동안 합니다 `INSERT` 및 `UPDATE` 문은 TableAdapter s를 통해 수동으로 조정할 수 있습니다 `InsertCommand` 및 `UpdateCommand` 속성, 이러한 사용자 지정 없어집니다 TableAdapter 구성 마법사를 다시 실행할 때마다.

임시 SQL 문을 사용 하는 Tableadapter의 때,으로 인해 계산된 열을 사용 하 여 작업 하는 경우 저장된 프로시저를 사용할 것이 좋습니다. 기존 저장된 프로시저를 사용 하는 경우 단순히 TableAdapter를 구성에 설명 된 대로 합니다 [를 사용 하 여 기존 저장 프로시저는 입력 데이터 집합의 Tableadapter에 대 한](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 자습서입니다. 그러나 TableAdapter 마법사를 저장된 프로시저를 만들 경우 것 처음에 주 쿼리에서 모든 계산된 열을 생략 하는 것이 중요 합니다. 기본 쿼리에 계산된 열을 포함 하는 경우 TableAdapter 구성 마법사를 알려줍니다, 완료 되 면 해당 저장된 프로시저를 만들 수 없습니다. 처음에 계산된 열 무료 기본 쿼리를 사용 하 여 TableAdapter를 구성 하 고 해당 저장된 프로시저 및 TableAdapter s 다음 수동으로 업데이트 해야 말해 `SelectCommand` 계산된 열을 포함 합니다. 이 방법은 사용 되는 비슷합니다는 [사용 하도록 TableAdapter 업데이트](updating-the-tableadapter-to-use-joins-vb.md)`JOIN`*s* 자습서입니다.

이 자습서에서는 s를 새 TableAdapter를 추가 하 고 우리 회사에 저장된 프로시저를 자동으로 만들도록 지정할 수 있습니다. 따라서 처음에 생략 해야 합니다는 `FullContactName` 기본 쿼리에서 계산된 열입니다.

열어서 시작 합니다 `NorthwindWithSprocs` 데이터 집합에는 `~/App_Code/DAL` 폴더. 디자이너에서 마우스를 상황에 맞는 메뉴에서 새 TableAdapter를 추가 하려면 선택 합니다. TableAdapter 구성 마법사를 시작 됩니다. 데이터를 쿼리 하는 데이터베이스를 지정 합니다. (`NORTHWNDConnectionString` 에서 `Web.config`) 다음을 클릭 합니다. 쿼리 및 수정에 대 한 저장된 프로시저를 아직 만들지 않은 것 이므로 `Suppliers` 테이블 만들기 마법사에 만들고 되 고 다음을 클릭 되도록 새 저장된 프로시저 옵션을 선택 합니다.


[![새 저장된 프로시저 만들기 옵션을 선택 합니다.](working-with-computed-columns-vb/_static/image8.png)](working-with-computed-columns-vb/_static/image7.png)

**그림 3**: 만들기의 새 저장된 프로시저 옵션을 선택 ([큰 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image9.png))


이후 단계는 기본 쿼리에 요청 합니다. 반환 하는 다음 쿼리를 입력 합니다 `SupplierID`, `CompanyName`를 `ContactName`, 및 `ContactTitle` 각 공급자에 대 한 열입니다. 이 쿼리는 계산된 열을 의도적으로 생략 하는 참고 (`FullContactName`); 4 단계에서에서이 열을 포함 하려면 해당 저장된 프로시저를 업데이트 합니다.


[!code-sql[Main](working-with-computed-columns-vb/samples/sample3.sql)]

주 쿼리를 입력 하 고 다음을 클릭 합니다 마법사를 사용 하면 생성 된 네 개의 저장된 프로시저 이름을 수 있도록 합니다. 이러한 저장된 프로시저의 이름을 `Suppliers_Select`, `Suppliers_Insert`를 `Suppliers_Update`, 및 `Suppliers_Delete`그림 4에서 볼 수 있듯이, 합니다.


[![자동 생성 저장된 프로시저의 이름을 사용자 지정](working-with-computed-columns-vb/_static/image11.png)](working-with-computed-columns-vb/_static/image10.png)

**그림 4**: Auto-Generated 저장 프로시저의 이름을 사용자 지정 ([큰 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image12.png))


다음 마법사 단계를 사용 하면 TableAdapter의 메서드 이름을 지정 하 고 데이터 액세스 및 업데이트 하는 데 패턴을 지정할 수 있습니다. 이 옵션을 선택 하는 모든 세 개의 확인란 유지 되지만 이름을 바꿀 합니다 `GetData` 메서드를 `GetSuppliers`입니다. 마법사를 완료 하려면 마침을 클릭 합니다.


[![GetData 메서드 GetSuppliers에 이름 바꾸기](working-with-computed-columns-vb/_static/image14.png)](working-with-computed-columns-vb/_static/image13.png)

**그림 5**: 이름 바꾸기는 `GetData` 메서드를 `GetSuppliers` ([클릭 하 여 큰 이미지 보기](working-with-computed-columns-vb/_static/image15.png))


마법사는 마침을 클릭 하면 4 개의 저장된 프로시저를 만들고이 형식화 된 데이터 집합에 TableAdapter 및 해당 DataTable을 추가 합니다.

## <a name="step-4-including-the-computed-column-in-the-tableadapter-s-main-query"></a>4 단계: 계산된 열을 포함 하 여 TableAdapter가 기본 쿼리에

이제 TableAdapter를 업데이트 해야 하 고 포함 하려면 3 단계에서에서 만든 DataTable을 `FullContactName` 계산된 열입니다. 이 두 단계로 이루어집니다.

1. 업데이트를 `Suppliers_Select` 저장 프로시저를 반환할는 `FullContactName` 계산된 열 및
2. DataTable 해당 포함 하도록 업데이트 `FullContactName` 열입니다.

서버 탐색기로 이동 하 고 저장 프로시저 폴더로 드릴 다운 하 여 시작 합니다. 열기는 `Suppliers_Select` 저장 프로시저 및 업데이트 합니다 `SELECT` 포함 하도록 쿼리를 `FullContactName` 계산된 열:


[!code-sql[Main](working-with-computed-columns-vb/samples/sample4.sql)]

도구 모음 저장 아이콘을 클릭 하 여, Ctrl + S를 눌러 또는 저장을 선택 하 여 저장된 프로시저의 변경 내용을 저장 `Suppliers_Select` 파일 메뉴에서 옵션입니다.

데이터 집합 디자이너로 돌아온 다음으로, 마우스 오른쪽 단추로 클릭는 `SuppliersTableAdapter`, 상황에 맞는 메뉴에서 구성 선택 합니다. 합니다 `Suppliers_Select` 열에 포함 되어 이제는 `FullContactName` 데이터 열 컬렉션의 열입니다.


[![DataTable의 열을 업데이트 하려면 TableAdapter의 구성 마법사 실행](working-with-computed-columns-vb/_static/image17.png)](working-with-computed-columns-vb/_static/image16.png)

**그림 6**: tableadapter의 DataTable의 열을 업데이트 하려면 구성 마법사를 실행 ([큰 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image18.png))


마법사를 완료 하려면 마침을 클릭 합니다. 이 자동으로 해당 열을 추가 하 여 `SuppliersDataTable`입니다. TableAdapter 마법사가 지능적 감지 하는 `FullContactName` 열은 계산된 열 및 읽기 전용입니다. 따라서 s 열을 설정 합니다 `ReadOnly` 속성을 `true`입니다. 이 확인 하려면에서 열을 선택 합니다 `SuppliersDataTable` 속성 창으로 이동한 다음 (그림 7 참조). 합니다 `FullContactName` 열 s `DataType` 및 `MaxLength` 속성도 적절 하 게 설정 됩니다.


[![FullContactName 열이 읽기 전용으로 표시 되어](working-with-computed-columns-vb/_static/image20.png)](working-with-computed-columns-vb/_static/image19.png)

**그림 7**: 합니다 `FullContactName` 열은 읽기 전용으로 표시 됩니다 ([클릭 하 여 큰 이미지 보기](working-with-computed-columns-vb/_static/image21.png))


## <a name="step-5-adding-agetsupplierbysupplieridmethod-to-the-tableadapter"></a>5 단계: 추가 된`GetSupplierBySupplierID`TableAdapter 메서드

이 자습서에 대 한 공급 업체에서 업데이트할 수 있는 표를 표시 하는 ASP.NET 페이지를 만들겠습니다. 이전 자습서를 업데이트 했습니다 비즈니스 논리 계층에서 단일 레코드 속성을 업데이트 하 고 업데이트 된 DataTable 보내를 강력한 형식화 된 DataTable로 DAL에서 특정 레코드에 변경 내용을 전파 하는 DAL를 검색 하 여 데이터베이스입니다. -DAL에서 업데이트 되는 레코드 검색-이 첫 번째 단계를 수행 하려면 먼저 추가 해야는 `GetSupplierBySupplierID(supplierID)` DAL 방법입니다.

마우스 오른쪽 단추로 클릭는 `SuppliersTableAdapter` 데이터 집합 디자인에서 상황에 맞는 메뉴에서 추가 쿼리 옵션을 선택 합니다. 3 단계에서에서 했던 것 처럼 자동으로 새 저장된 프로시저 만들기 옵션을 선택 하 여 미국에 대 한 새 저장된 프로시저를 생성 (참조 다시 그림 3이 마법사 단계 스크린샷). 이 메서드는 여러 열을 사용 하 여 레코드를 반환 하 고, 행을 반환 하는 선택 된 SQL 쿼리를 사용 하 고 다음을 클릭을 나타냅니다.


[![옵션 행을 반환 하는 선택](working-with-computed-columns-vb/_static/image23.png)](working-with-computed-columns-vb/_static/image22.png)

**그림 8**: 선택 옵션 행을 반환 하는 ([큰 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image24.png))


이후 단계를 사용 하도록 쿼리를이 메서드에 대 한에 대 한 요청입니다. 기본 쿼리로 이지만 특정 공급 업체에 대 한 동일한 데이터 필드를 반환 하는 다음을 입력 합니다.


[!code-sql[Main](working-with-computed-columns-vb/samples/sample5.sql)]

다음 화면에서는 자동으로 생성 되는 저장된 프로시저 이름입니다. 이 저장된 프로시저 이름을 `Suppliers_SelectBySupplierID` 다음을 클릭 합니다.


[![저장된 프로시저 Suppliers_SelectBySupplierID 이름](working-with-computed-columns-vb/_static/image26.png)](working-with-computed-columns-vb/_static/image25.png)

**그림 9**: 저장 프로시저의 이름을 `Suppliers_SelectBySupplierID` ([클릭 하 여 큰 이미지 보기](working-with-computed-columns-vb/_static/image27.png))


마지막으로, 마법사의 메시지에 패턴 및 TableAdapter에 사용할 메서드 이름에 액세스 하는 데이터입니다. 이 옵션을 선택 확인란을 모두 유지 되지만 이름을 바꿀 합니다 `FillBy` 및 `GetDataBy` 방법 `FillBySupplierID` 및 `GetSupplierBySupplierID`각각.


[![TableAdapter 메서드 FillBySupplierID 이름과 GetSupplierBySupplierID](working-with-computed-columns-vb/_static/image29.png)](working-with-computed-columns-vb/_static/image28.png)

**그림 10**: TableAdapter 메서드 이름을 `FillBySupplierID` 하 고 `GetSupplierBySupplierID` ([클릭 하 여 큰 이미지 보기](working-with-computed-columns-vb/_static/image30.png))


마법사를 완료 하려면 마침을 클릭 합니다.

## <a name="step-6-creating-the-business-logic-layer"></a>6 단계: 비즈니스 논리 레이어 만들기

1 단계에서에서 만든 계산된 열을 사용 하는 ASP.NET 페이지를 만들기 전에 먼저 BLL에 해당 하는 메서드를 추가 해야 합니다. 7 단계에서에서 만드는 것을 보면 ASP.NET 페이지에 보고 공급 업체를 편집 하는 사용자를 허용 됩니다. 따라서 최소한 모든 공급 업체 및 다른 특정 공급자를 업데이트 하는 메서드를 제공 하는 BLL 필요 합니다.

라는 새 클래스 파일을 만듭니다 `SuppliersBLLWithSprocs` 에 `~/App_Code/BLL` 폴더 다음 코드를 추가 합니다.


[!code-vb[Main](working-with-computed-columns-vb/samples/sample6.vb)]

다른 BLL 클래스 처럼 `SuppliersBLLWithSprocs` 에 `Protected` `Adapter` 의 인스턴스를 반환 하는 속성을 `SuppliersTableAdapter` 두 클래스 `Public` 메서드: `GetSuppliers` 및 `UpdateSupplier`합니다. `GetSuppliers` 메서드를 호출 하 고 반환 합니다 `SuppliersDataTable` 해당 반환한 `GetSupplier` 데이터 액세스 계층에서 메서드. 합니다 `UpdateSupplier` DAL s에 대 한 호출을 통해 업데이트 되 고 특정 공급자에 대 한 정보를 검색 하는 메서드 `GetSupplierBySupplierID(supplierID)` 메서드. 그런 다음 업데이트를 `CategoryName`, `ContactName`, 및 `ContactTitle` 속성 데이터 액세스 계층 s를 호출 하 여 데이터베이스에 이러한 변경 내용을 커밋합니다 `Update` 메서드를 수정 된 전달 `SuppliersRow` 개체입니다.

> [!NOTE]
> 제외 하 고 `SupplierID` 하 고 `CompanyName`, Suppliers 테이블에 열을 모두 허용 `NULL` 값입니다. 따라서 경우에 전달 된 `contactName` 또는 `contactTitle` 매개 변수는 `Nothing` 해당 설정 해야 `ContactName` 및 `ContactTitle` 속성을 `NULL` 사용 하 여 데이터베이스 값은 `SetContactNameNull` 및 `SetContactTitleNull`메서드를 각각.


## <a name="step-7-working-with-the-computed-column-from-the-presentation-layer"></a>7 단계: 프레젠테이션 계층에서 계산된 열 작업

계산 열이 추가 합니다 `Suppliers` DAL 테이블 및 BLL 적절 하 게 업데이트를 사용 하는 ASP.NET 페이지를 빌드할 준비가 `FullContactName` 계산된 열입니다. 열어서 시작 합니다 `ComputedColumns.aspx` 페이지에서 `AdvancedDAL` 폴더 및 디자이너 도구 상자에서 끌어서 GridView입니다. 집합 GridView s `ID` 속성을 `Suppliers` 및 스마트 태그를 바인딩할 라는 새로운 ObjectDataSource는 `SuppliersDataSource`합니다. ObjectDataSource를 사용 하 여 구성 된 `SuppliersBLLWithSprocs` 추가한 클래스 6 단계에서에서 백업 하 고 다음을 클릭 합니다.


[![SuppliersBLLWithSprocs 클래스를 사용 하는 ObjectDataSource 구성](working-with-computed-columns-vb/_static/image32.png)](working-with-computed-columns-vb/_static/image31.png)

**그림 11**: ObjectDataSource 사용 하도록 구성 된 `SuppliersBLLWithSprocs` 클래스 ([클릭 하 여 큰 이미지 보기](working-with-computed-columns-vb/_static/image33.png))


에 정의 된 두 개의 메서드를 가지는 `SuppliersBLLWithSprocs` 클래스: `GetSuppliers` 및 `UpdateSupplier`합니다. 이러한 두 메서드 SELECT에 지정 된 탭 각각 업데이트 및 확인 ObjectDataSource의 구성을 완료 하려면 마침을 클릭 합니다.

데이터 소스 구성 마법사를 완료 하면 Visual Studio가 반환 하는 데이터 필드의 각는 BoundField를 추가 합니다. 제거는 `SupplierID` BoundField 변경 및는 `HeaderText` 의 속성을 `CompanyName`, `ContactName`, `ContactTitle`, 및 `FullContactName` BoundFields 회사, 연락처 이름, 제목 및 전체 연락처 이름에 각각. 스마트 태그에서 GridView가 기본 제공 편집 기능을 켜려면 편집 사용 확인란을 확인 합니다.

BoundFields GridView를에 추가 하는 것 외에도 데이터 원본 마법사를 완료 해도 ObjectDataSource s를 설정 하려면 Visual Studio `OldValuesParameterFormatString` 속성을 원래\_{0}합니다. 이 설정을 다시 해당 기본값으로 되돌리기 {0} 합니다.

GridView 및 ObjectDataSource 같은이 편집을 마치면 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](working-with-computed-columns-vb/samples/sample7.aspx)]

그런 다음 브라우저를 통해이 페이지를 방문 합니다. 각 공급 업체를 포함 하는 표에 나열 됩니다 그림 12에서 볼 수 있듯이 `FullContactName` 열에서 값이 단순히 연결 하 여 다른 세 개의 열으로 포맷 `ContactName` (`ContactTitle`, `CompanyName`).


[![각 공급 업체는 표에 나열 된](working-with-computed-columns-vb/_static/image35.png)](working-with-computed-columns-vb/_static/image34.png)

**그림 12**: 각 공급 업체는 표에 나열 된 ([큰 이미지를 보려면 클릭](working-with-computed-columns-vb/_static/image36.png))


특정 공급 업체 포스트백을 발생 시키는 있으며 해당 행에 렌더링에 대 한 편집 단추를 클릭 하면 (그림 13 참조) 인터페이스의 편집 합니다. 처음 세 열 편집 인터페이스의 기본에서 렌더링-TextBox 컨트롤 `Text` 속성 데이터 필드의 값으로 설정 됩니다. 그러나 `FullContactName` 텍스트 열에 그대로 있습니다. 데이터 소스 구성 마법사를 완료할 때 GridView에는 BoundFields 추가 된 경우는 `FullContactName` BoundField s `ReadOnly` 속성이 설정 되 `True` 때문에 해당 `FullContactName` 열에는 `SuppliersDataTable` 에 해당 `ReadOnly` 속성이 설정 `True`합니다. 4 단계에서에서 설명 했 듯이 합니다 `FullContactName` s `ReadOnly` 속성이 설정 되 `True` TableAdapter 열 계산된 열 되었는지 검색 합니다.


[![FullContactName 열이 편집할 수 없습니다.](working-with-computed-columns-vb/_static/image38.png)](working-with-computed-columns-vb/_static/image37.png)

**그림 13**: 합니다 `FullContactName` 열이 편집할 수 없습니다 ([클릭 하 여 큰 이미지 보기](working-with-computed-columns-vb/_static/image39.png))


계속 해 서 및 편집할 수 있는 열 중 하나 이상의 값을 업데이트 하 고 업데이트를 클릭 합니다. 참고 하는 방법을 `FullContactName`의 값이 변경 내용을 반영 하도록 자동으로 업데이트 됩니다.

> [!NOTE]
> GridView 현재 사용 BoundFields 편집 가능한 필드에 대 한 기본 인터페이스를 편집 합니다. 이후를 `CompanyName` RequiredFieldValidator를 포함 하는 TemplateField로 변환 되어야 하며, 필드는 필수입니다. I 관심이 있는 독자를 연습으로 둡니다. 참조를 [편집 및 삽입 인터페이스에 유효성 검사 컨트롤 추가](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) 는 BoundField templatefield로 변환 하 고 유효성 검사 컨트롤 추가 대 한 단계별 지침에 대 한 자습서입니다.


## <a name="summary"></a>요약

Microsoft SQL Server 테이블에 대 한 스키마를 정의 하면 계산 열을 포함 합니다. 이 열 값은 일반적으로 동일한 레코드의 다른 열에서 값을 참조 하는 식에서 계산 됩니다. 값 이후 계산된 열 식에 기반한에 대 한 읽기 전용 이며 값을 할당할 수 없습니다는 `INSERT` 또는 `UPDATE` 문입니다. 이 과제가 해당를 자동으로 생성 하려고 하는 TableAdapter의 주 쿼리에서 계산된 열을 사용 하는 경우 `INSERT`, `UPDATE`, 및 `DELETE` 문입니다.

이 자습서에서는 계산된 열에 의해 야기 되는 문제를 우회 하는 기술을 설명 합니다. 특히 사용 했습니다 저장된 프로시저는 TableAdapter의 임시 SQL 문을 사용 하는 Tableadapter에 내재 된 때를 극복 하기 위해. 새로 만들기 TableAdapter 마법사 저장 프로시저를 때 처음에 근무 생성 되 고 데이터 수정 저장 프로시저를 방지 하기 때문에 계산된 열을 생략할 기본 쿼리에 있는 것이 중요 합니다. TableAdapter 처음 구성한 후 해당 `SelectCommand` 저장된 프로시저는 계산된 열을 포함 하도록 retooled 수 있습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자는 Hilton Geisenow 및 Teresa Murphy 있었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](adding-additional-datatable-columns-vb.md)
> [다음](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb.md)
