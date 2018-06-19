---
uid: web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb
title: 효율적으로 많은 양의 데이터 (VB)를 통한 페이징을 | Microsoft Docs
author: rick-anderson
description: 많은 양의 데이터에 해당 기본 데이터 소스 제어 retriev 작업할 때는 데이터 프레젠테이션 컨트롤의 기본 페이징 옵션은 적합 없습니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/15/2006
ms.topic: article
ms.assetid: 3e20e64a-8808-4b49-88d6-014e2629d56f
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 00057f9bfd9b1c479e500ac591db694388a5d358
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30890699"
---
<a name="efficiently-paging-through-large-amounts-of-data-vb"></a>효율적으로 많은 양의 데이터 (VB)를 통해 페이징
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_25_VB.exe) 또는 [PDF 다운로드](efficiently-paging-through-large-amounts-of-data-vb/_static/datatutorial25vb1.pdf)

> 데이터 프레젠테이션 컨트롤의 기본 페이징 옵션이 아닙니다 적합 한 많은 양의 데이터를 작업할 때의 기본 데이터 소스 제어 데이터의 하위 집합만 표시 되는 경우에 모든 레코드를 검색 합니다. 이 경우 사용자 지정으로 설정 해야 페이징 합니다.


## <a name="introduction"></a>소개

이전 자습서에서 설명한 두 가지 방법 중 하나에서 페이징을 구현할 수 있습니다.

- **기본 페이징** 단순히 페이징 사용 옵션을 확인 하 여 구현할 수 데이터의 웹 컨트롤에서 스마트 태그; 그러나 데이터 페이지를 볼 때마다는 ObjectDataSource 검색 *모든* 레코드에 페이지에만 이들의 하위 집합은 표시 되지만
- **그러나 사용자 지정 페이징** 기본의 성능 향상 됩니다. 사용자가 요청한 데이터의 특정 페이지에 대 한 표시 되어야 하는 데이터베이스에서 해당 레코드에만 검색 하 여 페이징 사용자 지정 페이징 포함 구현 하는 좀 더 많은 노력이 기본 페이징보다

구현 검사 checkbox 및 된의 용이성 때문에 완료 되었습니다. 기본 페이징 매력적인 옵션입니다. 해당 na 했습니다 접근 방식 모든 레코드를 검색 하지만에서는 두고 선택 하는 여러 동시 사용자가 있는 충분히 대용량 데이터 또는 사이트에 대 한 페이징 하는 경우. 이 경우 페이징 응답 시스템을 제공 하기 위해 사용자 지정으로 설정 해야 합니다.

사용자 지정 페이징 하는 문제 레코드 데이터의 특정 페이지에 필요한 정확한 집합을 반환 하는 쿼리를 작성할 수 있다는 점입니다. 다행히 Microsoft SQL Server 2005 제공 하는 새로운 키워드 순위 결과 얻으려면는 레코드의 적절 한 하위 집합을 효율적으로 검색할 수 있는 쿼리를 작성할 수 있습니다. 이 자습서에서는이 새 SQL Server 2005 키워드를 사용 하 여 GridView 컨트롤에서 사용자 지정 페이징을 구현 하는 방법을 살펴보겠습니다. 사용자 지정 페이징에 대 한 사용자 인터페이스는 다음 사용 하 여 한 페이지에서 한 단계씩 실행 하는 기본 페이징에 동일 하는 동안 사용자 지정 페이징 몇 배 기본 페이징보다 더 빠르게 수 있습니다.

> [!NOTE]
> 사용자 지정 페이징을 수행 하는 정확한 성능 향상을 통해 호출이 전달 하는 레코드 또는 데이터베이스 서버에 적용 되 고 부하의 총 수에 따라 다릅니다. 이 자습서의 끝에 사용자 지정 페이징을 통해 가져온 성능에서 이점을 보여 주는 몇 가지 대략적인 메트릭을 살펴보겠습니다.


## <a name="step-1-understanding-the-custom-paging-process"></a>1 단계: 사용자 지정 페이징 프로세스 이해

데이터를 페이징 하는 경우 페이지에 표시 된 정확한 레코드 요청 되는 데이터 페이지와 페이지당 표시 되는 레코드의 수에 따라 달라 집니다. 예를 들어 하 려 81 제품 페이징할 페이지당 10 개의 제품이 표시 한다고 가정 합니다. 첫 번째 페이지를 볼 때 d 원하는 제품 1부터 10; 두 번째 페이지를 볼 때 d에서는 제품 11부터 20 관심이 있을 수 있습니다.

검색 해야 하는 레코드 및 페이징 인터페이스 렌더링 되는 방식을 지정 하는 세 개의 변수 가지가 있습니다.

- **행 인덱스 이며 시작** 표시할 데이터를 페이지에 있는 첫 번째 행의 인덱스 이거나, 인덱스 페이지 인덱스를 한 페이지에 표시할 레코드 곱한 하나를 추가 하 여 계산할 수 있습니다. 예를 들어 첫 번째 페이지 (페이지 인덱스는 0 임)에 대해 한 번에 10 레코드를 페이징 하는 경우 시작 행 인덱스는 0 \* 10 + 1 또는 1;에 대 한 두 번째 페이지 (페이지의 인덱스는 1)를 시작 하는 행 인덱스는 1 \* 10 + 1 또는 11.
- **최대 행** 한 페이지에 표시할 레코드의 최대 수입니다. 이 변수는 마지막에 대 한 페이지 반환 페이지 크기 보다 적은 수의 레코드가 될 수 있으므로 최대 행 라고 합니다. 예를 들어 페이지당 10 81 제품 레코드를 통해 페이징, 실행 시 아홉 번째 및 마지막 페이지에 레코드를 하나만 갖습니다. 그러나 페이지가 없습니다. 최대 행 수 값 보다 더 많은 레코드를 표시 됩니다.
- **총 레코드 수** 통해 호출이 전달 하는 레코드의 총 수입니다. 지정된 된 페이지에 대 한 검색 레코드를 결정 하는 데 필요한이 변수 큰 t, 동안 페이징 인터페이스에서 지정 합니다. 예를 들어를 통해 페이징 되 81 제품 인 페이징 인터페이스 페이징 UI에에서 9 개의 페이지 번호를 표시 하려면 알고 있습니다.

기본 페이징을 사용 하 여 시작 하는 행 인덱스는 최대 행 수는 단순히 페이지 크기는 페이지 인덱스 및 페이지 크기에 1을 더한의 곱으로 계산 됩니다. 모든 레코드를 검색 하 여 기본 페이징 이후 데이터를 각 행에 대 한 인덱스의 페이지를 렌더링 하는 경우 데이터베이스 라고 받으므로 사소한 작업이 시작 하는 행 인덱스 행으로 이동 합니다. 총 레코드 수를 그대로 손쉽게 사용할 수 또한 s DataTable (또는 어떤 개체가 사용 되는 데이터베이스의 결과를 저장할)에 있는 레코드의 수에 단순히 합니다.

사용자 지정 페이징 구현을 시작 하는 행 인덱스 및 최대 행 수 변수를 지정 하에서 시작 하는 행 인덱스 및 레코드의 최대 행 수 까지의 그 후에 시작 하는 레코드의 정확한 하위 집합을만 반환 해야 합니다. 사용자 지정 페이징에는 두 가지 문제를 제공합니다.

- 지정된 된 시작 행 인덱스에 있는 레코드를 반환을 시작할 수 있도록를 통해 페이징 되 전체 데이터의 각 행과 행 인덱스를 효율적으로 연결할 있어야
- 통해 호출이 전달 하는 레코드의 총 수를 제공 해야

다음 두 단계에서 이러한 두 가지 문제에 응답 하는 데 필요한 SQL 스크립트를 검토 합니다. SQL 스크립트 뿐 아니라 DAL 및 BLL에 메서드를 구현 해야도 합니다.

## <a name="step-2-returning-the-total-number-of-records-being-paged-through"></a>2 단계: 통해 호출이 전달 하는 레코드의 총 수를 반환 합니다.

정확 하 게 표시 되 고 페이지에 대 한 레코드 하위 집합을 검색 하는 방법을 살펴보기 전에 먼저 통해 호출이 전달 하는 레코드의 총 수를 반환 하는 방법에 대해 s가 있습니다. 페이징 사용자 인터페이스를 올바르게 구성 하기 위해이 정보가 필요 합니다. 사용 하 여 특정 SQL 쿼리에서 반환 된 레코드의 총 수를 가져올 수 있습니다는 [ `COUNT` 집계 함수](https://msdn.microsoft.com/library/ms175997.aspx)합니다. 예를 들어에 있는 레코드의 총 수를 확인 하는 `Products` 테이블을 다음 쿼리를 사용할 수 있습니다.


[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample1.sql)]

이 정보를 반환 하는 DAL에 메서드를 추가 하는 s를 사용 합니다. 특히, DAL 메서드를 만들겠습니다 `TotalNumberOfProducts()` 를 실행 하는 `SELECT` 위에 표시 된 문의 합니다.

열어 시작는 `Northwind.xsd` 형식화 된 데이터 집합 파일에는 `App_Code/DAL` 폴더입니다. 그런 다음 마우스 오른쪽 단추로 클릭는 `ProductsTableAdapter` 디자이너에서 쿼리 추가 선택 합니다. म으로 이전 자습서에서 했습니다 이렇게 하면 DAL에 새 메서드를 추가할 수는 특정 SQL 문이나 저장된 프로시저를 호출 하면 실행 됩니다. 이전 자습서 우리의 TableAdapter 메서드의 경우와 마찬가지로이 중 하나에 대 한 하기로 임시 SQL 문을 사용 합니다.


![임시 SQL 문을 사용 하 여](efficiently-paging-through-large-amounts-of-data-vb/_static/image1.png)

**그림 1**: 특별 SQL 문을 사용 하 여


다음 화면에서 어떤 유형의 쿼리를 만들를 지정할 수 있습니다. 이 쿼리는 반환 단일 스칼라 값에 있는 레코드의 총 수 있으므로 `Products` 테이블 선택에서 `SELECT` 단일 값 옵션을 반환 하는 합니다.


![단일 값을 반환 하는 SELECT 문을 사용 하 여 쿼리를 구성 합니다.](efficiently-paging-through-large-amounts-of-data-vb/_static/image2.png)

**그림 2**: 단일 값을 반환 하는 SELECT 문을 사용 하 여 쿼리를 구성 합니다.


사용 하는 쿼리 유형을 나타내는, 후 다음 쿼리를 지정 해야 했습니다.


![제품 쿼리에서 선택 그룹을 사용 하 여](efficiently-paging-through-large-amounts-of-data-vb/_static/image3.png)

**그림 3**: SELECT COUNT를 사용 하 여 (\*) FROM 제품 쿼리


마지막으로, 메서드의 이름을 지정 합니다. 앞에서 언급 한, let s로 사용 하 여 `TotalNumberOfProducts`합니다.


![DAL 메서드 TotalNumberOfProducts 이름 지정](efficiently-paging-through-large-amounts-of-data-vb/_static/image4.png)

**그림 4**: DAL 메서드 TotalNumberOfProducts 이름 지정


완료 날짜를 클릭 한 후 마법사는 추가 된 `TotalNumberOfProducts` 에 dal과 메서드. SQL 쿼리에서 결과 경우 DAL에서 스칼라 반환 메서드 반환 nullable 형식 `NULL`합니다. 그러나 우리의 `COUNT` 쿼리,는 항상 반환 이외`NULL` 값; DAL 메서드 nullable 정수를 반환 하는 그럼에도 불구 하 고 있습니다.

DAL 메서드 외에 BLL에 메서드가 필요 합니다. 열기는 `ProductsBLL` 클래스 파일을 추가 `TotalNumberOfProducts` 메서드를 단순히 DAL s에 호출 `TotalNumberOfProducts` 메서드:


[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample2.vb)]

DAL s `TotalNumberOfProducts` 메서드 nullable 정수를 반환 하지만 म 생성 했습니다는 `ProductsBLL` s 클래스 `TotalNumberOfProducts` 메서드는 표준 정수 반환 하도록 합니다. 따라서 할 필요는 `ProductsBLL` s 클래스 `TotalNumberOfProducts` 메서드 반환 값에 대 한 부분의 DAL s에 의해 반환 null을 허용 하는 정수 `TotalNumberOfProducts` 메서드. 하지만에 대 한 호출 `GetValueOrDefault()` nullable 정수 이면 않으면 nullable 정수 값을 반환 `null`, 기본 정수 값 0을 반환 합니다.

## <a name="step-3-returning-the-precise-subset-of-records"></a>3 단계: 정확한 레코드 하위 집합 반환

다음이 작업은 DAL 및 BLL 시작 하는 행 인덱스를 허용 하는 메서드를 만드는 것 및 최대 행 수 변수 앞에서 설명한 및 적절 한 레코드를 반환 합니다. 그 전에 let s 필요한 SQL 스크립트에서 먼저 찾습니다. 우리 당면 과제 이어야 한다는 것뿐입니다 म 시작 행 인덱스에 (그리고 레코드의 최대 레코드 수)를 시작 하는 해당 레코드를 반환할 수 있습니다를 통해 페이징 되 전체 결과의 각 행에 인덱스를 효율적으로 할당할 수 있습니다.

이미 있는 경우 열을 행 인덱스로 사용 되는 데이터베이스 테이블에는 챌린지 아닙니다. 얼핏 보기에 생각할 수 있습니다는 `Products` 테이블 s `ProductID` 첫 번째 제품에 필드가 충분 합니다 `ProductID` 1, 두 번째는 2, 등입니다. 그러나 제품을 삭제 실행이 방법을 사용 하는 시퀀스에서 간격이 유지 합니다.

다음 두 가지 일반 기술, 페이징할 수 데이터를 행 인덱스를 효율적으로 연결할 때 사용 레코드를 검색할 정확한 하위 집합을 사용할 수 있게 가지가 있습니다.

- **SQL Server 2005 s를 사용 하 여 `ROW_NUMBER()` 키워드** 새 SQL Server 2005로의 `ROW_NUMBER()` 키워드를 일정 한 순서에 따라 각 반환 된 레코드와 순위를 연결 합니다. 이 순위 각 행에 대해 행 인덱스도 사용할 수 있습니다.
- **테이블 변수를 사용 하 여 및 `SET ROWCOUNT`**  SQL Server s [ `SET ROWCOUNT` 문을](https://msdn.microsoft.com/library/ms188774.aspx) 는 쿼리; 종료 전에 처리 해야 총 레코드 수를 지정 하는 데 사용할 수 [테이블 변수](http://www.sqlteam.com/item.asp?ItemID=9454) 지역 변수가 T-SQL akin를 표 형식 데이터를 저장할 수 있는 [임시 테이블](http://www.sqlteam.com/item.asp?ItemID=2029)합니다. 이 접근 방식은 동일 하 게 모두 Microsoft SQL Server 2005 및 SQL Server 2000 (반면는 `ROW_NUMBER()` 방법은 SQL Server 2005에만 작동).  
  
  여기서는 테이블 변수를 만들려면는 `IDENTITY` 열과 해당 데이터를 통해 페이징 될 테이블의 기본 키에 대 한 열입니다. 있으므로 순차적 행 인덱스를 연결 하는 테이블 변수로 통해 페이징 될 데이터가 있는 테이블의 내용을 덤프 됩니다는 다음으로, (통해는 `IDENTITY` 열)는 테이블의 각 레코드에 대 한 합니다. 테이블 변수가 채워진 후는 `SELECT` 테이블 변수에서 문을 특정 레코드를 추출 하기 위해 실행할 수는 기본 테이블과 조인 합니다. `SET ROWCOUNT` 테이블 변수로 덤프 해야 하는 레코드의 수를 제한 하는 지능적으로 문을 사용 합니다.  
  
  이러한 접근 방식을의 효율성 요청 되는 페이지 번호를 기반으로 `SET ROWCOUNT` 값 행 인덱스 이며 시작을 더한 최대 행 값이 할당 됩니다. 데이터의 후속 페이지 첫 번째 같은 숫자가 낮은 페이지를 페이징할 때는이 방법이 매우 효율적입니다. 그러나 끝 근처에 있는 페이지를 검색할 때 기본 페이징와 비슷한 성능을 보여줍니다.

이 자습서를 사용 하 여 사용자 지정 페이징을 구현 하는 `ROW_NUMBER()` 키워드입니다. 테이블 변수를 사용 하 여 대 한 자세한 내용은 및 `SET ROWCOUNT` 기술 참조 [A 더 효율적으로 큰 결과 집합을 통해 페이징](http://www.4guysfromrolla.com/webtech/042606-1.shtml)합니다.

`ROW_NUMBER()` 키워드는 순위는 다음 구문을 사용 하 여 특정 순서를 통해 반환 된 각 레코드와 연결 된:


[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample3.sql)]

`ROW_NUMBER()` 표시 된 순서와 관련 하 여 각 레코드에 대 한 순위를 지정 하는 숫자 값을 반환 합니다. 예를 들어 가장에서 주문한 각 제품에 대 한 순위를 가장 적게 하는 데 비용이 사용 있습니다 다음 쿼리.


[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample4.sql)]

그림 5의 결과 Visual Studio에서 쿼리 창을 통해를 실행 하는 경우이 쿼리를 보여 줍니다. 각 행에 대 한 가격 순위 함께 가격으로 정렬 하는 제품을 참고 합니다.


![가격 순위에 대 한 포함 된 각 반환 된 레코드](efficiently-paging-through-large-amounts-of-data-vb/_static/image5.png)

**그림 5**: The 가격 순위에 대 한 포함 된 각 반환 된 레코드


> [!NOTE]
> `ROW_NUMBER()` SQL Server 2005에서 사용할 수 있는 많은 새 순위 함수 중 하나일 뿐입니다. 에 대 한 보다 철저 한 설명은 `ROW_NUMBER()`, 다른 순위 함수를 함께 읽기 [Microsoft SQL Server 2005를 사용 하 여 순위 결과 반환](http://www.4guysfromrolla.com/webtech/010406-1.shtml)합니다.


결과에서 지정 된 순위 때 `ORDER BY` 열에는 `OVER` 절 (`UnitPrice`, 위 예에서), SQL Server 결과 정렬 해야 합니다. 이것은 빠른 작업으로, 결과 정렬 열 위에 클러스터형된 인덱스가 있으면 포함 된 경우 인덱스로 하지만 그렇지 않은 경우 비용이 많이 드는 될 수 있습니다. 충분히 큰 쿼리의 성능은 개선 하려면 기준인 결과으로 정렬 열에 대 한 비클러스터형 인덱스를 추가 하는 것이 좋습니다. 참조 [순위 함수 및 SQL Server 2005의 성능](http://www.sql-server-performance.com/ak_ranking_functions.asp) 를 더 자세히 살펴보려면 성능 고려 사항에 대 한 합니다.

반환 된 순위 정보 `ROW_NUMBER()` 에서 직접 사용할 수는 `WHERE` 절. 그러나, 반환 하는 파생된 테이블을 사용할 수 있습니다는 `ROW_NUMBER()` 다음에 사용할 수 있는 결과 `WHERE` 절. 다음 쿼리에서 파생된 테이블을 사용 하 여 함께 ProductName 및 UnitPrice 열을 반환 하는 예를 들어는 `ROW_NUMBER()` 결과 한 다음 사용 하는 `WHERE` 11-20을 해당 제품 가격 차수가 반환 하도록 절은:


[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample5.sql)]

이 개념을 좀 더 확장, 특정 페이지에서 시작 하는 행 인덱스 및 최대 행 수 값을 원하는 데이터를 검색이 방법을 이용 하면:


[!code-html[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample6.html)]

> [!NOTE]
> 이 자습서의 나중에 알 수 있듯이 *`StartRowIndex`* 제공한는 ObjectDataSource 인덱싱된 0부터 시작 하는 반면는 `ROW_NUMBER()` SQL Server 2005에서 반환 된 값 1에서 시작 인덱싱됩니다. 따라서는 `WHERE` 절은 레코드를 반환 합니다. 여기서 `PriceRank` 보다 엄격 하 게 크면 *`StartRowIndex`* 보다 작거나 같음 및 *`StartRowIndex`*  +  *`MaximumRows`*.


해당 म 것은 사용 이제 방법을 설명 했습니다 `ROW_NUMBER()` 될 수 있습니다 DAL 및 BLL에 메서드로이 논리를 구현 하려면 이제 해야 시작 하는 행 인덱스 및 최대 행 수 값 데이터의 특정 페이지를 검색 하는 데 사용 합니다.

순서 결정 해야 하는이 쿼리를 만들 때 기준인 결과 순위를 지정할; s 제품 알파벳 순서로 이름 기준으로 정렬할 수 있도록 합니다. 즉, 있는지와이 자습서에서는 사용자 지정 페이징 구현에서는 됩니다 정렬할 수도 있습니다 보다 사용자 지정 페이지 매김 된 보고서를 만들 수 있습니다. 다음 자습서에서는 하지만 살펴보겠습니다 어떻게 이러한 기능을 제공할 수 있습니다.

이전 섹션에서 임의 SQL 문 처럼 DAL 메서드를 생성 합니다. 와 같은 TableAdapter 마법사 대상이 t에서 사용 하는 Visual Studio에서 T-SQL 파서 아쉽게도 `OVER` 사용 되는 구문은 `ROW_NUMBER()` 함수입니다. 따라서 저장 프로시저로이 DAL 메서드를 만들어야 합니다. 보기 메뉴 (또는 적중된 Ctrl + Alt + S)에서 서버 탐색기를 선택 하 고 확장 된 `NORTHWND.MDF` 노드. 새 저장된 프로시저를 추가 하려면 저장 프로시저 노드를 마우스 오른쪽 단추로 클릭 하 고 새 저장 프로시저 추가 선택 (그림 6 참조).


![새 저장된 프로시저를 페이징 하는 제품에 대 한 추가](efficiently-paging-through-large-amounts-of-data-vb/_static/image6.png)

**그림 6**: 페이징 작업을 하는 제품에 대 한 새 저장된 프로시저를 추가 합니다.


이 저장된 프로시저는 두 개의 정수 입력된 매개 변수-수락 해야 `@startRowIndex` 및 `@maximumRows` 사용 및는 `ROW_NUMBER()` 함수를 기준으로 정렬는 `ProductName` 필드에는 행만 지정 된 보다 큰 반환 `@startRowIndex` 및 보다 작은 또는 같음 `@startRowIndex`  +  `@maximumRow` s입니다. 새 저장된 프로시저에 다음 스크립트를 입력 하 고 데이터베이스에 저장된 프로시저를 추가 하려면 저장 아이콘을 클릭 합니다.


[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample7.sql)]

저장된 프로시저를 만든 후 테스트 하는 데를 보십시오. 마우스 오른쪽 단추로 클릭는 `GetProductsPaged` 저장된 프로시저는 서버 탐색기에서 이름을 지정 하 고 Execute 옵션을 선택 합니다. Visual Studio를 다음 묻는 입력된 매개 변수를 `@startRowIndex` 및 `@maximumRow` s (그림 7 참조). 다른 값을 사용 하 고 결과 확인 합니다.


![에 대 한 값을 입력에서 @startRowIndex 및 @maximumRows 매개 변수](efficiently-paging-through-large-amounts-of-data-vb/_static/image7.png)

<strong>그림 7</strong>:에 대 한 값을 입력에서 @startRowIndex 및 @maximumRows 매개 변수


후 이러한 선택 매개 변수 값을 입력, 출력 창에 결과가 표시 됩니다. 그림 8 10 둘 다에 전달 하는 경우 결과 보여 줍니다는 `@startRowIndex` 및 `@maximumRows` 매개 변수입니다.


[![반환 되는 레코드는에 표시 되는지 두 번째 데이터 페이지](efficiently-paging-through-large-amounts-of-data-vb/_static/image9.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image8.png)

**그림 8**: 반환 되는 레코드는에 표시 되는지 두 번째 데이터 페이지 ([전체 크기 이미지를 보려면 클릭](efficiently-paging-through-large-amounts-of-data-vb/_static/image10.png))


사용 하 여 만든 저장 프로시저를 만들려는 준비 된 우리는 `ProductsTableAdapter` 메서드. 열기는 `Northwind.xsd` 형식화 된 데이터 집합에서 오른쪽 클릭은 `ProductsTableAdapter`, 쿼리 추가 옵션을 선택 합니다. 임시 SQL 문을 사용 하 여 쿼리를 만드는 대신 기존 저장된 프로시저를 사용 하 여 만듭니다.


![기존 저장된 프로시저를 사용 하 여 DAL 메서드 만들기](efficiently-paging-through-large-amounts-of-data-vb/_static/image11.png)

**그림 9**: 기존 저장된 프로시저를 사용 하 여 DAL 메서드 만들기


다음으로 호출할 저장된 프로시저를 선택 하 라는 메시지가 나타나면 했습니다. 선택 된 `GetProductsPaged` 드롭 다운 목록에서 저장 프로시저입니다.


![GetProductsPaged 선택 드롭다운 목록에서 저장 프로시저](efficiently-paging-through-large-amounts-of-data-vb/_static/image12.png)

**그림 10**:는 GetProductsPaged 선택 드롭다운 목록에서 저장 프로시저


다음 화면에서 다음 묻는 어떤 종류의 데이터가 저장된 프로시저에서 반환: 표 형식 데이터, 단일 값 또는 값이 없습니다. 이후는 `GetProductsPaged` 저장된 프로시저 여러 레코드를 반환할 수 있습니다, 표 형식 데이터를 반환 하는지 나타냅니다.


![저장된 프로시저 테이블 형식 데이터를 반환 하는지 나타냅니다.](efficiently-paging-through-large-amounts-of-data-vb/_static/image13.png)

**그림 11**: 저장된 프로시저 테이블 형식 데이터를 반환 하는지 나타냅니다.


마지막으로 만든 하려는 메서드의 이름을 나타냅니다. 이 이전 자습서에서와 마찬가지로 계속 및 DataTable 채우기 모두를 사용 하 여 메서드를 만들를 DataTable을 반환 합니다. 첫 번째 메서드 이름을 `FillPaged` 및 두 번째 `GetProductsPaged`합니다.


![메서드 FillPaged 이름과 GetProductsPaged](efficiently-paging-through-large-amounts-of-data-vb/_static/image14.png)

**그림 12**: 메서드 FillPaged 이름과 GetProductsPaged


또한 제품의 특정 페이지를 반환 하는 DAL 메서드 생성도 해야 BLL에 이러한 기능을 제공 합니다. DAL 메서드와 마찬가지로 BLL의 GetProductsPaged 메서드 시작 하는 행 인덱스 및 최대 행 수를 지정 하기 위한 두 개의 정수 입력 받아들여야 하 고 지정 된 범위 안에 있는 레코드만 반환 해야 합니다. 단순히 하 여 호출 아래로 DAL의 GetProductsPaged 메서드 같이 ProductsBLL 클래스에서 이러한 BLL 메서드를 만듭니다.


[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample8.vb)]

모든 이름을 사용할 수 BLL의 메서드에 입력된 매개 변수를 사용 하도록 선택 하지만 하겠지만, 알 수 있듯이 `startRowIndex` 및 `maximumRows` 추가에서 구성할 필요가이 방법을 사용 하려면 ObjectDataSource를 구성할 때 작업 합니다.

## <a name="step-4-configuring-the-objectdatasource-to-use-custom-paging"></a>4 단계: 사용자 지정 페이징을 사용 하 여 ObjectDataSource 구성

완료 하는 레코드의 특정 하위 집합에 액세스 하기 위한 BLL 및 DAL 방법을 사용 하 여 사용자 지정 페이징을 사용 하 여 해당 원본 레코드를 통해 해당 페이지를 제어할 준비 된 GridView를 만들려고 했습니다. 열어 시작는 `EfficientPaging.aspx` 페이지에 `PagingAndSorting` 폴더를 페이지에는 GridView를 추가 하 고 새 ObjectDataSource 컨트롤을 사용 하도록 구성 합니다. 우리의 지난 자습서에서 자주 했습니다. 사용 하도록 구성 된 ObjectDataSource는 `ProductsBLL` s 클래스 `GetProducts` 메서드. 그러나이 이번에 사용 하려는 `GetProductsPaged` 메서드 대신, 이후에 `GetProducts` 메서드가 반환 되 *모든* 데이터베이스에서 제품의 반면 `GetProductsPaged` 레코드의 특정 하위 집합만 반환 합니다.


![ObjectDataSource ProductsBLL 클래스의 GetProductsPaged 메서드를 사용 하도록 구성](efficiently-paging-through-large-amounts-of-data-vb/_static/image15.png)

**그림 13**: ObjectDataSource ProductsBLL 클래스의 GetProductsPaged 메서드를 사용 하도록 구성


읽기 전용 GridView 만드는 다시 we, 이후 방법 드롭다운 목록에서 INSERT, UPDATE, 설정 하 하 고 각 탭 (없음)을를 삭제 합니다.

다음으로, ObjectDataSource 만들라는 우리의 원본에 대 한는 `GetProductsPaged` s 메서드에 `startRowIndex` 및 `maximumRows` 매개 변수 값을 입력 합니다. 이러한 입력된 매개 변수는 실제로 수 GridView에서 자동으로 설정 하면 소스 집합 None으로 두고 마침을 클릭 합니다.


![입력된 매개 변수 소스 None으로 유지](efficiently-paging-through-large-amounts-of-data-vb/_static/image16.png)

**그림 14**: None으로 입력된 매개 변수 소스를 그대로 둡니다.


ObjectDataSource 마법사를 완료 한 후 GridView가 BoundField 또는 CheckBoxField 각 제품 데이터 필드에 대해 포함 됩니다. 자유롭게 보시기 GridView의 모양을 조정할 수 있습니다. I 했습니다 표시 하지 않도록 선택한는 `ProductName`, `CategoryName`, `SupplierName`, `QuantityPerUnit`, 및 `UnitPrice` BoundFields 합니다. 또한 스마트 태그에서 페이징 사용 확인란을 선택 하 여 페이징을 지원 하기 위해 GridView를 구성 합니다. 이러한 변경 된 후 GridView 및 ObjectDataSource 선언적 태그는 다음과 비슷하게 표시 됩니다.


[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample9.aspx)]

그러나 브라우저를 통해 페이지를 방문 하는 경우 GridView에는 없는를 찾을 수 있습니다.


![GridView가 स व र](efficiently-paging-through-large-amounts-of-data-vb/_static/image17.png)

**그림 15**: GridView가 स व र


ObjectDataSource에서 사용 중이기 때문에 현재 0 값으로 둘 다에 대해 GridView 없거나는 `GetProductsPaged` `startRowIndex` 및 `maximumRows` 입력 매개 변수입니다. 따라서 결과 SQL 쿼리 없는 레코드를 반환 하 고 따라서 GridView 표시 되지 않습니다.

이 해결 하려면 사용자 지정 페이징을 사용 하 여 ObjectDataSource를 구성 해야 합니다. 다음 단계에서는를 수행할 수 있습니다.

1. **ObjectDataSource s 설정 `EnablePaging` 속성을 `true`**  으로 전달 해야 하는 ObjectDataSource 표시는 `SelectMethod` 두 개의 추가 매개 변수: 시작 하는 행 인덱스를 지정할 수 하나의 ([ `StartRowIndexParameterName` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.startrowindexparametername.aspx)), 최대 행을 지정 하 고 다른 하나 ([`MaximumRowsParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.maximumrowsparametername.aspx)).
2. **ObjectDataSource s 설정 `StartRowIndexParameterName` 및 `MaximumRowsParameterName` 그에 따라 속성** 는 `StartRowIndexParameterName` 및 `MaximumRowsParameterName` 속성에 전달 된 입력된 매개 변수의 이름을 나타냅니다는 `SelectMethod` 사용자 지정 페이징 목적입니다. 기본적으로 이러한 매개 변수 이름은 `startIndexRow` 및 `maximumRows`, 하는 이유를 만들 때의 `GetProductsPaged` 메서드 BLL, 입력된 매개 변수에 대 한 이러한 값 사용. BLL s에 대 한 서로 다른 매개 변수 이름을 사용 하도록 선택한 경우 `GetProductsPaged` 메서드와 같은 `startIndex` 및 `maxRows`ObjectDataSource s를 설정 해야 하는 예제에 대 한 `StartRowIndexParameterName` 및 `MaximumRowsParameterName` 속성 적절 하 게 (예:에 대 한 startIndex `StartRowIndexParameterName` 및에 대 한 maxRows `MaximumRowsParameterName`).
3. **ObjectDataSource s 설정 [ `SelectCountMethod` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selectcountmethod(VS.80).aspx) 의 총 수의 레코드 되 고 페이지를 통해 반환 되는 메서드의 이름에 (`TotalNumberOfProducts`)** 이전에 설명한 대로 `ProductsBLL`의 클래스`TotalNumberOfProducts`실행 하는 DAL 메서드를 사용 하 여 호출이 전달 하는 레코드의 총 수를 반환 하는 메서드는 `SELECT COUNT(*) FROM Products` 쿼리 합니다. 이 정보는 objectdatasource 올바르게 페이징 인터페이스를 렌더링 하는 데 필요 합니다.
4. **제거는 `startRowIndex` 및 `maximumRows` `<asp:Parameter>` ObjectDataSource s 선언 태그에서에서 요소를** 마법사를 통해 ObjectDataSource를 구성할 때 Visual Studio 자동으로 추가 두 `<asp:Parameter>` 요소 에 대 한는 `GetProductsPaged`의 메서드 매개 변수를 입력 합니다. 설정 하 여 `EnablePaging` 를 `true`, 이러한 매개 변수를 자동으로 전달 됩니다;는 ObjectDataSource를 전달 하려고 시도 선언적 구문에도 표시, *4 개의* 에 매개 변수는 `GetProductsPaged` 메서드 및 두 개의 매개 변수는 `TotalNumberOfProducts` 메서드. 이러한 확장을 제거할 것을 잊은 경우 `<asp:Parameter>` 같은 오류 메시지를 얻게 됩니다 브라우저를 통해 페이지를 방문 하는 경우 요소: *ObjectDataSource 'ObjectDataSource1' 찾을 수 없습니다 제네릭이 아닌 메서드를 가진 ' TotalNumberOfProducts' 매개 변수: startRowIndex, maximumRows*합니다.

다음과 같이 변경한 후 ObjectDataSource s 선언적 구문 다음과 같이 표시 됩니다.


[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample10.aspx)]

`EnablePaging` 및 `SelectCountMethod` 속성이 설정 되어 있는지와 `<asp:Parameter>` 요소가 제거 되었습니다. 그림 16 이러한 변경이 이루어진 후 속성 창의 스크린 샷을 보여줍니다.


![사용자 지정 페이징을 사용 하려면 ObjectDataSource 컨트롤 구성](efficiently-paging-through-large-amounts-of-data-vb/_static/image18.png)

**그림 16**: 사용자 지정 페이징을 사용 하려면 ObjectDataSource 컨트롤 구성


다음과 같이 변경한 후 브라우저를 통해이 페이지를 방문 합니다. 목록에 10 개의 제품이 표시 되어야으로 사전순으로 정렬 합니다. 한 번에 한 페이지씩 데이터를 단계별로 실행 되도록 보십시오. 만 지정한 페이지에 대 한 표시 되어야 하는 레코드를 검색 하는 대로 visual 사이는 차이점이의 최종 사용자 관점에서 기본 페이징 및 사용자 지정 페이징 상태인 동안 많은 양의 데이터를 통해 페이지 사용자 지정 페이징 보다 효율적으로.


[![데이터, 제품 이름, s에 의해 Ordered가 사용 하 여 사용자 지정 페이징 페이징](efficiently-paging-through-large-amounts-of-data-vb/_static/image20.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image19.png)

**그림 17**:를 사용 하 여 사용자 지정 페이징 페이징은 Data, 제품 이름, s에 의해 Ordered ([전체 크기 이미지를 보려면 클릭](efficiently-paging-through-large-amounts-of-data-vb/_static/image21.png))


> [!NOTE]
> 페이지를 사용자 지정 페이징을 사용 하 여 ObjectDataSource s에 의해 반환 된 값을 계산 `SelectCountMethod` GridView의 보기 상태에 저장 됩니다. 다른 GridView 변수는 `PageIndex`, `EditIndex`, `SelectedIndex`, `DataKeys` 등에 컬렉션에 저장 된 *제어 상태가*, GridView s의 값에 관계 없이 유지 되는 `EnableViewState` 속성입니다. 이후는 `PageCount` 값은 유지 게시할 마지막 페이지로 이동 하는 데 대 한 링크를 포함 하는 페이징 인터페이스를 사용 하는 경우에 상태 보기를 사용 하는 GridView의 뷰 상태를 사용할 수 있습니다. (페이징 인터페이스에 대 한 직접 링크를 마지막으로 포함 되지 않은 경우 페이지, 다음 뷰 상태를 비활성화할 수 있습니다.)


포스트백 마지막 페이지 링크를 클릭 하 고 업데이트 하 여 GridView를 지시 해당 `PageIndex` 속성입니다. GridView 할당의 마지막 페이지 링크를 클릭 하면 해당 `PageIndex` 속성 하나는 값을 보다 작은 해당 `PageCount` 속성입니다. 비활성화 된 뷰 상태와는 `PageCount` 게시할 손실 되는 값 및 `PageIndex` 대신 최대 정수 값이 할당 됩니다. GridView를 곱하여 시작 하는 행 인덱스를 확인 하려고 하는 다음으로 `PageSize` 및 `PageCount` 속성입니다. 이 인해 프로그램 `OverflowException` 이후 제품 허용 된 최대 정수 크기를 초과 합니다.

## <a name="implement-custom-paging-and-sorting"></a>사용자 지정 페이징을 구현 및 정렬

현재 사용자 지정 페이징 구현을 만들 때 데이터를 통해 페이징 되는 기준인 순서 정적으로 지정 해야는 `GetProductsPaged` 저장 프로시저입니다. 그러나 수 기록한 GridView s 스마트 태그는 페이징 사용 옵션 외에도 정렬 사용 확인란을 포함 합니다. 그러나이 현재 사용자 지정 페이징 구현에서 GridView에 정렬 지원 추가 데이터만 데이터의 현재 표시 된 페이지의 레코드를 정렬 됩니다. 예를 들어 GridView도는 페이징을 지원 하 고 데이터의 첫 번째 페이지를 볼 때 제품 이름을 내림차순으로 정렬 하는 다음을 구성 하는 경우 1 페이지에서 제품의 순서를 반대로 합니다 것입니다. 그림 18에서 볼 수 있듯이 등 카 호랑이 하면로 표시 첫 번째 제품 71 다른 제품을 사전순으로; 카 호랑이 뒤에 오는 무시 역방향 알파벳 순서 정렬 첫 번째 페이지에서 해당 레코드에만 정렬에 것으로 간주 됩니다.


[![만 데이터 페이지에 표시 되는 현재 정렬](efficiently-paging-through-large-amounts-of-data-vb/_static/image23.png)](efficiently-paging-through-large-amounts-of-data-vb/_static/image22.png)

**그림 18**: 정렬 된만 데이터 페이지에 표시 되는 현재 ([전체 크기 이미지를 보려면 클릭](efficiently-paging-through-large-amounts-of-data-vb/_static/image24.png))


데이터 BLL s에서 검색 된 후 발생 하는 정렬 하기 때문에 데이터의 현재 페이지에만 적용 정렬 `GetProductsPaged` 메서드와이 메서드가 특정 페이지에 대 한 해당 레코드를 반환 합니다. 정렬 식에 전달 하도록 설정 해야 올바르게 정렬을 구현는 `GetProductsPaged` 메서드 데이터의 특정 페이지를 반환 하기 전에 데이터를 적절 하 게 순위 지정할 수 있도록 합니다. 다음이 자습서에서이 수행 하는 방법을 살펴보겠습니다.

## <a name="implementing-custom-paging-and-deleting"></a>사용자 지정 페이징 및 삭제를 구현 합니다.

데이터가 있는 마지막 페이지에서 마지막 레코드를 삭제할 때 볼 수 있습니다 하는 사용자 지정 페이징 기술을 사용 하 여 페이징 되는 GridView에서 삭제 기능을 사용 하도록 설정 하면 GridView 사라집니다 적절 하 게 감소 하는 대신 GridView의 `PageIndex`. 이 버그를 재현 하려면 방금 방금 만든 자습서에 대 한 삭제를 사용 합니다. 여기서 표시 되어야 단일 제품 81 제품을 한 번에 10 개의 product 통해 페이징 म 이후 마지막 페이지 (페이지 9)로 이동 합니다. 이 제품을 삭제 합니다.

마지막으로 제품을 GridView 삭제 시 *해야* 자동으로 여덟 번째 페이지로 이동 하 고 이러한 기능은 기본 페이징을 사용 하 여 발생 합니다. 그러나 사용자 지정 페이징을 사용 하 여 마지막 페이지에는 마지막으로 제품을 삭제 한 후 GridView 단순히 사라집니다 화면에서 모두. 정확한 원인을 *이유* 이 자습서의 범위를 벗어나지만이 작업은 이루어지고 참조 [사용자 지정 페이징 된 GridView에서 마지막 페이지에 있는 마지막 레코드를 삭제](http://scottonwriting.net/sowblog/posts/7326.aspx) 의 소스에 대 한 하위 수준 세부 정보에 대 한 이 문제입니다. 요약 하자면에서 것 s 다음 단계를 수행 하는 GridView 삭제 단추를 클릭할 때 발생 합니다.

1. 레코드 삭제
2. 지정 된 표시 하려면 적절 한 레코드를 가져올 `PageIndex` 및 `PageSize`
3. 확인 하 고 `PageIndex` GridView s 감소 시킬 자동으로 수행 하는 경우 데이터 원본;의 데이터 페이지의 수를 초과 하지 않는 `PageIndex` 속성
4. 2 단계에서에서 얻은 레코드를 사용 하 여 GridView에 적절 한 페이지의 데이터 바인딩

해당에서 2 단계 사실에서 형태소 분석 문제는 `PageIndex` 표시할 레코드를 클릭 한 다음는 여전히 때 사용 되는 `PageIndex` 유일한 레코드 삭제 된 마지막 페이지입니다. 2 단계에서 따라서 *없는* 데이터의 마지막 페이지에는 더 이상 레코드가 포함 되어 있으므로 레코드가 반환 됩니다. 그런 다음 3 단계에서에서 GridView 인식 하는 해당 `PageIndex` 속성은 데이터 원본에서 페이지의 총 수보다 큽니다 (म 이후 했습니다 삭제 마지막 페이지의 마지막 레코드) 하 고 따라서 감소 해당 `PageIndex` 속성. 4 단계에서에서 GridView 자체에 바인딩하려 2 단계;에서 검색 되는 데이터 그러나 반환 된 레코드가 2 단계에서는 따라서 그 결과 빈 GridView입니다. 기본 페이징을 사용 하 여이 문제 대상이 t 노출 하기 때문에 2 단계에서에서 *모든* 데이터 소스에서 레코드를 검색 합니다.

이 문제를 해결 하는 두 가지 옵션이 있습니다. GridView s에 대 한 이벤트 처리기를 만들려면 첫 번째는 `RowDeleted` 방금 삭제 된 페이지에 표시 된 레코드 수를 결정 하는 이벤트 처리기입니다. 하나의 레코드만 했습니다 삭제 레코드 받아야 마지막 고 GridView s 감소 해야 `PageIndex`합니다. 물론,만 포함 하려고 업데이트 하는 `PageIndex` 삭제 작업에 실제로 성공 하면 얻는 다음을 통해는 `e.Exception` 속성은 `null`합니다.

이 접근 방식은 업데이트 하므로 `PageIndex` 1 단계의 전후에 그러나 2 단계 전에 합니다. 따라서 2 단계에서에서 적절 한 레코드 집합이 반환 됩니다. 이를 위해 다음과 같은 코드를 사용 합니다.


[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample11.vb)]

ObjectDataSource s에 대 한 이벤트 처리기를 만들려면 다른 해결 방법은 `RowDeleted` 이벤트를 생성 하 고 설정 하는 `AffectedRows` 속성 값이 1 합니다. GridView 업데이트 1 단계에서에서 (그러나 다시 2 단계에서에서 데이터를 검색 하기 전에) 레코드를 삭제 한 후 해당 `PageIndex` 하나 이상의 행이 작업에 의해 영향을 받은 경우 속성을 사용 합니다. 그러나는 `AffectedRows` 는 objectdatasource 속성은 설정 되지 않으며 따라서이 단계를 생략 합니다. 이 단계를 실행 하는 한 가지 방법은 수동으로 설정 하는 것은 `AffectedRows` 삭제 작업이 성공적으로 완료 되는 경우 속성을 사용 합니다. 다음과 같은 코드를 사용 하 여 수행할 수 있습니다.


[!code-vb[Main](efficiently-paging-through-large-amounts-of-data-vb/samples/sample12.vb)]

코드 숨김 클래스에서 모두 이러한 이벤트 처리기에 대 한 코드를 찾을 수는 `EfficientPaging.aspx` 예제입니다.

## <a name="comparing-the-performance-of-default-and-custom-paging"></a>기본 및 사용자 지정 페이징의 성능 비교

사용자 지정 페이징만 검색 하는 레코드에 필요한 반면 기본 페이징 반환 하므로 *모든* 보고 있는 각 페이지에 대 한 레코드의 것 s 분명히 사용자 지정 페이징을 기본 페이징 보다 더 효율적입니다. 그러나 단지 얼마나는 사용자 지정 페이징? 사용자 지정 페이징에 기본 페이징에서 이동 하 여 어떤 종류의 성능 향상을 볼 수 있습니다?

안타깝게도, 없어 s 없는 적합 크기 모두 여기에 응답 합니다. 성능 향상은 다양 한 요인에 따라 달라 집니다, 그리고 웹 서버와 데이터베이스 서버 간의 데이터베이스 서버와 통신 채널에 수를 통해 페이징 되는 레코드와 로드 되 고 2 개가 포함 된 가장 두드러진 합니다. 몇 십 개의 레코드가 있는 작은 테이블에 대 한 성능 차이 무시할 수 있습니다. 그러나 많은 행을 수십만 건까지 있는 대규모 테이블에 대 한 성능 차이 예입니다.

문서 [ASP.NET 2.0 SQL Server 2005와 함께 사용자 지정 페이징](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx), 필자는 데이터베이스 테이블에 페이징 하는 경우 이러한 두 페이징 기술 간 성능 면에서 차이가에서는 몇 가지 성능 테스트를 포함 합니다. 50, 000 레코드입니다. SQL Server 수준에서 쿼리를 실행 하는 두 시간 다루었습니다이 테스트에서는 (사용 하 여 [SQL 프로파일러](https://msdn.microsoft.com/library/ms173757.aspx)) 사용 하 여 ASP.NET 페이지에서 [ASP.NET의 추적 기능](https://msdn.microsoft.com/library/y13fw6we.aspx)합니다. 이러한 테스트 단일 활성 사용자와 개발 상자 내에서 실행 된 하 고 따라서 없는 과학 이므로 일반적인 웹 사이트 부하 패턴을 모방지 않습니다 염두에 둬야 합니다. 그럼에도 불구 하 고 결과 충분히 큰 양의 데이터로 작업 하는 경우 기본 인스턴스 및 사용자 지정 페이징 실행 시간에 상대 차이점을 설명 합니다.


|  | **Avg. 기간 (초)** | **읽기** |
| --- | --- | --- |
| **기본 SQL 프로필러를 페이징** | 1.411 | 383 |
| **사용자 지정 페이징 SQL 프로파일러** | 0.002 | 29 |
| **기본 페이징 ASP.NET 추적** | 2.379 | *해당 없음* |
| **사용자 지정 페이징 ASP.NET 추적** | 0.029 | *해당 없음* |


볼 수 있듯이 읽기 덜 354 평균 필요한 데이터의 특정 페이지를 검색 하 고 짧은 시간에 완료 됩니다. ASP.NET 페이지에서 사용자 지정 페이지에서 수에서 1/100에 가까우면 렌더링할<sup>번째</sup> 기본 페이징을 사용 하는 경우는 데 걸린 시간입니다. 참조 [내 문서](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx) 코드와 데이터베이스와 함께 이러한 결과 대 한 자세한 내용은 사용자가 자신의 환경에서이 테스트를 재현 하는 다운로드할 수 있습니다.

## <a name="summary"></a>요약

기본 페이징 데이터 웹 컨트롤 s 스마트 태그에서 검사 페이징 사용 확인란을 구현 하는 작업도 매우 간단 하지만 이러한 단순성 되는 성능 대신. 사용자 데이터의 모든 페이지를 요청할 때 기본 페이징을 사용 하 여 *모든* 레코드가 반환 하지만 그 중 작은 줄어 일부 데이터만 표시 될 수 있습니다. 이 성능 오버 헤드를 방지 하기 위해는 ObjectDataSource는 대체 페이징 옵션 사용자 지정 페이징을 제공 합니다.

사용자 지정 페이징 개선 기본 표시 되어야 하는 레코드에만 검색 하 여 s 성능 문제를 페이징 하는 동안 그 s 사용자 지정 페이징을 구현 하는 조금 더 복잡된 합니다. 첫째, 액세스 하는 (올바르고 효율적으로 작동할) 요청 되는 레코드의 특정 하위 집합 쿼리를 작성 되어야 합니다. 이 다양 한 방법으로;에서 수행할 수 있습니다. 새 SQL Server 2005 s를 사용 하 되는이 자습서에서는 검사 했습니다 `ROW_NUMBER()` 순위 함수 결과 한 다음 멤버만 반환할 결과 인 순위 지정된 된 범위 내에 있게 합니다. 또한 통해 호출이 전달 하는 레코드의 총 수를 결정 하는 수단을 추가 해야 합니다. 이러한 DAL 및 BLL 메서드를 만든 후도 구성 된 ObjectDataSource 총 레코드 수를 통해 호출 되 고 시작 하는 행 인덱스 및 최대 행 수 값 BLL에 통과 올바르게 확인할 수 있도록 해야 합니다.

사용자 지정 페이징을 구현에 몇 가지 단계 필요 하 고 거의 하지과 마찬가지로 간단 기본 페이징, 사용자 지정 페이징을 충분히 많은 양의 데이터를 페이징할 때는 반드시 필요 합니다. 검사 결과 보여주었습니다, 사용자 지정 페이징 ASP.NET 페이지의 렌더링 시간에서 초를 늘리는 수 되며 수 부담을 덜고 데이터베이스 서버에서 하나 이상의 크기 순서 대로 정렬 됩니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](paging-and-sorting-report-data-vb.md)
> [다음](sorting-custom-paged-data-vb.md)
