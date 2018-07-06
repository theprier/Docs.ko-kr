---
uid: web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs
title: 많은 양의 데이터 (C#)를 효율적으로 페이징 | Microsoft Docs
author: rick-anderson
description: 많은 양의 데이터를 해당 기본 데이터 소스 컨트롤 retriev로 작업할 때 데이터 프레젠테이션 컨트롤의 기본 페이징 옵션이 적합 하지 않습니다...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/15/2006
ms.topic: article
ms.assetid: 59c01998-9326-4ecb-9392-cb9615962140
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs
msc.type: authoredcontent
ms.openlocfilehash: a6d023f299d3c36e0b9f0d00f2b531d73657135c
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37367883"
---
<a name="efficiently-paging-through-large-amounts-of-data-c"></a>많은 양의 데이터 (C#)를 효율적으로 페이징
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_25_CS.exe) 또는 [PDF 다운로드](efficiently-paging-through-large-amounts-of-data-cs/_static/datatutorial25cs1.pdf)

> 데이터 프레젠테이션 컨트롤의 기본 페이징 옵션이 아닙니다 적합 한 많은 양의 데이터를 작업할 때 해당 기본 데이터 소스 컨트롤 데이터의 하위 집합만 표시 되는 경우에 모든 레코드를 검색 합니다. 이러한 상황에서는 설정 해야 합니다에 사용자 지정 페이징 합니다.


## <a name="introduction"></a>소개

이전 자습서에서 설명한 대로 두 가지 방법 중 하나에서 페이징을 구현할 수 있습니다.

- **기본 페이징은** 페이징 사용 옵션을 선택 하면 구현할 수 있습니다 데이터 웹 컨트롤 s의에서 스마트 태그, 단, 데이터 페이지를 볼 때마다 ObjectDataSource 검색 *모든* 레코드의도 페이지에서의 하위 집합만 표시는 되지만
- **그러나 사용자 지정 페이징을** 기본 성능이 개선 되는 사용자에 의해 요청 된 데이터의 특정 페이지를 표시 해야 하는 데이터베이스에서 레코드를 검색 하 여 페이징 사용자 지정 페이징을 포함을 구현 하는 약간 더 많은 노력이 기본 페이징은 보다

구현만 확인 확인란 다시 용이성으로 인해 완료 되었습니다. 기본 페이징은 매력적인 옵션입니다. 레코드의 모든 검색은 na ve 접근 방식을 사용 두고 선택 하는 많은 동시 사용자를 사용 하 여 충분히 대용량 데이터 또는 사이트에 대 한 페이징 하는 경우. 이러한 상황에서는 페이징 응답 시스템을 제공 하기 위해 사용자 지정으로 설정 해야 합니다.

사용자 지정 페이징의 과제 레코드 데이터의 특정 페이지에 필요한 정확한 집합을 반환 하는 쿼리를 작성할 수 있다는 것입니다. 다행 스럽게도 Microsoft SQL Server 2005 제공 새 키워드 순위 결과 대 한 적절 한 레코드 하위 집합을 효율적으로 검색할 수는 쿼리를 작성할 수 있게 하는 합니다. 이 자습서에서는이 새 SQL Server 2005 키워드를 사용 하 여 GridView 컨트롤의 사용자 지정 페이징을 구현 하는 방법을 살펴보겠습니다. 사용자 지정 페이징에 대 한 사용자 인터페이스는 기본 페이징, 한 페이지에서 사용 하 여 다음 단계별 실행에 대 한 동일한 사용자 지정 페이징을 몇 배 많은 규모로 기본 페이징보다 더 빠르게 수 있습니다.

> [!NOTE]
> 사용자 지정 페이징을 수행 하는 정확한 성능 향상을 통해 페이징 되 고 레코드와 데이터베이스 서버에 적용 되는 부하의 총에 따라 달라 집니다. 이 자습서의 끝에 사용자 지정 페이징을 수집한 성능 이점을 보여 주는 몇 가지 대략적인 메트릭을 살펴보겠습니다.


## <a name="step-1-understanding-the-custom-paging-process"></a>1 단계: 사용자 지정 페이징 프로세스 이해

데이터를 페이징 하는 경우 페이지에 표시 되는 정확한 레코드 요청 되는 데이터 페이지 및 페이지당 표시 되는 레코드의 수에 따라 달라 집니다. 예를 들어 하 려 81 제품을 통해 페이지 페이지당 10 개 제품을 표시 한다고 가정 합니다. 첫 번째 페이지를 볼 때 d 원하는 제품 1부터 10; 두 번째 페이지를 볼 때 제품 11 통해 20, 및 등 수 d 했습니다.

검색 해야 하는 레코드 및 페이징 인터페이스 렌더링 되는 방식을 지정 하는 세 개의 변수는

- **행 인덱스 시작** 페이지에 표시할 데이터의 첫 번째 행의 인덱스; 인덱스 페이지 인덱스를 한 페이지에 표시할 레코드를 곱하여 하나를 추가 하 여 계산할 수 있습니다. 예를 들어, 첫 번째 페이지 (페이지 인덱스는 0)에 대해 한 번에 10 레코드를 페이징 하는 경우 시작 행 인덱스는 0 \* 10 + 1 또는 1입니다; 두 번째 페이지 (페이지 인덱스는 1)에 대 한 시작 행 인덱스는 1 \* 10 + 1 또는 11입니다.
- **최대 행** 페이지당 표시할 레코드의 최대 수입니다. 이 변수는 마지막에 대 한 페이지 반환 페이지 크기 보다 적은 수의 레코드 수 있으므로 최대 행 라고 합니다. 예를 들어 페이지당 10 81 제품 레코드를 통해 페이징 하는 경우 아홉 번째 및 마지막 페이지에 레코드를 하나만 갖습니다. 그러나 페이지가 없습니다. 최대 행 수 값 보다 더 많은 레코드를 표시 됩니다.
- **총 레코드 수** 통해 페이징 되 고 레코드의 총 수입니다. 이 변수 올바르지 t 필요한 지정된 된 페이지를 검색 하기 위해 레코드를 결정 하는 동안에서 페이징 인터페이스를 지정 합니다. 예를 들어, 81 제품을 통해 페이징 되 고 있으면 페이징 인터페이스 페이징 UI에서에서 9 페이지 번호 표시를 알고 있습니다.

기본 페이징을 사용 하 여 시작 하는 행 인덱스는 최대 행은 단순히 페이지 크기 페이지 인덱스 및 페이지 크기 1을 더한 값의 곱으로 계산 됩니다. 기본 페이징은에서 레코드를 모두 검색 하므로 데이터를 각 행에 대 한 인덱스의 페이지를 렌더링 하는 경우 데이터베이스 라고 용이해 간단한 작업이 시작 행 인덱스 행으로 이동 합니다. 총 레코드 수를 손쉽게 사용할 수 있으므로 또한 s DataTable (또는 데이터베이스 결과 포함 하 되 어떤 개체)의 레코드 수가 하기만 하면 됩니다.

사용자 지정 페이징 구현을 시작 하는 행 인덱스 및 최대 행 변수를 지정 하 그 후 레코드의 최대 행 수가 최대 행 시작 인덱스에서 시작 하는 레코드의 정확한 하위 집합을만 반환 해야 합니다. 사용자 지정 페이징을 두 가지 과제를 제공합니다.

- 지정된 된 시작 행 인덱스에 대 한 레코드를 반환 합니다. 시작할 수 있습니다 있도록 통해 페이징 되 고 전체 데이터의 각 행과 행 인덱스를 효율적으로 연결할 수 있어야 했습니다.
- 통해 페이징 되 고 레코드의 총 수를 제공 해야

다음 두 단계에서 이러한 두 가지 과제에 응답 하는 데 필요한 SQL 스크립트를 살펴보겠습니다. SQL 스크립트를 외에도 BLL 및 DAL에서 메서드를 구현 해야 했습니다.

## <a name="step-2-returning-the-total-number-of-records-being-paged-through"></a>2 단계를 통해 페이징 되 고 레코드의 총 수를 반환

정확 하 게 표시 되는 페이지에 대 한 레코드 하위 집합을 검색 하는 방법을 살펴보기 전에 수 s를 통해 페이징 되 고 레코드의 총 수를 반환 하는 방법을 소개 합니다. 페이징 사용자 인터페이스를 제대로 구성 하기 위해이 정보가 필요 합니다. 사용 하 여 특정 SQL 쿼리에서 반환 된 레코드의 총 수를 가져올 수 있습니다 합니다 [ `COUNT` 집계 함수](https://msdn.microsoft.com/library/ms175997.aspx)합니다. 예를 들어, 레코드의 총 수를 확인 하는 `Products` 테이블 다음 쿼리에 사용할 수 있습니다.


[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample1.sql)]

이 정보를 반환 하는 DAL에 메서드를 추가 하는 s 수 있습니다. 특히 라는 DAL 메서드를 만들겠습니다 `TotalNumberOfProducts()` 를 실행 하는 `SELECT` 위에 표시 된 문.

열어서 시작 합니다 `Northwind.xsd` 형식화 된 데이터 집합 파일에는 `App_Code/DAL` 폴더. 그런 다음 마우스 오른쪽 단추로 클릭는 `ProductsTableAdapter` 디자이너에서 쿼리 추가 선택 합니다. 대로 ve 이전 자습서에서는 표시 이렇게는 DAL에 새 메서드를 추가할 수는 특정 SQL 문이나 저장된 프로시저를 호출 하면 실행 됩니다. TableAdapter 메서드는 이전 자습서에서와 마찬가지로이 하나에 대 한 하기로 임시 SQL 문을 사용 하 여 합니다.


![임시 SQL 문을 사용 하 여](efficiently-paging-through-large-amounts-of-data-cs/_static/image1.png)

**그림 1**: 특별 SQL 문을 사용 하 여


다음 화면에서 만들 쿼리의 형식을 지정할 수 있습니다. 이 쿼리는 반환 된 단일 스칼라 값을 레코드의 총 수 있으므로 합니다 `Products` 테이블 선택는 `SELECT` 단일 값 옵션을 반환 하는 합니다.


![단일 값을 반환 하는 SELECT 문을 사용 하 여 쿼리를 구성 합니다.](efficiently-paging-through-large-amounts-of-data-cs/_static/image2.png)

**그림 2**: 단일 값을 반환 하는 SELECT 문을 사용 하 여 쿼리를 구성 합니다.


사용 하 여 쿼리의 형식을 나타내는, 후 다음 쿼리가 지정 해야 합니다.


![제품 쿼리에서 선택 그룹 사용](efficiently-paging-through-large-amounts-of-data-cs/_static/image3.png)

**그림 3**: SELECT COUNT를 사용 하 여 (\*) FROM 제품 쿼리


마지막으로, 메서드에 대 한 이름을 지정 합니다. 앞서 언급 한, s를 사용 하 여 `TotalNumberOfProducts`입니다.


![DAL 메서드 TotalNumberOfProducts 이름](efficiently-paging-through-large-amounts-of-data-cs/_static/image4.png)

**그림 4**: DAL 메서드 TotalNumberOfProducts 이름


완료를 클릭 하면 마법사가 추가 된 `TotalNumberOfProducts` DAL 방법입니다. SQL 쿼리에서 결과 경우 DAL에서 스칼라 반환 메서드 반환 nullable 형식 `NULL`합니다. 그러나 우리의 `COUNT` 쿼리,는 항상 반환 이외`NULL` DAL 메서드가 null을 허용 하는 정수를 반환 하는 하지만; 값입니다.

DAL 메서드 외에도 BLL에 메서드도 필요 했습니다. 엽니다는 `ProductsBLL` 추가한 클래스 파일을 `TotalNumberOfProducts` DAL s에을 호출 하는 메서드 `TotalNumberOfProducts` 메서드:


[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample2.cs)]

DAL s `TotalNumberOfProducts` 메서드가 null을 허용 하는 정수를 반환 하지만에서는 만든 ve 합니다 `ProductsBLL` s 클래스 `TotalNumberOfProducts` 표준 정수를 반환 하도록 메서드. 따라서 하도록 해야 합니다 `ProductsBLL` s 클래스 `TotalNumberOfProducts` DAL s에 의해 반환 된 null 허용 정수 값 부분을 반환 하는 메서드 `TotalNumberOfProducts` 메서드. 하지만에 대 한 호출 `GetValueOrDefault()` nullable 정수 이면이 있으면; null 허용 정수 값을 반환 합니다 `null`, 기본 정수 값 0을 반환 합니다.

## <a name="step-3-returning-the-precise-subset-of-records"></a>3 단계: 정확한 레코드 하위 집합 반환

다음 태스크를 시작 하는 행 인덱스를 허용 하는 BLL 및 DAL 메서드를 만들 때 및 최대 행 변수 앞에서 설명한 및 적절 한 레코드를 반환 합니다. 작업을 수행 하기 전에 let s 필요한 SQL 스크립트를 먼저 확인 합니다. Us의 당면 과제는 우리가 시작 행 인덱스 (및 레코드의 최대 레코드 수까지)를 시작 하는 해당 레코드를 반환할 수 있습니다 있도록 통해 페이징 되 고 전체 결과의 각 행에 인덱스를 효율적으로 할당할 수 이어야 합니다.

이미 있으면 열 행 인덱스로 사용 되는 데이터베이스 테이블의 문제가 아닙니다. 얼핏 보기에 우리가 생각 하는 합니다 `Products` 테이블 s `ProductID` 필드 충분할 첫 번째 제품에 `ProductID` 1, 2는 두 번째 등. 그러나 제품을 삭제 하면이 방법을 실행 하는 시퀀스에서 간격이 유지 합니다.

두 가지 일반 기술을 효율적으로 데이터를 통해 페이지를 사용 하 여 행 인덱스를 연결 하는 데 검색할 레코드의 정확한 하위 집합을 사용할 수 있게 합니다.

- **SQL Server 2005를 사용 하 `ROW_NUMBER()` 키워드** SQL Server 2005로 새는 `ROW_NUMBER()` 키워드 순위를 일정 한 순서에 따라 반환 된 각 레코드를 사용 하 여 연결 합니다. 이 순위는 각 행에 대해 행 인덱스로 사용할 수 있습니다.
- **테이블 변수를 사용 하 고 `SET ROWCOUNT`**  SQL Server s [ `SET ROWCOUNT` 문](https://msdn.microsoft.com/library/ms188774.aspx) ; 종료 하기 전에 쿼리를 처리 해야 하는 총 레코드 수를 지정 하려면 사용할 수 있습니다 [테이블 변수와](http://www.sqlteam.com/item.asp?ItemID=9454) akin를 표 형식 데이터를 보유할 수 있는 T-SQL 변수가 로컬 [임시 테이블](http://www.sqlteam.com/item.asp?ItemID=2029)합니다. 이 방법은 동일 하 게 Microsoft SQL Server 2005 및 SQL Server 2000 잘 (반면는 `ROW_NUMBER()` 방법은 SQL Server 2005 에서만 작동).  
  
  여기서 테이블 변수를 만드는 것을 `IDENTITY` 열과 해당 데이터를 통해 페이징 될 테이블의 기본 키 열입니다. 순차 행 인덱스를 연결 하므로 테이블 변수로 데이터를 통해 페이징 될 테이블의 내용을 덤프 어 (통해를 `IDENTITY` 열) 테이블의 각 레코드에 대 한 합니다. 테이블 변수의 채워진 후는 `SELECT` 문은 테이블 변수를 기본 테이블과 조인, 특정 레코드를 실행할 수 있습니다. `SET ROWCOUNT` 문을 지능적으로 테이블 변수를 덤프할 수 해야 하는 레코드의 수를 제한 하려면 사용 합니다.  
  
  이 방법은의 효율성 요청 된 페이지 번호를 기반으로 `SET ROWCOUNT` 값 행 인덱스 시작 최대 행 수를 더한 값이 할당 됩니다. 데이터의 후속 페이지를 첫 번째 페이지 낮은 번호가 매겨진 페이징할 때는이 방법은 매우 효율적입니다. 그러나 끝 페이지를 검색 하는 경우 기본 페이징와 비슷한 성능이 필요 합니다.

이 자습서를 사용 하 여 사용자 지정 페이징을 구현 된 `ROW_NUMBER()` 키워드입니다. 테이블 변수를 사용 하 여 대 한 자세한 내용은 및 `SET ROWCOUNT` 기법을 참조 하세요 [는 큰 결과 집합을 통해 페이징에 대 한 자세한 효율적인 방법은](http://www.4guysfromrolla.com/webtech/042606-1.shtml)합니다.

`ROW_NUMBER()` 키워드는 다음 구문을 사용 하 여 특정 순서를 통해 반환 된 각 레코드를 사용 하 여 순위를 연결 합니다.


[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample3.sql)]

`ROW_NUMBER()` 표시 된 순서와 관련 하 여 각 레코드에 대 한 순위를 지정 하는 숫자 값을 반환 합니다. 예를 들어, 가장에서 순서가 지정 된 각 제품에 대 한 순위를 가장 적은 비용이에서는 사용할 수 다음 쿼리.


[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample4.sql)]

그림 5의 결과 Visual Studio에서 쿼리 창을 통해 실행 하는 경우이 쿼리를 보여 줍니다. 각 행에 대 한 가격 순위를 함께 가격으로 제품으로 정렬 됨을 참고 합니다.


![가격 등급에 포함 된 각 반환 된 레코드](efficiently-paging-through-large-amounts-of-data-cs/_static/image5.png)

**그림 5**: The 가격 등급에 포함 된 각 반환 된 레코드


> [!NOTE]
> `ROW_NUMBER()` SQL Server 2005에서 사용할 수 있는 많은 새 순위 함수 중 하나일 뿐입니다. 에 대 한 자세한 설명은 `ROW_NUMBER()`, 다른 순위 함수를 함께 읽을 [Microsoft SQL Server 2005를 사용 하 여 순위 결과 반환](http://www.4guysfromrolla.com/webtech/010406-1.shtml)합니다.


지정 된 결과 순위 지정 하는 경우 `ORDER BY` 열에는 `OVER` 절 (`UnitPrice`, 위의 예에서), SQL Server에서 결과 정렬 해야 합니다. 이 빠른 작업에서 결과 정렬 열 위에 클러스터형 인덱스가 있는 경우를 다루는 경우 인덱스를 이지만 그렇지 않은 경우 더 높은 비용이 들 수 있습니다. 성능 향상을 위해 충분히 큰 쿼리에 대 한, 사용 되는 결과으로 정렬 열에 대 한 비클러스터형 인덱스를 추가 하는 것이 좋습니다. 참조 [SQL Server 2005의 성능과 순위 함수](http://www.sql-server-performance.com/ak_ranking_functions.asp) 더 자세히 살펴보고 성능 고려 사항에 대 한 합니다.

반환 된 순위 정보 `ROW_NUMBER()` 에서 직접 사용할 수는 `WHERE` 절. 하지만 파생된 테이블을 반환 사용할 수는 `ROW_NUMBER()` 한 다음에 나타날 수 있는 결과 `WHERE` 절. 예를 들어 다음 쿼리를 사용 하 여 파생된 테이블 UnitPrice 및 ProductName 열에 반환 된 `ROW_NUMBER()` 결과 사용 하 여 다음을 `WHERE` 만 가격 차수가 해당 제품을 반환 하는 절은 11 ~ 20 개 사이로:


[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample5.sql)]

이 개념을 좀 더 확장을 원하는 시작 행 인덱스 및 최대 행 값이 지정 된 데이터의 특정 페이지를 검색 하려면이 방법을 이용 하면:


[!code-html[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample6.html)]

> [!NOTE]
> 이 자습서에서는 나중에 살펴볼 합니다 *`StartRowIndex`* 제공한 ObjectDataSource 인덱싱된 0부터 시작 하는 반면는 `ROW_NUMBER()` SQL Server 2005에서 반환 된 값은 1부터 인덱싱됩니다. 따라서 합니다 `WHERE` 절 해당 레코드를 반환 합니다. 여기서 `PriceRank` 보다 엄격 하 게 크면 *`StartRowIndex`* 보다 작거나 같음 *`StartRowIndex`*  +  *`MaximumRows`*.


이제는 우리 하는 방법을 설명 하는 ve `ROW_NUMBER()` 수 시작 행 인덱스 및 최대 행 값이 지정 된 데이터의 특정 페이지를 검색 하는 데, 이제 해야 BLL 및 DAL 메서드로이 논리를 구현 합니다.

순서를 결정 해야 합니다이 쿼리를 만들 때 사용 되는 결과 순위를 지정할; s를 제품 이름별 사전순으로 정렬할 수 있습니다. 이이 자습서에서는 사용자 지정 페이징 구현에서는 됩니다 정렬할 수도 있습니다 보다는 사용자 지정 페이지 매김된 된 보고서를 만들 수 것을 의미 합니다. 다음 자습서에서는 그러나 살펴보겠습니다 어떻게 이러한 기능을 제공할 수 있습니다.

이전 섹션에서 임시 SQL 문 처럼 DAL 메서드를 생성 합니다. 아쉽게도 같은 TableAdapter 마법사 만들어지고 t에서 사용 하는 Visual Studio에서 T-SQL 파서를 `OVER` 구문에서 사용 하는 `ROW_NUMBER()` 함수입니다. 따라서이 DAL 메서드는 저장된 프로시저를 만들어야 합니다. 보기 메뉴 (또는 적중된 Ctrl + Alt + S)에서 서버 탐색기를 선택 하 고 확장 된 `NORTHWND.MDF` 노드. 새 저장된 프로시저를 추가 하려면 저장 프로시저 노드를 마우스 오른쪽 단추로 클릭 하 고 새 저장 프로시저 추가 선택 (그림 6 참조).


![새 저장된 프로시저는 제품을 통해 페이징에 대 한 추가](efficiently-paging-through-large-amounts-of-data-cs/_static/image6.png)

**그림 6**: 페이징 제품에 대 한 새 저장된 프로시저 추가


이 저장된 프로시저 두 정수 입력된 매개 변수를 수락 해야 `@startRowIndex` 및 `@maximumRows` 사용 하 여를 `ROW_NUMBER()` 함수 기준으로 정렬 합니다 `ProductName` 필드에 지정 된 것 보다 큰 행만을 반환 `@startRowIndex` 및 미만 또는 같음 `@startRowIndex`  +  `@maximumRow` s입니다. 새 저장된 프로시저에 다음 스크립트를 입력 하 고 데이터베이스에 저장된 프로시저를 추가 하려면 저장 아이콘을 클릭 합니다.


[!code-sql[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample7.sql)]

저장된 프로시저를 만든 후이 테스트 하려면 잠시 시간이 소요 됩니다. 마우스 오른쪽 단추로 클릭는 `GetProductsPaged` 저장된 프로시저는 서버 탐색기에서 이름을 지정 하 고 실행 옵션을 선택 합니다. Visual Studio 다음 묻는 입력된 매개 변수의 `@startRowIndex` 고 `@maximumRow` s (그림 7 참조). 다른 값을 사용 하 고 결과 검사 합니다.


![에 대 한 값을 입력 합니다 @startRowIndex 고 @maximumRows 매개 변수](efficiently-paging-through-large-amounts-of-data-cs/_static/image7.png)

<strong>그림 7</strong>:의 값을 입력 합니다 @startRowIndex 고 @maximumRows 매개 변수


이후에 이러한 선택 매개 변수 값을 입력, 출력 창에 결과가 표시 됩니다. 그림 8 둘 다에 대해 10에서 전달 하는 경우 결과 표시 합니다 `@startRowIndex` 및 `@maximumRows` 매개 변수.


[![반환 되는 레코드는에 표시 되는지 두 번째 데이터 페이지](efficiently-paging-through-large-amounts-of-data-cs/_static/image9.png)](efficiently-paging-through-large-amounts-of-data-cs/_static/image8.png)

**그림 8**: 반환 되는 레코드는 표시 되도록 데이터의 두 번째 페이지 ([큰 이미지를 보려면 클릭](efficiently-paging-through-large-amounts-of-data-cs/_static/image10.png))


이 사용 하 여 만든 저장 프로시저를 만들려면 준비 된 것을 `ProductsTableAdapter` 메서드. 엽니다는 `Northwind.xsd` 형식화 된 데이터 집합을 오른쪽 단추로 클릭은 `ProductsTableAdapter`, 추가 쿼리 옵션을 선택 합니다. 임시 SQL 문을 사용 하 여 쿼리를 만드는 대신 기존 저장된 프로시저를 사용 하 여 만듭니다.


![기존 저장된 프로시저를 사용 하는 DAL 메서드 만들기](efficiently-paging-through-large-amounts-of-data-cs/_static/image11.png)

**그림 9**: 기존 저장된 프로시저를 사용 하는 DAL 메서드 만들기


다음으로, 하 라는 프롬프트가 호출할 저장된 프로시저를 선택 합니다. 선택 된 `GetProductsPaged` 드롭 다운 목록에서 프로시저를 저장 합니다.


![GetProductsPaged 선택 드롭다운 목록에서 프로시저를 저장 합니다.](efficiently-paging-through-large-amounts-of-data-cs/_static/image12.png)

**그림 10**:는 GetProductsPaged 선택 드롭다운 목록에서 프로시저를 저장 합니다.


다음 화면에서 다음 묻는 어떤 종류의 데이터는 저장된 프로시저에서 반환 됩니다: 테이블 형식 데이터, 단일 값 또는 값이 없습니다. 이후를 `GetProductsPaged` 저장된 프로시저가 여러 레코드를 반환을 나타내는 표 형식 데이터를 반환 합니다.


![저장된 프로시저가 반환 테이블 형식 데이터를 나타냅니다.](efficiently-paging-through-large-amounts-of-data-cs/_static/image13.png)

**그림 11**: 저장된 프로시저가 반환 테이블 형식 데이터를 나타냅니다.


마지막으로 생성 하려는 메서드의 이름을 나타냅니다. 이전 자습서에서와 마찬가지로 계속 해 서 DataTable 채우기 모두를 사용 하 여 메서드를 만듭니다 및 DataTable을 반환 합니다. 첫 번째 메서드 이름을 `FillPaged` 하 고 두 번째 `GetProductsPaged`입니다.


![메서드 FillPaged 이름과 GetProductsPaged](efficiently-paging-through-large-amounts-of-data-cs/_static/image14.png)

**그림 12**: 메서드 FillPaged 이름과 GetProductsPaged


또한 제품의 특정 페이지를 반환 하는 DAL 메서드 생성 해야 BLL에 이러한 기능을 제공 합니다. DAL 메서드처럼 BLL의 GetProductsPaged 메서드 시작 행 인덱스 및 최대 행 수를 지정 하는 것에 대 한 두 개의 정수 입력을 수락 해야 하 고 지정된 된 범위 내에 있는 레코드만 반환 해야 합니다. 단순히에 대 한 호출은 아래로 DAL의 GetProductsPaged 메서드를 다음과 같이 ProductsBLL 클래스에는 이러한 BLL 메서드를 만듭니다.


[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample8.cs)]

모든 이름을 사용할 수 있습니다 BLL의 메서드에 입력된 매개 변수를 사용 하도록 선택 하지만, 곧 알 수 있듯이 `startRowIndex` 고 `maximumRows` 추가에서 덕분 약간의 작업이이 메서드를 사용 하는 ObjectDataSource를 구성 하는 경우.

## <a name="step-4-configuring-the-objectdatasource-to-use-custom-paging"></a>4 단계: 사용자 지정 페이징을 사용 하 여 ObjectDataSource 구성

전체 레코드의 특정 하위 집합에 액세스 하기 위한 BLL 및 DAL 메서드를 사용 하 여 사용자 지정 페이징을 사용 하 여 해당 기본 레코드를 통해 해당 페이지 제어 준비 된 GridView를 만드는 것입니다. 열어서 시작 합니다 `EfficientPaging.aspx` 페이지에 `PagingAndSorting` 폴더 페이지에 GridView를 추가 하 고 새 ObjectDataSource 컨트롤을 사용 하도록 구성 합니다. 이전 자습서에서는 종종 있었습니다 ObjectDataSource를 사용 하도록 구성 합니다 `ProductsBLL` s 클래스 `GetProducts` 메서드. 이 이때 단, 사용 하려는 합니다 `GetProductsPaged` 메서드 대신 이후 합니다 `GetProducts` 메서드가 반환 되는 *모든* 데이터베이스에서 제품의 반면 `GetProductsPaged` 레코드의 특정 하위 집합만 반환 합니다.


![S ProductsBLL 클래스 GetProductsPaged 메서드를 사용 하는 ObjectDataSource 구성](efficiently-paging-through-large-amounts-of-data-cs/_static/image15.png)

**그림 13**: ProductsBLL 클래스의 GetProductsPaged 메서드를 사용 하는 ObjectDataSource 구성


읽기 전용 GridView를 만들어 다시 우리 이후로 잠시 메서드 드롭 다운 목록에서 INSERT, UPDATE, 설정 하 고 탭 (없음)를 삭제 합니다.

다음으로 ObjectDataSource 마법사 묻는의 소스를 `GetProductsPaged` s 메서드에 `startRowIndex` 및 `maximumRows` 매개 변수 값을 입력 합니다. 이러한 입력된 매개 변수에 실제로 설정할 GridView에서 자동으로, 따라서 단순히 소스 집합 None으로 두고 마침을 클릭 합니다.


![입력된 매개 변수 원본 None으로 유지](efficiently-paging-through-large-amounts-of-data-cs/_static/image16.png)

**그림 14**: 입력된 매개 변수 원본 None으로 유지


ObjectDataSource 마법사를 완료 한 후 GridView가 BoundField 또는 CheckBoxField 제품 데이터 필드에 대해 포함 됩니다. 자유롭게 하다 면 GridView의 모양을 조정할 수 있습니다. I ve만 표시 하도록 선택한 합니다 `ProductName`, `CategoryName`, `SupplierName`, `QuantityPerUnit`, 및 `UnitPrice` BoundFields 합니다. 또한 스마트 태그의 페이징 사용 확인란을 선택 하 여 페이징을 지원 하기 위해 GridView를 구성 합니다. 이러한 변경 이후 GridView 및 ObjectDataSource 선언적 태그는 다음과 같아야 합니다.


[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample9.aspx)]

그러나 브라우저를 통해 페이지를 방문할 경우 GridView 위치가 없습니다 찾을 수 있습니다.


![GridView가 표시 되지 않음](efficiently-paging-through-large-amounts-of-data-cs/_static/image17.png)

**그림 15**: GridView가 표시 되지 않음


ObjectDataSource 현재 사용 중 이므로 0 값으로 둘 다에 대해 GridView 없습니다 합니다 `GetProductsPaged` `startRowIndex` 및 `maximumRows` 매개 변수를 입력 합니다. 따라서 없는 레코드를 반환 하는 결과 SQL 쿼리 및 따라서 GridView 표시 되지 않습니다.

이 해결 하려면 사용자 지정 페이징을 사용 하 여 ObjectDataSource 구성 해야 합니다. 다음 단계에서는이 수행할 수 있습니다.

1. **ObjectDataSource가 설정 `EnablePaging` 속성을 `true`**  이를 통과 해야 하는 ObjectDataSource에 나타냅니다 합니다 `SelectMethod` 두 개의 추가 매개 변수: 시작 하는 행 인덱스를 지정할 수 ([ `StartRowIndexParameterName` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.startrowindexparametername.aspx)), 최대 행 수를 지정 하 고 ([`MaximumRowsParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.maximumrowsparametername.aspx)).
2. **ObjectDataSource가 설정 `StartRowIndexParameterName` 및 `MaximumRowsParameterName` 그에 따라 속성** 는 `StartRowIndexParameterName` 및 `MaximumRowsParameterName` 속성에 전달 된 입력된 매개 변수의 이름을 나타냅니다는 `SelectMethod` 사용자 지정 페이징 목적입니다. 기본적으로 이러한 매개 변수 이름은 `startIndexRow` 및 `maximumRows`, 하는 것을 만들 때는 `GetProductsPaged` 메서드 BLL은 입력된 매개 변수의이 값 사용. BLL s에 대해 다른 매개 변수 이름을 사용 하도록 선택한 경우 `GetProductsPaged` 메서드와 같은 `startIndex` 하 고 `maxRows`ObjectDataSource s를 설정 해야 하는 예제에 대 한 `StartRowIndexParameterName` 및 `MaximumRowsParameterName` 속성 적절 하 게 (예:에 대 한 startIndex `StartRowIndexParameterName` 및에 대 한 maxRows `MaximumRowsParameterName`).
3. **집합 ObjectDataSource s [ `SelectCountMethod` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selectcountmethod(VS.80).aspx) 의 총 수의 레코드 중 페이징 통해 반환 되는 메서드의 이름 (`TotalNumberOfProducts`)** 이전에 설명한 대로 `ProductsBLL`의 클래스`TotalNumberOfProducts`메서드를 실행 하는 DAL 메서드를 사용 하 여 페이징 되 고 레코드의 총 수를 반환 합니다.는 `SELECT COUNT(*) FROM Products` 쿼리 합니다. 이 정보는 ObjectDataSource 올바르게 페이징 인터페이스를 렌더링 하기 위해 필요 합니다.
4. **제거 합니다 `startRowIndex` 하 고 `maximumRows` `<asp:Parameter>` ObjectDataSource가 선언적 태그의에서 요소** ObjectDataSource 마법사를 통해 구성에 Visual Studio 자동으로 추가 두 `<asp:Parameter>` 요소 에 대 한는 `GetProductsPaged`의 메서드 매개 변수를 입력 합니다. 설정 하 여 `EnablePaging` 에 `true`, 이러한 매개 변수를 자동으로 전달 됩니다; ObjectDataSource 전달 하려고도 선언적 구문에 표시 된 *4* 매개 변수는 `GetProductsPaged` 메서드 하는 두 매개 변수는 `TotalNumberOfProducts` 메서드. 이 제거 해야 하는 경우 `<asp:Parameter>` 요소와 같은 오류 메시지를 얻게 되는 브라우저를 통해 페이지를 방문 하는 경우: *ObjectDataSource 'ObjectDataSource1' 찾을 수 없습니다는 제네릭이 아닌 메서드는 ' TotalNumberOfProducts' 매개 변수: startRowIndex, maximumRows*합니다.

다음과 같이 변경한 후 ObjectDataSource가 선언적 구문을 다음과 같이 표시 됩니다.


[!code-aspx[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample10.aspx)]

합니다 `EnablePaging` 하 고 `SelectCountMethod` 속성이 설정 되어 있는지 및 `<asp:Parameter>` 요소가 제거 되었습니다. 그림 16에서는 이러한 변경이 이루어진 후 속성 창의 스크린 샷이 보여 줍니다.


![사용자 지정 페이징을 사용 하려면 ObjectDataSource 컨트롤 구성](efficiently-paging-through-large-amounts-of-data-cs/_static/image18.png)

**그림 16**: 사용자 지정 페이징을 사용 하려면 ObjectDataSource 컨트롤 구성


다음과 같이 변경한 후 브라우저를 통해이 페이지를 방문 합니다. 10 개의 제품이 나열, 표시 사전순으로 정렬 합니다. 시간을 내어 한 번에 데이터 한 페이지를 단계별로 실행 합니다. 지정된 된 페이지에 대 한 표시 해야 하는 레코드만 검색으로 visual 차이가 없습니다 최종 사용자가의 관점에서 기본 페이징 및 사용자 지정 페이징을 상태인 동안 많은 양의 데이터를 통해 페이지 보다 효율적으로 사용자 지정 페이징 합니다.


[![데이터, Ordered의 이름, 제품에는 사용 하 여 사용자 지정 페이징 페이징](efficiently-paging-through-large-amounts-of-data-cs/_static/image20.png)](efficiently-paging-through-large-amounts-of-data-cs/_static/image19.png)

**그림 17**: 데이터, Ordered의 이름, 제품에는 사용 하 여 사용자 지정 페이징 페이징 ([큰 이미지를 보려면 클릭](efficiently-paging-through-large-amounts-of-data-cs/_static/image21.png))


> [!NOTE]
> 사용자 지정 페이징을 사용 하 여 페이지 수는 ObjectDataSource가 반환한 값 `SelectCountMethod` GridView가의 뷰 상태에 저장 됩니다. 다른 GridView 변수를 `PageIndex`, `EditIndex`를 `SelectedIndex`를 `DataKeys` 등에 컬렉션에 저장 됩니다 *상태를 제어*를 GridView s의 값에 관계 없이 유지 되는 `EnableViewState` 속성입니다. 하므로 `PageCount` 값은 유지 게시할 마지막 페이지로 이동 하는 링크가 포함 된 페이징 인터페이스를 사용 하는 경우에 상태 보기를 사용 하 여 반드시 GridView가의 뷰 상태를 사용할 수 있습니다. (페이징 인터페이스에 대 한 직접 링크를 마지막 포함 되지 않은 경우 페이지의 뷰 상태를 비활성화할 수 있습니다.)


포스트백을 발생 시키는 마지막 페이지 링크를 클릭 하 고 업데이트 GridView 지시 해당 `PageIndex` 속성입니다. 마지막 페이지 링크를 클릭 하면 GridView 할당 해당 `PageIndex` 속성을 하나 값 보다 작은 해당 `PageCount` 속성입니다. 비활성화 상태 보기를 사용 하 여는 `PageCount` 게시할 손실 되는 값 및 `PageIndex` 대신 최대 정수 값이 할당 됩니다. GridView를 곱하여 시작 행 인덱스를 확인 하려고 하는 다음에 `PageSize` 및 `PageCount` 속성입니다. 이 인해는 `OverflowException` 제품 허용 되는 최대 정수 크기를 초과 하므로 합니다.

## <a name="implement-custom-paging-and-sorting"></a>구현 사용자 지정 페이징 및 정렬

현재 사용자 지정 페이징 구현을 통해 데이터 페이징 되는 순서를 만들 때 정적으로 지정할 필요는 `GetProductsPaged` 저장 프로시저입니다. 그러나 있습니다 기록한 GridView가 스마트 태그에는 페이징 사용 옵션 외에 정렬 사용 확인란을 선택 합니다. 아쉽게도 현재 사용자 지정 페이징 구현 GridView에 정렬 지원을 추가 데이터의 현재 표시 된 페이지의 레코드를 정렬만 됩니다. 예를 들어, 또한 페이징을 지원 하 여 데이터의 첫 번째 페이지를 볼 때 제품 이름을 내림차순으로 정렬 하는 다음 GridView를 구성 하는 경우 1 페이지에서 제품의 순서를 반대로 것입니다. 그림 18에서 볼 수 있듯이 이러한 카 호랑이로 표시 첫 번째 제품 71 다른 제품 다음에 오는 카 호랑이 사전순으로; 무시 하는 역방향 알파벳 순으로 정렬 하는 경우 정렬에서 첫 번째 페이지의 레코드만 간주 됩니다.


[![정렬 되는 데이터에만 표시 현재 페이지](efficiently-paging-through-large-amounts-of-data-cs/_static/image23.png)](efficiently-paging-through-large-amounts-of-data-cs/_static/image22.png)

**그림 18**: 정렬 되는 데이터에만 표시 현재 페이지 ([큰 이미지를 보려면 클릭](efficiently-paging-through-large-amounts-of-data-cs/_static/image24.png))


데이터가 BLL s에서 검색 된 후 발생 정렬 하기 때문에 데이터의 현재 페이지에만 적용 정렬 `GetProductsPaged` 메서드와이 메서드가 특정 페이지에 대해 해당 레코드를 반환 합니다. 올바르게 정렬를 구현 하려면 정렬 식을 전달 해야 합니다 `GetProductsPaged` 메서드 데이터의 특정 페이지를 반환 하기 전에 데이터를 적절 하 게 순위 수 있도록 합니다. 다음 자습서에서이 작업을 수행 하는 방법을 살펴보겠습니다.

## <a name="implementing-custom-paging-and-deleting"></a>사용자 지정 페이징 및 삭제를 구현 합니다.

마지막 페이지에서 마지막 레코드를 삭제 하는 경우 볼 수 있습니다 하는 사용자 지정 페이징 기술을 사용 하 여 데이터 페이징 되는 GridView에서 삭제 기능을 사용 하도록 설정 하는 GridView 사라집니다 적절 하 게 감소 하는 대신 GridView의 `PageIndex`. 이 버그를 재현 하려면 방금 우리가 방금 전에 만든 자습서에 대 한 삭제를 사용 하도록 설정 합니다. 81 제품을 한 번에 10 개 제품을 통해 페이징 하는 것 이므로 단일 제품에 표시 됩니다는 여기서 마지막 페이지 (페이지 9)로 이동 합니다. 이 제품을 삭제 합니다.

마지막으로 제품을 GridView를 삭제 하면 *해야* 여덟 번째 페이지로 자동으로 이동 하 고 이러한 기능은 기본 페이징을 사용 하 여 직접 제작한 잠금에서 합니다. 그러나 사용자 지정 페이징을 사용 하 여 마지막 페이지에서 마지막 제품을 삭제 한 후 GridView 단순히이 화면에서 사라지면 완전히 합니다. 정확한 원인을 *이유* 은이 자습서에서 다루지 bit 이런; 참조 [GridView를 사용 하 여 사용자 지정 페이징의 마지막 페이지에 있는 마지막 레코드를 삭제](http://scottonwriting.net/sowblog/posts/7326.aspx) 의 원본에 대 한 하위 수준 세부 정보에 대 한 이 문제입니다. 요약 하자면에서이 삭제 단추를 클릭할 때 GridView에서 수행 되는 단계의 다음 시퀀스에서는 인해 s:

1. 레코드 삭제
2. 지정 된 표시 하려면 적절 한 레코드를 가져올 `PageIndex` 및 `PageSize`
3. 않았는지 확인 합니다 `PageIndex` GridView가 자동으로 감소 시킵니다 수행 하는 경우 데이터 소스에서 데이터 페이지 수를 넘지 않는 `PageIndex` 속성
4. 2 단계에서에서 가져온 레코드를 사용 하 여 GridView에 적절 한 데이터 페이지를 바인딩

2 단계는 사실에서 형태소 분석 문제를 `PageIndex` 때 표시할 레코드를 클릭 한 다음 계속 사용 합니다 `PageIndex` 유일한 레코드 삭제 된 마지막 페이지의 합니다. 2 단계에 따라서 *없습니다* 데이터의 마지막 페이지에는 더 이상 레코드가 포함 되어 있으므로 레코드가 반환 됩니다. 그런 다음 3 단계에서에서 GridView를 인식 하는 해당 `PageIndex` 속성은 데이터 원본에는 페이지의 총 수보다 큽니다 (이후로 ve 삭제 마지막 페이지에 있는 마지막 레코드) 및 감소 하므로 해당 `PageIndex` 속성. 4 단계에서에서 2 단계;에서 검색 되는 데이터에 자신을 바인딩하도록 GridView 시도 그러나 반환 된 레코드가 2 단계에서 따라서 그 결과 빈 GridView입니다. 기본 페이징을 사용 하 여이 문제가 되지 않습니다 t 노출 하기 때문에 2 단계 *모든* 데이터 원본의 레코드를 검색 합니다.

이 문제를 해결 하는 두 가지 옵션이 했습니다. 첫 번째는 GridView s에 대 한 이벤트 처리기를 만들려면 `RowDeleted` 만 삭제 된 페이지에 표시 된 레코드 수를 결정 하는 이벤트 처리기입니다. 했습니다. 하나의 레코드를 삭제 하는 레코드 받아야 마지막 고 GridView가 감소 해야 `PageIndex`합니다. 물론 집합만 업데이트는 `PageIndex` 삭제 작업이 실제로 성공 하면 얻는 없도록 함으로써 합니다 `e.Exception` 속성은 `null`합니다.

이 방법은 업데이트 하기 때문에 `PageIndex` 1 단계 후 하지만 2 단계 전에 합니다. 따라서 2 단계에서에서 적절 한 레코드 집합이 반환 됩니다. 이렇게 하려면 다음과 같은 코드를 사용 합니다.


[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample11.cs)]

다른 해결 방법은 ObjectDataSource s에 대 한 이벤트 처리기를 만들려면 `RowDeleted` 이벤트 및 설정 하는 `AffectedRows` 속성 값이 1 합니다. GridView 업데이트 1 단계에서에서 (하지만 다시 2 단계에서에서 데이터를 검색 하기 전에) 레코드를 삭제 한 후 해당 `PageIndex` 속성 작업에 의해 영향을 받은 하나 이상의 행 하는 경우. 그러나는 `AffectedRows` ObjectDataSource가 속성을 설정 하지 않은 하 고 따라서이 단계를 생략 하면 됩니다. 이 단계를 실행 하는 한 가지 방법은 수동으로 설정 하는 것은 `AffectedRows` 삭제 작업이 성공적으로 완료 되 면 속성입니다. 다음과 같은 코드를 사용 하 여 수행할 수 있습니다.


[!code-csharp[Main](efficiently-paging-through-large-amounts-of-data-cs/samples/sample12.cs)]

코드 숨김 클래스에서 이러한 이벤트 처리기의 둘 다에 대 한 코드를 찾을 수 있습니다는 `EfficientPaging.aspx` 예제입니다.

## <a name="comparing-the-performance-of-default-and-custom-paging"></a>기본 및 사용자 지정 페이징의 성능 비교

기본 페이징은 반환 하는 반면 에서만 사용자 지정 페이징을 필요한 레코드를 검색 하므로 *모든* 표시 되는 각 페이지에 대 한 레코드의 해당 s 사용자 지정 페이징을 기본 페이징은 보다 더 효율적 임을 선택을 취소 합니다. 그러나 훨씬 더 효율적으로 사용자 지정 페이징을? 사용자 지정 페이징을 기본 페이징에서 이동 하 여 어떤 종류의 성능 향상을 확인할 수 있습니다?

아쉽게도 있는 s 상황에 맞는 모든 여기에 답변 합니다. 다양 한 요인에 따라 달라 집니다 성능 향상, 웹 서버와 데이터베이스 서버 간의 데이터베이스 서버와 통신 채널을 통해 페이징 되 고 레코드와 로드 기간 두가 배치 가장 두드러진 합니다. 소수의 수십 개의 레코드를 사용 하 여 작은 테이블에 대 한 성능 차이 무시할 수 있습니다. 그러나 수천 개의 행을 수백 수천 개의 대형 테이블에 대 한 성능 차이 예입니다.

필자의 아티클을 [SQL Server 2005를 사용 하 여 ASP.NET 2.0의 사용자 지정 페이징](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx), 데이터베이스 테이블에 페이징 하는 경우 이러한 두 페이징 기술 간 성능 차이 보이게 필자는 몇 가지 성능 테스트가 포함 50,000 개의 레코드입니다. 이러한 테스트에서 SQL Server 수준에서 쿼리를 실행 하는 시간이 모두 살펴봤습니다 (사용 하 여 [SQL Profiler](https://msdn.microsoft.com/library/ms173757.aspx)) 및 사용 하 여 ASP.NET 페이지 [ASP.NET 추적 기능](https://msdn.microsoft.com/library/y13fw6we.aspx)합니다. 이러한 테스트 단일 활성 사용자를 사용 하 여 개발 상자 내에서 실행 된 및 따라서 과학 없는 일반적인 웹 사이트 부하 패턴을 모방 하지 마십시오 염두에서에 둡니다. 그럼에도 불구 하 고 결과 충분히 많은 양의 데이터를 사용 하 여 작업 하는 경우 기본 인스턴스 및 사용자 지정 페이징을 실행 시간이 상대 차이점을 설명 합니다.


|  | **평균 기간 (초)** | **읽기** |
| --- | --- | --- |
| **기본 SQL Profiler 페이징** | 1.411 | 383 |
| **사용자 지정 페이징 SQL Profiler** | 0.002 | 29 |
| **기본 페이징 ASP.NET 추적** | 2.379 | *해당 없음* |
| **사용자 지정 페이징 ASP.NET 추적** | 0.029 | *해당 없음* |


알 수 있듯이 평균 읽기 덜 354 필요한 데이터의 특정 페이지를 검색 하 고 시간에 비해 훨씬 빨리 완료 됩니다. ASP.NET 페이지에서 사용자 지정 페이지 있었습니다 1/100에 가까우면에 렌더링할<sup>번째</sup> 기본 페이징을 사용 하는 경우 걸린 시간입니다. 참조 [필자의 기사](http://aspnet.4guysfromrolla.com/articles/031506-1.aspx) 코드 및 데이터베이스와 함께 이러한 결과 대 한 자세한 내용은 자신의 환경에서 이러한 테스트를 재현 하는 다운로드할 수 있습니다.

## <a name="summary"></a>요약

기본 페이징은 데이터 웹 컨트롤 s 스마트 태그에만 확인 페이징 사용 확인란을 구현 하기가 매우 쉽습니다 이지만 성능 하더라도 이러한 단순성을 제공 합니다. 사용자 데이터의 모든 페이지를 요청할 때 기본 페이징을 *모든* 정도의 작은 일부만 표시 될 수 있지만 레코드가 반환 됩니다. 이 성능 오버 헤드를 방지 하기 위해 ObjectDataSource를 대체 페이징 옵션 사용자 지정 페이징을 제공 합니다.

사용자 지정 페이징을 표시 되어야 하는 레코드를 검색 하 여 s 성능 문제를 페이징 하는 기본 특징을 향상 하는 동안 해당 s 사용자 지정 페이징을 구현 하기가 더 복잡된 합니다. 먼저 (올바르고 효율적으로)에 액세스 하는 요청 되는 레코드의 특정 하위 집합 쿼리를 작성 되어야 합니다. 다양 한 방법으로;에서이 작업을 수행할 수 있습니다. 새 SQL Server 2005 s를 사용 하는이 자습서에서는 검사할 것 `ROW_NUMBER()` 순위를 매기는 함수 결과 한 다음만 반환할 결과 해당 순위 지정된 된 범위에 속합니다. 또한를 통해 페이징 되 고 레코드의 총 수를 확인 하는 수단을 추가 해야 합니다. 이러한 BLL 및 DAL 메서드를 만든 후도 총 레코드 수를 통해 페이징 되는 및 BLL에 시작 하는 행 인덱스 및 최대 행 수 값을 전달 올바르게 수를 알 수 있도록 ObjectDataSource를 구성 해야 합니다.

사용자 지정 페이징을 구현 단계 수가 필요가 고 아니더라도 기본 페이징은 하기만 하는 동안 사용자 지정 페이징을 충분히 많은 양의 데이터를 페이징 하는 경우 반드시 필요 합니다. 결과 검사 따르면, 사용자 지정 페이징 ASP.NET 페이지의 렌더링 시간에서 초를 버릴 수 하 고 하나 이상의 엄청나게 데이터베이스 서버의 부하를 옅게 나타낼 수 있습니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](paging-and-sorting-report-data-cs.md)
> [다음](sorting-custom-paged-data-cs.md)
