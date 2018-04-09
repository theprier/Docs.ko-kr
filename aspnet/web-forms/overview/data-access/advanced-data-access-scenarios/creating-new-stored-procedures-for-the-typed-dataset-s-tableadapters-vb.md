---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
title: 형식화 된 데이터 집합의 Tableadapter (VB)에 대 한 저장 프로시저 새로 만들기 | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서 생성 된 코드에서 SQL 문을 했으며 문을 실행할 데이터베이스에 전달 합니다. 다른 방법은 s를 사용 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/18/2007
ms.topic: article
ms.assetid: a5a4a9ba-d18d-489a-a6b0-a3c26d6b0274
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
msc.type: authoredcontent
ms.openlocfilehash: 3df3623f5575a48a22fb1a2c3bc719975a80b9c6
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="creating-new-stored-procedures-for-the-typed-datasets-tableadapters-vb"></a>형식화 된 데이터 집합의 Tableadapter (VB)에 대 한 새로운 저장 프로시저
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_67_VB.zip) 또는 [PDF 다운로드](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/datatutorial67vb1.pdf)

> 이전 자습서에서 생성 된 코드에서 SQL 문을 했으며 문을 실행할 데이터베이스에 전달 합니다. 다른 접근 방식은 SQL 문은 데이터베이스에서 미리 정의 된 저장된 프로시저를 사용 하는 것입니다. 이 자습서에서는 TableAdapter 마법사 us에 대 한 새 저장된 프로시저를 생성 하는 방법에 설명 합니다.


## <a name="introduction"></a>소개

이 자습서에 대 한 데이터 액세스 계층 (DAL) 형식의 데이터 집합을 사용합니다. 에 설명 된 대로 [데이터 액세스 계층을 만들려면](../introduction/creating-a-data-access-layer-vb.md) 자습서, 강력한 형식의 DataTables 및 Tableadapter의 형식화 된 데이터 집합으로 구성 합니다. Datatable 데이터 액세스 작업을 수행 하려면 기본 데이터베이스를 사용 하 여 Tableadapter 인터페이스 하는 동안 시스템에서 논리적 엔터티를 나타냅니다. 여기에 데이터가 있는 Datatable을 채우는, 스칼라 데이터를 반환 하는 쿼리를 실행 하 고 삽입, 업데이트 및 데이터베이스에서 레코드를 삭제 합니다.

Tableadapter에서 실행 되는 SQL 명령 중 하나가 임시 SQL 문이 같은 수 `SELECT columnList FROM TableName`, 또는 저장 프로시저입니다. Tableadapter 가이드의 아키텍처에는 임시 SQL 문을 사용 합니다. 하지만 많은 개발자 및 데이터베이스 관리자 보안, 유지 관리의 편의성 및 updateability 이유로 임시 SQL 문을 통해 저장된 프로시저를 선호 합니다. 다른 유연성에 대 한 임시 SQL 문이 ardently 선호합니다. 나만의 작업에서는 임시 SQL 문이 저장된 프로시저 우선적 했지만 이전 자습서를 간소화 하기 위해 임시 SQL 문 사용 하도록 선택 했습니다.

때 TableAdapter를 정의 하거나 새 메서드 추가, TableAdapter의 마법사를 사용 것과 마찬가지로 쉽게 새 저장된 프로시저 만들기 또는 임시 SQL 문을 사용 하는 것 처럼 기존 저장된 프로시저를 사용 합니다. 이 자습서에서는 자동 생성 저장된 프로시저 TableAdapter의 마법사 하는 방법을 검토 합니다. 다음 자습서 기존와 수동으로 만든 저장된 프로시저를 사용 하는 TableAdapter의 메서드를 구성 하는 방법을 살펴보겠습니다.

> [!NOTE]
> Rob Howard의 블로그 항목을 참조 [Don 저장 프로시저 아직 사용 t?](http://grokable.com/2003/11/dont-use-stored-procedures-yet-must-be-suffering-from-nihs-not-invented-here-syndrome/) 및 [프랑 Bouma](https://weblogs.asp.net/fbouma/) s 블로그 항목 [저장 프로시저는 불량 M Kay?](https://weblogs.asp.net/fbouma/archive/2003/11/18/38178.aspx) 의 장단점에 역동적인 토론에 대 한 저장된 프로시저 및 임시 SQL 합니다.


## <a name="stored-procedure-basics"></a>저장된 프로시저 기본 사항

함수는 모든 프로그래밍 언어에 공통적으로 적용 되는 구문입니다. 함수는 함수를 호출할 때 실행 되는 문 모음입니다. 함수는 입력된 매개 변수를 사용할 수 있습니다 및 필요에 따라 값을 반환할 수 있습니다. *[저장 프로시저](http://en.wikipedia.org/wiki/Stored_procedure)*  는 프로그래밍 언어의 함수와 많은 공통점이 공유 하는 데이터베이스 구조입니다. 저장된 프로시저는 저장된 프로시저를 호출할 때 실행 되는 T-SQL 문 집합 이루어져 있습니다. 저장된 프로시저는 많은 입력된 매개 변수를 0을 허용할 수 있습니다 및 스칼라 값, 출력 매개 변수를 반환할 수 있습니다, 가장 일반적으로 결과에서 설정 하거나 `SELECT` 쿼리 합니다.

> [!NOTE]
> 저장된 프로시저는 종종 sprocs 또는 Sp 라고 합니다.


저장된 프로시저를 사용 하 여 만들어집니다는 [ `CREATE PROCEDURE` ](https://msdn.microsoft.com/library/aa258259(SQL.80).aspx) T-SQL 문입니다. 예를 들어 다음 T-SQL 스크립트 저장된 프로시저를 만듭니다 `GetProductsByCategoryID` 라는 단일 매개 변수를 사용 하 `@CategoryID` 반환는 `ProductID`, `ProductName`, `UnitPrice`, 및 `Discontinued` 필드의 열에는 `Products` 일치 하는 테이블 `CategoryID` 값:


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample1.sql)]

이 저장된 프로시저를 만든 후 다음 구문을 사용 하 여 호출할 수 있습니다.


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample2.sql)]

> [!NOTE]
> 다음 자습서는 Visual Studio IDE에서 저장된 프로시저를 만들면 살펴보겠습니다. 그러나이 자습서에서는 하겠습니다 us에 대 한 저장된 프로시저를 자동으로 생성 된 TableAdapter 마법사를 통해.


데이터를 단순히 반환 하는 것 외에도 저장된 프로시저는 단일 트랜잭션의 범위 내에서 여러 데이터베이스 명령을 수행 하려면 자주 사용 됩니다. 라는 저장된 프로시저 `DeleteCategory`, 예를 들어 걸릴 수 있습니다는 `@CategoryID` 매개 변수 두 개를 수행 하 고 `DELETE` 문을: 관련된 제품 및 지정 된 범주를 삭제 하면 다른 하나를 삭제 하려면 먼저 하나입니다. 저장된 프로시저 내에 여러 명령문은 *하지* 트랜잭션 내에서 자동으로 줄 바꿈된 합니다. 추가 T-SQL 명령을 여러 명령을 원자 단위 연산으로 처리 되는 s 저장된 프로시저를 위해 실행 해야 합니다. 이후 자습서에서 사용 되는 트랜잭션의 범위 내에서 저장된 프로시저의 명령을 래핑하는 방법을 살펴보겠습니다.

아키텍처 내에서 저장된 프로시저를 사용 하는 경우 데이터 액세스 계층의 메서드 임시 SQL 문을 실행 하는 것이 아니라 특정 저장된 프로시저를 호출 합니다. 이 응용 프로그램의 아키텍처 내에서 정의 하는 것이 아니라에서 SQL 문 실행 (데이터베이스)의 위치를 중앙 집중화 합니다. 풀링할 때 이러한 중앙 집중식 찾을, 분석 및 쿼리를 튜닝 작업을 좀 더 쉽게 하 게 되 고 데이터베이스가 사용 되 고 위치 및 방법에 대 한 훨씬 더 명확 하 게 그림을 제공 합니다.

저장된 프로시저 기본 사항에 대 한 자세한 내용은이 자습서의 끝에 추가 정보 섹션의 리소스를 참조 하십시오.

## <a name="step-1-creating-the-advanced-data-access-layer-scenarios-web-pages"></a>1 단계: 고급 데이터 액세스 계층 시나리오 웹 페이지 만들기

저장된 프로시저를 사용 하 여 DAL를 만드는 방법에 논의 시작 하기 전에 s를 먼저 잠시이 기능 및 다음 몇 가지 자습서에 대 한 필요한 웹 사이트 프로젝트에 ASP.NET 페이지를 만들 수 있습니다. 라는 새 폴더를 추가 하 여 시작 `AdvancedDAL`합니다. 다음에 해당 폴더에 있는 각 페이지에 연결할 수 있도록 다음 ASP.NET 페이지 추가 `Site.master` 마스터 페이지:

- `Default.aspx`
- `NewSprocs.aspx`
- `ExistingSprocs.aspx`
- `JOINs.aspx`
- `AddingColumns.aspx`
- `ComputedColumns.aspx`
- `EncryptingConfigSections.aspx`
- `ManagedFunctionsAndSprocs.aspx`


![고급 데이터 액세스 계층 시나리오 자습서에 대 한 ASP.NET 페이지 추가](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image1.png)

**그림 1**: 고급 데이터 액세스 계층 시나리오 자습서에 대 한 ASP.NET 페이지 추가


다른 폴더에서와 같이 `Default.aspx` 에 `AdvancedDAL` 폴더는 해당 섹션의 자습서를 나열 합니다. 이전에 설명한 대로 `SectionLevelTutorialListing.ascx` 이 기능을 제공 하는 사용자 정의 컨트롤입니다. 따라서이 사용자 정의 컨트롤을 추가 `Default.aspx`의 디자인 뷰에서 페이지 하려면 솔루션 탐색기에서 끌어서 합니다.


[![Default.aspx로 SectionLevelTutorialListing.ascx 사용자 정의 컨트롤 추가](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image3.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image2.png)

**그림 2**: 추가 된 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 `Default.aspx` ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image4.png))


마지막으로, 이러한 페이지에 항목으로 추가 된 `Web.sitemap` 파일입니다. 특히, 일괄 처리 된 데이터로 작업 한 후 다음 태그를 추가 `<siteMapNode>`:


[!code-xml[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample3.xml)]

업데이트 한 후 `Web.sitemap`, 브라우저를 통해 자습서 웹 사이트를 보려면 보십시오. 이제는 왼쪽 메뉴에서 고급 DAL 시나리오 자습서에 대 한 항목이 포함 됩니다.


![이제 사이트 맵 고급 DAL 시나리오 자습서에 대 한 항목을 포함](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image5.png)

**그림 3**: 이제 사이트 맵 고급 DAL 시나리오 자습서에 대 한 항목을 포함


## <a name="step-2-configuring-a-tableadapter-to-create-new-stored-procedures"></a>2 단계: 저장 프로시저를 새로 만드는 TableAdapter를 구성 합니다.

임시 SQL 문 대신 저장된 프로시저를 사용 하는 데이터 액세스 계층을 만드는 작업을 보여 주기 위해 let s 만들 새 입력 데이터 집합에는 `~/App_Code/DAL` 라는 폴더 `NorthwindWithSprocs.xsd`합니다. 에서는 이전 자습서에서 자세히이 프로세스를 통해 실행, 이후 나와 있는 단계를 통해 신속 하 게 진행 됩니다. 어려운 점이 있거나 단계별 지침을 만들고 입력 데이터 집합을 구성에 추가 해야 하는 경우 다시 참조는 [데이터 액세스 계층을 만들려면](../introduction/creating-a-data-access-layer-vb.md) 자습서입니다.

마우스 오른쪽 단추로 클릭 하 여 새 데이터 집합을 프로젝트에 추가 `DAL` 폴더를 그림 4에 나와 있는 것 처럼에 데이터 집합 서식 파일을 선택 하 고 새 항목 추가 선택 합니다.


[![NorthwindWithSprocs.xsd 이라는 프로젝트에 새 형식화 된 데이터 집합 추가](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image7.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image6.png)

**그림 4**: 프로젝트 이름이 새 입력 데이터 집합을 추가 `NorthwindWithSprocs.xsd` ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image8.png))


이 새 입력 데이터 집합을 만듭니다 해당 디자이너를 열고, 새 TableAdapter를 만들고 TableAdapter 구성 마법사를 시작 합니다. TableAdapter 구성 마법사 s 첫 번째 단계를 요청 하는 실행 되도록 데이터베이스를 선택 하 합니다. Northwind 데이터베이스에 연결 문자열은 드롭 다운 목록에 나열 되어야 합니다. 이 옵션을 선택 하 고 클릭 합니다.

이 다음 화면에서 TableAdapter는 데이터베이스에 액세스 하는 방법을 선택할 수 있습니다. 이전 자습서의 첫 번째 옵션을 사용 하 여 SQL 문을 선택합니다. 이 자습서에 대 한 두 번째 옵션을 선택 하 고 새 저장된 프로시저 만들기 다음을 클릭 합니다.


[![새 저장된 프로시저를 만들 TableAdpater 지시 합니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image10.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image9.png)

**그림 5**: 새 저장 프로시저 만들기에 TableAdpater 지시 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image11.png))


임시 SQL 문을 사용 하 여, 다음 단계에서에서는 입력 하도록 요청 하는 것 처럼는 `SELECT` TableAdapter s 주 쿼리에 대 한 문을 합니다. 하지만 사용 하는 대신는 `SELECT` 문에서 임시 쿼리를 직접 수행 하려면 여기에 입력 된 TableAdapter s 만들어집니다.이 포함 하는 저장된 프로시저 `SELECT` 쿼리 합니다.

다음을 사용 하 여 `SELECT` 이 TableAdapter에 대 한 쿼리:


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample4.sql)]


[![선택 쿼리를 입력 합니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image13.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image12.png)

**그림 6**: 입력의 `SELECT` 쿼리 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image14.png))


> [!NOTE]
> 위의 쿼리는의 주 쿼리에서 약간 다릅니다는 `ProductsTableAdapter` 에 `Northwind` 형식화 된 데이터 집합입니다. 이전에 설명한 대로 `ProductsTableAdapter` 에 `Northwind` 형식화 된 데이터 집합 범주 이름 및 각 s 제품 범주와 공급 업체에 대 한 회사 이름을 다시 가져오기 하려면 두 개의 상관된 하위 쿼리를 포함 합니다. [TableAdapter를 사용 하 여 조인 업데이트](updating-the-tableadapter-to-use-joins-vb.md) 이 TableAdapter에 관련 데이터를이 추가 대해서는 자습서입니다.


고급 옵션 단추를 클릭 하 여 보십시오. 여기에서 마법사도를 생성할지 여부를 insert, update 및 delete 문을 TableAdapter, 낙관적 동시성을 사용할 것인지 및 삽입과 업데이트 후 데이터 테이블 새로 고쳐야 하면 여부에 대 한를 지정할 수 있습니다. 생성 Insert, Update 및 Delete 문 옵션은 기본적으로 선택 됩니다. 체크 둡니다. 이 자습서에서 사용 하 여 낙관적 동시성 옵션을 선택 취소 되어 있음 둡니다.

TableAdapter 마법사에서 자동으로 생성 하는 저장된 프로시저를 데 새로 고침 데이터 테이블 옵션 무시 되도록 나타납니다. 이 확인란이 선택 되어 있는지 여부, 결과 삽입 및 업데이트에 관계 없이 저장된 프로시저 3 단계에서에서 알 수 있듯이 방금 삽입 또는 업데이트 just 레코드를 검색 합니다.


![옵션을 선택 하는 생성 Insert, Update 및 Delete 문을 상태로 둡니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image15.png)

**그림 7**: 옵션을 선택 하는 생성 Insert, Update 및 Delete 문을 그대로 둡니다.


> [!NOTE]
> 마법사는 추가 조건에는 사용 하 여 낙관적 동시성 옵션을 선택 하는 경우 추가 `WHERE` 데이터가 다른 필드에 변경 내용이 있는 경우 업데이트 하는 것을 방지 하는 절. 다시 참조는 [낙관적 동시성 구현](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md) TableAdapter s 기본 제공 낙관적 동시성 제어 기능을 사용 하 여 대 한 자세한 내용은 자습서입니다.


입력 한 후의 `SELECT` 쿼리하고 다음 클릭 생성 Insert, Update 및 Delete 문 옵션이 선택 되어 있는지를 확인 합니다. 그림 8 에서처럼이 다음 화면에서 만들어집니다. 저장된 프로시저의 이름을 선택, 삽입, 업데이트 및 데이터 삭제에 대 한 메시지가 표시 됩니다. 이러한 저장 프로시저 이름을 변경 `Products_Select`, `Products_Insert`, `Products_Update`, 및 `Products_Delete`합니다.


[![저장된 프로시저 이름 바꾸기](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image17.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image16.png)

**그림 8**: 저장 프로시저 이름 바꾸기 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image18.png))


TableAdapter 마법사는 네 개의 저장된 프로시저를 만드는 데 사용할 T-SQL을 보려면 SQL 스크립트 미리 보기 단추를 클릭 합니다. SQL 스크립트 미리 보기 대화 상자에서 스크립트를 파일에 저장 되거나 클립보드로 복사 있습니다.


![저장된 프로시저를 생성 하는 데 SQL 스크립트를 미리 보려면](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image19.png)

**그림 9**: 저장된 프로시저를 생성 하는 데 SQL 스크립트 미리 보기


저장된 프로시저 이름을 지정 후 이름 TableAdapter s 해당 메서드 옆을 클릭 합니다. 임시 SQL 문이 사용할 때와 마찬가지로 기존 DataTable 채우기 또는 새 반환 하는 메서드를 만들 수 있습니다. TableAdapter 삽입, 업데이트 및 삭제 레코드에 대 한 DB 부하 패턴을 포함할지 여부를 지정할 수도 있습니다. 이 옵션을 선택 하는 모든 세 확인란 나 가지만 반환 하는 DataTable 메서드 이름 바꾸기 `GetProducts` (에서처럼 그림 10).


[![메서드 이름을 채우기 및 GetProducts](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image21.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image20.png)

**그림 10**: 메서드 이름을 `Fill` 및 `GetProducts` ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image22.png))


마법사가 수행할 단계를 요약 한를 보려면 다음을 클릭 합니다. "마침" 단추를 클릭 하 여 마법사를 완료 합니다. 마법사가 완료 되 면 돌아갑니다 DataSet s 이제 포함 해야 하는 디자이너에는 `ProductsDataTable`합니다.


[![데이터 집합의 디자이너 새로 추가 된 ProductsDataTable를 보여 줍니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image24.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image23.png)

**그림 11**: 새로 추가 된 데이터 집합의 디자이너 표시 `ProductsDataTable` ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image25.png))


## <a name="step-3-examining-the-newly-created-stored-procedures"></a>3 단계: 검사 새로 만든된 저장된 프로시저

2 단계에서에서 자동으로 사용 되는 TableAdapter 마법사는 선택, 삽입, 업데이트 및 데이터를 삭제 하기 위한 저장된 프로시저를 생성 합니다. 이러한 저장된 프로시저를 표시 하거나 서버 탐색기로 이동 하는 데이터베이스 s Stored Procedures 폴더에 드릴 다운 하 여 Visual Studio를 통해 수정할 수 있습니다. 그림 12에서 볼 수 있듯이 Northwind 데이터베이스에는 네 개의 새 저장된 프로시저: `Products_Delete`, `Products_Insert`, `Products_Select`, 및 `Products_Update`합니다.


![2 단계에서 만든 네 개의 저장된 프로시저는 데이터베이스 s 저장된 프로시저 폴더에서 찾을 수 있습니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image26.png)

**그림 12**: s 데이터베이스 저장된 프로시저 폴더에 2 단계에서 만든 네 개의 저장된 프로시저를 찾을 수


> [!NOTE]
> 서버 탐색기에 표시 되지 않는 경우 보기 메뉴를 이동한 서버 탐색기 옵션을 선택 합니다. 2 단계에서에서 추가 제품 관련 된 저장된 프로시저 표시 되지 않으면 저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택를 새로 고칩니다.


를 확인 하거나 저장된 프로시저를 수정 하려면 서버 탐색기에서 해당 이름을 두 번 클릭 하거나, 또는 저장된 프로시저를 마우스 오른쪽 단추로 클릭 하 고 열기를 선택 합니다. 그림 13은는 `Products_Delete` 저장 프로시저를 열 때.


[![저장된 프로시저 열고 Visual Studio 내에서 수정할 수](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image28.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image27.png)

**그림 13**: 저장 프로시저 열 수 및 수정에서 내에서 Visual Studio ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image29.png))


두는 `Products_Delete` 및 `Products_Select` 저장된 프로시저는 매우 간단 합니다. `Products_Insert` 및 `Products_Update` 저장된 프로시저를 모두 수행 하는 정밀 검사를 보증 반면에 `SELECT` 문을 한 후 해당 `INSERT` 및 `UPDATE` 문. 예를 들어 다음 SQL 모여는 `Products_Insert` 저장 프로시저:


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample5.sql)]

저장된 프로시저는 입력된 매개 변수로 받아들입니다는 `Products` 에서 반환 된 열은 `SELECT` TableAdapter의 마법사 및 이러한 값에 지정 된 쿼리에 사용 되는 `INSERT` 문. 다음은 `INSERT` 문는 `SELECT` 쿼리를 사용 하 여 반환 하는 `Products` 열 값 (포함 하는 `ProductID`) 새로 추가 된 레코드의 합니다. 새로 추가 된 업데이트를 사용 하 여 일괄 처리 업데이트 패턴 것으로 자동으로 새 레코드를 추가 하는 경우이 새로 고침 기능이 유용 합니다. `ProductRow` 인스턴스 `ProductID` 데이터베이스에서 할당 된 자동 증분 값을 사용 하 여 속성입니다.

다음 코드에서는이 기능을 보여 줍니다. 포함 된는 `ProductsTableAdapter` 및 `ProductsDataTable` 에 대해 생성 된 `NorthwindWithSprocs` 형식화 된 데이터 집합입니다. 새 제품을 만들어 데이터베이스에 추가 되는 `ProductsRow` 인스턴스를 해당 값을 제공 하 고 TableAdapter s 호출 `Update` 전달 하는 메서드는 `ProductsDataTable`합니다. Tableadapter 내부적으로 `Update` 메서드 열거는 `ProductsRow` 전달 된 DataTable의 인스턴스 (이 예제의 하나 뿐입니다-방금 추가한 하나)를 수행 하 고 적절 한 삽입, 업데이트 또는 삭제 명령입니다. 이 경우에 `Products_Insert` 저장된 프로시저가 실행 되 면 새 레코드를 추가 하는 `Products` 테이블 및 새로 추가 된 레코드의 세부 정보를 반환 합니다. `ProductsRow` 인스턴스의 `ProductID` 값이 업데이트 됩니다. 이후에 `Update` 메서드가 완료, s 새로 추가 된 레코드에 액세스할 수 있습니다 `ProductID` 통해 값는 `ProductsRow` s `ProductID` 속성입니다.


[!code-vb[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample6.vb)]

`Products_Update` 마찬가지로 저장된 프로시저를 포함 한 `SELECT` 다음 문을 해당 `UPDATE` 문.


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample7.sql)]

에 대 한 두 개의 입력된 매개 변수를 포함 하는이 저장 프로시저는 참고 `ProductID`: `@Original_ProductID` 및 `@ProductID`합니다. 이 기능을 통해 시나리오의 기본 키를 변경 될 수 있습니다. 예를 들어 직원 데이터베이스에 각 직원 레코드로 사용할 수 있습니다 직원의 사회 보장 번호 해당 기본 키입니다. 기존 직원의 주민 등록 번호를 변경 하려면 새 주민 등록 번호와 원래 제공 되어야 합니다. 에 대 한는 `Products` 때문에 테이블, 이러한 기능은 필요 하지 않습니다는 `ProductID` 열은 프로그램 `IDENTITY` 열 이며 변경할 수 없습니다. 실제로 `UPDATE` 의 문에서 `Products_Update` 저장된 프로시저 대상이 포함 되어는 `ProductID` 열 목록에 있는 열입니다. 따라서 동안 `@Original_ProductID` 에 사용 되는 `UPDATE` 문이 s `WHERE` 는 대 한 불필요 절은 `Products` 테이블 및으로 대체할 수 있습니다는 `@ProductID` 매개 변수입니다. 저장된 프로시저 s 매개 변수를 수정 하는 경우 반드시 해당 저장된 프로시저를 사용 하는 TableAdapter 메서드에 업데이트 됩니다.

## <a name="step-4-modifying-a-stored-procedure-s-parameters-and-updating-the-tableadapter"></a>4 단계: 저장된 프로시저 s 매개 변수를 수정 및 TableAdapter를 업데이트 합니다.

이후는 `@Original_ProductID` 매개 변수는 불필요, let s에서 제거는 `Products_Update` 완전히 저장 프로시저입니다. 열기는 `Products_Update` 저장 프로시저를 삭제는 `@Original_ProductID` 매개 변수를 누르고는 `WHERE` 절은 `UPDATE` 문, 매개 변수 이름에서 사용 되는 변경 `@Original_ProductID` 를 `@ProductID`합니다. 다음과 같이 변경한 후 T-SQL 저장된 프로시저 내에서 다음과 같이 표시 됩니다.


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample8.sql)]

데이터베이스를 이러한 변경 내용을 저장 하려면 도구 모음에 저장 아이콘을 클릭 하거나 Ctrl + S를 적중 합니다. 이 시점에서 `Products_Update` 저장된 프로시저에 필요 하지 않으면는 `@Original_ProductID` 입력된 매개 변수는 있지만 TableAdapter 이러한 매개 변수를 전달 하도록 구성 됩니다. TableAdapter에 송신할 매개 변수를 볼 수는 `Products_Update` 데이터 집합 디자이너에서 TableAdapter를 선택 하면 속성 창으로 이동 하 고에서 줄임표를 클릭 하 여 저장 프로시저는 `UpdateCommand` s `Parameters` 컬렉션입니다. 이 그림 14에 표시 된 매개 변수 컬렉션 편집기 대화 상자를 엽니다.


![매개 변수 컬렉션 편집기 목록이 사용 되는 매개 변수는 Products_Update에 전달 된 저장 프로시저](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image30.png)

**그림 14**:에 전달 된 매개 변수 컬렉션 편집기 목록이 사용 되는 매개 변수는 `Products_Update` 저장 프로시저


선택 하 여 여기에서이 매개 변수를 제거할 수 있습니다는 `@Original_ProductID` 제거 단추를 클릭 하 고 멤버 목록에서 매개 변수입니다.

또는 메서드 중 일부에 대 한 디자이너에서 TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 구성을 선택 하 여 사용 되는 매개 변수를 새로 고칠 수 있습니다. 이 선택, 삽입, 업데이트에 사용 되는 저장된 프로시저 나열 하면 TableAdapter 구성 마법사가 나타납니다 및 매개 변수와 함께 삭제 저장된 프로시저 받을 가능성이 있습니다. 업데이트 드롭 다운 목록에서 클릭 하는 경우 확인할 수 없습니다는 `Products_Update` 저장된 프로시저는 이제 더 이상 포함 된 입력된 매개 변수를 예상 `@Original_ProductID` (그림 15 참조). TableAdapter에 사용 되는 매개 변수 컬렉션을 자동으로 업데이트 하려면 마침을 클릭 하면 됩니다.


[![또는 TableAdapter의 구성 마법사를 사용 하 여 해당 메서드 매개 변수 컬렉션을 새로 고칠 수 있습니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image32.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image31.png)

**그림 15**: tableadapter 구성 마법사가 해당 메서드 매개 변수 컬렉션 새로 고침 하는 데 사용할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image33.png))


## <a name="step-5-adding-additional-tableadapter-methods"></a>5 단계: 추가 TableAdapter 메서드 추가

설명 된 단계 2로 새 TableAdapter를 만들 때 쉽습니다을 자동으로 생성 하는 해당 저장된 프로시저. TableAdapter에 추가 메서드를 추가 하는 경우 true입니다. S 추가 하도록이 설명 하기는 `GetProductByProductID(productID)` 메서드는 `ProductsTableAdapter` 2 단계에서에서 만든 합니다. 이 메서드가 걸립니다 입력으로는 `ProductID` 값 및 지정된 된 제품에 대 한 세부 정보를 반환 합니다.

TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 추가 쿼리를 선택 하 여 시작 합니다.


![TableAdapter에 새 쿼리 추가](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image34.png)

**그림 16**: TableAdapter에 새 쿼리 추가


TableAdapter는 데이터베이스에 액세스 하는 방법에 대 한 먼저 입력 하 라는 TableAdapter 쿼리 구성 마법사가 시작 됩니다. 만든 새 저장된 프로시저를 하려면 새 저장된 프로시저 옵션을 선택 하 고 클릭 합니다.


[![새 저장된 프로시저 옵션을 선택](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image36.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image35.png)

**그림 17**: 새 저장된 프로시저 옵션을 선택 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image37.png))


다음 화면에서는 쿼리를 실행, 행 또는 단일 스칼라 값의 집합을 반환 합니다 또는 수행의 유형을 식별 하는 `UPDATE`, `INSERT`, 또는 `DELETE` 문. 이후는 `GetProductByProductID(productID)` 메서드는 행을 반환, row 옵션을 선택한 다음 적중 반환 하는 SELECT를 그대로 둡니다.


[![Row 옵션을 반환 하는 선택](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image39.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image38.png)

**그림 18**: 옵션 행을 반환 하는 선택 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image40.png))


다음 화면 TableAdapter s 주 쿼리의 저장된 프로시저의 이름 목록이 표시 됩니다 (`dbo.Products_Select`). 다음 저장된 프로시저 이름을 바꿉니다 `SELECT` 문에서 지정된 된 제품에 대 한 제품 필드를 모두 반환 합니다.


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample9.sql)]


[![선택 쿼리를 저장된 프로시저 이름 바꾸기](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image42.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image41.png)

**그림 19**: 저장 프로시저 이름을으로 대체 한 `SELECT` 쿼리 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image43.png))


후속 화면에서는 생성 되는 저장된 프로시저 이름을 지정 합니다. 이름을 입력 `Products_SelectByProductID` 고 다음을 클릭 합니다.


[![새 저장된 프로시저 Products_SelectByProductID 이름](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image45.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image44.png)

**그림 20**: 새 저장 프로시저 이름을 `Products_SelectByProductID` ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image46.png))


마법사의 마지막 단계를 메서드 이름을 생성으로 채우기 사용할지 DataTable 패턴을 변경, DataTable 패턴 중 하나 또는 둘 다 반환할 수 있습니다. 이 메서드에 대 한 옵션을 선택 하는 두 옵션을 유지 되지만 하는 메서드 이름을 바꿀 `FillByProductID` 및 `GetProductByProductID`합니다. 다음 마법사를 수행 하 고 마법사를 완료 하려면 마침을 클릭 단계의 요약 정보를 보려면 클릭 합니다.


[![FillByProductID 및 GetProductByProductID TableAdapter의 메서드 이름 바꾸기](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image48.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image47.png)

**그림 21**:에 TableAdapter의 메서드 이름 바꾸기 `FillByProductID` 및 `GetProductByProductID` ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image49.png))


TableAdapter는 새 메서드를 사용할 수 있는 마법사를 완료 한 후 `GetProductByProductID(productID)` 는 호출 되 면 실행 됩니다는 `Products_SelectByProductID` 방금 만든 프로시저를 저장 합니다. Stored Procedures 폴더에 차례로 드릴를 열어 서버 탐색기에서 새 저장된 프로시저를 보려면 잠시 `Products_SelectByProductID` (표시 되지 않으면 저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 새로 고침을 선택).

`SelectByProductID` 저장 프로시저는 `@ProductID` 입력된 매개 변수로 실행 하 고는 `SELECT` 마법사에 회사 이름을 입력 하는 문을 합니다.


[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample10.sql)]

## <a name="step-6-creating-a-business-logic-layer-class"></a>6 단계: 비즈니스 논리 계층 클래스 만들기

자습서 시리즈 프레젠테이션 계층 내용을 모든 호출에는 비즈니스 논리 BLL (계층)의 계층화 된 아키텍처를 유지 하기 위해 strived가 있습니다. 디자인 결정을 내리게 준수, 하려면 먼저 클래스를 만드는 BLL 새 형식화 된 데이터 집합에 대 한 프레젠테이션 계층에서 제품 데이터에 액세스할 수 있습니다 전에 해야 합니다.

라는 새 클래스 파일을 만들 `ProductsBLLWithSprocs.vb` 에 `~/App_Code/BLL` 폴더 다음 코드를 추가 합니다.


[!code-vb[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample11.vb)]

이 클래스를 모방는 `ProductsBLL` 클래스 사용 되지만 이전 자습서에서 의미 체계는 `ProductsTableAdapter` 및 `ProductsDataTable` 에서 개체는 `NorthwindWithSprocs` 데이터 집합입니다. 예를 들어는 것이 아니라는 `Imports NorthwindTableAdapters` 으로 클래스 파일의 시작 부분에 문을 `ProductsBLL` ,는 `ProductsBLLWithSprocs` 클래스에서 사용 하 `Imports NorthwindWithSprocsTableAdapters`합니다. 마찬가지로,는 `ProductsDataTable` 및 `ProductsRow` 이 클래스에서 사용 되는 개체와 접두사는 `NorthwindWithSprocs` 네임 스페이스입니다. `ProductsBLLWithSprocs` 클래스는 두 가지 데이터 액세스 메서드를 제공 `GetProducts` 및 `GetProductByProductID`, 및 메서드를 추가, 업데이트 및 단일 제품 인스턴스를 삭제 합니다.

## <a name="step-7-working-with-thenorthwindwithsprocsdataset-from-the-presentation-layer"></a>7 단계: 작업에서`NorthwindWithSprocs`프레젠테이션 계층에서 데이터 집합

이 시점에서 저장된 프로시저를 사용 하 여 액세스 하 고 기본 데이터베이스 데이터를 수정 하는 DAL을 만들었습니다. 또한 모든 제품 또는 특정 제품 함께 메서드를 추가, 업데이트 및 삭제 제품을 검색 하는 방법과 함께 기초적인 BLL를 구축 했으므로 합니다. 이 자습서를 반올림 하려면 let s BLL s를 사용 하는 ASP.NET 페이지를 만들 `ProductsBLLWithSprocs` 표시, 업데이트 및 삭제할 레코드에 대 한 클래스입니다.

열기는 `NewSprocs.aspx` 페이지에 `AdvancedDAL` 폴더 및 이름을 지정 하 고 디자이너 도구 상자에서 끌어서는 GridView `Products`합니다. GridView에서 s 스마트 태그 라는 새 ObjectDataSource 바인딩할 선택 `ProductsDataSource`합니다. ObjectDataSource 사용 하도록 구성 된 `ProductsBLLWithSprocs` 22 그림에에서 나와 있는 것 처럼 클래스입니다.


[![ObjectDataSource ProductsBLLWithSprocs 클래스를 사용 하도록 구성](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image51.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image50.png)

**그림 22**: 구성에 사용 하 여 ObjectDataSource는 `ProductsBLLWithSprocs` 클래스 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image52.png))


선택 탭의 드롭다운 목록에 두 가지 옵션이 `GetProducts` 및 `GetProductByProductID`합니다. GridView에서 모든 제품을 전시 하기 할 것 이므로 선택 된 `GetProducts` 메서드. UPDATE, INSERT 및 DELETE 탭에 있는 드롭 다운 목록에는 한 가지 방법은 하기만 됩니다. 각 이러한 드롭 다운 목록에는 적절 한 방법을 선택 확인 하 한 다음 마침을 클릭 합니다.

ObjectDataSource 마법사를 완료 한 후 Visual Studio 제품 데이터 필드에 대 한 GridView에 BoundFields 및는 CheckBoxField 추가 합니다. 편집 사용 및 스마트 태그에 있는 삭제 사용 옵션을 선택 하 여 GridView s 기본 제공 편집 및 삭제 기능 켭니다.


[![페이지 편집 및 삭제 지원이 설정 된 GridView에 포함](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image54.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image53.png)

**그림 23**: 페이지에는 편집 및 삭제 지원을 사용 하도록 설정 된 GridView 포함 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image55.png))


म으로 했습니다 설명 ObjectDataSource의 마법사 완료 시 이전 자습서에서 Visual Studio 설정에서 `OldValuesParameterFormatString` 원래 속성\_{0}. 이 해야 작동 하도록 데이터 수정 기능에 대 한 순서 대로 {0}의 기본값으로 되돌릴 수 제대로 우리의 BLL에 메서드에서 필요한 매개 변수를 제공 합니다. 따라서로 설정 해야는 `OldValuesParameterFormatString` {0}에는 속성 또는 선언적 구문에서 속성을 모두 제거 합니다.

설정 편집 및 삭제 GridView에서 지원 및 ObjectDataSource s를 반환 하는 데이터 소스 구성 마법사를 완료 한 후 `OldValuesParameterFormatString` 속성의 기본값을, s 페이지 선언적 태그 다음과 같이 표시 됩니다.


[!code-aspx[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample12.aspx)]

이 시점에서 있습니다 수를 정리 GridView 유효성 검사를 포함 하도록 편집 하는 인터페이스를 사용자 지정 하 여 필요는 `CategoryID` 및 `SupplierID` 열 dropdownlist 활용, 렌더링 및 등입니다. 클라이언트 쪽 확인 삭제 단추를 추가할 수도 있습니다 및 이러한 향상 된이 기능을 구현 하는 시간이을 확인해 보십시오. 그러나 이러한 항목 이전 자습서에서 설명 되었을, 이후 하지 다룰 것으로 다시 여기입니다.

여부 또는 not GridView 향상에 관계 없이 브라우저에서 페이지의 핵심 기능을 테스트 합니다. 그림 24에서 볼 수 있듯이 페이지는 행별 편집 및 삭제 기능을 제공 하는 GridView에 제품을 나열 합니다.


[![제품 보기, 편집 및 GridView에서 삭제](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image57.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image56.png)

**그림 24**: The 제품 볼 수 있습니다, 편집, 및 GridView에서 삭제 됨 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image58.png))


## <a name="summary"></a>요약

형식화 된 데이터 집합에서 TableAdapters 임시 SQL 문을 사용 하 여 데이터베이스에서 또는 저장된 프로시저를 통해 데이터에 액세스할 수 있습니다. TableAdapter 마법사는 새로 만드는 하도록 할 수 있습니다 또는 때 저장된 프로시저를 사용에 기존의 저장된 프로시저 중 하나를 사용할 수 있습니다에 대 한 저장 프로시저에 따라는 `SELECT` 쿼리 합니다. 이 자습서에서는 저장된 프로시저를 자동으로 생성 하는 방법을 탐색할 했습니다.

저장된 프로시저를 사용 하면 자동으로 생성 된 시간을 절약 하면서 마법사 대상이 t가 만든 저장된 프로시저에 어떤 것 만들어져 자체에 맞춰 있는 경우도 있습니다. 한 가지 예는 `Products_Update` 저장 프로시저를 둘 다 필요 합니다. `@Original_ProductID` 및 `@ProductID` 도 입력 매개 변수는 `@Original_ProductID` 된 불필요 한 매개 변수입니다.

대부분의 시나리오에서 저장된 프로시저 생성 이미 또는 더욱 세밀 하 게 저장된 프로시저의 명령에 대 한 제어 하기 위해 수동으로 작성 하는 것이 좋겠습니다. 두 경우 모두 해당 메서드에 대 한 기존 저장된 프로시저를 사용 하 여 TableAdapter를 지시 해야 합니다. 다음 자습서에서이 수행 하는 방법을 표시 해야 합니다.

만족도 매우 프로그래밍!

## <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [저장 프로시저를 만들고 유지 관리](https://msdn.microsoft.com/library/aa214299(SQL.80).aspx)
- [저장된 프로시저에서 스칼라 데이터 검색](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)
- [SQL Server 저장 프로시저 기본 사항](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1)
- [저장된 프로시저: 개요](http://www.sqlteam.com/item.asp?ItemID=563)
- [저장된 프로시저를 작성합니다.](http://www.4guysfromrolla.com/webtech/111499-1.shtml)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Hilton Geisenow 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs.md)
> [다음](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
