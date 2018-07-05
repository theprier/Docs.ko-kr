---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs
title: 구현 하는 낙관적 동시성 (C#) | Microsoft Docs
author: rick-anderson
description: 여러 사용자가 데이터를 편집할 수 있도록 웹 응용 프로그램에 두 사용자가 편집 하 고 동일한 데이터를 동시에 위험이 있습니다. 이 tutori에서 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/17/2006
ms.topic: article
ms.assetid: 56e15b33-93b8-43ad-8e19-44c6647ea05c
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs
msc.type: authoredcontent
ms.openlocfilehash: 120fdca43b7e68127277f6889504f173938117e4
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37397774"
---
<a name="implementing-optimistic-concurrency-c"></a>낙관적 동시성 구현 (C#)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_21_CS.exe) 또는 [PDF 다운로드](implementing-optimistic-concurrency-cs/_static/datatutorial21cs1.pdf)

> 여러 사용자가 데이터를 편집할 수 있도록 웹 응용 프로그램에 두 사용자가 편집 하 고 동일한 데이터를 동시에 위험이 있습니다. 이 자습서에서는 이러한 위험을 처리 하는 낙관적 동시성 제어를 구현 하겠습니다.


## <a name="introduction"></a>소개

에 데이터를 볼 수 있도록 하는 웹 응용 프로그램 또는 데이터를 수정할 수 있는 단일 사용자만 포함 하는 경우 실수로 다른의 변경 내용을 덮어쓰지 두 개의 동시 사용자 위험이 없는 합니다. 여러 사용자가 데이터를 업데이트 또는 삭제를 허용 하는 웹 응용 프로그램에 대 한 그런데 다른 동시 사용자와 충돌 한 사용자의 수정 가능성입니다. 원위치에서 동시성 정책 없이 두 명의 사용자가 동시에 단일 레코드를 편집 하는 경우 사용자가 자신의 변경 내용을 커밋합니다 마지막 재정의 첫 번째 변경 합니다.

예를 들어는 두 사용자 Jisun과 Sam 된 모두 페이지를 방문 하는 업데이트 및 GridView 컨트롤을 통해 제품을 삭제 하는 방문자를 허용 하는 응용 프로그램에서 한다고 가정 합니다. 둘 다 동시에 GridView의 편집 단추를 클릭 합니다. Jisun 제품 이름을 "Chai Tea"로 변경 하 고 [업데이트] 단추를 클릭 합니다. 최종적인 결론은는 `UPDATE` 를 설정 하는 데이터베이스에 전송 되는 문 *모든* 제품의 업데이트 가능한 필드 (Jisun 단일 필드를 업데이트 하는 경우에 `ProductName`). 이 시점에서, 데이터베이스에 값 "Chai 차를" 음료, 공급 업체 특이 한 액체 등이 특정 제품 범주 그러나 Sam의 화면에서 GridView 여전히 제품 이름을 표시 편집 가능한 GridView 행에서 "Chai"으로 합니다. 몇 초 후 Jisun의 변경 사항이 커밋되기 Sam 입력 하면 조미료에 범주를 업데이트 하 고 업데이트를 클릭 합니다. 이 인해를 `UPDATE` "Chai" 제품 이름을 설정 하는 데이터베이스에 전송 하는 문을 `CategoryID` 해당 음료 범주 ID 및 등입니다. 제품 이름을 Jisun의 변경 내용은 덮어썼습니다. 그림 1이이 일련을의 이벤트를 그래픽으로 보여 줍니다.


[![두 명의 사용자가 동시에 레코드를 업데이트 하는 경우 있습니다 s 잠재적인 사용자 s에 대 한 변경을 다른를 덮어쓰려면](implementing-optimistic-concurrency-cs/_static/image2.png)](implementing-optimistic-concurrency-cs/_static/image1.png)

**그림 1**: 다른 덮어쓰기 때 두 사용자가 동시에 업데이트를 레코드 있습니다 s 잠재적 사용자 s에 대 한 변경 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image3.png))


마찬가지로, 두 명의 사용자가 페이지를 방문 하는 한 명의 사용자는 다른 사용자에 의해 삭제 될 때 레코드를 업데이트 하는 도중 수 있습니다. 또는 사용자 페이지를 로드 하는 경우이 고 삭제 단추를 클릭 하면 이면 다른 사용자가 변경 했습니다 해당 레코드의 콘텐츠입니다.

세 가지 [동시성 제어](http://en.wikipedia.org/wiki/Concurrency_control) 전략을 사용할 수 있습니다.

- **아무 작업도 수행** -동시 사용자가 동일한 레코드를 수정 하는 경우 (기본 동작) win 마지막 커밋 수
- [**낙관적 동시성** ](http://en.wikipedia.org/wiki/Optimistic_concurrency_control) -있을 동시성 충돌 합니다, 대부분의 경우 이러한 충돌이 발생 하지 않습니다; 따라서는 충돌이 발생 하는 경우 단순히에 게 사용자를 가정 하는 해당 변경 내용 다른 사용자가 동일한 데이터를 수정 하기 때문에 저장할 수 없습니다.
- **비관적 동시성** -동시성 충돌은 일반적 이며 다른 사용자의 동시 작업으로 인해 해당 변경 내용이 저장 되지 않은 총 사용자가 되 고를 허용 하지 않습니다는 가정; 하나의 사용자 레코드 업데이트 시작 되 면 따라서 잠그지 를 편집 하거나 사용자가 수정 커밋될 때까지 해당 레코드를 삭제 하면 다른 사용자가 차단

기본 동시성 확인 전략 사용한 지금이 자습서의 모든-즉, 마지막으로 쓴 승리 하도록 했습니다. 이 자습서에서는 낙관적 동시성 제어를 구현 하는 방법을 검토 합니다.

> [!NOTE]
> 이 자습서 시리즈의 예제를 비관적 동시성에 살펴봅니다 하지 않습니다. 비관적 동시성 거의 같은 잠그므로 없으면 제대로 무시를 사용할 다른 사용자에 게 데이터를 업데이트 하지 못할 수 있습니다. 예를 들어 사용자 편집에 대 한 레코드를 잠그고 잠금을 해제 하기 전에 해당 요일의 유지 한 다음, 하는 경우 다른 사용자는 원래 사용자 반환 하 고 자신의 업데이트를 완료 될 때까지 해당 레코드를 업데이트할 수 됩니다. 따라서 비관적 동시성은 사용 하는 경우에는 일반적으로 시간 제한에 도달 하면 잠금 취소 하는 합니다. 티켓 판매 있는 웹 사이트 사용자는 주문 프로세스를 완료 하는 동안 짧은 기간 동안 특정 좌석 배정 위치 잠금에 비관적 동시성 제어의 예시입니다.


## <a name="step-1-looking-at-how-optimistic-concurrency-is-implemented"></a>1 단계: 어떻게 낙관적 동시성을 살펴보면 구현

낙관적 동시성 제어 업데이트나 삭제 프로세스를 시작 하는 경우와 마찬가지로 업데이트 되거나 삭제 된 레코드에 동일한 값 함으로써 작동 합니다. 예를 들어,는 편집 가능한 GridView의 편집 단추를 클릭 하는 경우 레코드의 값은 데이터베이스에서 읽고 텍스트 상자 및 기타 웹 컨트롤에 표시 합니다. GridView에서 원래 값이 저장 됩니다. 나중에 사용자 자신의 변경 하 고 [업데이트] 단추를 클릭 한 후 원래 값 및 새 값 보내집니다 비즈니스 논리 계층으로 이동한 다음 데이터 액세스 계층. 데이터 액세스 계층에는 사용자 편집을 시작 하는 원래 값은 데이터베이스에서 값과 동일 하는 경우에 레코드를 업데이트는 SQL 문을 실행 해야 합니다. 그림 2에서는이 이벤트 시퀀스를 보여 줍니다.


[![성공 하려면 업데이트 또는 삭제, 원래 값을 현재 데이터베이스 값 이어야 합니다.](implementing-optimistic-concurrency-cs/_static/image5.png)](implementing-optimistic-concurrency-cs/_static/image4.png)

**그림 2**:에 대 한 업데이트 또는 삭제 성공에는 원래 값 해야 수 값과 같은 현재 데이터베이스를 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image6.png))


낙관적 동시성을 구현 하는 방법은 여러 가지가 있습니다 (참조 [Peter A. Bromberg](http://peterbromberg.net/)의 [Optmistic 동시성 업데이트 논리](http://www.eggheadcafe.com/articles/20050719.asp) 간략히 다양 한 옵션에 대 한). ADO.NET 입력 데이터 집합에는 확인란의 눈금만 사용 하 여 구성할 수 있는 한 구현을 제공 합니다. 입력 데이터 집합의 TableAdapter 보강 TableAdapter의 낙관적 동시성을 사용 하도록 설정 `UPDATE` 하 고 `DELETE` 모든의 원래 값의 비교를 포함 하도록 문을 `WHERE` 절. 다음 `UPDATE` 문을 현재 데이터베이스 값 GridView에서 레코드를 업데이트 하는 경우 원래 검색 된 값과 같은 경우에 해당 이름 및 제품의 가격을 예를 들어 업데이트 합니다. `@ProductName` 및 `@UnitPrice` 반면 매개 변수는 사용자가 입력 한 새 값이 포함 `@original_ProductName` 및 `@original_UnitPrice` 편집 단추를 클릭할 때 GridView에 원래 로드 된 값을 포함 합니다.


[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample1.sql)]

> [!NOTE]
> 이 `UPDATE` 문을 읽기 쉽도록 간소화 되었습니다. 실제로 `UnitPrice` 체크 인를 `WHERE` 절 이후 더 개입 됩니다 `UnitPrice` 포함 될 수 있습니다 `NULL` 가 고 있는지 확인 `NULL = NULL` 항상 False를 반환 합니다 (대신 사용 해야 `IS NULL`).


다른 기본을 사용 하는 것 외에도 `UPDATE` 낙관적 동시성에도 해당 DB 서명의 수정 TableAdapter를 구성 하는 문을 직접 메서드. 첫 번째 자습서에서 설명한 대로 [ *데이터 액세스 레이어 만들기*](../introduction/creating-a-data-access-layer-cs.md), 입력된 매개 변수로 값 DB 직접 메서드 스칼라의 목록을 수락 하는 되었는지 (강력한 DataRow 대신 또는 DataTable 인스턴스)입니다. 낙관적 동시성을 직접 DB를 사용 하는 경우 `Update()` 고 `Delete()` 메서드는 원래 값에 대 한 입력된 매개 변수를 포함 합니다. 일괄 처리를 사용 하 여에 대 한 BLL의 코드 패턴을 업데이트 하는 또한 (의 `Update()` 스칼라 값 보다는 Datarow Datatable을 허용 하는 메서드 오버 로드)도 변경 해야 합니다.

대신이 기존 확장 보다 보겠습니다 (BLL에 맞게 변경 해야)는 낙관적 동시성을 사용 하는 DAL의 Tableadapter 대신 새 형식화 된 데이터 집합을 만들려면 라는 `NorthwindOptimisticConcurrency`를 추가 하는 한 `Products` TableAdapter는 낙관적 동시성을 사용합니다. 그런 다음, 만듭니다는 `ProductsOptimisticConcurrencyBLL` 낙관적 동시성 DAL을 지원 하도록 적절 하 게 수정 된 비즈니스 논리 계층 클래스입니다. 이 전에 살펴본 후에 ASP.NET 페이지를 만들 준비가 드리겠습니다.

## <a name="step-2-creating-a-data-access-layer-that-supports-optimistic-concurrency"></a>2 단계: 낙관적 동시성을 지 원하는 데이터 액세스 레이어 만들기

새 입력 데이터 집합을 만들려면 마우스 오른쪽 단추로 클릭 합니다 `DAL` 내의 폴더를 `App_Code` 폴더 라는 새 데이터 집합을 추가 하 고 `NorthwindOptimisticConcurrency`입니다. 첫 번째 자습서에서 살펴본 것 처럼 수행 하므로 추가 새 TableAdapter를 형식화 된 데이터 집합을 자동으로 TableAdapter 구성 마법사를 시작 합니다. 첫 번째 화면에서 우리가 하 라는 메시지가 나타나면 데이터베이스에 연결 하 여 동일한 Northwind 데이터베이스에 연결-를 지정 합니다 `NORTHWNDConnectionString` 설정에서 `Web.config`합니다.


[![동일한 Northwind 데이터베이스에 연결](implementing-optimistic-concurrency-cs/_static/image8.png)](implementing-optimistic-concurrency-cs/_static/image7.png)

**그림 3**: 동일한 Northwind 데이터베이스에 연결 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image9.png))


다음으로 데이터를 쿼리 하는 방법에 대 한 프롬프트가:를 임시 SQL 문을 통해 새 저장 프로시저 또는 기존 저장 프로시저입니다. 우리의 원래 DAL에서 임시 SQL 쿼리를 사용 하므로이 옵션 여기도 사용 합니다.


[![임시 SQL 문을 사용 하 여 검색할 데이터를 지정 합니다.](implementing-optimistic-concurrency-cs/_static/image11.png)](implementing-optimistic-concurrency-cs/_static/image10.png)

**그림 4**: 데이터를 임시 SQL 문을 사용 하 여 검색 지정 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image12.png))


다음 화면에서 제품 정보를 검색 하는 데 SQL 쿼리를 입력 합니다. 에 사용 되는 정확히 동일한 SQL 쿼리를 사용 하겠습니다 합니다 `Products` 일부만 반환 하는 우리의 원래 DAL에서 TableAdapter를 `Product` 제품의 공급자 및 범주 이름과 함께 열:


[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample2.sql)]


[![원래 DAL에서 제품 TableAdapter에서 같은 SQL 쿼리를 사용 합니다.](implementing-optimistic-concurrency-cs/_static/image14.png)](implementing-optimistic-concurrency-cs/_static/image13.png)

**그림 5**:에서 같은 SQL 쿼리를 사용 합니다 `Products` 원래 DAL에서 TableAdapter ([클릭 하 여 큰 이미지 보기](implementing-optimistic-concurrency-cs/_static/image15.png))


다음 화면으로 이동 하기 전에 고급 옵션 단추를 클릭 합니다. 이 TableAdapter 사용 낙관적 동시성 제어 하도록 단순히 "낙관적 동시성 사용" 확인란을 확인 합니다.


[![검사 하 여 낙관적 동시성 제어를 사용 하도록 설정 합니다 &quot;낙관적 동시성을 사용 하 여&quot; 확인란](implementing-optimistic-concurrency-cs/_static/image17.png)](implementing-optimistic-concurrency-cs/_static/image16.png)

**그림 6**: "낙관적 동시성 사용" 확인란을 선택 하 여 낙관적 동시성 제어를 사용 하도록 설정 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image18.png))


마지막으로, TableAdapter DataTable 채우기와; DataTable을 반환 하는 데이터 액세스 패턴을 사용 해야 함을 나타내려면 또한 DB 직접 메서드를 만들어야 함을 나타냅니다. 메서드 이름을 변경 반환 DataTable 패턴 getdata에서 우리의 원래 DAL에서 사용한 명명 규칙을 반영 하도록 GetProducts를 합니다.


[![모든 데이터 액세스 패턴을 활용 하는 TableAdapter가](implementing-optimistic-concurrency-cs/_static/image20.png)](implementing-optimistic-concurrency-cs/_static/image19.png)

**그림 7**: TableAdapter 사용할 모든 데이터 액세스 패턴에 있는 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image21.png))


강력한 형식의 데이터 집합 디자이너를 포함 하는 마법사를 완료 한 후 `Products` DataTable 및 TableAdapter. DataTable에서 이름을 바꾸려면 잠시 `Products` 에 `ProductsOptimisticConcurrency`, DataTable의 제목 표시줄을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 이름 바꾸기를 선택 하 여 수행할 수 있습니다.


[![DataTable 및 TableAdapter 형식화 된 데이터 집합에 추가 되었습니다.](implementing-optimistic-concurrency-cs/_static/image23.png)](implementing-optimistic-concurrency-cs/_static/image22.png)

**그림 8**:는 DataTable 및 TableAdapter 형식화 된 데이터 집합에 추가 되었습니다 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image24.png))


간의 차이점을 볼 수는 `UPDATE` 및 `DELETE` 간에 쿼리를 `ProductsOptimisticConcurrency` TableAdapter (사용 하는 낙관적 동시성) 및 (하지 않습니다)는 제품 TableAdapter를 TableAdapter 클릭 하 고 속성 창으로 이동 합니다. 에 `DeleteCommand` 하 고 `UpdateCommand` 속성 `CommandText` 하위 DAL의 업데이트나 삭제 관련 메서드를 호출할 때 데이터베이스에 전송 되는 실제 SQL 구문을 볼 수 있습니다. 에 대 한 합니다 `ProductsOptimisticConcurrency` TableAdapter를 `DELETE` 문이 사용:


[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample3.sql)]

반면는 `DELETE` 우리의 원래 DAL에서 제품 TableAdapter에 대 한 문을 훨씬 더 간단 합니다.


[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample4.sql)]

알 수 있듯이 `WHERE` 절을 `DELETE` 낙관적 동시성을 사용 하는 TableAdapter에 대 한 문을 각 간의 비교를 포함 합니다.는 `Product` 테이블의 기존 열 값 및 원래 값을 시간에는 GridView (DetailsView 또는 FormView) 마지막으로 채워집니다. 이외의 다른 모든 필드 이후 `ProductID`, `ProductName`, 및 `Discontinued` 가질 수 있습니다 `NULL` 확인, 추가 매개 변수 및 값을 정확히 비교 포함 되어 있습니다 `NULL` 값을 `WHERE` 절.

않습니다 추가할 것 모든 추가 Datatable 낙관적 동시성 사용 데이터 집합에이 자습서에서는 ASP.NET 페이지는 업데이트 및 제품 정보 삭제만 제공 됩니다. 그러나 것도 추가 해야 합니다 `GetProductByProductID(productID)` 메서드를는 `ProductsOptimisticConcurrency` TableAdapter.

이렇게 하려면 마우스 오른쪽 단추로 클릭 TableAdapter의 제목 표시줄 (영역 오른쪽 위에 합니다 `Fill` 및 `GetProducts` 메서드 이름) 상황에 맞는 메뉴에서 추가 쿼리를 선택 합니다. TableAdapter 쿼리 구성 마법사 시작 됩니다. TableAdapter의 초기 구성으로 만들도록 선택한 대로 `GetProductByProductID(productID)` 임시 SQL 문을 사용 하는 방법 (그림 4 참조). 하므로 합니다 `GetProductByProductID(productID)` 특정 제품에 대 한 정보를 반환 하는 메서드,이 쿼리 임을 나타내려면를 `SELECT` 행을 반환 하는 형식을 쿼리 합니다.


[![쿼리 형식으로 표시 된 &quot;행을 반환 하는 SELECT&quot;](implementing-optimistic-concurrency-cs/_static/image26.png)](implementing-optimistic-concurrency-cs/_static/image25.png)

**그림 9**: 쿼리 형식으로 표시를 "`SELECT` 행을 반환 하는" ([클릭 하 여 큰 이미지 보기](implementing-optimistic-concurrency-cs/_static/image27.png))


다음 화면에서 SQL 쿼리를 미리 로드 된 TableAdapter의 기본 쿼리를 사용 하 라는 메시지가 나타나면 했습니다. 절을 포함 하도록 기존 쿼리를 보강 `WHERE ProductID = @ProductID`그림 10에 나와 있는 것 처럼 합니다.


[![추가 WHERE 절을 미리 로드 쿼리에 특정 제품 레코드를 반환할 수](implementing-optimistic-concurrency-cs/_static/image29.png)](implementing-optimistic-concurrency-cs/_static/image28.png)

**그림 10**: 추가 된 `WHERE` 절을 특정 제품 레코드를 반환할 Pre-Loaded 쿼리에 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image30.png))


생성 된 메서드 이름에 마지막으로 변경 `FillByProductID` 고 `GetProductByProductID`입니다.


[![FillByProductID GetProductByProductID를 메서드 이름 바꾸기](implementing-optimistic-concurrency-cs/_static/image32.png)](implementing-optimistic-concurrency-cs/_static/image31.png)

**그림 11**: 메서드를 이름 바꾸기 `FillByProductID` 하 고 `GetProductByProductID` ([클릭 하 여 큰 이미지 보기](implementing-optimistic-concurrency-cs/_static/image33.png))


이 마법사를 완료를 사용 하 여 TableAdapter 이제 포함 된 데이터를 검색 하기 위한 두 가지 방법: `GetProducts()`를 반환 하는 *모든* 제품; 및 `GetProductByProductID(productID)`, 지정된 된 제품을 반환 하는 합니다.

## <a name="step-3-creating-a-business-logic-layer-for-the-optimistic-concurrency-enabled-dal"></a>3 단계: 낙관적 동시성 사용 DAL에 대 한 비즈니스 논리 레이어 만들기

이 기존 `ProductsBLL` 클래스에는 일괄 처리 업데이트와 DB 직접 패턴을 사용 하는 예제입니다. 합니다 `AddProduct` 메서드 및 `UpdateProduct` 오버 로드 모두 전달 일괄 처리 업데이트 패턴을 사용을 `ProductRow` TableAdapter의 Update 메서드에 인스턴스. 합니다 `DeleteProduct` 메서드를 다른 한편으로 사용 하 여 TableAdapter의 호출 DB 직접 패턴을 `Delete(productID)` 메서드.

새 `ProductsOptimisticConcurrency` TableAdapter, DB 직접 메서드는 이제 원래 값에서 전달도 필요 합니다. 예를 들어 합니다 `Delete` 메서드는 이제 10 개의 입력 매개 변수 예상: 원래 `ProductID`, `ProductName`, `SupplierID`, `CategoryID`, `QuantityPerUnit`, `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`, 및 `Discontinued`합니다. 이러한 추가 입력된 매개 변수이 값을 사용 `WHERE` 절을 `DELETE` 문이 데이터베이스의 현재 값이 원래 항목까지 매핑되는 경우 지정된 된 레코드를 삭제 하는 전용 데이터베이스에 전송 합니다.

TableAdapter의에 대 한 메서드 시그니처를 동안 `Update` 일괄 처리 업데이트 패턴에 사용 된 메서드가 변경 되지 않은, 원래 및 새 값을 기록 하는 데 필요한 코드에 있습니다. 따라서이 기존 낙관적 동시성 사용 DAL을 사용 하기 보다는 `ProductsBLL` 클래스, 우리의 새 DAL을 사용 하 여 작업에 대 한 새 비즈니스 논리 계층 클래스를 만들어 보겠습니다.

라는 클래스를 추가 `ProductsOptimisticConcurrencyBLL` 에 `BLL` 내에 폴더를 `App_Code` 폴더입니다.


![ProductsOptimisticConcurrencyBLL 클래스 BLL 폴더에 추가](implementing-optimistic-concurrency-cs/_static/image34.png)

**그림 12**: 추가 된 `ProductsOptimisticConcurrencyBLL` 클래스 BLL 폴더


다음으로, 다음 코드를 추가 합니다 `ProductsOptimisticConcurrencyBLL` 클래스:


[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample5.cs)]

사용 하 여 확인 `NorthwindOptimisticConcurrencyTableAdapters` 클래스 선언의 시작 위의 문입니다. `NorthwindOptimisticConcurrencyTableAdapters` 네임 스페이스에 포함 된 `ProductsOptimisticConcurrencyTableAdapter` DAL의 메서드를 제공 하는 클래스입니다. 또한 클래스 선언 전 알게는 `System.ComponentModel.DataObject` ObjectDataSource 마법사의 드롭다운 목록에서이 클래스를 포함 하도록 Visual Studio에 지시 하는 특성입니다.

`ProductsOptimisticConcurrencyBLL`의 `Adapter` 속성은 인스턴스에 대 한 빠른 액세스를 제공 합니다 `ProductsOptimisticConcurrencyTableAdapter` 클래스를 원래 클래스 BLL에에서 사용 되는 패턴을 따릅니다 (`ProductsBLL`, `CategoriesBLL`등). 마지막으로 `GetProducts()` 메서드 단순히 호출 DAL의 `GetProducts()` 메서드와 반환을 `ProductsOptimisticConcurrencyDataTable` 개체 채워집니다를 `ProductsOptimisticConcurrencyRow` 데이터베이스에서 각 제품 레코드에 대 한 인스턴스.

## <a name="deleting-a-product-using-the-db-direct-pattern-with-optimistic-concurrency"></a>DB 직접 패턴을 사용 하 여 낙관적 동시성을 사용 하 여 제품 삭제

낙관적 동시성을 사용 하는 DAL에 대해 DB 직접 패턴을 사용할 경우 메서드는 새 값과 원래 값을 전달 합니다. 삭제에 대 한 값이 없는 새, 따라서 원래 값만 전달 해야 합니다. 이 BLL에 차례로 해야 수락 원래 매개 변수를 모두 입력된 매개 변수로 합니다. 저를 `DeleteProduct` 에서 메서드는 `ProductsOptimisticConcurrencyBLL` DB 직접 메서드를 사용 하는 클래스입니다. 이이 메서드 필요한 입력된 매개 변수로 모든 10 개의 product 데이터 필드에 다음 코드 에서처럼 DAL에 전달 하는 것을 의미 합니다.


[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample6.cs)]

원래 값-GridView (또는 DetailsView 또는 FormView) 마지막으로 로드 된 값-삭제 단추를 클릭할 때 데이터베이스의 값과 다르면는 `WHERE` 절 데이터베이스 레코드 및 레코드를 사용 하 여 일치 하지 않습니다 영향을 받습니다. 따라서 TableAdapter의 `Delete` 메서드는 반환 `0` 마스터 페이지 및 BLL의 `DeleteProduct` 메서드는 반환 `false`합니다.

## <a name="updating-a-product-using-the-batch-update-pattern-with-optimistic-concurrency"></a>일괄 처리 업데이트 패턴을 사용 하 여 낙관적 동시성을 사용 하 여 제품 업데이트

TableAdapter의 앞에서 설명한 대로 `Update` 일괄 처리 업데이트 패턴에 대 한 메서드가 낙관적 동시성 사용 되는 여부에 관계 없이 동일한 메서드 서명이 있습니다. 즉,는 `Update` 메서드는 Datarow, DataTable, 또는 형식화 된 데이터 집합의 배열을 DataRow를 필요로 합니다. 원래 값을 지정 하는 것에 대 한 추가 입력된 매개 변수가 없는 합니다. DataTable의 추적 원본 및 수정 된 값을 해당 DataRow(s)에 대 한 때문에 이것이 가능 합니다. DAL 발급 하는 경우 해당 `UPDATE` 문에서 `@original_ColumnName` 반면 DataRow의 원래 값을 사용 하 여 매개 변수가 채워집니다는 `@ColumnName` 매개 변수는 DataRow의 수정 된 값으로 채워집니다.

에 `ProductsBLL` 클래스 (DAL이 원래, 비 낙관적 동시성 사용), 코드는 다음과 같은 순서의 이벤트가 수행 하는 제품 정보를 업데이트 하는 일괄 처리 업데이트 패턴을 사용 하는 경우:

1. 현재 데이터베이스 제품 정보에 `ProductRow` TableAdapter의를 사용 하 여 인스턴스 `GetProductByProductID(productID)` 메서드
2. 새 값을 할당 합니다 `ProductRow` 1 단계에서에서 인스턴스
3. TableAdapter의 호출 `Update` 전달 하는 메서드는 `ProductRow` 인스턴스

그러나 때문에이 일련의 단계를 낙관적 동시성 올바르게 지원 하지 않습니다는 `ProductRow` 에 채워진 단계 1 채워집니다 데이터베이스에서 직접 데이터 행에서 사용 하는 원래 값에 현재 존재 하는 의미는 데이터베이스 및 GridView 편집 프로세스의 시작 부분에 바인딩된 되지 것입니다. 대신는 낙관적 동시성-DAL을 사용할 때 해야 alter는 `UpdateProduct` 다음 단계를 사용 하는 메서드 오버 로드 합니다.

1. 현재 데이터베이스 제품 정보에 `ProductsOptimisticConcurrencyRow` TableAdapter의를 사용 하 여 인스턴스 `GetProductByProductID(productID)` 메서드
2. 할당 된 *원래* 값을 `ProductsOptimisticConcurrencyRow` 1 단계에서에서 인스턴스
3. 호출 된 `ProductsOptimisticConcurrencyRow` 인스턴스의 `AcceptChanges()` 현재 값이 "원래" 항목에는 DataRow를 지시 하는 메서드
4. 할당 된 *새* 값을 `ProductsOptimisticConcurrencyRow` 인스턴스
5. TableAdapter의 호출 `Update` 전달 하는 메서드는 `ProductsOptimisticConcurrencyRow` 인스턴스

지정 된 제품 레코드에 대 한 현재 데이터베이스 값의 모든 읽기를 1 단계. 이 단계는에서 불필요 합니다 `UpdateProduct` 업데이트 하는 오버 로드 *모든* 제품 열 (이러한 값으로 덮어쓰여지는 2 단계에서에서)으로 열 값의 하위 집합만에 전달 되는 오버 로드 하는 데 필수적 이지만 입력된 매개 변수입니다. 원래 값에 할당 된 후를 `ProductsOptimisticConcurrencyRow` 인스턴스를 `AcceptChanges()` 현재 DataRow 값에 사용할 원래 값으로 표시 하는 메서드가 호출 되는 `@original_ColumnName` 에서 매개 변수를 `UPDATE` 문. 새 매개 변수 값에 할당 된 다음에 `ProductsOptimisticConcurrencyRow` , 그리고 마지막으로 `Update` 메서드를 호출 하면 데이터 행에 전달 합니다.

다음 코드에서는 `UpdateProduct` 모든 제품 데이터를 받아들이는 오버 로드가 입력된 매개 변수로 필드입니다. 여기에 표시 되지 합니다 `ProductsOptimisticConcurrencyBLL` 이 자습서도 있습니다. 다운로드에 포함 하는 클래스는 `UpdateProduct` 입력된 매개 변수로 제품의 이름과 가격을 허용 하는 오버 로드 합니다.


[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample7.cs)]

## <a name="step-4-passing-the-original-and-new-values-from-the-aspnet-page-to-the-bll-methods"></a>4 단계: ASP.NET 페이지에서 BLL 메서드에 원래 및 새 값을 전달

DAL 및 완료 하는 BLL을 사용 하 여 주기를 시스템에서 기본적으로 제공 하는 낙관적 동시성 논리를 활용할 수 있는 ASP.NET 페이지를 만듭니다. 특히 데이터 웹 컨트롤 (GridView, DetailsView 또는 FormView) 원래 값 및 ObjectDataSource 비즈니스 논리 계층에 두 개의 값 집합을 전달 해야 해야 합니다. 또한 ASP.NET 페이지를 정상적으로 동시성 위반을 처리할 구성 되어야 합니다.

열어서 시작 합니다 `OptimisticConcurrency.aspx` 페이지에 `EditInsertDelete` 폴더 및 GridView 설정 디자이너에 추가 해당 `ID` 속성을 `ProductsGrid`. GridView의 스마트 태그를 만들도록 선택할 라는 새로운 ObjectDataSource는 `ProductsOptimisticConcurrencyDataSource`합니다. 낙관적 동시성을 지 원하는 DAL을 사용 하려면이 ObjectDataSource, 것 이므로 사용 하도록 구성 된 `ProductsOptimisticConcurrencyBLL` 개체입니다.


[![ObjectDataSource 사용 ProductsOptimisticConcurrencyBLL 개체에](implementing-optimistic-concurrency-cs/_static/image36.png)](implementing-optimistic-concurrency-cs/_static/image35.png)

**그림 13**: ObjectDataSource 사용 합니다 `ProductsOptimisticConcurrencyBLL` 개체 ([클릭 하 여 큰 이미지 보기](implementing-optimistic-concurrency-cs/_static/image37.png))


선택 된 `GetProducts`, `UpdateProduct`, 및 `DeleteProduct` 마법사의 드롭다운 목록에서 메서드. UpdateProduct 메서드와 같이, 모든 제품의 데이터 필드를 허용 하는 오버 로드를 사용 합니다.

## <a name="configuring-the-objectdatasource-controls-properties"></a>ObjectDataSource 컨트롤의 속성 구성

마법사를 완료 한 후 ObjectDataSource의 선언 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample8.aspx)]

알 수 있듯이 합니다 `DeleteParameters` 컬렉션에 포함을 `Parameter` 에서 10 개의 입력된 매개 변수의 각 인스턴스는 `ProductsOptimisticConcurrencyBLL` 클래스의 `DeleteProduct` 메서드. 마찬가지로 합니다 `UpdateParameters` 컬렉션에 포함을 `Parameter` 에서 입력된 매개 변수의 각 인스턴스 `UpdateProduct`합니다.

ObjectDataSource의 관련 데이터를 수정 하는 이러한 이전 자습서를 제거할 것 `OldValuesParameterFormatString` BLL 메서드에 전달할 이전 (또는 원래) 값 뿐만 아니라 새 값을 필요로 하는이 속성 때문에이 시점에서 속성입니다. 또한이 속성 값이 원래 값에 대 한 입력된 매개 변수 이름을 나타냅니다. BLL에 원래 값에서 전달, 하므로 수행 *되지* 이 속성을 제거 합니다.

> [!NOTE]
> 값을 `OldValuesParameterFormatString` 속성의 원래 값을 필요로 하는 BLL 입력된 매개 변수 이름에 매핑해야 합니다. 이러한 매개 변수 이름을 때문 `original_productName`, `original_supplierID`등, 그대로 둘 수 있습니다를 `OldValuesParameterFormatString` 속성 값으로 `original_{0}`합니다. 그러나 하는 경우, BLL 메서드의 입력된 매개 변수 했습니다과 같은 이름을 `old_productName`, `old_supplierID`등, 업데이트 해야 합니다 `OldValuesParameterFormatString` 속성을 `old_{0}`입니다.


BLL 메서드에 원래 값을 올바르게 전달할 ObjectDataSource에 대 한 순서에서 수행 해야 하는 하나의 최종 속성 설정 방법이 있습니다. ObjectDataSource에는 [ConflictDetection 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.conflictdetection.aspx) 에 할당할 수 있습니다 [두 값 중 하나](https://msdn.microsoft.com/library/system.web.ui.conflictoptions.aspx):

- `OverwriteChanges` -기본값입니다. BLL 메서드의 원래 입력된 매개 변수를 원래 값을 보내지 않습니다.
- `CompareAllValues` -BLL 메서드에; 원래 값을 보내지 낙관적 동시성을 사용 하는 경우이 옵션을 선택 합니다.

잠시 시간을 설정 하는 `ConflictDetection` 속성을 `CompareAllValues`입니다.

## <a name="configuring-the-gridviews-properties-and-fields"></a>GridView의 속성 및 필드를 구성합니다.

올바르게 구성 하는 ObjectDataSource의 속성을 사용 하 여 살펴보겠습니다 GridView를 설정 합니다. 먼저, 편집 및 삭제를 지원 하기 위해 GridView, 것 이므로 GridView의 스마트 태그에서 편집을 사용 하도록 설정 및 삭제 사용 확인란을 클릭 합니다. CommandField 추가입니다 `ShowEditButton` 하 고 `ShowDeleteButton` 로 설정 됩니다 `true`.

에 바인딩된 경우를 `ProductsOptimisticConcurrencyDataSource` ObjectDataSource를 GridView는 각 제품의 데이터 필드에 대 한 필드를 포함 합니다. GridView를 편집할 수 있지만 사용자 환경도 적합 합니다. 합니다 `CategoryID` 고 `SupplierID` BoundFields로 렌더링 됩니다. 텍스트 상자에 사용자 id로 적절 한 category와 supplier를 입력 하도록 요구 합니다. 숫자 필드에 유효성 검사 컨트롤이 제품의 이름을 제공 된 단가 재고 단위, 순서 및 재주문 수준 값의 단위는 둘 다 적절 한 숫자 값 및 보다 큰 하거나 않도록 같은를 서식 없이 수는 0.

설명한 대로 합니다 *편집 및 삽입 인터페이스에 유효성 검사 컨트롤 추가* 하 고 *데이터 수정 인터페이스 사용자 지정* 자습서, 사용자 인터페이스를 사용자 지정할 수 있습니다 BoundFields를 TemplateFields 바꿉니다. 다음과 같은 방법으로이 GridView 및 해당 편집 인터페이스 수정 했습니다.

- 제거 합니다 `ProductID`하십시오 `SupplierName`, 및 `CategoryName` BoundFields
- 변환를 `ProductName` 를 templatefield로 BoundField RequiredFieldValidation 컨트롤을 추가 합니다.
- 변환 합니다 `CategoryID` 및 `SupplierID` BoundFields TemplateFields에 텍스트 상자 대신 Dropdownlist를 사용 하는 편집 인터페이스를 조정 합니다. 이러한 TemplateFields'에 `ItemTemplates`서 `CategoryName` 및 `SupplierName` 데이터 필드가 표시 됩니다.
- 변환 된 `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`, 및 `ReorderLevel` BoundFields TemplateFields CompareValidator 컨트롤을 추가 하 합니다.

이전 자습서에서 이러한 작업을 수행 하는 방법을 이미 살펴보았습니다 하므로에서는 방금 여기 최종 선언적 구문을 나열 했으며 사례로 구현을 유지 합니다.


[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample9.aspx)]

에 매우 근접해 있는 완벽 하 게 작업 예제입니다. 그러나 증가 하며 문제를 일으킬 수 있는 몇 가지 미묘한 있습니다. 또한 동시성 위반이 발생 하는 경우 사용자를 경고 하는 몇 가지 인터페이스가 필요 합니다.

> [!NOTE]
> 순서로 데이터 웹 컨트롤에 대 한 원래 값 (BLL에 전달 되어)는 ObjectDataSource 올바르게 전달할 것이 중요 하는 GridView의 `EnableViewState` 속성이 `true` (기본값). 뷰 상태를 해제 하면 원래 값을 다시 게시 될 때 손실 됩니다.


## <a name="passing-the-correct-original-values-to-the-objectdatasource"></a>ObjectDataSource를 올바른 원래 값을 전달합니다.

GridView를 구성한 방법에 문제가 몇 가지 있습니다. 경우 ObjectDataSource의 `ConflictDetection` 속성이로 설정 되어 `CompareAllValues` (그대로 우리), ObjectDataSource의 `Update()` 또는 `Delete()` 메서드는 호출 하는 GridView (DetailsView 또는 FormView), ObjectDataSource 복사 하려고 합니다 GridView의 원래 값에 적절 한 `Parameter` 인스턴스. 이 프로세스의 그래픽 표현에 대 한 그림 2를 다시 참조 합니다.

특히 GridView의 원래 값 때마다 데이터를 GridView에 바인딩되어 양방향 데이터 바인딩 문에서 값이 할당 됩니다. 따라서 모든 필요한 원래 값을 양방향 데이터 바인딩을 통해 캡처되는 고 변환할 수 있는 형식으로 제공 되는 것입니다.

이 중요 한 이유를 확인 하려면 잠시 브라우저에서 페이지를 방문 합니다. 예상 대로 GridView 편집 및 삭제 단추가 맨 왼쪽 열에서 각 제품을 나열 합니다.


[![제품을 GridView에 나열 됩니다.](implementing-optimistic-concurrency-cs/_static/image39.png)](implementing-optimistic-concurrency-cs/_static/image38.png)

**그림 14**: GridView에 있는 제품 나열 됩니다 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image40.png))


모든 제품에 대 한 삭제 단추를 클릭 하면는 `FormatException` throw 됩니다.


[![모든 제품 결과 FormatException에서 삭제 하려고 합니다.](implementing-optimistic-concurrency-cs/_static/image42.png)](implementing-optimistic-concurrency-cs/_static/image41.png)

**그림 15**:에서 모든 제품 결과 삭제를 시도 하는 `FormatException` ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image43.png))


합니다 `FormatException` ObjectDataSource가 원래에서 읽으려고 할 때 발생 하는 `UnitPrice` 값입니다. 있으므로 합니다 `ItemTemplate` 에 `UnitPrice` 통화 형식으로 (`<%# Bind("UnitPrice", "{0:C}") %>`), $19.95 같은 통화 기호가 포함 되어 있습니다. `FormatException` ObjectDataSource가이 문자열을 변환 하려고 시도할 때 발생 한 `decimal`합니다. 이 문제를 피하기에 다양 한 옵션이 했습니다.

- 통화 형식에서 제거 된 `ItemTemplate`합니다. 즉, 사용 하는 대신 `<%# Bind("UnitPrice", "{0:C}") %>`를 사용 하 여 `<%# Bind("UnitPrice") %>`입니다. 이러한 단점은 가격의 형식이 더 이상 되어 있는 것입니다.
- 표시를 `UnitPrice` 의 통화 형식으로 `ItemTemplate`를 사용 하지만 `Eval` 이 작업을 수행 하는 키워드입니다. 이전에 설명한 대로 `Eval` 단방향 데이터 바인딩을 수행 합니다. 여전히 제공 해야는 `UnitPrice` 에서 양방향 데이터 바인딩 문을 계속 해야 하므로 원래 값에 대 한 값을 `ItemTemplate`,이 좋지만이 레이블 웹 컨트롤에서 해당 `Visible` 속성 `false`. ItemTemplate에 다음 태그를 사용할 수 했습니다.


[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample10.aspx)]

- 통화 형식에서 제거 합니다 `ItemTemplate`를 사용 하 여 `<%# Bind("UnitPrice") %>`입니다. Gridview의 `RowDataBound` Label 웹 제어는 이벤트 처리기, 프로그래밍 방식으로 액세스 합니다 `UnitPrice` 값이 표시 되 고 설정 해당 `Text` 속성을 서식이 지정 된 버전.
- 유지 된 `UnitPrice` 통화 형식으로 합니다. Gridview의 `RowDeleting` 이벤트 처리기에서 기존 원본 바꾸기 `UnitPrice` 사용 하 여 10 진수 값을 실제 값 ($19.95) `Decimal.Parse`합니다. 유사한 수행 하는 방법에 살펴보았습니다 합니다 `RowUpdating` 이벤트 처리기는 [ *처리 BLL 및 DAL 수준의 예외 ASP.NET 페이지에서* ](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md) 자습서입니다.

두 번째 방법에서는 이동 하기로 하는 경우 예제에 대 한 추가 숨겨진된 레이블 웹 컨트롤 `Text` 속성이 바인딩되는 형식이 지정 되지 않은 양방향 데이터 `UnitPrice` 값입니다.

이 문제를 해결 한 후 모든 제품에 대 한 삭제 버튼을 다시 클릭 하십시오. 이 시간을 얻을 수는 `InvalidOperationException` ObjectDataSource가 BLL의 호출 하려고 할 때 `UpdateProduct` 메서드.


[![ObjectDataSource 송신 하려는 입력 매개 변수를 사용 하 여 메서드를 찾을 수 없습니다.](implementing-optimistic-concurrency-cs/_static/image45.png)](implementing-optimistic-concurrency-cs/_static/image44.png)

**그림 16**: ObjectDataSource 송신 하려는 입력 매개 변수를 사용 하 여 메서드를 찾을 수 없습니다 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image46.png))


예외 메시지를 살펴보면 라는 사실은 의심할 ObjectDataSource는 BLL을 호출 하려고 `DeleteProduct` 메서드를 포함 하는 `original_CategoryName` 및 `original_SupplierName` 매개 변수를 입력 합니다. 때문에 이것이 합니다 `ItemTemplate` 에 대 한은 `CategoryID` 및 `SupplierID` TemplateFields 현재 포함 하 고 양방향 바인딩 문을 `CategoryName` 및 `SupplierName` 데이터 필드입니다. 대신 포함 해야 `Bind` 문을 사용 하 여는 `CategoryID` 고 `SupplierID` 데이터 필드입니다. 이를 위해 사용 하 여 기존 바인딩 문을 바꿉니다 `Eval` 문, 숨겨진된 레이블 컨트롤을 추가한 `Text` 바인딩할 속성을 합니다 `CategoryID` 및 `SupplierID` 같이 양방향 데이터 바인딩을 사용 하 여 데이터 필드 아래:


[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample11.aspx)]

이러한 변경으로 기꺼이 이제 성공적으로 삭제 하 고 제품 정보를 편집할 수 있습니다! 5 단계에서에서 동시성 위반을 발견 되 고 있는지 확인 하는 방법을 살펴보겠습니다. 이제 몇 분 동안 업데이트 하려는 있고 예상 대로 작동 하는 업데이트 및 단일 사용자에 대 한 삭제 되도록 몇 가지 레코드를 삭제 합니다.

## <a name="step-5-testing-the-optimistic-concurrency-support"></a>5 단계: 테스트 낙관적 동시성 지원

동시성 위반 되 고 검색 된 대신 데이터를 무조건 덮어씁니다 되어 결과 확인 하려면이 페이지에 두 개의 브라우저 창을 열고 해야 합니다. 브라우저 인스턴스 모두에 Chai에 대 한 편집 단추를 클릭 합니다. 그런 다음 하나의 브라우저, 이름을 "Chai Tea"로 변경 하 고 업데이트를 클릭 합니다. 업데이트는 성공 하 고 새 제품 이름으로 "Chai Tea"를 사용 하 여 미리 편집 상태로 GridView를 반환 해야 합니다.

그러나 다른 브라우저 창 인스턴스에서 제품 이름 TextBox 여전히 표시 "Chai" 됩니다. 이 두 번째 브라우저 창에서 업데이트를 `UnitPrice` 에 `25.00`입니다. 낙관적 동시성을 지원 하지 않는 두 번째 브라우저 인스턴스의 업데이트를 클릭 하는 제품 이름을 다시 변경 "Chai", 첫 번째 브라우저 인스턴스가 수행한 변경 내용을 덮어쓰게 됩니다. 그러나 사용 하는 낙관적 동시성을 사용 하 여 두 번째 브라우저 인스턴스에서 업데이트 단추를 클릭 하면 결과 [DBConcurrencyException](https://msdn.microsoft.com/library/system.data.dbconcurrencyexception.aspx)합니다.


[![DBConcurrencyException Throw 되는 동시성 위반이 검색 되 면](implementing-optimistic-concurrency-cs/_static/image48.png)](implementing-optimistic-concurrency-cs/_static/image47.png)

**그림 17**: 때는 동시성 위반이 검색 되는 `DBConcurrencyException` 이 Throw 됩니다 ([클릭 하 여 큰 이미지 보기](implementing-optimistic-concurrency-cs/_static/image49.png))


`DBConcurrencyException` DAL의 일괄 처리 업데이트 패턴은 사용 하는 경우에 throw 됩니다. DB 직접 패턴 예외가 발생 하지 않습니다, 그리고 단순히 행이 없는 받는 나타냅니다. 이 설명 하기 두 브라우저 인스턴스 GridView 편집 전 상태로 돌아갑니다. 다음으로, 첫 번째 브라우저 인스턴스에서 편집 단추를 클릭 "Chai"로 다시 "Chai Tea"에서 제품 이름 및 업데이트를 클릭 합니다. 두 번째 브라우저 창에서 Chai에 대 한 삭제 단추를 클릭 합니다.

삭제를 클릭 하면 페이지가 포스트백, ObjectDataSource의를 호출 하는 GridView `Delete()` 메서드와 ObjectDataSource에 호출 합니다 `ProductsOptimisticConcurrencyBLL` 클래스의 `DeleteProduct` 메서드를 원래 값에 따라 전달 합니다. 원래 `ProductName` 값이 두 번째 브라우저 인스턴스가 현재과 일치 하지 않습니다 "Chai Tea" `ProductName` 데이터베이스의 값입니다. 따라서 합니다 `DELETE` 데이터베이스에 실행 된 문이 데이터베이스에 레코드가 없으므로 0 개의 행에 영향을 줍니다는 `WHERE` 절을 충족 합니다. `DeleteProduct` 메서드가 반환 되는 `false` ObjectDataSource의 데이터는 GridView에 차츰 회복 하 고 있습니다.

최종 사용자의 관점에서 플래시 화면 발생 한 두 번째 브라우저 창에 Chai 차에 대 한 삭제 버튼을 클릭 하면 이며, 전환, 시 제품 그대로 있습니다 "Chai" (제품 이름 변경 첫 번째 브라우저에서 나열 된 이제 있지만 인스턴스)입니다. 사용자가 삭제 단추를 다시 클릭 하면 삭제는 성공, GridView의 원래 `ProductName` 값 ("Chai") 이제 일치 하는 데이터베이스의 값입니다.

두이 경우 모두에서 사용자 환경은 멀리 적합 합니다. 명확 하 게 사용자의 핵심 요소 정보를 표시 하려고 하지 않습니다는 `DBConcurrencyException` 일괄 처리 업데이트 패턴을 사용 하는 동안 예외가 발생 합니다. 고 동작 DB 직접 패턴을 사용 하는 경우는 다소 혼동 스 러 사용자 명령이 실패 했지만 이유의 정확한 표시 되지 않습니다.

이러한 두 가지 문제를 해결 하려면 레이블 웹 컨트롤에 대 한 설명을 업데이트 또는 삭제 하지 못했습니다. 이유를 제공 하는 페이지에서 만들 수 있습니다. 확인할 수 있습니다 일괄 처리 업데이트 패턴의 경우 여부는 `DBConcurrencyException` 필요에 따라 경고 레이블 표시 GridView의 사후 수준 이벤트 처리기에서 예외가 발생 했습니다. DB 직접 메서드에 대 한 BLL 메서드의 반환 값을 검사할 수 있습니다 (되 `true` 행씩이 영향을 받는 경우 `false` 그렇지 않은 경우) 하 고 필요에 따라 경고나 정보 메시지를 표시 합니다.

## <a name="step-6-adding-informational-messages-and-displaying-them-in-the-face-of-a-concurrency-violation"></a>6 단계: 정보 메시지를 추가 하 고 동시성 위반을 발생 하는 경우 표시

동시성 위반이 발생 하면 나타나는 동작 DAL의 일괄 처리 업데이트 또는 직접 패턴 DB 사용 하는 여부에 따라 달라 집니다. 이 자습서는 업데이트 및 삭제에 사용 되는 DB 직접 패턴에 사용 되는 일괄 처리 업데이트 패턴을 사용 하 여 두 패턴을 사용 합니다. 시작 하려면 삭제 하거나 데이터를 업데이트 하려고 할 때 동시성 위반이 발생 했음을 설명 하는 페이지로 두 Label 웹 컨트롤을 추가 해 보겠습니다. 레이블 컨트롤의 설정 `Visible` 하 고 `EnableViewState` 속성을 `false`;이 하면 해당 특정 페이지 방문 위치 제외 하 고 각 페이지 방문에서 숨길 수 해당 `Visible` 프로그래밍 방식으로 속성 `true`합니다.


[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample12.aspx)]

설정 외에도 해당 `Visible`, `EnabledViewState`, 및 `Text` 속성을 설정 했습니다 합니다 `CssClass` 속성을 `Warning`, 큰, 빨간색, 기울임꼴, 굵게 글꼴에 표시할의 레이블을 하면 합니다. 이 CSS `Warning` 클래스 정의 되어 Styles.css에 추가 년대 합니다 *삽입, 업데이트 및 삭제와 관련 된 이벤트 검사* 자습서입니다.

이러한 레이블은 추가한 후 Visual Studio의 디자이너는 그림 18과 유사 합니다.


[![페이지에 추가 된 두 개의 레이블 컨트롤](implementing-optimistic-concurrency-cs/_static/image51.png)](implementing-optimistic-concurrency-cs/_static/image50.png)

**그림 18**: 두 개의 레이블 컨트롤에 추가 된 페이지 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image52.png))


이러한 레이블 웹 컨트롤을 사용 하 여 동시성 위반이 발생 했을 때에 시점에 적절 한 레이블을 결정 하는 방법을 검토 준비가 우리 `Visible` 속성 설정할 수 있습니다 `true`, 정보 메시지를 표시 합니다.

## <a name="handling-concurrency-violations-when-updating"></a>업데이트 하는 경우 동시성 위반을 처리 합니다.

먼저 일괄 처리 업데이트 패턴을 사용 하는 경우 동시성 위반을 처리 하는 방법을 살펴보겠습니다. 일괄 처리를 사용 하 여 이러한 위반은 업데이트 패턴 원인 이므로 `DBConcurrencyException` 예외가 throw 됩니다 결정 하는 ASP.NET 페이지에 코드를 추가 해야 하는지 여부를 `DBConcurrencyException` 업데이트 과정에서 예외가 발생 했습니다. 따라서 다른 사용자 레코드 편집 시작 시 동일한 데이터를 수정 했습니다 때문에 해당 변경 내용이 저장 되지 않은 설명 하는 사용자가 메시지를 표시 해야 했습니다 및 업데이트 단추를 클릭할 때입니다.

설명한 것 처럼 합니다 *처리 BLL 및 DAL 수준의 예외 ASP.NET 페이지에서* 자습서에서 이러한 예외를 감지 하 여 데이터 웹 컨트롤의 사후 수준 이벤트 처리기에 표시 하지 않을 수 있습니다. GridView의에 대 한 이벤트 처리기를 생성 해야 하므로 `RowUpdated` 경우를 확인 하는 이벤트를 `DBConcurrencyException` 예외를 throw 했습니다. 이 이벤트 처리기가 이벤트 처리기 코드 아래에 나와 있는 것 처럼 업데이트 과정에서 발생 하는 모든 예외에 대 한 참조를 전달 합니다.


[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample13.cs)]

경우는 `DBConcurrencyException` 예외를이 이벤트 처리기 표시를 `UpdateConflictMessage` 컨트롤 레이블 지정 및 예외 처리 된 것을 나타냅니다. 이 코드를 사용 하 여 레코드를 업데이트 하는 중 동시성 위반이 발생 하는 경우 사용자의 변경 내용을 손실 됩니다는 있는 백업이 덮어써 지 다른 사용자가 수정한 내용을 동시에 있으므로. 특히 GridView 편집 전 상태로 돌아갑니다 이며 현재 데이터베이스 데이터에 연결 됩니다. 이렇게 하면 GridView 행 이전에 보이지는 다른 사용자의 변경 내용으로 업데이트 됩니다. 또한는 `UpdateConflictMessage` 레이블 컨트롤 방금 사용자에 게 설명 됩니다. 이 이벤트 순서는 그림 19에 자세히 설명 되어 있습니다.


[![사용자가의 동시성 위반이 발생 하면 업데이트 손실 됩니다.](implementing-optimistic-concurrency-cs/_static/image54.png)](implementing-optimistic-concurrency-cs/_static/image53.png)

**그림 19**: 사용자가의 동시성 위반이 발생 하면 업데이트 손실 됩니다 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image55.png))


> [!NOTE]
> 또는 GridView 미리 편집 상태를 반환 하는 대신 수 상태로 두면 GridView 편집 상태로 설정 하 여 합니다 `KeepInEditMode` 전달-의 속성 `GridViewUpdatedEventArgs` 개체 true입니다. 이 방법을 사용 하는 경우 단, 반드시 데이터를 GridView에 바인딩됩니다 (호출 하 여 해당 `DataBind()` 메서드)는 다른 사용자의 값 편집 인터페이스에 로드 됩니다. 이 자습서를 사용 하 여 다운로드할 수 있는 코드에 다음 두 줄의 코드는 `RowUpdated` 이벤트 처리기가 주석; GridView 코드의 다음이 줄에서 동시성 위반 후 편집 모드로 유지 합니다. 주석 처리를 단순히 제거 합니다.


## <a name="responding-to-concurrency-violations-when-deleting"></a>삭제 하는 경우 동시성 위반에 응답

DB 직접 패턴을 사용 하면 예외가 없습니다 동시성 위반이 발생 하는 경우 발생 합니다. 대신, database 문을 단순히 영향을 줍니다 모든 레코드를 사용 하 여 WHERE 절이 일치 하지 않습니다으로 레코드가 없습니다. 모든 데이터 수정 메서드에 BLL에서 만든 정확 하 게 하나의 레코드를을 받는 있는지 여부를 나타내는 부울 값을 반환 되도록 설계 되었습니다. 따라서 레코드를 삭제 하는 경우 동시성 위반이 발생 하는 경우 확인을 살펴볼 수는 BLL의 반환 값 `DeleteProduct` 메서드.

BLL 메서드에 대 한 반환 값을 통해 ObjectDataSource의 사후 수준 이벤트 처리기에서 검사할 수를 `ReturnValue` 의 속성을 `ObjectDataSourceStatusEventArgs` 개체가 이벤트 처리기에 전달 합니다. 반환 값을 결정 하는 데 관심이 있으므로 합니다 `DeleteProduct` ObjectDataSource의에 대 한 이벤트 처리기를 만들려면 먼저 메서드를 `Deleted` 이벤트입니다. 합니다 `ReturnValue` 형식의 속성은 `object` 수 `null` 경우 예외가 발생 하 고 메서드가 중단 되어 값을 반환할 수 있습니다. 따라서에서는 먼저 확인 해야 하는 `ReturnValue` 속성이 아닙니다 `null` 및 부울 값입니다. 살펴봅니다이 검사를 통과 하는 것으로 가정 합니다 `DeleteConflictMessage` 경우 컨트롤의 레이블을 합니다 `ReturnValue` 는 `false`. 다음 코드를 사용 하 여이 수행할 수 있습니다.


[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample14.cs)]

동시성 위반을 발생 하는 경우 사용자의 삭제 요청이 취소 됩니다. GridView는 Delete 단추를 클릭 하면 그 페이지 로드는 사용자는 레코드 간의 시간 동안 발생 한 변경 내용을 보여 주는 새로 고쳐집니다. 이러한 위반은 그러한 경우는 `DeleteConflictMessage` 레이블이 표시 됩니다 (그림 20 참조)만 발생 합니다.


[![동시성 위반이 발생 하는 경우 사용자가의 삭제 취소 됩니다.](implementing-optimistic-concurrency-cs/_static/image57.png)](implementing-optimistic-concurrency-cs/_static/image56.png)

**그림 20**: 사용자가의 동시성 위반이 발생 하는 경우 삭제 취소 됩니다 ([큰 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image58.png))


## <a name="summary"></a>요약

동시성 위반에 대 한 기회가 여러 허용 하는 모든 응용 프로그램에 존재 하는 동시 사용자 데이터를 업데이트 또는 삭제 합니다. 동시에 두 명의 사용자가 마지막 쓰기 "wins" 가져옵니다 누구 든 지 동일한 데이터를 업데이트할 때 덮어씁니다 다른 사용자의 변경에 대 한 이러한 위반이 처리 하지 않은 하는 경우. 또는 개발자 중 낙관적 또는 비관적 동시성 제어를 구현할 수 있습니다. 낙관적 동시성 제어는 동시성 위반 빈도가 및 단순히 업데이트를 허용 하지 않습니다 또는 삭제 명령에서 동시성 위반을 증가로 가정 합니다. 비관적 동시성 제어 가정 위반 빈도가 및 업데이트 또는 삭제 명령 단순히 한 사용자의 거부 하는 동시성은 허용 되지 않습니다. 비관적 동시성 제어를 사용 하 여 레코드 업데이트 잠가 수정 하거나 잠겨 있는 동안에 레코드를 삭제 하면 다른 사용자가 모든 것을 방지 합니다.

.NET의 형식화 된 데이터 집합 낙관적 동시성 제어를 지원 하기 위한 기능을 제공 합니다. 특히 합니다 `UPDATE` 고 `DELETE` 모든 테이블의 열을 포함 하는 데이터베이스에 실행 한 문은, 될 때 있던 되므로 업데이트 하거나 삭제 하면 원래 데이터를 사용 하 여 레코드의 현재 데이터 일치 하는 경우만 발생 합니다 해당 update 또는 delete를 수행 합니다. DAL에 낙관적 동시성을 지원 하도록 구성 되 면 BLL 메서드를 업데이트 해야 합니다. 또한 BLL에 호출 하는 ASP.NET 페이지는 ObjectDataSource 데이터 웹 컨트롤과에서 원래 값을 검색 하 고 아래 BLL에 전달 되도록 구성 되어야 합니다.

BLL 및 DAL을 업데이트 하 고 ASP.NET 페이지에이 자습서에서 살펴본 것 처럼 ASP.NET 웹 응용 프로그램에서 낙관적 동시성 제어를 구현 해야 합니다. 이 추가 된 작업의 시간과 노력 정도로 인지 여부는 응용 프로그램에 따라 달라 집니다. 자주 동시 사용자 데이터를 업데이트 했거나 업데이트 하는 데이터가 서로 다른 한 다음 동시성 제어 없으면 주요 문제 중 하나입니다. 그러나 정기적으로 여러 사용자가 동일한 데이터를 사용 하 여 사이트의 경우 동시성 제어 방지할 수 있습니다는 한 사용자의 업데이트 또는 삭제 모르게 다른 사람의 덮어씁니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](customizing-the-data-modification-interface-cs.md)
> [다음](adding-client-side-confirmation-when-deleting-cs.md)
