---
uid: web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-vb
title: "사용자 지정 정렬 (VB) 데이터를 페이징 | Microsoft Docs"
author: rick-anderson
description: "이전 자습서에서는 웹 페이지에서 데이터를 presentating 때 사용자 지정 페이징을 구현 하는 방법을 배웠습니다. 이 자습서에서는 이전 확장 하는 방법을 표시..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/15/2006
ms.topic: article
ms.assetid: 4823a186-caaf-4116-a318-c7ff4d955ddc
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-vb
msc.type: authoredcontent
ms.openlocfilehash: ee02915a5c69d824c6450157b0c734a2e2ab5c11
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="sorting-custom-paged-data-vb"></a>사용자 지정 정렬 (VB) 데이터를 페이징
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_26_VB.exe) 또는 [PDF 다운로드](sorting-custom-paged-data-vb/_static/datatutorial26vb1.pdf)

> 이전 자습서에서는 웹 페이지에서 데이터를 presentating 때 사용자 지정 페이징을 구현 하는 방법을 배웠습니다. 이 자습서에서는 사용자 지정 페이징을 정렬에 대 한 지원을 포함 하도록 앞의 예제를 확장 하는 방법을 알아봅니다.


## <a name="introduction"></a>소개

기본 페이징에 비해 여러 가지 크기 순서 대로 정렬, 사실상 페이징 구현을 선택 하는 많은 양의 데이터를 페이징할 때는 페이징 하는 사용자 지정을 만드는 사용자 지정 페이징 데이터 페이징의 성능 향상 시킬 수 있습니다. 그러나 사용자 지정 페이징을 구현 하는 것은 기본 페이징, 정렬 목록에 추가 하는 경우에 특히 구현 보다 훨씬 복잡 합니다. 이 자습서에서는 정렬에 대 한 지원을 포함 하도록 앞에서 예제를 확장 합니다 *및* 사용자 지정 페이징 합니다.

> [!NOTE]
> 시작 보십시오 선언적 구문 내에서 복사 되기 전에이 자습서에서는 이전 기반 하므로 `<asp:Content>` 이전 자습서의 웹 페이지에서 요소 (`EfficientPaging.aspx`) 간의 붙여넣습니다는 `<asp:Content>` 는 요소`SortParameter.aspx` 페이지. 단계 1을 다시 참조는 [편집 및 삽입 인터페이스에 유효성 검사 컨트롤 추가](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) 에 대 한 자세한 내용은 ASP.NET 페이지의 기능을 다른 복제 자습서입니다.


## <a name="step-1-reexamining-the-custom-paging-technique"></a>1 단계: 사용자 지정 페이징 기술을 다시 검토

제대로 작동 하려면 사용자 지정 페이징에 효율적으로 시작 하는 행 인덱스 및 최대 행 매개 변수를 지정 하는 레코드의 특정 하위를 얻을 수 있는 몇 가지 기법을 구현 해야 합니다. 이 목표를 달성 하기 위해 사용할 수 있는 기술의 몇 가지가 있습니다. 이 작업을 수행 하는 트 이전 자습서에서 사용 하 여 Microsoft SQL Server 2005 s 새 `ROW_NUMBER()` 순위 함수입니다. 즉,는 `ROW_NUMBER()` 지정 된 정렬 순서에 따라 순위를 지정 하는 쿼리에서 반환 된 각 행에 행 번호를 할당 순위 함수입니다. 그런 다음 레코드의 적절 한 하위 집합 번호가 매겨진된 결과의 특정 섹션을 반환 하 여 가져옵니다. 다음 쿼리는이 기술을 사용 하 여 기준으로 사전순으로 정렬 결과 순위를 지정 하는 경우 11 20-번호가 매겨진 해당 제품을 반환 하는 방법을 보여 줍니다는 `ProductName`:


[!code-sql[Main](sorting-custom-paged-data-vb/samples/sample1.sql)]

이 방법은 특정 정렬 순서를 사용 하 여 페이징 하는 데 적합 (`ProductName` 이 경우 사전순으로 정렬), 쿼리는 다른 정렬 식 별로 정렬 결과 표시 하도록 수정 해야 합니다. 이상적으로 위의 쿼리 다시 작성할 수 있습니다에 매개 변수를 사용 하는 `OVER` 절을 다음과 같이 합니다.


[!code-sql[Main](sorting-custom-paged-data-vb/samples/sample2.sql)]

매개 변수가 있는 반면 `ORDER BY` 절이 허용 되지 않습니다. 대신, 허용 하는 저장된 프로시저 만들어야는 `@sortExpression` 입력된 매개 변수는 있지만 경우 다음 방법 중 하나를 사용 하 합니다.

- 각; 사용할 수 있는 정렬 식에 대 한 하드 코딩 된 쿼리를 작성 합니다. 다음을 사용 하 여 `IF/ELSE` T-SQL 문을 실행할 쿼리를 결정 합니다.
- 사용 하 여 한 `CASE` 동적 제공 하는 문을 `ORDER BY` 식을 기반으로 `@sortExpressio` n 입력 매개 변수; 동적으로 쿼리 결과 정렬 섹션에 사용 된 참조 [SQL의 전원 `CASE` 문을](http://www.4guysfromrolla.com/webtech/102704-1.shtml) 자세한 내용은 합니다.
- 저장된 프로시저에서 문자열로 적절 한 쿼리를 작성할 하 고 사용 하 여 [는 `sp_executesql` 시스템 저장 프로시저](https://msdn.microsoft.com/library/ms188001.aspx) 동적 쿼리를 실행 합니다.

이러한 해결 방법을 각각의 몇 가지 단점이 있습니다. 첫 번째 옵션은 각 가능한 정렬 식에 대 한 쿼리를 만드는 해야 하므로 다른 두 가지로 유지 관리가 없습니다. 따라서 나중 GridView에 새, 정렬 가능한 필드를 추가 해야 합니다 되돌아가서 저장된 프로시저를 업데이트 합니다. 두 번째 방법은 첫 같은 유지 관리 문제에서 마찬가지로 것도 쉽지 문자열이 아닌 데이터베이스 열을 기준으로 정렬할 때 성능 문제를 소개 하는 몇 가지 미묘한에 있습니다. 고 동적 SQL을 사용 하는 세 번째 선택 공격자가 선택한 입력된 매개 변수 값에서 전달 저장된 프로시저를 실행할 수 있는 경우 SQL 삽입 공격에 대 한 위험을 도입 합니다.

이러한 방법 중 완벽 한 상태인 동안 세 개의 최상의 세 번째 옵션은 것 같습니다. 동적 SQL의 용도와 다른 두 없는 유연성 수준을 제공 합니다. 또한 SQL 삽입 공격은 공격자가 자신이 선택한 입력된 매개 변수를 전달 하는 저장된 프로시저를 실행할 수 있는 경우에 문제가 수 있습니다. DAL에서 매개 변수가 있는 쿼리를 사용 하는 이후 ADO.NET 의미 공격자가 저장된 프로시저를 직접 실행할 수 있는 경우 SQL 삽입 공격 취약점만 존재 하는 아키텍처를 통해 데이터베이스에 전송 되는 이러한 매개 변수 보호할 수 있습니다.

이 기능을 구현 하려면 라는 Northwind 데이터베이스에 새 저장된 프로시저를 만듭니다 `GetProductsPagedAndSorted`합니다. 이 저장된 프로시저에서 세 개의 입력 매개 변수를 허용 해야: `@sortExpression`, 형식의 입력된 매개 변수 `nvarchar(100`) 결과 정렬 해야 및 직후에 주입 방법을 지정 하는 `ORDER BY` 의 텍스트는 `OVER` 및절이없습니다.`@startRowIndex` 및 `@maximumRows`, 동일한 두 개의 정수 입력된 매개 변수에서의 `GetProductsPaged` 저장 프로시저 이전 자습서에서 검사 합니다. 만들기는 `GetProductsPagedAndSorted` 다음 스크립트를 사용 하 여 프로시저를 저장 합니다.


[!code-sql[Main](sorting-custom-paged-data-vb/samples/sample3.sql)]

저장된 프로시저에 대 한 값을 확인 하 여 시작 된 `@sortExpression` 매개 변수를 지정 합니다. 누락 된 경우 결과 순으로 순위가 지정 `ProductID`합니다. 다음으로, 동적 SQL 쿼리가 생성 됩니다. 참고 동적 SQL 쿼리를 여기 Products 테이블에서 모든 행을 검색 하는 데 사용 하 여 이전 쿼리에서 약간 다릅니다. 이전 예에서 얻 었 관련된 s 제품 범주별 s 및 공급 업체의 이름 하위 쿼리를 사용 합니다. 이 덕분에 되었습니다에서 [데이터 액세스 계층을 만들려면](../introduction/creating-a-data-access-layer-vb.md) 자습서 대신이 구성 요소를 사용 하 여 수행 되었습니다 및 `JOIN`의 TableAdapter에 연결 된 insert, 만들 자동으로 없기 때문에 업데이트 및 삭제 메서드 등에 대 한 쿼리 합니다. 그러나 `GetProductsPagedAndSorted` 저장된 프로시저를 사용 해야 `JOIN` 범주 또는 공급자 이름으로 배열 된 결과 대 한 합니다.

정적 쿼리 부분을 연결 하 여이 동적 쿼리 작성 및 `@sortExpression`, `@startRowIndex`, 및 `@maximumRows` 매개 변수입니다. 이후 `@startRowIndex` 및 `@maximumRows` 정수 매개 변수는 올바르게 연결 하기 위해 nvarchars로 변환 해야 합니다. 통해 실행 되 면이 동적 SQL 쿼리를 생성 `sp_executesql`합니다.

이 저장된 프로시저에 대 한 서로 다른 값으로 테스트 하는 `@sortExpression`, `@startRowIndex`, 및 `@maximumRows` 매개 변수입니다. 서버 탐색기에서 저장된 프로시저 이름을 마우스 오른쪽 단추로 클릭 하 고 실행을 선택 합니다. 그러면입니다 (그림 1 참조) 입력된 매개 변수 입력할 수 있는 저장 프로시저 실행 대화 상자를 표시 됩니다. 에 대 한 범주를 사용 하 여 범주 이름으로 결과 정렬 하는 `@sortExpression` ; CompanyName을 사용 하 여를 공급 업체의 회사 이름으로 정렬 하려면 매개 변수 값입니다. 매개 변수 값을 제공한 후 확인을 클릭 합니다. 결과 출력 창에 표시 됩니다. 그림 2 반환 제품 순위를 지정할 때 11 20-기준으로 정렬할 때 결과 표시는 `UnitPrice` 내림차순으로 정렬 합니다.


![저장된 프로시저 s 세 가지 입력된 매개 변수에 다른 값을 사용해 보십시오.](sorting-custom-paged-data-vb/_static/image1.png)

**그림 1**: s 3 개의 저장된 프로시저 입력 매개 변수에 대 한 다른 값을 사용 합니다.


[![저장 프로시저의 결과 출력 창에 표시 됩니다.](sorting-custom-paged-data-vb/_static/image3.png)](sorting-custom-paged-data-vb/_static/image2.png)

**그림 2**: s The 저장 프로시저 결과 출력 창에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-custom-paged-data-vb/_static/image4.png))


> [!NOTE]
> 결과에서 지정 된 순위 때 `ORDER BY` 열에는 `OVER` 절, SQL Server 결과 정렬 해야 합니다. 이것은 빠른 작업에서 결과 정렬 열 위에 클러스터형된 인덱스가 있으면 포함 된 경우 인덱스로 하지만 그렇지 않은 경우 비용이 많이 드는 될 수 있습니다. 충분히 큰 쿼리의 성능을 향상 시키기 위해 기준인 결과으로 정렬 열에 대 한 비클러스터형 인덱스를 추가 하는 것이 좋습니다. 참조 [순위 함수 및 SQL Server 2005의 성능](http://www.sql-server-performance.com/ak_ranking_functions.asp) 내용을 확인 합니다.


## <a name="step-2-augmenting-the-data-access-and-business-logic-layers"></a>2 단계: 데이터 액세스 및 비즈니스 논리 계층 확장

와 `GetProductsPagedAndSorted` 만든 저장된 프로시저, 다음 단계는이 응용 프로그램 아키텍처를 통해 해당 저장된 프로시저를 실행할 수 있도록 합니다. 이 수반 DAL 및 BLL에 적절 한 메서드를 추가 합니다. 에 dal과 메서드를 추가 하 여 시작 s를 사용 합니다. 열기는 `Northwind.xsd` 형식화 된 데이터 집합을 마우스 오른쪽 단추로 클릭은 `ProductsTableAdapter`, 상황에 맞는 메뉴에서 추가 쿼리 옵션을 선택 합니다. 이 새 DAL 방법을-기존 저장된 프로시저를 사용 하도록 구성 하려면 이전 자습서에서 수행한 것 처럼 `GetProductsPagedAndSorted`,이 경우. 기존 저장된 프로시저를 사용 하도록 새 TableAdapter 메서드를 지정 하 여 시작 합니다.


![기존 저장된 프로시저를 사용 하도록 선택](sorting-custom-paged-data-vb/_static/image5.png)

**그림 3**: 기존 저장된 프로시저를 사용 하도록 선택


사용 하도록 저장된 프로시저를 지정 하려면는 `GetProductsPagedAndSorted` 다음 화면에서 드롭 다운 목록에서 프로시저를 저장 합니다.


![GetProductsPagedAndSorted를 사용 하 여 저장 프로시저](sorting-custom-paged-data-vb/_static/image6.png)

**그림 4**:는 GetProductsPagedAndSorted를 사용 하 여 저장 프로시저


이 저장된 프로시저로 그 결과, 다음 화면에서 테이블 형식 데이터를 반환 하는지 레코드 집합을 반환 합니다.


![저장된 프로시저 테이블 형식 데이터를 반환 하는지 나타냅니다.](sorting-custom-paged-data-vb/_static/image7.png)

**그림 5**: 저장된 프로시저 테이블 형식 데이터를 반환 하는지 나타냅니다.


마지막으로, 두 채우기를 사용 하는 DAL 메서드 DataTable 만들고 반환 메서드 이름을 지정 하는 DataTable 패턴 `FillPagedAndSorted` 및 `GetProductsPagedAndSorted`각각.


![메서드 이름 선택](sorting-custom-paged-data-vb/_static/image8.png)

**그림 6**: 메서드 이름을 선택


해당 म 것은 사용 이제 했습니다 확장 DAL BLL를 설정 하려면 준비 된 것입니다. 열기는 `ProductsBLL` 클래스 파일을 새 메서드 추가 `GetProductsPagedAndSorted`합니다. 이 메서드를 세 개의 입력 매개 변수를 허용 해야 합니다. `sortExpression`, `startRowIndex`, 및 `maximumRows` DAL s에 호출 해야 하 고 `GetProductsPagedAndSorted` 메서드를 다음과 같이:


[!code-vb[Main](sorting-custom-paged-data-vb/samples/sample4.vb)]

## <a name="step-3-configuring-the-objectdatasource-to-pass-in-the-sortexpression-parameter"></a>3 단계: SortExpression 매개 변수에서 단계에 ObjectDataSource 구성

DAL 및 BLL 활용 하는 메서드를 포함 하도록 확장할 필요는 `GetProductsPagedAndSorted` 상태를 유지 하는 모든 저장된 프로시저에서 ObjectDataSource를 구성 하는 것은 `SortParameter.aspx` 페이지 새 BLL 메서드를 사용 하 고 전달 하는 `SortExpression` 매개 변수를 기반으로 사용자가 요청 하 여 결과 정렬 하는 열입니다.

ObjectDataSource s 변경 하 여 시작 `SelectMethod` 에서 `GetProductsPaged` 를 `GetProductsPagedAndSorted`합니다. 속성 창에서 데이터 소스 구성 마법사를 통해 또는 직접 선언 구문을 통해 수행할 수 있습니다. 다음으로, ObjectDataSource s에 대 한 값을 제공 해야 [ `SortParameterName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sortparametername.aspx)합니다. ObjectDataSource GridView s에 전달 하려고 시도할 경우이 속성이 설정 되어 `SortExpression` 속성을는 `SelectMethod`합니다. 특히,는 ObjectDataSource 이름인의 값과 같은 입력된 매개 변수를 찾습니다는 `SortParameterName` 속성입니다. BLL s 이후 `GetProductsPagedAndSorted` 메서드에 정렬 식 라는 입력된 매개 변수는 `sortExpression`, ObjectDataSource s 설정 `SortExpression` 속성 sortExpression 합니다.

이러한 두 가지 변경에 확인 한 후 ObjectDataSource s 선언적 구문 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](sorting-custom-paged-data-vb/samples/sample5.aspx)]

> [!NOTE]
> 이전 자습서와 함께 ObjectDataSource가 있는지를 확인 하는 대로 *하지* SelectParameters 컬렉션에서 sortExpression, startRowIndex, 또는 maximumRows 입력된 매개 변수를 포함 합니다.


GridView에서 정렬 기능을 사용 하면 확인란을 정렬 사용 GridView s 스마트 태그를 설정 하는 GridView s `AllowSorting` 속성을 `true` 못하여 LinkButton로 렌더링을 각 열에 대 한 헤더 텍스트입니다. 링크 단추가 헤더 중 하나에서 최종 사용자가 포스트백 계속 하 고 다음 단계 동안 실행 합니다.

1. GridView 업데이트 해당 [ `SortExpression` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx) 의 값에는 `SortExpression` 헤더 링크 클릭 필드의
2. ObjectDataSource BLL s 호출 `GetProductsPagedAndSorted` GridView s 전달 메서드를 `SortExpression` s 메서드에 대 한 값으로 속성 `sortExpression` 입력된 매개 변수 (적절 한 함께 `startRowIndex` 및 `maximumRows` 입력 매개 변수 값)
3. BLL DAL s 호출 `GetProductsPagedAndSorted` 메서드
4. DAL 실행는 `GetProductsPagedAndSorted` 저장 프로시저를 시작 전달에 `@sortExpression` 매개 변수 (함께 `@startRowIndex` 및 `@maximumRows` 입력 매개 변수 값)
5. 저장된 프로시저가 있는 bll ObjectDataSource; 게 반환 하는 데이터의 적절 한 하위 집합 반환 이 데이터는 GridView에 바인딩될, HTML로 렌더링 되는 되어 최종 사용자에 게 전송

그림 7 나와 기준으로 정렬 된 결과의 첫 번째 페이지는 `UnitPrice` 오름차순입니다.


[![UnitPrice 하 여 결과 정렬](sorting-custom-paged-data-vb/_static/image10.png)](sorting-custom-paged-data-vb/_static/image9.png)

**그림 7**: The 결과 UnitPrice로 정렬 됩니다 ([전체 크기 이미지를 보려면 클릭](sorting-custom-paged-data-vb/_static/image11.png))


현재 구현에서는 제품 이름, 범주 이름, 단위 테스트 및 단가 당 수량을 기준으로 결과 제대로 정렬 수, 하는 동안 런타임 예외가 이름 결과 공급자가 결과 정렬 하려고 (그림 8 참조).


![다음 런타임 예외에서 공급자 결과에서 결과 정렬 하려고 합니다.](sorting-custom-paged-data-vb/_static/image12.png)

**그림 8**: 결과 다음 런타임 예외에서 공급자 결과를 정렬 하려고 합니다.


이 예외가 발생 하기 때문에 `SortExpression` GridView s `SupplierName` BoundField로 설정 된 `SupplierName`합니다. 그러나 이름을 s 공급 업체에서는 `Suppliers` 테이블 실제로 호출 `CompanyName` 별칭으로이 열 이름은 했습니다 `SupplierName`합니다. 그러나는 `OVER` 절에서 사용 하는 `ROW_NUMBER()` 함수 별칭을 사용할 수 없습니다 및 실제 열 이름을 사용 해야 합니다. 따라서 변경는 `SupplierName` BoundField의 `SortExpression` 에서 CompanyName에 공급 업체 이름 (그림 9 참조). 그림 10과 같이 공급자가이 변경 후 결과 정렬할 수 있습니다.


![공급 업체 이름 BoundField의 SortExpression CompanyName을 변경](sorting-custom-paged-data-vb/_static/image13.png)

**그림 9**: 공급 업체 이름 BoundField의 SortExpression CompanyName을 변경


[![공급자를 통해 결과 정렬 이제 수 있습니다.](sorting-custom-paged-data-vb/_static/image15.png)](sorting-custom-paged-data-vb/_static/image14.png)

**그림 10**: The 결과 수 이제 기준으로 정렬할 수 공급 업체 ([전체 크기 이미지를 보려면 클릭](sorting-custom-paged-data-vb/_static/image16.png))


## <a name="summary"></a>요약

이전 자습서에서 검사 했습니다 사용자 지정 페이징 구현 기준인 결과가 정렬 순서 디자인 타임에 지정할 수 필요 합니다. 즉,이 구현한 사용자 지정 페이징 구현을 제공할 수 없습니다, 같은 시간에 정렬 기능 의미 합니다. 이 자습서에서는 극복 했습니다이 제한을 포함 하 여 첫 번째 범위에서 저장된 프로시저를 확장 하 여 한 `@sortExpression` 결과 수 정렬 기준이 되는 입력된 매개 변수입니다.

이 만들면 저장 프로시저 및 DAL 및 BLL에 새 메서드를 만들고, 후 अ स म र 모두 정렬 제공 되는 GridView를 구현할 수 및 페이징 ObjectDataSource 현재 GridView s에 전달 하도록 구성 하 여 사용자 지정 `SortExpression` BLL 속성 `SelectMethod`.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Carlos Santos 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

>[!div class="step-by-step"]
[이전](efficiently-paging-through-large-amounts-of-data-vb.md)
[다음](creating-a-customized-sorting-user-interface-vb.md)
