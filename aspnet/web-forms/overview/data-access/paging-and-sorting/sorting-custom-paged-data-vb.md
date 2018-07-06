---
uid: web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-vb
title: 페이징 (VB) 데이터 사용자 지정 정렬 | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서 웹 페이지에서 데이터를 presentating 때 사용자 지정 페이징을 구현 하는 방법을 알게 되었습니다. 이 자습서에서는 이전 확장 하는 방법을 표시 하는 중...
ms.author: aspnetcontent
ms.date: 08/15/2006
ms.assetid: 4823a186-caaf-4116-a318-c7ff4d955ddc
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 7a660f697676e20d8987af150b10fc6694ce7c57
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37805316"
---
<a name="sorting-custom-paged-data-vb"></a>사용자 지정 페이징 정렬 데이터 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_26_VB.exe) 또는 [PDF 다운로드](sorting-custom-paged-data-vb/_static/datatutorial26vb1.pdf)

> 이전 자습서에서 웹 페이지에서 데이터를 presentating 때 사용자 지정 페이징을 구현 하는 방법을 알게 되었습니다. 이 자습서 정렬 사용자 지정 페이징 지원을 포함 하도록 앞의 예제를 확장 하는 방법을 볼 수 있습니다.


## <a name="introduction"></a>소개

기본 페이징에 비해 몇 배 많은 규모로, 많은 양의 데이터를 페이징할 때는 사실상 페이징 구현 선택에 페이징 하는 사용자 지정 하 여 사용자 지정 페이징 데이터의 페이징의 성능을 향상 시킬 수 있습니다. 그러나 사용자 지정 페이징을 구현 하는 것은 기본 페이징 정렬 목록에 추가 하는 경우에 특히 구현 보다 더 복잡 합니다. 이 자습서에서는 정렬에 대 한 지원을 포함 하도록 앞에서 예제 확장할 예정 *고* 사용자 지정 페이징 합니다.

> [!NOTE]
> 시작 부분에서 선언적 구문을 복사할 잠시 전에이 자습서 이전 기반 이므로 합니다 `<asp:Content>` 이전 자습서가의 웹 페이지에서 요소 (`EfficientPaging.aspx`) 사이의 붙여넣습니다는 `<asp:Content>` 요소에는 `SortParameter.aspx` 페이지. 1 단계를 다시 참조를 [편집 및 삽입 인터페이스에 유효성 검사 컨트롤 추가](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) 다른 하나의 ASP.NET 페이지의 기능을 복제에 대 한 자세한 논의 자습서입니다.


## <a name="step-1-reexamining-the-custom-paging-technique"></a>1 단계: 사용자 지정 페이징 기술을 다시 검토

사용자 지정 페이징이 제대로 작동 하려면에서는 시작 하는 행 인덱스 및 최대 행 매개 변수를 지정 하는 레코드의 특정 하위 집합을 효율적으로 나옵니다는 몇 가지 기법을 구현 해야 합니다. 이 목표를 달성 하기 위해 사용할 수 있는 기술의 몇 가지 있습니다. 이 작업을 수행 살펴보았습니다 이전 자습서에서 사용 하 여 Microsoft SQL Server 2005가 새 `ROW_NUMBER()` 순위 함수입니다. 즉,는 `ROW_NUMBER()` 행 번호를 지정 된 정렬 순서에 따라 순위가 지정 되는 쿼리가 반환한 각 행에 할당 순위 함수입니다. 그런 다음 적절 한 레코드 하위 집합 번호가 매겨진된 결과의 특정 섹션을 반환 하 여 가져옵니다. 다음 쿼리는이 기술을 사용 하 여 결과 순위에 따라 사전순으로 정렬 하는 경우 11부터 20까지 번호가 매겨진 해당 제품을 반환 하는 방법을 보여 줍니다는 `ProductName`:


[!code-sql[Main](sorting-custom-paged-data-vb/samples/sample1.sql)]

이 기술은 특정 정렬 순서를 사용 하 여 페이징 적합 (`ProductName` 이 경우 사전순으로 정렬), 쿼리를 다른 정렬 식을 사용 하 여 정렬 된 결과 표시 하도록 수정 해야 합니다. 하지만 합니다. 이상적으로 위의 쿼리 다시 작성할 수 있습니다의 매개 변수를 사용 하는 `OVER` 절을 다음과 같이 합니다.


[!code-sql[Main](sorting-custom-paged-data-vb/samples/sample2.sql)]

그러나 매개 변수가 있는 `ORDER BY` 절이 허용 되지 않습니다. 대신 허용 하는 저장된 프로시저를 만들어야 합니다를 `@sortExpression` 입력된 매개 변수 이지만 다음 해결 방법 중 하나를 사용 합니다.

- 각; 사용할 수 있는 정렬 식에 대 한 하드 코드 된 쿼리를 작성 합니다. 사용 하 여 `IF/ELSE` T-SQL 문을 실행 하는 쿼리를 확인 합니다.
- 사용 하 여는 `CASE` 동적 제공 하는 문을 `ORDER BY` 식을 기반으로 합니다 `@sortExpressio` n 입력 매개 변수에서 동적으로 쿼리 결과 정렬 절을 사용을 참조 하십시오 [SQL의 Power `CASE` 문을](http://www.4guysfromrolla.com/webtech/102704-1.shtml) 자세한 내용은 합니다.
- 저장된 프로시저에 문자열로 적절 한 쿼리를 작성 하 고 사용 하 여 [는 `sp_executesql` 시스템 저장 프로시저](https://msdn.microsoft.com/library/ms188001.aspx) 동적 쿼리를 실행 합니다.

이러한 해결 방법을 각각의 몇 가지 단점이 있습니다. 첫 번째 옵션은 각 가능한 정렬 식에 대 한 쿼리를 만든 필요 하므로 다른 두도 유지 관리가 아닙니다. 따라서 나중에 GridView에 새, 정렬 가능 필드를 추가 하려는 경우 해야 돌아가서 저장된 프로시저를 업데이트 합니다. 두 번째 방법은 문자열이 아닌 데이터베이스 열을 기준으로 정렬 하는 경우 성능 문제를 소개 하 고 또한 첫 번째와 동일한 유지 관리 문제에서 발생 하는 몇 가지 미묘한 측면 들에 있습니다. 고 동적 SQL을 사용 하는 세 번째 선택 사항은 공격자가 자신이 선택한 입력된 매개 변수 값 전달 저장된 프로시저를 실행할 수 있는 경우 SQL 삽입 공격에 대 한 위험을 소개 합니다.

이러한 방법 중 완벽 한 상태인 동안 세 번째 옵션은 세 가지는 것이 생각 합니다. 동적 SQL의 용도 사용 하 여 다른 두 하지 유연성 수준을 제공 합니다. 또한 SQL 삽입 공격만 경우 이용할 수 있습니다는 공격자가 자신이 선택한 입력된 매개 변수에 전달 저장된 프로시저를 실행할 수 있습니다. 매개 변수가 있는 쿼리를 사용 하는 DAL을 하므로 ADO.NET는 SQL 삽입 공격 취약성 공격자가 저장된 프로시저를 직접 실행할 수 있는 경우에 존재 하므로 아키텍처를 통해 데이터베이스에 전송 되는 이러한 매개 변수 보호할 수 있습니다.

이 기능을 구현 하려면 명명 된 Northwind 데이터베이스에 새 저장된 프로시저를 만들 `GetProductsPagedAndSorted`합니다. 이 저장된 프로시저에서 세 개의 입력 매개 변수를 수락 해야: `@sortExpression`, 형식의 입력된 매개 변수 `nvarchar(100`) 결과 정렬 해야와 바로 뒤에 삽입 됩니다 하는 방법을 지정 하는 합니다 `ORDER BY` 에서 텍스트를 `OVER` 절 및 `@startRowIndex` 하 고 `@maximumRows`, 동일한 두 개의 정수 입력된 매개 변수를는 `GetProductsPaged` 저장 프로시저는 이전 자습서에서 검사 합니다. 만들기는 `GetProductsPagedAndSorted` 다음 스크립트를 사용 하 여 프로시저를 저장 합니다.


[!code-sql[Main](sorting-custom-paged-data-vb/samples/sample3.sql)]

저장된 프로시저에 대 한 값을 확인 하 여 시작 된 `@sortExpression` 매개 변수를 지정 합니다. 누락 된 경우 결과 순으로 순위가 지정 `ProductID`합니다. 다음으로, 동적 SQL 쿼리가 생성 됩니다. 동적 SQL 쿼리를 여기 Products 테이블에서 모든 행을 검색 하는 데 사용 되는 이전 쿼리에서 약간 다른 것을 참고 합니다. 이전 예제에서 얻은 연결된 s 제품 범주별 하위 쿼리를 사용 하 여 공급 업체 및 s 이름입니다. 년대 결정 했지만이 [데이터 액세스 레이어 만들기](../introduction/creating-a-data-access-layer-vb.md) 자습서를 사용 하는 대신 수행 된 `JOIN`의 TableAdapter 연결된 삽입을 자동으로 만들 수 없습니다 때문에 업데이트 및 이러한 메서드를 삭제 쿼리 합니다. 그러나 합니다 `GetProductsPagedAndSorted` 저장된 프로시저를 사용 해야 합니다 `JOIN` 범주 또는 공급 업체 이름을 기준으로 정렬할 결과 대 한 합니다.

정적 쿼리 부분을 연결 하 여이 동적 쿼리 작성 하며 `@sortExpression`, `@startRowIndex`, 및 `@maximumRows` 매개 변수입니다. 이후 `@startRowIndex` 및 `@maximumRows` 정수 매개 변수가 올바르게 연결 하기 위해 nvarchars로 변환 해야 합니다. 통해 실행 되 면이 동적 SQL 쿼리를 생성 `sp_executesql`합니다.

잠시 다른 값이 저장된 프로시저를 테스트 하는 `@sortExpression`, `@startRowIndex`, 및 `@maximumRows` 매개 변수입니다. 서버 탐색기에서 저장된 프로시저 이름을 마우스 오른쪽 단추로 클릭 하 고 실행을 선택 합니다. (그림 1 참조) 입력된 매개 변수를 입력할 수는 저장 프로시저 실행 대화 상자를 표시 됩니다. 범주 이름으로 결과 정렬 하려면에 대 한 범주를 사용 하 여는 `@sortExpression` 공급자의 회사 이름을 기준으로 정렬 하려면 CompanyName을 사용 하 여 매개 변수 값입니다. 매개 변수 값을 입력 한 후 확인을 클릭 합니다. 결과 출력 창에 표시 됩니다. 그림 2 기준으로 정렬할 때 11 ~ 20 순위 제품을 반환 하는 경우 결과 보여 줍니다는 `UnitPrice` 내림차순으로 정렬 합니다.


![저장된 프로시저 s 세 개의 입력 매개 변수에 다른 값을 사용해 보십시오.](sorting-custom-paged-data-vb/_static/image1.png)

**그림 1**:가 세 개의 저장된 프로시저 입력 매개 변수 값이 다른 시도


[![저장 프로시저의 결과 출력 창에 표시 됩니다.](sorting-custom-paged-data-vb/_static/image3.png)](sorting-custom-paged-data-vb/_static/image2.png)

**그림 2**: 저장 프로시저는 s 결과 출력 창에 표시 됩니다 ([큰 이미지를 보려면 클릭](sorting-custom-paged-data-vb/_static/image4.png))


> [!NOTE]
> 지정 된 결과 순위 지정 하는 경우 `ORDER BY` 열에는 `OVER` 절을 SQL Server에서 결과 정렬 해야 합니다. 이 결과 정렬할 열 위에 클러스터형 인덱스가 있는 경우 빠른 작업을 다루는 경우 인덱스를 하지만 그렇지 않은 경우 더 높은 비용이 들 수 있습니다. 충분히 큰 쿼리에 대 한 성능 향상을 위해 사용 되는 결과으로 정렬 열에 대 한 비클러스터형 인덱스를 추가 하는 것이 좋습니다. 가리킵니다 [SQL Server 2005의 성능과 순위 함수](http://www.sql-server-performance.com/ak_ranking_functions.asp) 대 한 자세한 내용은 합니다.


## <a name="step-2-augmenting-the-data-access-and-business-logic-layers"></a>2 단계: 데이터 액세스 및 비즈니스 논리 계층 확대

사용 하 여는 `GetProductsPagedAndSorted` 만든 저장된 프로시저를 다음 단계는 응용 프로그램 아키텍처를 통해 해당 저장된 프로시저를 실행 하는 수단을 제공 합니다. 이 BLL 및 DAL에 적절 한 메서드를 추가 해야 합니다. S를 DAL에 메서드를 추가 하 여 시작할 수 있습니다. 열기는 `Northwind.xsd` 형식화 된 데이터 집합을 마우스 오른쪽 단추로 클릭은 `ProductsTableAdapter`, 상황에 맞는 메뉴에서 추가 쿼리 옵션을 선택 합니다. 이 새 DAL 방법-기존 저장된 프로시저를 사용 하 여를 구성 하려면 이전 자습서에서 했던 것 처럼 `GetProductsPagedAndSorted`,이 경우. 기존 저장된 프로시저를 사용 하 여 새 TableAdapter 메서드를 클릭 하 여 시작 합니다.


![기존 저장된 프로시저를 사용 하도록 선택](sorting-custom-paged-data-vb/_static/image5.png)

**그림 3**: 기존 저장된 프로시저를 사용 하도록 선택


사용 하도록 저장된 프로시저를 지정 하려면 선택 합니다 `GetProductsPagedAndSorted` 다음 화면에서 드롭 다운 목록에서 프로시저를 저장 합니다.


![GetProductsPagedAndSorted를 사용 하 여 저장 프로시저](sorting-custom-paged-data-vb/_static/image6.png)

**그림 4**: GetProductsPagedAndSorted를 사용 하 여 저장 프로시저


이 저장된 프로시저 결과 다음 화면에서 나타내는 표 형식 데이터를 반환 레코드 집합을 반환 합니다.


![저장된 프로시저가 반환 테이블 형식 데이터를 나타냅니다.](sorting-custom-paged-data-vb/_static/image7.png)

**그림 5**: 저장된 프로시저가 반환 테이블 형식 데이터를 나타냅니다.


마지막으로 두는 채우기를 사용 하는 DAL 메서드 DataTable 만들고 메서드 명명 DataTable 패턴을 반환 `FillPagedAndSorted` 고 `GetProductsPagedAndSorted`, 각각.


![메서드 이름을 선택 합니다.](sorting-custom-paged-data-vb/_static/image8.png)

**그림 6**: 메서드 이름을 선택 합니다.


이제는 우리 ve 확장 DAL BLL을 설정 하려면 준비 된 것입니다. 엽니다는 `ProductsBLL` 클래스 파일 및 새 메서드를 추가 `GetProductsPagedAndSorted`합니다. 이 메서드를 세 개의 입력 매개 변수를 수락 해야 합니다. `sortExpression`, `startRowIndex`, 및 `maximumRows` DAL s에 호출 해야 하 고 `GetProductsPagedAndSorted` 메서드를 다음과 같이 합니다.


[!code-vb[Main](sorting-custom-paged-data-vb/samples/sample4.vb)]

## <a name="step-3-configuring-the-objectdatasource-to-pass-in-the-sortexpression-parameter"></a>3 단계: SortExpression 매개 변수에 전달 하는 ObjectDataSource 구성

DAL 및 BLL을 활용 하는 메서드를 포함 하도록 확장할 필요는 `GetProductsPagedAndSorted` 유지 하는 모든 저장된 프로시저에서 ObjectDataSource를 구성 하는 것을 `SortParameter.aspx` 페이지 전달 하 고 새 BLL 메서드를 사용 하는 `SortExpression` 매개 변수를 기반를 사용자가 요청 하 여 결과 정렬 하는 열입니다.

ObjectDataSource가 변경 하 여 시작 `SelectMethod` 에서 `GetProductsPaged` 에 `GetProductsPagedAndSorted`입니다. 속성 창에서 데이터 소스 구성 마법사를 통해 선언적 구문을 통해 직접 수행할 수 있습니다. 다음으로 ObjectDataSource s에 대 한 값을 제공 해야 [ `SortParameterName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sortparametername.aspx)합니다. 이 속성을 설정 하는 경우 ObjectDataSource GridView에서 전달 하려고 시도 `SortExpression` 속성을는 `SelectMethod`합니다. 특히 입력된 매개 변수 값으로 이름이 같은지 ObjectDataSource 찾습니다는 `SortParameterName` 속성입니다. BLL s 이후 `GetProductsPagedAndSorted` 메서드는 정렬 식 입력된 된 매개 변수 `sortExpression`, 집합 ObjectDataSource의 `SortExpression` 속성 sortExpression 합니다.

구성을 변경한 후 이러한 두 ObjectDataSource가 선언적 구문을 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](sorting-custom-paged-data-vb/samples/sample5.aspx)]

> [!NOTE]
> 이전 자습서를 사용 하 여 ObjectDataSource에 있는지를 확인 *되지* SelectParameters 컬렉션 sortExpression, startRowIndex, 또는 maximumRows 입력된 매개 변수를 포함 합니다.


GridView에서 정렬 기능을 사용 GridView가 스마트 태그를 GridView s (으)로 설정 하는 정렬 사용 확인란을 단순히 확인 `AllowSorting` 속성을 `true` LinkButton으로 렌더링 하도록 각 열에 대 한 헤더 텍스트를 발생 합니다. Linkbutton 헤더 중 하나에서 최종 사용자가 포스트백 근거가 하 고 다음 단계를 지정 전까지 대기 합니다.

1. GridView 업데이트를 해당 [ `SortExpression` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx) 의 값에는 `SortExpression` 인 헤더 링크를 클릭 한 필드의
2. BLL s를 호출 하는 ObjectDataSource `GetProductsPagedAndSorted` GridView가 전달 하는 메서드 `SortExpression` s 메서드에 대 한 값으로 속성 `sortExpression` 입력된 매개 변수 (적절 한 함께 `startRowIndex` 및 `maximumRows` 입력 매개 변수 값)
3. BLL은 DAL s 호출 `GetProductsPagedAndSorted` 메서드
4. DAL 실행를 `GetProductsPagedAndSorted` 저장 프로시저에 전달 합니다 `@sortExpression` 매개 변수 (함께 `@startRowIndex` 및 `@maximumRows` 입력 매개 변수 값)
5. 저장된 프로시저 ObjectDataSource;를 반환 하는 BLL에 적절 한 데이터 하위 집합을 반환 합니다. 이 데이터를 GridView에 바인딩된를 HTML로 렌더링 되어 최종 사용자에 게 전송

그림 7은 기준으로 정렬 된 결과의 첫 페이지는 `UnitPrice` 오름차순으로 정렬 합니다.


[![UnitPrice 하 여 결과 정렬](sorting-custom-paged-data-vb/_static/image10.png)](sorting-custom-paged-data-vb/_static/image9.png)

**그림 7**: 결과 UnitPrice로 정렬 됩니다 ([큰 이미지를 보려면 클릭](sorting-custom-paged-data-vb/_static/image11.png))


현재 구현에는 제품 이름, 범주 이름, 수량 단위 및 단가 당 결과 정렬할 수 올바르게, 하는 동안 런타임 예외가 이름 결과 공급자가 결과 정렬 하려고 (그림 8 참조).


![다음 런타임 예외에서 공급자 결과 기준으로 결과 정렬 하려고 합니다.](sorting-custom-paged-data-vb/_static/image12.png)

**그림 8**: 다음 런타임 예외에서 공급자 결과 기준으로 결과 정렬 하려고 합니다.


때문에이 예외가 발생 합니다 `SortExpression` GridView s `SupplierName` BoundField로 설정 된 `SupplierName`합니다. 그러나 s 공급자 이름에 `Suppliers` 테이블은 실제로 호출 `CompanyName` 없어졌으며 별칭으로이 열 이름은 `SupplierName`합니다. 그러나 합니다 `OVER` 절에서 사용 하는 `ROW_NUMBER()` 함수 별칭을 사용할 수 없습니다 및 실제 열 이름을 사용 해야 합니다. 따라서 변경 합니다 `SupplierName` BoundField의 `SortExpression` 에서 CompanyName 공급 업체 이름 (그림 9 참조). 그림 10에서 알 수 있듯이, 공급자가 이렇게이 변경한 후 결과 정렬할 수 있습니다.


![공급 업체 이름 BoundField의 SortExpression CompanyName 변경](sorting-custom-paged-data-vb/_static/image13.png)

**그림 9**: 공급 업체 이름 BoundField의 SortExpression CompanyName 변경


[![공급 업체에서 결과 정렬할 수 있습니다.](sorting-custom-paged-data-vb/_static/image15.png)](sorting-custom-paged-data-vb/_static/image14.png)

**그림 10**: The 결과 이제 정렬할 수 있습니다 공급자 ([큰 이미지를 보려면 클릭](sorting-custom-paged-data-vb/_static/image16.png))


## <a name="summary"></a>요약

이전 자습서에서 검사할 사용자 지정 페이징을 구현 되는 결과가 정렬 순서 디자인 타임에 지정할 수는 필요 합니다. 즉,이 구현에서는 사용자 지정 페이징 구현을 제공할 수 없습니다, 동시에 정렬 기능 의미 합니다. 이 제한을 포함 하는 첫 번째에서 저장된 프로시저를 확장 하 여 여러에서는이 자습서는 `@sortExpression` 입력된 매개 변수는 결과 정렬 수 없습니다.

모두 정렬 제공 되는 GridView를 구현 하는 일을 할 및 페이징 전달할 GridView에서 현재 ObjectDataSource를 구성 하 여 사용자 지정 된 후이 만드는 저장 프로시저 및 BLL 및 DAL에서 새 메서드를 만들고, `SortExpression` BLL 속성 `SelectMethod`.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Carlos Santos 했습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](efficiently-paging-through-large-amounts-of-data-vb.md)
> [다음](creating-a-customized-sorting-user-interface-vb.md)
