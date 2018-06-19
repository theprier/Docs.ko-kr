---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs
title: 낙관적 동시성 (C#) 구현 | Microsoft Docs
author: rick-anderson
description: 웹 응용 프로그램의 여러 사용자가 데이터를 편집할 수 있는 경우는 두 명의 사용자가 편집 하 고 동일한 데이터 동시에 위험이 있습니다. 이 tutori에서...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/17/2006
ms.topic: article
ms.assetid: 56e15b33-93b8-43ad-8e19-44c6647ea05c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs
msc.type: authoredcontent
ms.openlocfilehash: 27441ea9343055b3139468036fc6f201c77667e5
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30891050"
---
<a name="implementing-optimistic-concurrency-c"></a>낙관적 동시성 (C#) 구현
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_21_CS.exe) 또는 [PDF 다운로드](implementing-optimistic-concurrency-cs/_static/datatutorial21cs1.pdf)

> 웹 응용 프로그램의 여러 사용자가 데이터를 편집할 수 있는 경우는 두 명의 사용자가 편집 하 고 동일한 데이터 동시에 위험이 있습니다. 이 자습서에서는 이러한 위험을 처리 하는 낙관적 동시성 제어를 구현 합니다.


## <a name="introduction"></a>소개

에 데이터를 볼 수 있도록 하는 웹 응용 프로그램 또는 데이터를 수정할 수 있는 한 명의 사용자만 포함 하는 경우 서로 변경 내용을 실수로 덮어쓰지 두 명의 동시 사용자의 위험이 있습니다. 그러나 여러 사용자가 데이터를 업데이트 또는 삭제를 허용 하는 웹 응용 프로그램에 대 한,는 한 사용자의 수정 다른 동시 사용자와 충돌에 대 한 잠재적인. 모든 동시성 정책이 적용 되어 있는 없이 두 명의 사용자가 동시에 단일 레코드를 편집할 때 사용자가 자신의 변경 내용을 커밋합니다 마지막 덮어씁니다가 첫 번째 변경한을 합니다.

예를 들어 있는지 Jisun 및 Sam, 두 사용자가 둘 다 방문 페이지를 업데이트 하는 GridView 컨트롤을 통해 제품도 삭제 방문자를 허용 하는 응용 프로그램에 한다고 가정 합니다. 둘 다에서 같은 시간 GridView에서 편집 단추를 클릭 합니다. Jisun 제품 이름을 "Chai 찻잔"로 변경 하 고 업데이트 단추를 클릭 합니다. 결과는 `UPDATE` 설정 하는 데이터베이스에 전송 되는 문을 *모든* 제품의 업데이트 가능한 필드 (Jisun만 한 필드를 업데이트 하는 경우에 `ProductName`). 이 시점에서, 데이터베이스 "Chai 차," 음료,이 특정 제품에 대해 공급 업체 삼 화 음료 범주 값을 가집니다. 그러나 Sam의 화면에 GridView 여전히 표시 제품 이름을 편집 가능한 GridView 행에서 "Chai"으로 됩니다. 몇 초 후 Jisun의 변경 사항이 커밋되기 Sam 조미료 하는 범주를 업데이트 하 고 업데이트를 클릭 합니다. 이 인해는 `UPDATE` "Chai"를 제품 이름을 설정 하는 데이터베이스에 보내는 문은 `CategoryID` 해당 음료 범주 ID 및 등입니다. 제품 이름을 Jisun의 변경 내용은 덮어썼습니다. 그림 1이이 일련을의 이벤트를 그래픽으로 보여 줍니다.


[![두 명의 사용자가 동시에 레코드를 업데이트 하는 경우 있습니다 s 잠재적인 s 한 명의 사용자에 대 한 변경을 다른를 덮어쓰려면](implementing-optimistic-concurrency-cs/_static/image2.png)](implementing-optimistic-concurrency-cs/_static/image1.png)

**그림 1**: 다른 s Overwrite로 때 두 사용자가 동시에 업데이트 된 레코드가 있습니다 s 가능성 s 한 명의 사용자에 대 한 변경 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image3.png))


마찬가지로, 두 명의 사용자가 페이지를 방문 하는 한 명의 사용자는 다른 사용자에 의해 삭제 될 때 레코드를 업데이트 하는 중간 수 있습니다. 또는 사이의 사용자 페이지를 로드 하는 경우 삭제 단추를 클릭할 때, 다른 사용자가 변경 했습니다 해당 레코드의 콘텐츠입니다.

세 가지 [동시성 제어](http://en.wikipedia.org/wiki/Concurrency_control) 전략을 사용할 수 있습니다.

- **아무 작업도 수행 하지** -동시 사용자가 동일한 레코드를 수정 하는 경우 (기본 동작) win 마지막 커밋 수
- [**낙관적 동시성** ](http://en.wikipedia.org/wiki/Optimistic_concurrency_control) -는 동시성 충돌 합니다, 대부분의 이러한 충돌이 발생 하지 않습니다; 시간 수 있지만 따라서는 충돌이 발생 하는 경우 단순히 사용자에 게 알립니다 가정 하는 변경 다른 사용자가 동일한 데이터를 수정 하기 때문에 저장할 수 없습니다.
- **비관적 동시성** -가정 동시성 충돌은 일반적 이며 다른 사용자의 동시 작업으로 인해 해당 변경 내용이 저장 되지 않은 총 사용자가 기간을 허용 하지 않습니다; 따라서 한 사용자가 레코드 업데이트를 시작 하는 경우이 잠글 수 를 다른 사용자 편집 하거나 사용자는 수정 커밋될 때까지 해당 레코드를 삭제할 것을 방지

기본 동시성 확인 전략 사용한 지금까지 자습서의 모든-즉, 마지막 쓰기가 win 하도록 했습니다. 이 자습서에서는 낙관적 동시성 제어를 구현 하는 방법을 검토 합니다.

> [!NOTE]
> 이 자습서 시리즈의 비관적 동시성 예제에서는 표시 되지 않습니다. 비관적 동시성은 등 잠그므로 거의 사용 되지 않으면 제대로 무시 합니다 다른 사용자가 데이터를 업데이트 하지 못할 수 있습니다. 예를 들어 사용자 편집에 대 한 레코드를 잠그고 잠금 해제 하기 전에 날에 대 한 유지 한 다음, 하는 경우 다른 사용자는 원래 사용자 반환 하 고 그의 업데이트를 완료 될 때까지 해당 레코드를 업데이트할 수 됩니다. 따라서 비관적 동시성은 사용 하는 경우, 즉 일반적으로 도달 하면 잠금을 취소 하는 시간 제한이 있습니다. 티켓 판매 웹 사이트의 경우 사용자는 주문 프로세스를 완료 하는 동안 짧은 기간 동안 특정 좌석 위치 잠금는 비관적 동시성 제어의 예시입니다.


## <a name="step-1-looking-at-how-optimistic-concurrency-is-implemented"></a>1 단계: 낙관적 동시성 방법을 살펴보고 구현

낙관적 동시성 제어는 업데이트 또는 삭제 프로세스를 시작할 때 업데이트 되거나 삭제 되는 레코드에 동일한 값에서 작동 합니다. 예를 들어 편집 가능한 GridView에 있는 편집 단추를 클릭 하면 레코드의 값은 데이터베이스에서 읽고 입력란 및 기타 웹 컨트롤에 표시 합니다. GridView에서 원래 값이 저장 됩니다. 이상 버전에서는 사용자가 변경한 내용이 설정 하 고 업데이트 단추를 클릭 한 후 원래 값과 새 값 보내집니다 비즈니스 논리 계층 및 다음 데이터 액세스 계층. 데이터 액세스 계층에는 사용자 편집을 시작 하는 원래 값은 데이터베이스에 여전히 값과 동일 하는 경우에 레코드를 업데이트 됨을 알리는 SQL 문을 실행 해야 합니다. 그림 2에서는이 이벤트 시퀀스를를 보여 줍니다.


[![성공 하려면 Update 또는 Delete에 대 한 원래 값을 현재 데이터베이스 값 이어야 합니다.](implementing-optimistic-concurrency-cs/_static/image5.png)](implementing-optimistic-concurrency-cs/_static/image4.png)

**그림 2**: For Update 또는 Delete는 원래 값 해야 수와 같으면 현재 데이터베이스 값 Succeed로 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image6.png))


낙관적 동시성을 구현 하는 방법은 여러 가지가 (참조 [Peter A. Bromberg](http://peterbromberg.net/)의 [Optmistic 동시성 업데이트 논리](http://www.eggheadcafe.com/articles/20050719.asp) 다양 한 옵션에 대 한 간단한 설명에 대 한). ADO.NET 형식화 된 데이터 집합에는 확인란의 틱 방금으로 구성할 수 있는 한 구현을 제공 합니다. TableAdapter의를 보완 하는 형식화 된 데이터 집합에서 TableAdapter에 대 한 낙관적 동시성을 사용 하도록 설정 `UPDATE` 및 `DELETE` 모든의 원래 값의 비교를 포함 하도록 문을 `WHERE` 절. 다음 `UPDATE` 문, 현재 데이터베이스 값을 GridView에서 레코드를 업데이트할 때 처음 검색 된 값은 경우에 해당 이름 및 제품의 가격을 예를 들어 업데이트 합니다. `@ProductName` 및 `@UnitPrice` 반면 매개 변수는 사용자가 입력 한 새 값이 들어 `@original_ProductName` 및 `@original_UnitPrice` 편집 단추 클릭 했을 때 GridView에 원래 로드 된 값이 포함:


[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample1.sql)]

> [!NOTE]
> 이 `UPDATE` 문의 가독성을 높이기 위해 간소화 되었습니다. 실제로 `UnitPrice` 체크 인는 `WHERE` 절 이후 더 개입 됩니다 `UnitPrice` 포함 될 수 있습니다 `NULL` s 및 있는지 확인 `NULL = NULL` 항상 False를 반환 합니다 (대신 사용 해야 `IS NULL`).


다른 기본 사용할 뿐 아니라 `UPDATE` 메서드를 직접 문, 낙관적 동시성에도 해당 DB의 서명을 수정 TableAdapter를 구성 합니다. 이 첫 번째 자습서에서 설명한 대로 [ *데이터 액세스 계층을 만들려면*](../introduction/creating-a-data-access-layer-cs.md), 입력된 매개 변수로 값 DB 직접 메서드 내용이 스칼라의 목록을 허용 하는 것 (대신 강력한 형식의 DataRow 또는 DataTable 인스턴스)입니다. 낙관적 동시성을 직접 DB를 사용 하는 경우 `Update()` 및 `Delete()` 방법의 원래 값에 대 한 입력된 매개 변수를 포함 합니다. 또한 일괄 처리를 사용 하기 위한 BLL에는 코드 업데이트 패턴 (의 `Update()` 스칼라 값 보다는 Datarow Datatable을 허용 하는 메서드 오버 로드)도 변경 해야 합니다.

대신 확장 우리의 기존 보다 보겠습니다 (BLL에 맞게 변경 해야)는 낙관적 동시성을 사용 하려면 DAL의 Tableadapter 대신 새 형식화 된 데이터 집합을 만들 라는 `NorthwindOptimisticConcurrency`에 추가 하는 `Products` TableAdapter를 낙관적 동시성을 사용 합니다. 그런 다음, 만들겠습니다는 `ProductsOptimisticConcurrencyBLL` 비즈니스 논리 계층 가진 클래스를 DAL 낙관적 동시성을 지원 하기 위해 적절 하 게 수정 합니다. 이 기반이 살펴본 후 ASP.NET 페이지를 만들 준비가 됩니다.

## <a name="step-2-creating-a-data-access-layer-that-supports-optimistic-concurrency"></a>2 단계: 낙관적 동시성을 지원 하는 데이터 액세스 계층 만들기

새 형식화 된 데이터 집합을 만들려면 마우스 오른쪽 단추로 클릭는 `DAL` 내의 폴더는 `App_Code` 폴더 라는 새 데이터 집합을 추가 하 고 `NorthwindOptimisticConcurrency`합니다. 첫 번째 자습서에서 살펴본 것 처럼 이렇게 하면 소요 됩니다 새 TableAdapter를 입력 한 데이터 집합을 자동으로 TableAdapter 구성 마법사를 시작 합니다. 첫 번째 화면에서 우리는 지정 하 라는 메시지가 데이터베이스에 연결-사용 하 여 동일한 Northwind 데이터베이스에 연결 하는 `NORTHWNDConnectionString` 에서 설정 `Web.config`합니다.


[![같은 Northwind 데이터베이스에 연결](implementing-optimistic-concurrency-cs/_static/image8.png)](implementing-optimistic-concurrency-cs/_static/image7.png)

**그림 3**: 같은 Northwind 데이터베이스에 연결 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image9.png))


다음으로 데이터를 쿼리 하는 방법에 대 한 프롬프트가: 특별 SQL 문을 통해 새 저장 프로시저 또는 기존 저장 프로시저입니다. 원래 우리의 DAL에서 임시 SQL 쿼리를 사용 하므로이 옵션을 사용 여기 뿐입니다.


[![임시 SQL 문을 사용 하 여 검색할 데이터를 지정 합니다.](implementing-optimistic-concurrency-cs/_static/image11.png)](implementing-optimistic-concurrency-cs/_static/image10.png)

**그림 4**: 특별 SQL 문을 사용 하 여 검색할 데이터 지정 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image12.png))


다음 화면에서 제품 정보를 검색 하는 데 SQL 쿼리를 입력 합니다. 에 사용 되는 동일한 SQL 쿼리가 사용는 `Products` 모두 반환 우리의 원래 DAL에서 TableAdapter는 `Product` 제품의 공급 업체 및 범주 이름과 함께 열:


[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample2.sql)]


[![원래 DAL에서 제품 TableAdapter에서 동일한 SQL 쿼리를 사용 합니다.](implementing-optimistic-concurrency-cs/_static/image14.png)](implementing-optimistic-concurrency-cs/_static/image13.png)

**그림 5**:에서 동일한 SQL 쿼리를 사용 하 여는 `Products` 원래 DAL에서 TableAdapter ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image15.png))


다음 화면으로 이동 하기 전에 고급 옵션 단추를 클릭 합니다. 를이 TableAdapter 사용한 낙관적 동시성 제어 하려면 단순히 "낙관적 동시성 사용" 확인란을 확인 합니다.


[![검사 하 여 낙관적 동시성 제어를 사용 하도록 설정 된 &quot;낙관적 동시성을 사용 하 여&quot; 확인란](implementing-optimistic-concurrency-cs/_static/image17.png)](implementing-optimistic-concurrency-cs/_static/image16.png)

**그림 6**: "낙관적 동시성 사용" 확인란을 선택 하 여 낙관적 동시성 제어를 사용 하도록 설정 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image18.png))


마지막으로, TableAdapter DataTable 채우기와 DataTable; 반환 하는 데이터 액세스 패턴을 사용 해야 함을 나타내는합니다 또한 DB 직접 메서드를 만들어야 함을 나타냅니다. 반환 되는 메서드 이름을 DataTable 패턴 GetData GetProducts 하에서 변경 명명 규칙을 반영 하기 위해 원래 우리의 DAL에서 사용 했습니다.


[![모든 데이터 액세스 패턴을 활용 하는 TableAdapter가](implementing-optimistic-concurrency-cs/_static/image20.png)](implementing-optimistic-concurrency-cs/_static/image19.png)

**그림 7**:는 TableAdapter 활용 모든 데이터 액세스 방식이 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image21.png))


강력한 형식의 데이터 집합 디자이너는 포함 하는 마법사를 완료 한 후 `Products` DataTable 및 TableAdapter. DataTable의 이름을 바꾸려면 잠시 `Products` 를 `ProductsOptimisticConcurrency`, DataTable의 제목 표시줄을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 이름 바꾸기를 선택 하 여 수행할 수 있는 합니다.


[![DataTable 및 TableAdapter 형식화 된 데이터 집합에 추가 되었습니다.](implementing-optimistic-concurrency-cs/_static/image23.png)](implementing-optimistic-concurrency-cs/_static/image22.png)

**그림 8**: A DataTable 및 TableAdapter 형식화 된 데이터 집합에 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image24.png))


간의 차이점을 볼 수는 `UPDATE` 및 `DELETE` 간 쿼리는 `ProductsOptimisticConcurrency` TableAdapter (사용 하 여 낙관적 동시성) 및 (하지 않습니다)는 제품 TableAdapter를 TableAdapter 클릭 하 고 속성 창으로 이동 합니다. 에 `DeleteCommand` 및 `UpdateCommand` 속성의 `CommandText` 하위 속성 DAL의 update 또는 delete 관련 메서드를 호출할 때에 데이터베이스에 전송 되는 실제 SQL 구문을 볼 수 있습니다. 에 대 한는 `ProductsOptimisticConcurrency` TableAdapter는 `DELETE` 문이 사용 되었습니다.


[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample3.sql)]

반면는 `DELETE` 우리의 원래 DAL에서 제품 TableAdapter에 대해 문을 훨씬 더 간단 합니다.


[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample4.sql)]

볼 수 있듯이 `WHERE` 절에는 `DELETE` 낙관적 동시성을 사용 하는 TableAdapter에 대해 문을 비교 하 여 각 포함 된 `Product` 테이블의 기존 열 값 및 원래 값이 시간에는 GridView (또는 DetailsView 또는 FormView) 마지막 채워졌습니다. 이외의 다른 모든 필드 이후 `ProductID`, `ProductName`, 및 `Discontinued` 가질 수 있습니다 `NULL` 값, 추가 매개 변수 및 검사는 올바르게 비교를 위해 포함 `NULL` 값에 `WHERE` 절.

म 않습니다 대로 추가할 모든 추가 Datatable 낙관적 동시성 사용 데이터 집합에이 자습서에 대 한 가격 ASP.NET 페이지 업데이트 및 삭제 제품 정보를 제공 합니다. 그러나 우리 여전히 추가할 필요가 `GetProductByProductID(productID)` 메서드는 `ProductsOptimisticConcurrency` TableAdapter.

이렇게 하려면 마우스 오른쪽 단추로 클릭 TableAdapter의 제목 표시줄 (영역 오른쪽 위에 `Fill` 및 `GetProducts` 메서드 이름은) 상황에 맞는 메뉴에서 추가 쿼리를 선택 합니다. TableAdapter 쿼리 구성 마법사 시작 됩니다. 우리의 TableAdapter의 초기 구성으로 만들도록 선택한 대로 `GetProductByProductID(productID)` 임시 SQL 문을 사용 하 여 메서드 (그림 4 참조). 이후는 `GetProductByProductID(productID)` 이 쿼리 임을 나타내려면, 특정 제품에 대 한 정보를 반환 하는 메서드는 `SELECT` 쿼리 행을 반환 하는 형식입니다.


[![쿼리 형식을로 표시 한 &quot;행을 반환 하는 SELECT&quot;](implementing-optimistic-concurrency-cs/_static/image26.png)](implementing-optimistic-concurrency-cs/_static/image25.png)

**그림 9**: 쿼리 형식을로 표시 된 "`SELECT` 행을 반환 하는" ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image27.png))


다음 화면에서 SQL 쿼리를 미리 로드 된 TableAdapter의 기본 쿼리로 사용에 대 한 표시 우리 됩니다. 확장 하는 절을 포함 하도록 기존 쿼리 `WHERE ProductID = @ProductID`그림 10에 나타난 것 처럼 합니다.


[![추가 WHERE 절을 특정 제품 레코드를 반환할 수 미리 로드 된 쿼리](implementing-optimistic-concurrency-cs/_static/image29.png)](implementing-optimistic-concurrency-cs/_static/image28.png)

**그림 10**: 추가 된 `WHERE` 특정 제품 레코드를 반환할 수 Pre-Loaded 쿼리 절 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image30.png))


마지막으로 생성 된 메서드 이름을 변경 `FillByProductID` 및 `GetProductByProductID`합니다.


[![FillByProductID 및 GetProductByProductID 메서드 이름 바꾸기](implementing-optimistic-concurrency-cs/_static/image32.png)](implementing-optimistic-concurrency-cs/_static/image31.png)

**그림 11**: 하는 메서드 이름 바꾸기 `FillByProductID` 및 `GetProductByProductID` ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image33.png))


이 마법사를 완료 된 TableAdapter 이제 포함 된 데이터를 검색 하기 위한 두 가지 방법: `GetProducts()`를 반환 하 *모든* 제품; 및 `GetProductByProductID(productID)`, 지정된 된 제품을 반환 하는 합니다.

## <a name="step-3-creating-a-business-logic-layer-for-the-optimistic-concurrency-enabled-dal"></a>3 단계: 낙관적 동시성 사용 DAL에 대 한 비즈니스 논리 계층 만들기

이 기존 `ProductsBLL` 클래스에는 일괄 처리 업데이트와 직접 패턴 DB 사용 하는 예제입니다. `AddProduct` 메서드 및 `UpdateProduct` 를 전달 하는 일괄 처리 업데이트 패턴을 사용 하 여 두 오버 로드는 `ProductRow` TableAdapter의 Update 메서드를 인스턴스. `DeleteProduct` 메서드, 반면에 사용 하 여 TableAdapter의 호출 DB 직접 패턴 `Delete(productID)` 메서드.

새 `ProductsOptimisticConcurrency` TableAdapter, DB 직접 메서드는 이제 원래 값에서 전달도 필요 합니다. 예를 들어는 `Delete` 메서드에서 입력 매개 변수를 10 이제 예상: 원래 `ProductID`, `ProductName`, `SupplierID`, `CategoryID`, `QuantityPerUnit`, `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`, 및 `Discontinued`합니다. 이러한 추가 입력된 매개 변수의이 값에 사용 하 여 `WHERE` 절은 `DELETE` 문이 데이터베이스의 현재 값이 원래까지 매핑할 경우 지정된 된 레코드를 삭제 하는 전용 데이터베이스에 전송 합니다.

TableAdapter의에 대 한 메서드 서명을 동안 `Update` 일괄 처리 업데이트 패턴에 사용 되는 방법을 변경 하지 않은, 원래과 새 값을 기록 하는 데 필요한 코드에 있습니다. 따라서을 우리의 기존 낙관적 동시성 사용 DAL을 사용 하기 보다는 `ProductsBLL` 클래스, 우리의 새 DAL 작업에 대 한 새 비즈니스 논리 계층 클래스를 만들어 보겠습니다.

라는 클래스를 추가 `ProductsOptimisticConcurrencyBLL` 에 `BLL` 내의 폴더는 `App_Code` 폴더입니다.


![BLL 폴더로 ProductsOptimisticConcurrencyBLL 클래스를 추가 합니다.](implementing-optimistic-concurrency-cs/_static/image34.png)

**그림 12**: 추가 된 `ProductsOptimisticConcurrencyBLL` BLL 폴더로 클래스


다음 코드를 다음으로 추가 된 `ProductsOptimisticConcurrencyBLL` 클래스:


[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample5.cs)]

사용 하는 참고 `NorthwindOptimisticConcurrencyTableAdapters` 클래스 선언의 시작 부분 위에 문입니다. `NorthwindOptimisticConcurrencyTableAdapters` 네임 스페이스에 포함 된 `ProductsOptimisticConcurrencyTableAdapter` DAL의 메서드를 제공 하는 클래스입니다. 또한 클래스 선언 앞 있습니다는 `System.ComponentModel.DataObject` ObjectDataSource 마법사의 드롭다운 목록에서이 클래스를 포함 하도록 Visual Studio를 지정 하는 특성입니다.

`ProductsOptimisticConcurrencyBLL`의 `Adapter` 속성에 빠르게 액세스할의 인스턴스는 `ProductsOptimisticConcurrencyTableAdapter` 클래스 하 고 원래 BLL 클래스에 사용 되는 패턴을 따릅니다 (`ProductsBLL`, `CategoriesBLL`등). 마지막으로 `GetProducts()` 메서드를 단순히는 DAL 호출 `GetProducts()` 메서드와 반환은 `ProductsOptimisticConcurrencyDataTable` 개체는 `ProductsOptimisticConcurrencyRow` 데이터베이스의 각 제품 레코드에 대 한 인스턴스.

## <a name="deleting-a-product-using-the-db-direct-pattern-with-optimistic-concurrency"></a>DB 직접 패턴을 사용 하 여 낙관적 동시성 관련 제품 삭제

낙관적 동시성을 사용 하는 DAL에 대해 DB 직접 패턴을 사용 하는 경우 메서드는 새 값 및 원래 값을 전달 합니다. 삭제에 대 한 값이 없는 새, 따라서 원래 값만 시 전달할 필요 합니다. 우리의 BLL에 다음 해야 수락 원래 매개 변수를 모두 입력된 매개 변수로 합니다. 죠는 `DeleteProduct` 에서 메서드는 `ProductsOptimisticConcurrencyBLL` 클래스 DB 직접 메서드를 사용 합니다. 이이 메서드를 입력된 매개 변수로 10 개 제품 데이터 필드에 가져간 다음 코드 에서처럼 DAL에 전달 해야 함을 의미 합니다.


[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample6.cs)]

원래 값-GridView (또는 DetailsView 또는에 FormView) 마지막 로드 된 값-삭제 단추를 클릭할 때 데이터베이스의 값과 다르면는 `WHERE` 절 데이터베이스 레코드 및 레코드가 없는과 일치 하지 않습니다 영향을 받습니다. 따라서 TableAdapter의 `Delete` 메서드는 반환 `0` 및 BLL의 `DeleteProduct` 메서드는 반환 `false`합니다.

## <a name="updating-a-product-using-the-batch-update-pattern-with-optimistic-concurrency"></a>일괄 처리 업데이트 패턴을 사용 하 여 낙관적 동시성 관련 제품 업데이트

TableAdapter의 앞에서 설명한 것 처럼 `Update` 일괄 처리 업데이트 패턴에 대 한 메서드가 낙관적 동시성 사용 여부에 관계 없이 동일한 메서드 서명이 있습니다. 즉,는 `Update` 메서드에서 예상 된 DataRow Datarow, DataTable, 또는 형식화 된 데이터 집합의 배열입니다. 원래 값을 지정 하기 위한 추가 입력된 매개 변수가 없는 합니다. DataTable의 추적 원래 및 수정 된 값에 대 한 해당 DataRow(s) 때문에 이것이 가능 합니다. DAL 발급 하는 경우 해당 `UPDATE` 문에서 `@original_ColumnName` 반면 매개 변수 데이터 행의 원래 값으로 채워집니다는 `@ColumnName` 매개 변수는 데이터 행의 수정 된 값으로 채워집니다.

에 `ProductsBLL` 클래스 (DAL 우리의 원래, 비 낙관적 동시성을 사용 하 여), 코드는 다음과 같은 순서로 이벤트가 수행 하는 제품 정보를 업데이트 하려면 일괄 처리 업데이트 패턴을 사용 하는 경우:

1. 현재 데이터베이스의 제품 정보를 읽기는 `ProductRow` TableAdapter의를 사용 하 여 인스턴스 `GetProductByProductID(productID)` 메서드
2. 새 값을 할당는 `ProductRow` 1 단계에서에서 인스턴스
3. TableAdapter의 호출 `Update` 전달 하는 메서드는 `ProductRow` 인스턴스

그러나 때문에이 일련의 단계를 낙관적 동시성을 올바르게 지원 하지 않습니다는 `ProductRow` 에 채워진 1 단계 채워집니다의 데이터베이스에서 직접 데이터 행에서 사용 하는 원래 값의 현재 존재 하는 의미는 데이터베이스 및 편집 프로세스의 시작 부분에 GridView에 바인딩된 되지 것입니다. 대신 사용 하는 낙관적 동시성 DAL를 사용할 때 필요 변경 하는 `UpdateProduct` 다음 단계를 사용 하는 메서드 오버 로드 합니다.

1. 현재 데이터베이스의 제품 정보를 읽기는 `ProductsOptimisticConcurrencyRow` TableAdapter의를 사용 하 여 인스턴스 `GetProductByProductID(productID)` 메서드
2. 할당 된 *원래* 값에 `ProductsOptimisticConcurrencyRow` 1 단계에서에서 인스턴스
3. 호출 된 `ProductsOptimisticConcurrencyRow` 인스턴스의 `AcceptChanges()` 해당 현재 값으로 "원래" DataRow를 지정 하는 메서드
4. 할당 된 *새* 값에 `ProductsOptimisticConcurrencyRow` 인스턴스
5. TableAdapter의 호출 `Update` 전달 하는 메서드는 `ProductsOptimisticConcurrencyRow` 인스턴스

현재 데이터베이스 값의 모든 페이지에서 지정한 제품 레코드에 대 한 읽기를 1 단계. 이 단계는에서 불필요 한는 `UpdateProduct` 를 업데이트 하는 오버 로드 *모든* 제품 열 (으로 이러한 값은 덮어 씀 2 단계), 하지만 여기서는 열 값의 하위 집합만 변수로 저장 되어 이러한 오버 로드에 대 한 입력된 매개 변수입니다. 원래 값에 할당 된 후는 `ProductsOptimisticConcurrencyRow` 인스턴스는 `AcceptChanges()` 메서드가 호출 되 면 현재 DataRow 값에 사용할 원래 값으로 표시 하는입니다는 `@original_ColumnName` 의 매개 변수는 `UPDATE` 문. 새 매개 변수 값에 할당 된 다음에 `ProductsOptimisticConcurrencyRow` 고 마지막으로 `Update` 메서드가 호출 되 면 데이터 행에 전달 합니다.

다음 코드는 `UpdateProduct` 모든 제품 데이터를 허용 하는 오버 로드는 입력된으로 매개 변수 필드입니다. 여기에 표시 되지 동안는 `ProductsOptimisticConcurrencyBLL` 이 자습서도 있습니다. 다운로드에 포함 된 클래스는 `UpdateProduct` 입력된 매개 변수로 제품의 이름과 가격을 허용 하는 오버 로드 합니다.


[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample7.cs)]

## <a name="step-4-passing-the-original-and-new-values-from-the-aspnet-page-to-the-bll-methods"></a>4 단계: ASP.NET 페이지에서를 BLL 메서드에 원래 값과 새 값을 전달

DAL 및 BLL 완료 했으므로 이제 남은 것 시스템에 기본 제공 하는 낙관적 동시성 논리를 사용할 수 있는 ASP.NET 페이지를 만듭니다. 특히, 웹 컨트롤 (GridView, DetailsView, 또는 FormView) 데이터의 원래 값과는 ObjectDataSource 비즈니스 논리 계층에 두 개의 값 집합을 전달 해야 기억해 야 합니다. 또한 ASP.NET 페이지를 정상적으로 동시성 위반을 처리할 구성 되어야 합니다.

열어 시작는 `OptimisticConcurrency.aspx` 페이지에 `EditInsertDelete` 폴더는 GridView 설정 디자이너에 추가 하 고 해당 `ID` 속성을 `ProductsGrid`합니다. GridView의 스마트 태그에서 만들도록 선택한 라는 새 ObjectDataSource `ProductsOptimisticConcurrencyDataSource`합니다. 낙관적 동시성을 지 원하는 DAL을 사용 하려면이 ObjectDataSource 할 것 이므로 사용 하도록 구성 된 `ProductsOptimisticConcurrencyBLL` 개체입니다.


[![ObjectDataSource 사용 ProductsOptimisticConcurrencyBLL 개체는](implementing-optimistic-concurrency-cs/_static/image36.png)](implementing-optimistic-concurrency-cs/_static/image35.png)

**그림 13**: ObjectDataSource 사용는 `ProductsOptimisticConcurrencyBLL` 개체 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image37.png))


선택 된 `GetProducts`, `UpdateProduct`, 및 `DeleteProduct` 마법사의 드롭다운 목록에서 메서드. UpdateProduct 메서드에 대 한 모든 제품의 데이터 필드를 허용 하는 오버 로드를 사용 합니다.

## <a name="configuring-the-objectdatasource-controls-properties"></a>ObjectDataSource 컨트롤의 속성 구성

마법사를 완료 한 후 ObjectDataSource의 선언적 태그는 다음과 같이 표시 됩니다.


[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample8.aspx)]

볼 수 있듯이 `DeleteParameters` 컬렉션에 포함 되어는 `Parameter` 에서 10 개의 입력된 매개 변수의 각 인스턴스는 `ProductsOptimisticConcurrencyBLL` 클래스의 `DeleteProduct` 메서드. 마찬가지로,는 `UpdateParameters` 컬렉션에 포함 되어는 `Parameter` 에 입력된 매개 변수 마다 인스턴스가 `UpdateProduct`합니다.

관련 데이터를 수정 하는 이러한 이전 자습서, ObjectDataSource의 제거할 것 `OldValuesParameterFormatString` 이 시점에서이 속성에 전달 되도록 이전 (또는 원래) 값 뿐 아니라 새 값 BLL 메서드 필요 함을 표시 되므로 속성입니다. 또한이 속성 값에는 원래 값에 대 한 입력된 매개 변수 이름을 나타냅니다. BLL에 원래 값에서 전달, 이후 수행 *하지* 이 속성을 제거 합니다.

> [!NOTE]
> 값은 `OldValuesParameterFormatString` 속성 BLL에 원래 값을 예상 하는 입력된 매개 변수 이름에 매핑해야 합니다. 이러한 매개 변수 이름을 이후 `original_productName`, `original_supplierID`등의 그대로 둘 수 있습니다는 `OldValuesParameterFormatString` 속성 값으로 `original_{0}`합니다. 그러나 BLL 메서드의 입력된 매개 변수를 갖는 경우와 같은 이름을 `old_productName`, `old_supplierID`, 등의를 업데이트 해야 하는 `OldValuesParameterFormatString` 속성을 `old_{0}`합니다.


ObjectDataSource 올바르게 BLL 메서드를 원래 값을 전달 하는 순서로 수행 해야 하는 최종 속성 설정 중 하나 있습니다. ObjectDataSource에는 [ConflictDetection 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.conflictdetection.aspx) 에 할당할 수 있는 [두 값 중 하나](https://msdn.microsoft.com/library/system.web.ui.conflictoptions.aspx):

- `OverwriteChanges` -기본값입니다. 원래 입력된 매개 변수는 BLL 메서드도 원래 값을 전송 하지 않습니다.
- `CompareAllValues` -는 BLL 방식의을 원래 값에 전송 낙관적 동시성을 사용 하는 경우이 옵션을 선택 합니다.

설정 하는 `ConflictDetection` 속성을 `CompareAllValues`합니다.

## <a name="configuring-the-gridviews-properties-and-fields"></a>GridView의 속성 및 필드를 구성합니다.

ObjectDataSource의 속성이 올바르게 구성 되어 있는 살펴봅시다 GridView에 설치 하 합니다. 첫째, 편집 및 삭제를 지원 하기 위해 GridView 할 것 이므로 GridView의 스마트 태그에서 편집을 사용 하도록 설정 및 삭제 사용 확인란을 클릭 합니다. CommandField 추가 합니다. 해당 `ShowEditButton` 및 `ShowDeleteButton` 으로 설정 되어 `true`합니다.

에 바인딩된 경우는 `ProductsOptimisticConcurrencyDataSource` ObjectDataSource를 GridView는 각 제품의 데이터 필드에 대 한 필드를 포함 합니다. 이러한 GridView를 편집할 수 있는 동안 사용자 경험 결코 좋습니다. `CategoryID` 및 `SupplierID` BoundFields 텍스트 상자로 렌더링 될 사용자를 적절 한 범주 및 공급 업체 ID 번호를 입력 해야 합니다. 숫자 필드와 제품의 이름을 제공 하 고 있는지 단가, 재고, 주문 및 재주문 수준 값의 단위는 둘 다 적절 한 숫자 값 및 보다 큰 크거나 없는 유효성 검사 컨트롤에 대 한 서식이 없는 수 있습니다. 0입니다.

설명한 것 처럼는 *편집 및 삽입 인터페이스에 유효성 검사 컨트롤 추가* 및 *데이터 수정 인터페이스 사용자 지정* 자습서, 사용자 인터페이스 사용자 지정 하는 BoundFields TemplateFields 대체 됩니다. 다음과 같은 방법으로이 GridView와 편집 인터페이스를 수정 했습니다.

- 제거는 `ProductID`, `SupplierName`, 및 `CategoryName` BoundFields
- 변환에서 `ProductName` BoundField를 TemplateField RequiredFieldValidation 컨트롤을 추가 합니다.
- 변환의 `CategoryID` 및 `SupplierID` BoundFields TemplateFields를 받아 텍스트 상자 대신 dropdownlist 활용 사용 하도록 편집 하는 인터페이스를 조정 합니다. 이러한 TemplateFields' `ItemTemplates`, `CategoryName` 및 `SupplierName` 데이터 필드가 표시 됩니다.
- 변환에서 `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`, 및 `ReorderLevel` BoundFields TemplateFields 및 CompareValidator 컨트롤을 추가 합니다.

이전 자습서에서 이러한 작업을 수행 하는 방법을 이미 검사 했습니다 우리, 이후 합니다만 마지막으로 선언적 구문 여기 나열 했으며 사례로 구현을 유지.


[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample9.aspx)]

We 're 매우 가까이 완벽 하 게 작업 예제 필요 합니다. 그러나 증가 하 고 문제를 일으킬 수 있는 몇 가지 미묘한 있습니다. 또한 동시성 위반이 발생 했을 때 경고 메시지를 표시 하는 몇 가지 인터페이스 여전히 필요 합니다.

> [!NOTE]
> 순서로 데이터 웹 컨트롤에 대 한 올바르게 ObjectDataSource (전달 되는 다음 BLL에)에 원래 값을 전달 하는 것이 중요 하는 GridView의 `EnableViewState` 속성이 `true` (기본값). 뷰 상태를 비활성화 하면 포스트백에 원래 값이 손실 됩니다.


## <a name="passing-the-correct-original-values-to-the-objectdatasource"></a>ObjectDataSource에 올바른 원래 값을 전달

GridView 구성 된 방식으로 관련 된 문제의 두 가지가 있습니다. 경우 ObjectDataSource의 `ConflictDetection` 속성이 `CompareAllValues` (그대로 우리), ObjectDataSource의 `Update()` 또는 `Delete()` 메서드는 호출 하는 GridView (또는 DetailsView 또는 FormView), ObjectDataSource에서 복사를 시도 GridView의 원래 값에 적절 한 `Parameter` 인스턴스. 이 프로세스의 그래픽 표현에 대 한 그림 2 다시 참조 합니다.

특히, GridView의 원래 값 때마다 데이터가 GridView에 바인딩되는 양방향 데이터 바인딩 문에 값이 할당 됩니다. 따라서은 양방향 데이터 바인딩을 통해 모든 필요한 원래 값은 캡처 함을 변환 가능한 형식으로 제공 되는 필수적입니다.

이 중요 한 이유를 확인 하려면 잠시 브라우저에서 페이지를 방문 합니다. 예상 대로 GridView 편집 및 삭제 단추가 왼쪽 열에 있는 각 제품을 나열 합니다.


[![제품은 GridView에 나열 된](implementing-optimistic-concurrency-cs/_static/image39.png)](implementing-optimistic-concurrency-cs/_static/image38.png)

**그림 14**: The 제품은 GridView에 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image40.png))


모든 제품에 대 한 삭제 단추를 클릭 하는 경우는 `FormatException` throw 됩니다.


[![FormatException의 모든 제품 결과 삭제 하려고 합니다.](implementing-optimistic-concurrency-cs/_static/image42.png)](implementing-optimistic-concurrency-cs/_static/image41.png)

**그림 15**:에 Any 제품 결과 삭제를 시도 하는 `FormatException` ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image43.png))


`FormatException` 원래를 읽을 수는 ObjectDataSource 할 때 발생 `UnitPrice` 값입니다. 이후는 `ItemTemplate` 에 `UnitPrice` 는 통화 형식으로 설정 (`<%# Bind("UnitPrice", "{0:C}") %>`), $19.95 같은 통화 기호를 포함 합니다. `FormatException` 에이 문자열을 변환 하는 ObjectDataSource 시도할 때 발생 한 `decimal`합니다. 이 문제를 방지 하기 위해 다양 한 옵션 해야 합니다.

- 서식을 통화 제거는 `ItemTemplate`합니다. 즉, 사용 하는 대신 `<%# Bind("UnitPrice", "{0:C}") %>`를 사용 하 여 `<%# Bind("UnitPrice") %>`합니다. 이러한 단점은 가격의 형식이 더 이상 지정 되었는지입니다.
- 표시는 `UnitPrice` 에 통화로 형식이 지정 된는 `ItemTemplate`를 사용 하지만 `Eval` 이를 위해 키워드입니다. 이전에 설명한 대로 `Eval` 단방향 데이터 바인딩을 수행 합니다. 여전히 제공 해야 할는 `UnitPrice` 의 양방향 데이터 바인딩을 문과 여전히 되므로 원래 값에 대 한 값은 `ItemTemplate`,이 좋지만이 레이블 웹 컨트롤에 해당 `Visible` 속성이로 설정 되어 `false`합니다. ItemTemplate에 다음 태그를 사용할 수 있습니다.


[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample10.aspx)]

- 서식을 통화 제거는 `ItemTemplate`를 사용 하 여 `<%# Bind("UnitPrice") %>`합니다. GridView의에서 `RowDataBound` Label 웹 제어는 이벤트 처리기, 프로그래밍 방식 액세스는 `UnitPrice` 값이 표시 되어 설정 해당 `Text` 속성 형식이 지정 된 버전을 합니다.
- 둡니다는 `UnitPrice` 는 통화 형식으로 설정 합니다. GridView의에서 `RowDeleting` 이벤트 처리기를 기존 원본을 교체 `UnitPrice` 사용 하 여 10 진수 값을 실제 값 ($19.95) `Decimal.Parse`합니다. 유사한 수행 하는 방법에 살펴보았습니다는 `RowUpdating` 의 이벤트 처리기는 [ *처리 BLL-및 ASP.NET 페이지에서 DAL 수준 예외* ](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md) 자습서입니다.

이 예에서는 두 번째 접근 방식으로 이동 하기로 하는 경우에 대 한 추가 숨겨진된 Label 웹 컨트롤 `Text` 속성은 양방향 데이터에는 형식이 지정 되지 않은 바인딩된 `UnitPrice` 값입니다.

이 문제를 해결 한 후 모든 제품에 대 한 삭제 단추를 다시 클릭 하십시오. 이 시간을 얻을 수는 `InvalidOperationException` 는 ObjectDataSource BLL의 호출 하려고 할 때 `UpdateProduct` 메서드.


[![ObjectDataSource 송신 하는 입력 매개 변수를 사용 하 여 메서드를 찾을 수 없습니다.](implementing-optimistic-concurrency-cs/_static/image45.png)](implementing-optimistic-concurrency-cs/_static/image44.png)

**그림 16**:는 ObjectDataSource 송신 하는 입력 매개 변수를 사용 하 여 메서드를 찾을 수 없습니다 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image46.png))


예외 메시지를 살펴보면 것은 분명는 ObjectDataSource는 BLL 호출 하려는 `DeleteProduct` 포함 된 메서드 `original_CategoryName` 및 `original_SupplierName` 입력 매개 변수입니다. ¿¡´는 `ItemTemplate` 에 대 한 s는 `CategoryID` 및 `SupplierID` TemplateFields 현재 사용 하는 양방향 바인딩 문을 포함 하는 `CategoryName` 및 `SupplierName` 데이터 필드입니다. 대신, 이므로 포함할 필요가 `Bind` 으로 문을 `CategoryID` 및 `SupplierID` 데이터 필드입니다. 이를 위해으로 기존 바인딩 문을 바꿉니다 `Eval` 문, 다음 숨겨진된 레이블 컨트롤을 추가 하 고 `Text` 속성이 바인딩되는 `CategoryID` 및 `SupplierID` 같이 양방향 데이터 바인딩을 사용 하 여 데이터 필드 아래:


[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample11.aspx)]

이러한 변경 내용으로는 성공적으로 삭제 하 고 제품 정보를 편집할 수 이제! 5 단계 동시성 위반 항목이 발견 되 고 있는지 확인 하는 방법을 살펴보겠습니다. 하지만 지금은 업데이트를 시도 하는 데 몇 분 정도 걸리며이 예상 대로 작동 하려면 해당 업데이트 및 삭제는 단일 사용자에 대 한 몇 가지 레코드 삭제.

## <a name="step-5-testing-the-optimistic-concurrency-support"></a>5 단계: 테스트 낙관적 동시성 지원

검색 된 (하지 않고 데이터를 덮어씁니다 맹목적으로 결과) 동시성 위반 되는 작업을 확인 하려면이 페이지에 두 개의 브라우저 창을 열고 해야 합니다. 브라우저 인스턴스 모두에 chai 편집 단추를 클릭 합니다. 그런 다음 하나의 브라우저, 이름을 "Chai 찻잔"로 변경 하 고 업데이트를 클릭 합니다. 업데이트는 성공 하 고를 새 제품 이름으로 "Chai 찻잔"와 미리 편집 상태로 GridView를 반환 해야 합니다.

그러나 다른 브라우저 창 인스턴스의 제품 이름 텍스트 상자에 붙여넣습니다 여전히 표시 "Chai" 됩니다. 이 두 번째 브라우저 창에서 업데이트 된 `UnitPrice` 를 `25.00`합니다. 낙관적 동시성을 지원 하지 않는 두 번째 브라우저 인스턴스에서 업데이트를 클릭 하는 제품 이름으로 다시 변경할 수 있으므로 첫 번째 브라우저 인스턴스에서에서 변경한 내용을 덮어쓰지 "Chai". 하지만 낙관적 동시성을 사용 두 번째 브라우저 인스턴스에서 업데이트 단추를 클릭 하면 번째로 [DBConcurrencyException](https://msdn.microsoft.com/library/system.data.dbconcurrencyexception.aspx)합니다.


[![DBConcurrencyException Throw 되는 동시성 위반이 검색 되 면](implementing-optimistic-concurrency-cs/_static/image48.png)](implementing-optimistic-concurrency-cs/_static/image47.png)

**그림 17**: 때 정도 동시성 위반이 검색 되는 `DBConcurrencyException` Throw 됩니다 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image49.png))


`DBConcurrencyException` DAL의 일괄 처리 업데이트 패턴을 사용 하는 경우에 throw 됩니다. DB 직접 패턴 예외가 발생 하지 않으므로, 행이 없는 영향을 받은 의미일 뿐입니다. 이 설명 하기 브라우저 인스턴스 모두 GridView 편집 전 상태로 돌아갑니다. 다음으로, 첫 번째 브라우저 인스턴스에서 편집 단추를 클릭 하 고 "Chai" 이동 "Chai 찻잔"에서 제품 이름을 변경 하 고 업데이트를 클릭 합니다. 두 번째 브라우저 창에서 chai 삭제 단추를 클릭 합니다.

삭제를 클릭 하면 페이지 다시 게시, ObjectDataSource의를 호출 하는 GridView `Delete()` 메서드와 ObjectDataSource를 호출는 `ProductsOptimisticConcurrencyBLL` 클래스의 `DeleteProduct` 원래 값을 따라 전달 하는 메서드. 원래 `ProductName` 두 번째 브라우저 인스턴스 현재와 일치 하지 않습니다 "Chai 찻잔"에 대 한 값 `ProductName` 데이터베이스의 값입니다. 따라서는 `DELETE` 데이터베이스에 실행 된 문이 데이터베이스에 레코드가 없기 때문 0 개의 행에 영향을 하는 `WHERE` 절을 충족 합니다. `DeleteProduct` 메서드 반환 `false` ObjectDataSource의 데이터는 GridView에 리바운드 및 합니다.

최종 사용자의 관점에서 깜박이게 화면 발생 한 두 번째 브라우저 창에서 Chai 찻잔에 대 한 삭제 단추를 클릭 하 고, 다시 전달 되 면 제품은 남아 있지만 이제 "Chai" (제품 이름 변경은 첫 번째 브라우저로 나열 됩니다. 인스턴스)입니다. 사용자가 삭제 단추를 다시 클릭 하면 삭제가 성공 GridView의 원래 대로 `ProductName` 값 ("Chai") 이제 일치 하는 데이터베이스의 값입니다.

이러한 경우 모두 사용자 환경은 이상적인에 크게 못 미치는 것입니다. 명확 하 게 하지는 않을 사용자에 게 주요 표시는 `DBConcurrencyException` 일괄 처리 업데이트 패턴을 사용 하는 경우는 예외입니다. DB 직접 패턴을 사용 하는 경우 동작은 다소 혼동 스 러 사용자 명령이 실패 했지만 이유의 정확 하 게 표시 되지 않으며

이 두 가지 문제를 해결 하려면 업데이트 또는 삭제 실패 이유를 설명을 제공 하는 페이지에서 레이블 웹 컨트롤을 만들 수 있습니다. 확인할 수 있습니다 일괄 처리 업데이트 패턴에 대 한 여부는 `DBConcurrencyException` 필요에 따라 경고 레이블 표시 GridView의 사후 수준의 이벤트 처리기에서 예외가 발생 했습니다. DB 직접적인 방법에 대 한 BLL 메서드의 반환 값 조사할 수 있습니다 (즉 `true` 한 행의 영향을 받은 경우 `false` 그렇지 않은 경우) 하 고 필요에 따라 정보 메시지를 표시 합니다.

## <a name="step-6-adding-informational-messages-and-displaying-them-in-the-face-of-a-concurrency-violation"></a>6 단계: 정보 메시지를 추가 하 고 동시성 위반을 한 경우에도 표시

동시성 위반이 발생 하면 나타나는 동작 DAL의 일괄 업데이트 또는 직접 패턴 DB 사용 하는 여부에 따라 달라 집니다. 이 자습서는 업데이트 및 삭제 하는 데 사용 되는 DB 직접 패턴에 사용 되 고 일괄 처리 업데이트 패턴의 두 패턴을 사용 합니다. 시작 하려면 삭제 하거나 데이터를 업데이트 하려고 할 때 동시성 위반이 발생 했음을 설명 하는 가격 페이지에 두 Label 웹 컨트롤을 추가 해 보겠습니다. 레이블 컨트롤의 설정 `Visible` 및 `EnableViewState` 속성을 `false`; 이렇게 하면 각 페이지 방문 하는 것에 대 한 특정 페이지 방문 where 점을 제외 하 고 숨길 자신의 `Visible` 프로그래밍 방식으로 속성 `true`합니다.


[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample12.aspx)]

설정 뿐만 아니라 해당 `Visible`, `EnabledViewState`, 및 `Text` 속성을 준비할는 `CssClass` 속성을 `Warning`, 큰, 빨간색, 기울임꼴, 굵은 글꼴로 표시할의 레이블을 이르게 됩니다. 이 CSS `Warning` 클래스 정의 되어 Styles.css에 추가에 다시 고 *삽입, 업데이트 및 삭제와 관련 된 이벤트를 검사* 자습서입니다.

이러한 레이블을 추가한 후 Visual Studio의 디자이너는 그림 18 비슷해야 합니다.


[![페이지에 추가 된 두 Label 컨트롤](implementing-optimistic-concurrency-cs/_static/image51.png)](implementing-optimistic-concurrency-cs/_static/image50.png)

**그림 18**: 두 레이블 컨트롤에 추가 된 페이지 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image52.png))


위치에 다음 레이블 웹 컨트롤을 사용 준비가 동시성 위반이 발생 했을 때,을 가리키고 적절 한 레이블을 결정 하는 방법을 검토 `Visible` 속성 설정할 수 있습니다 `true`, 정보 메시지를 표시 합니다.

## <a name="handling-concurrency-violations-when-updating"></a>업데이트 될 때 동시성 위반을 처리 합니다.

먼저 일괄 처리 업데이트 패턴을 사용 하는 경우 동시성 위반을 처리 하는 방법을 살펴보겠습니다. 일괄 처리와 이러한 위반은 패턴 원인 업데이트 이후는 `DBConcurrencyException` 예외를 throw 확인 하 여 ASP.NET 페이지에 코드를 추가 해야 하는지 여부를 `DBConcurrencyException` 업데이트 과정에서 예외가 발생 했습니다. 따라서 다른 사용자가 레코드를 편집은 시작 시 동일한 데이터를 수정 했습니다 때문에 해당 변경 내용이 저장 되지 않은 설명 하는 사용자가 메시지를 표시 해야 했습니다 및 업데이트 단추를 클릭할 때입니다.

설명한 것 처럼는 *처리 BLL-및 ASP.NET 페이지에서 DAL 수준 예외* 자습서, 이러한 예외를 검색 하 데이터 웹 컨트롤의 사후 수준의 이벤트 처리기에서 표시 되지 않습니다. GridView의에 대 한 이벤트 처리기를 만들어야 한다는 따라서 `RowUpdated` 지 검사 하는 이벤트는 `DBConcurrencyException` 예외가 발생 했습니다. 이 이벤트 처리기는 이벤트 처리기 아래 코드에 나와 있는 것 처럼 업데이트 과정 중에 발생 한 예외에 대 한 참조를 전달 됩니다.


[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample13.cs)]

경우는 `DBConcurrencyException` 이 이벤트 처리기 표시 하는 경우를 제외 하는 `UpdateConflictMessage` 컨트롤 레이블 지정 및 예외 처리 된 것을 나타냅니다. 이 코드가 레코드를 업데이트할 때 동시성 위반이 발생 하는 경우 사용자의 변경 내용이 되므로 손실 될가 덮어쓰게 다른 사용자의 수정 내용을 동시에입니다. 특히, GridView 미리 편집 상태로 되돌릴 및 현재 데이터베이스 데이터에 연결 합니다. 이렇게 하면 GridView 행 이전에 표시 되지 않은 다른 사용자의 변경 내용으로 업데이트 됩니다. 또한는 `UpdateConflictMessage` 방금 Label 컨트롤 사용자에 게 설명 합니다. 이 이벤트 시퀀스를 그림 19에 자세히 설명 되어 있습니다.


[![동시성 위반의에서는 업데이트 내용이 손실 s 사용자](implementing-optimistic-concurrency-cs/_static/image54.png)](implementing-optimistic-concurrency-cs/_static/image53.png)

**그림 19**: A의 업데이트의 동시성 위반을에서 손실 됩니다 ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image55.png))


> [!NOTE]
> 또는 GridView 미리 편집 상태를 반환 하는 대신 수 상태로 두면 GridView 편집 상태에서 설정 하 여는 `KeepInEditMode` 전달 기능에 대 한 속성 `GridViewUpdatedEventArgs` 개체 true입니다. 하지만이 방법을 사용를 확신할 수 데이터를 GridView에 바인딩됩니다 (호출 하 여 해당 `DataBind()` 메서드)을 다른 사용자의 값 편집 인터페이스에 로드 됩니다. 이 자습서와 함께 다운로드할 수 있는 코드에이 두 줄의 코드는 `RowUpdated` 주석으로 이벤트 처리기;이 줄의 코드는 GridView에 동시성 위반을 후 편집 모드에 그대로 주석 처리를 단순히 제거 합니다.


## <a name="responding-to-concurrency-violations-when-deleting"></a>동시성 위반을 삭제할 때 응답

DB 직접 패턴으로는 동시성 위반이 발생할 때 발생 하는 예외가 없습니다. 대신, database 문이 WHERE 절 인 모든 레코드와 일치 하지 않습니다으로 레코드가 없는 단순히에 적용 됩니다. BLL에서 만든 데이터 수정 방법을 정확 하 게 하나의 레코드를 영향을 여부를 나타내는 부울 값을 반환 되도록 설계 되었습니다. 따라서 동시성 위반을 레코드를 삭제할 때 발생 하는 경우를 확인 하려면를 조사할 수 있습니다는 BLL의 반환 값 `DeleteProduct` 메서드.

BLL 메서드에 대 한 반환 값을 통해 ObjectDataSource의 사후 수준의 이벤트 처리기에서 검사할 수 있습니다는 `ReturnValue` 의 속성은 `ObjectDataSourceStatusEventArgs` 개체를 이벤트 처리기에 전달 합니다. 반환 값을 결정 하는 데 관심이 있으므로 `DeleteProduct` ObjectDataSource의에 대 한 이벤트 처리기를 만들 필요 메서드를 `Deleted` 이벤트입니다. `ReturnValue` 형식의 속성은 `object` 수 및 `null` 경우 예외가 발생 하 고 메서드가 값을 반환할 수 전에 중단 되었습니다. 따라서에서는 먼저 확인 해야 하는 `ReturnValue` 속성은 없습니다 `null` 은 부울 값입니다. 이 검사에 통과 매개 변수를 표시 하는 것으로 가정은 `DeleteConflictMessage` 경우 레이블 컨트롤의 `ReturnValue` 은 `false`합니다. 다음 코드를 사용 하 여이 수행할 수 있습니다.


[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample14.cs)]

동시성 위반을 한 경우에도 사용자의 삭제 요청이 취소 됩니다. GridView는 사용자 시간부터 해당 레코드에 대해 발생 한 변경 내용을 로드 되는 페이지 및 삭제 단추를 클릭 하면 그 보여 주는 새로 고쳐집니다. 이러한 위반은 그러한 경우는 `DeleteConflictMessage` 레이블이 표시 됩니다 (그림 20 참조)만 발생 합니다.


[![사용자 삭제의 동시성 위반이 발생 한 경우에도 취소 됩니다.](implementing-optimistic-concurrency-cs/_static/image57.png)](implementing-optimistic-concurrency-cs/_static/image56.png)

**그림 20**: 동시성 위반이 발생 한 경우에도 삭제 취소 되는 사용자 s ([전체 크기 이미지를 보려면 클릭](implementing-optimistic-concurrency-cs/_static/image58.png))


## <a name="summary"></a>요약

동시성 위반 기회가 여러 수 있는 모든 응용 프로그램에 존재 하는 동시 사용자 데이터를 업데이트 또는 삭제 합니다. 경우 이러한 위반은 두 명의 사용자가 누구 든 지 가져옵니다에서 마지막 쓰기 "wins"에 있는 동일한 데이터를 동시에 업데이트 변경 내용을 변경 하면 다른 사용자의 덮어쓰지에 대해서 고려 하지 않습니다. 또는 개발자가 어느 낙관적 또는 비관적 동시성 제어를 구현할 수 있습니다. 낙관적 동시성 제어 가정 동시성 위반 빈번 하지 않습니다 및 단순히 업데이트를 허용 하지 않는 명령에 해당 합니다 동시성 위반을 삭제 합니다. 비관적 동시성 제어는 동시성 위반 빈도가 및 단순히 한 사용자의 거부 된 업데이트 또는 삭제 명령 허용 되지 않는 가정 합니다. 비관적 동시성 제어와 레코드 업데이트 잠가, 다른 사용자가을 수정 하거나 잠겨 있는 동안에 레코드를 삭제 하면 것을 방지 합니다.

.NET에서 형식의 DataSet 낙관적 동시성 제어를 지원 하기 위한 기능을 제공 합니다. 특히는 `UPDATE` 및 `DELETE` 모든 테이블의 열을 포함 하는 데이터베이스에 실행 한 문은, 경우에 현재 데이터 레코드의 사용자를 원래 데이터와 일치 하는 경우 update 또는 delete만 발생 하는지 해 확인 자신의 update 또는 delete를 수행 합니다. 낙관적 동시성을 지원 하기 위해 DAL를 구성한 후 BLL 메서드를 업데이트 해야 합니다. 또한 BLL에 호출 하는 ASP.NET 페이지는 ObjectDataSource 데이터 웹 컨트롤에서 원래 값을 검색 하 고 아래 BLL에 전달 되도록 구성 되어야 합니다.

DAL 및 BLL 업데이트 하 고 ASP.NET 페이지에이 자습서에서 살펴본 것 처럼 ASP.NET 웹 응용 프로그램에서 낙관적 동시성 제어를 구현 해야 합니다. 이 추가 된 작업의 시간과 노력이 현명한 투자 인지 아닌지 응용 프로그램에 따라 달라 집니다. 자주 동시 사용자 데이터를 업데이트 했거나 업데이트 하는 데이터는 서로 다른를 다음 동시성 제어 없으면 가장 중요 한 것입니다. 그러나 정기적으로 여러 사용자가 동일한 데이터를 사용할 사이트에, 하는 경우 동시성 제어 한 사용자의 업데이트나 삭제 작업 다른 사용자의 실수로 덮어쓰지 하지 않도록 할 수 있습니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

> [!div class="step-by-step"]
> [이전](customizing-the-data-modification-interface-cs.md)
> [다음](adding-client-side-confirmation-when-deleting-cs.md)
