---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-vb
title: 데이터 액세스 레이어의 연결 및 명령 수준 설정 (VB) 구성 | Microsoft Docs
author: rick-anderson
description: 자동으로 입력 데이터 집합에서 TableAdapters 데이터베이스에 연결 명령을 실행 하 고 결과 사용 하 여 DataTable을 채우는 주의 하는 중...
ms.author: aspnetcontent
ms.date: 08/03/2007
ms.assetid: d57dfa2b-d627-45cb-b5b1-abbf3159d770
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-vb
msc.type: authoredcontent
ms.openlocfilehash: 6d8f5aa0e114d22a3192b89f190baa83315bfa8c
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37818293"
---
<a name="configuring-the-data-access-layers-connection--and-command-level-settings-vb"></a>데이터 액세스 레이어의 연결 및 명령 수준 설정 (VB) 구성
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_72_VB.zip) 또는 [PDF 다운로드](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/datatutorial72vb1.pdf)

> 자동으로 입력 데이터 집합에서 TableAdapters 데이터베이스에 연결 명령을 실행 하 고 결과 사용 하 여 DataTable을 채우는 주의 합니다. 하지만 TableAdapter에 데이터베이스 연결 및 명령 수준 설정에 액세스 하는 방법을 알아보겠습니다 직접 이러한 세부 정보 및이 자습서에서는 처리 하려는 경우 경우가 있습니다.


## <a name="introduction"></a>소개

자습서 시리즈 전체에 데이터 액세스 계층 및 비즈니스 개체 계층화 된 아키텍처의 구현 하기 위해 형식화 된 데이터 집합 사용 했습니다. 에 설명 된 대로 합니다 [첫 번째 자습서](../introduction/creating-a-data-access-layer-vb.md)를 TableAdapters를 검색 및 기본 데이터를 수정 하려면 데이터베이스와 통신 하는 래퍼 역할도 하는 반면 데이터의 리포지토리로 사용 되는 Datatable 형식의 DataSet s입니다. Tableadapter는 데이터베이스 작업과 관련 된 복잡성을 캡슐화 하 고 데이터베이스에 연결, 명령 실행 또는 테이블로 결과 채우는 코드를 작성 하지 않고도 덕분입니다.

그러나 TableAdapter에 대 한 깊이 있는 땅 속에 ADO.NET 개체와 직접 작동 하는 코드를 작성 해야 경우 경우가 있습니다. 에 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md) 자습서, 예를 들어 추가한 메서드 시작, 커밋 및 ADO.NET 트랜잭션 롤백에 대 한 TableAdapter에 합니다. 이러한 메서드를 사용 하는 내부 수동으로 만든 `SqlTransaction` TableAdapter s에 할당 된 개체 `SqlCommand` 개체입니다.

이 자습서는 TableAdapter의 데이터베이스 연결 및 명령 수준 설정에 액세스 하는 방법을 살펴보겠습니다. 특히 기능을 추가 합니다 `ProductsTableAdapter` 수 있도록 기본 연결 문자열에 대 한 액세스를 명령 제한 시간 설정입니다.

## <a name="working-with-data-using-adonet"></a>ADO.NET을 사용 하 여 데이터를 사용 하 여 작업

Microsoft.NET Framework는 다양 한 데이터와 함께 작동 하도록 특별히 설계 된 클래스를 포함 합니다. 내에 있는 이러한 클래스는 [ `System.Data` 네임 스페이스](https://msdn.microsoft.com/library/system.data.aspx), 라고 합니다 *ADO.NET* 클래스입니다. 특정에 연결 된 일부 클래스 ADO.NET 산하 *데이터 공급자*합니다. 데이터 공급자의 정보 흐름 ADO.NET 클래스와 기본 데이터 저장소를 허용 하는 통신 채널을으로 생각할 수 있습니다. 특정 데이터베이스 시스템에 대해 특별히 설계 된 공급자 뿐만 아니라 OleDb 및 ODBC와 같은 일반화 된 공급자가 있습니다. 예를 들어, OleDb 공급자를 사용 하 여 Microsoft SQL Server 데이터베이스에 연결할 수 있지만, SqlClient 공급자는 훨씬 더 효율적으로 디자인 되었으며 특히 SQL Server에 최적화 된.

데이터를 프로그래밍 방식으로 액세스할 때 다음 패턴을 일반적으로 사용 됩니다.

1. 데이터베이스에 대 한 연결을 설정 합니다.
2. 명령을 실행 합니다.
3. 에 대 한 `SELECT` 쿼리 결과 레코드를 사용 하 여 작동 합니다.

이러한 각 단계를 수행 하기 위한 별도 ADO.NET 클래스가 있습니다. SqlClient 공급자를 사용 하 여 데이터베이스에 연결 하려면 예를 들어, 사용 된 [ `SqlConnection` 클래스](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection(VS.80).aspx)합니다. 문제에는 `INSERT`, `UPDATE`를 `DELETE`, 또는 `SELECT` 명령을 사용 하 여 데이터베이스에는 [ `SqlCommand` 클래스](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.aspx)합니다.

제외 하 고는 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md) 자습서에서는 하지 했습니다 Tableadapter 자동으로 생성 된 코드를 포함 하는 데 필요한 기능 때문에 낮은 수준의 ADO.NET 코드 직접 작성 하려면 데이터베이스에 연결, 명령을 실행, 데이터를 검색 및 Datatable에 데이터를 채웁니다. 그러나 이러한 하위 수준 설정을 사용자 지정 하려면 먼저 경우가 있을 수 있습니다. 다음 몇 단계를 통해 TableAdapters에서 내부적으로 사용 하는 ADO.NET 개체를 활용 하는 방법을 살펴보겠습니다.

## <a name="step-1-examining-with-the-connection-property"></a>1 단계: 연결 속성을 사용 하 여 검사

각 TableAdapter 클래스에는 `Connection` 데이터베이스 연결 정보를 지정 하는 속성입니다. 이 속성의 데이터 형식 및 `ConnectionString` 값 TableAdapter 구성 마법사에서 선택한 항목에 의해 결정 됩니다. 회수는 먼저 TableAdapter 형식화 된 데이터 집합을 추가할 때이 마법사에서는 데이터베이스에 대 한 원본 (그림 1 참조). 이 첫 번째 단계에서 드롭 다운 목록 데이터 연결 서버 탐색기에서에서 다른 데이터베이스를 비롯 하 여 구성 파일에 지정 된 해당 데이터베이스를 포함 합니다. 사용 하려는 데이터베이스 드롭다운 목록에 없는 경우 새 연결 단추를 클릭 하 고 필요한 연결 정보를 제공 하 여 새 데이터베이스 연결을 지정할 수 있습니다.


[![TableAdapter 구성 마법사의 첫 번째 단계](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image2.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image1.png)

**그림 1**: TableAdapter 구성 마법사의 첫 번째 단계는 ([큰 이미지를 보려면 클릭](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image3.png))


Let s TableAdapter s에 대 한 코드를 검사할 잠시 `Connection` 속성입니다. 설명한 것 처럼 합니다 [데이터 액세스 레이어 만들기](../introduction/creating-a-data-access-layer-vb.md) 자습서, 클래스 뷰 창으로 이동 하 고 드릴 다운 적절 한 클래스에 다음 멤버 이름을 두 번 클릭 하 여 자동으로 생성 된 TableAdapter 코드를 볼 수 있습니다.

보기 메뉴로 이동 하 고 클래스 뷰를 선택 하 여 (또는 Ctrl + Shift + C를 눌러) 클래스 보기 창으로 이동 합니다. 클래스 뷰 창의 위쪽 절반에서 드릴 다운 하는 `NorthwindTableAdapters` 네임 스페이스를 선택 하 고는 `ProductsTableAdapter` 클래스. 이 표시 됩니다는 `ProductsTableAdapter`의 멤버 아래에 있는 그림 2 에서처럼 클래스 보기의 절반입니다. 두 번 클릭 합니다 `Connection` 속성을 해당 코드를 참조 하세요.


![자동으로 생성 된 코드를 보려면 클래스 뷰에서 연결 속성을 두 번 클릭](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image4.png)

**그림 2**: 자동으로 생성 된 코드를 보려면 클래스 뷰에서 연결 속성을 두 번 클릭


TableAdapter가의 `Connection` 속성 및 기타 연결 관련 코드 다음과 같습니다.


[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample1.vb)]

TableAdapter 클래스의 인스턴스가 만들어질 때, 멤버 변수 `_connection` 값과 같음 `Nothing`합니다. 경우는 `Connection` 있는지 먼저 확인 속성에 액세스할를 `_connection` 멤버 변수를 인스턴스화해야 합니다. 되지 않은 경우는 `InitConnection` 인스턴스화하는 메서드가 호출 되 `_connection` 설정 하 고 해당 `ConnectionString` TableAdapter 구성 마법사가 첫 번째 단계에서 지정 된 연결 문자열 값 속성입니다.

합니다 `Connection` 속성에 할당할 수도 있습니다는 `SqlConnection` 개체입니다. 새 연결 이렇게 `SqlConnection` TableAdapter s의 각 개체 `SqlCommand` 개체입니다.

## <a name="step-2-exposing-connection-level-settings"></a>2 단계: 연결 수준의 설정은 노출

연결 정보를 TableAdapter 내에서 캡슐화 된 상태로 유지 하 고 다른 계층 응용 프로그램 아키텍처에 액세스할 수 없게 해야 합니다. 그러나 TableAdapter가의 연결 수준 정보에 액세스할 수 없거나 쿼리, 사용자 또는 ASP.NET 페이지에 대 한 사용자 지정 가능 해야 하는 경우 시나리오 있을 수 있습니다.

확장 s는 `ProductsTableAdapter` 에 `Northwind` 포함할 데이터 집합에는 `ConnectionString` 읽거나 TableAdapter에서 사용 하는 연결 문자열을 변경 하는 비즈니스 논리 계층에서 사용할 수 있는 속성.

> [!NOTE]
> A *연결 문자열* 는 데이터베이스, 인증 자격 증명 및 기타 데이터베이스 관련 설정의 위치를 사용 하려면 공급자와 같은 데이터베이스 연결 정보를 지정 하는 문자열입니다. 다양 한 데이터 저장소 및 공급자에서 사용 되는 연결 문자열 패턴의 목록에 대해서 [ConnectionStrings.com](http://www.connectionstrings.com/)합니다.


에 설명 된 대로 합니다 [데이터 액세스 레이어 만들기](../introduction/creating-a-data-access-layer-vb.md) 자습서에서는 입력 데이터 집합이의 자동으로 생성 된 클래스는 partial 클래스를 사용 하 여 확장할 수 있습니다. 먼저 프로젝트에 새 하위 폴더를 만듭니다 `ConnectionAndCommandSettings` 아래는 `~/App_Code/DAL` 폴더입니다.


![ConnectionAndCommandSettings 라는 하위 폴더를 추가 합니다.](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image5.png)

**그림 3**: 라는 하위 폴더를 추가 합니다. `ConnectionAndCommandSettings`


라는 새 클래스 파일 추가 `ProductsTableAdapter.ConnectionAndCommandSettings.vb` 다음 코드를 입력 합니다.


[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample2.vb)]

이 partial 클래스 추가 `Public` 라는 속성이 `ConnectionString` 에 `ProductsTableAdapter` 읽거나 기본 연결이 tableadapter에 대 한 연결 문자열을 업데이트 하려면 모든 계층을 허용 하는 클래스입니다.

이 partial 클래스를 사용 하 여 (저장)를 만들고 엽니다는 `ProductsBLL` 클래스입니다. 기존 방법 중 하나로 이동 하 고 입력 `Adapter` 및 IntelliSense를 불러오려면 기간 키를 누릅니다. 새 표시 `ConnectionString` 속성 IntelliSense, 즉는 프로그래밍 방식으로 읽을 하거나 조정할 수 있습니다 BLL에서이 값에서에서 사용할 수 있습니다.

## <a name="exposing-the-entire-connection-object"></a>전체 연결 개체를 노출합니다.

이 partial 클래스는 기본 연결 개체의 속성을 하나만 노출: `ConnectionString`합니다. 전체 연결 개체를 TableAdapter의 범위를 벗어나면 사용할 수 있도록 하려는 경우 변경할 수 있습니다 또는 `Connection`의 속성 보호 수준입니다. 1 단계에서에서 검사할 자동으로 생성 된 코드를 설명 하는 TableAdapter s 했습니다 `Connection` 속성으로 표시 됩니다 `Friend`, 것만 액세스할 수 있는지는 동일한 어셈블리에 클래스로 의미 합니다. 이 변경할 수 있지만 TableAdapter s를 통해 `ConnectionModifier` 속성입니다.

열기는 `Northwind` 데이터 집합을 클릭 합니다 `ProductsTableAdatper` 디자이너에서 속성 창으로 이동 합니다. 이 표시 됩니다는 `ConnectionModifier` 기본값인으로 `Assembly`합니다. 있도록를 `Connection` 변경 형식화 된 데이터 집합의 어셈블리 외부에서 사용할 수 있는 속성을 `ConnectionModifier` 속성을 `Public`입니다.


[![연결 속성 s 액세스 가능성 수준 ConnectionModifier 속성을 통해 구성할 수 있습니다.](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image7.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image6.png)

**그림 4**: 합니다 `Connection` 를 통해 액세스 가능성 수준을 구성할 수 있습니다 s 속성을 `ConnectionModifier` 속성 ([전체 크기 이미지를 보려면 클릭](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image8.png))


데이터 집합을 저장 한 다음를 반환 합니다 `ProductsBLL` 클래스입니다. 이전에 기존 방법 중 하나로 이동 하 고 입력 `Adapter` 및 IntelliSense를 불러오려면 기간 키를 누릅니다. 목록에 포함 해야는 `Connection` 속성에는 이제 프로그래밍 방식으로 읽거나 있습니다 BLL에서 연결 수준의 설정은 모든 할당을 의미 합니다.

## <a name="step-3-examining-the-command-related-properties"></a>3 단계: 명령 관련 속성 검사

기본적으로 자동으로 생성 하는 기본 쿼리는 TableAdapter 구성 `INSERT`, `UPDATE`, 및 `DELETE` 문입니다. 이 주 쿼리 s `INSERT`, `UPDATE`, 및 `DELETE` 문을 통해 ADO.NET 데이터 어댑터 개체로 TableAdapter가의 코드에서 구현 됩니다는 `Adapter` 속성입니다. 와 마찬가지로 해당 `Connection` 속성을 `Adapter`의 속성 데이터 형식은 사용 되는 데이터 공급자에 의해 결정 됩니다. 이 자습서는 SqlClient 공급자를 사용 하므로 합니다 `Adapter` 형식의 속성은 [ `SqlDataAdapter` ](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter(VS.80).aspx)합니다.

TableAdapter s `Adapter` 속성이 유형의 세 가지 속성 `SqlCommand` 를 사용 하는 문제를 `INSERT`를 `UPDATE`, 및 `DELETE` 문:

- `InsertCommand`
- `UpdateCommand`
- `DeleteCommand`

A `SqlCommand` 개체는 데이터베이스에 특정 쿼리를 전송 하는 일을 담당 하며 같은 속성이: [ `CommandText` ](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtext.aspx), 임시 SQL 문이나 저장된 프로시저 실행을 포함 하 고 [ `Parameters` ](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.parameters.aspx)의 컬렉션인 `SqlParameter` 개체입니다. 다시 살펴본 것 처럼 합니다 [데이터 액세스 레이어 만들기](../introduction/creating-a-data-access-layer-vb.md) 자습서에서는이 명령은 속성 창을 통해 개체를 사용자 지정할 수 있습니다.

TableAdapter의 기본 쿼리 외에도 다양 한 메서드를 포함할 수 있습니다를 호출 하면 디스패치 데이터베이스에 지정된 된 명령입니다. 기본 쿼리의 명령 개체 및 모든 추가 메서드에 대해 명령 개체는 tableadapter에 저장 됩니다 `CommandCollection` 속성입니다.

Let s 잠시에서 생성 된 코드를 확인 합니다 `ProductsTableAdapter` 에 `Northwind` 이러한 두 속성 및 해당 멤버 변수를 지원 및 도우미 메서드에 대 한 데이터 집합:


[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample3.vb)]

에 대 한 코드를 `Adapter` 하 고 `CommandCollection` 속성에는 항목을 밀접 하 게 모방는 `Connection` 속성입니다. 속성을 사용 하는 개체를 보유할 멤버 변수가 있습니다. 속성을 `Get` 접근자는 해당 멤버 변수를 확인 하 여 시작 `Nothing`합니다. 그렇다면 멤버 변수의 인스턴스를 만들고 핵심 명령 관련 속성을 할당 하는 초기화 메서드 호출 됩니다.

## <a name="step-4-exposing-command-level-settings"></a>4 단계: 노출 명령 수준 설정

이상적으로 명령 수준 정보를 캡슐화 된 데이터 액세스 계층 내에서 유지 되어야 합니다. 그러나이 정보는 아키텍처의 다른 계층에 필요, 것 노출 될 수 있습니다 부분 클래스를 통해 마찬가지로 연결 수준 설정을 사용 하 여 합니다.

TableAdapter에만 단일에 있으므로 `Connection` 속성인 연결 수준의 설정을 노출 하기 위한 코드는 매우 간단 합니다. TableAdapter는 여러 명령 개체를 포함할 수 있으므로 명령 수준 설정 수정 하는 경우 작업은 좀 더 복잡 한는 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand`에서 명령 개체의 변수 수와 함께 `CommandCollection` 속성입니다. 명령 수준 설정, 업데이트 하는 경우 이러한 설정은 모든 명령 개체에 전파 해야 합니다.

예를 들어는 별도 작업 실행 시간이 오래 걸리는 TableAdapter에 특정 쿼리 된 한다고 가정 합니다. TableAdapter를 사용 하 여 이러한 쿼리 중 하나를 실행 하려면, s 명령 개체를 증가 하려고 수 [ `CommandTimeout` 속성](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtimeout.aspx)합니다. 이 속성 명령이 실행 될 때까지 기다리는 시간 (초)를 지정 하며 기본값은 30입니다.

수 있도록 합니다 `CommandTimeout` BLL은으로 조정 해야 하는 속성에는 다음 추가 `Public` 메서드를 합니다 `ProductsDataTable` 2 단계에서에서 만든 partial 클래스 파일을 사용 하 여 (`ProductsTableAdapter.ConnectionAndCommandSettings.vb`):


[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample4.vb)]

이 메서드는 TableAdapter 인스턴스에서 모든 명령 문제에 대 한 명령 제한 시간을 설정 하려면 BLL 또는 프레젠테이션 계층에서 호출할 수 없습니다.

> [!NOTE]
> `Adapter` 하 고 `CommandCollection` 속성으로 표시 됩니다 `Private`, 즉 TableAdapter 내의 코드에서 액세스할 수만 있습니다. 달리는 `Connection` 속성, 이러한 액세스 한정자는 구성할 수 없습니다. 따라서 아키텍처의 다른 계층에 명령 수준 속성을 노출 하는 경우 제공 하려면 위에서 설명한 partial 클래스 접근 방식을 사용 해야 합니다는 `Public` 메서드 또는 속성을 읽거나 쓸는 `Private` 명령 개체입니다.


## <a name="summary"></a>요약

입력 데이터 집합에서 TableAdapters 데이터 액세스 세부 정보 및 복잡성을 캡슐화를 제공 합니다. Tableadapter를 사용 했습니다 없는 데이터베이스에 연결, 명령 실행 또는 테이블로 결과 채우는 ADO.NET 코드를 작성 하는 방법에 대 한 걱정 합니다. 모든 처리 됩니다 자동으로 주세요.

그러나 경우 연결 문자열 또는 기본 연결이 나 명령을 시간 제한 값을 변경 하는 등 낮은 수준의 ADO.NET 세부 정보를 사용자 지정 해야 하는 경우가 있을 수 있습니다. TableAdapter에 자동으로 생성 `Connection`, `Adapter`, 및 `CommandCollection` 있지만 속성은 `Friend` 또는 `Private`, 기본적으로 합니다. 이 내부 정보를 포함 하도록 partial 클래스를 사용 하 여 TableAdapter를 확장 하 여 노출 될 수 있습니다 `Public` 메서드 또는 속성입니다. Tableadapter 한편 `Connection` TableAdapter s를 통해 속성 액세스 한정자를 구성할 수 있습니다 `ConnectionModifier` 속성입니다.

즐거운 프로그래밍!

## <a name="about-the-author"></a>저자 소개

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적의 저자 이자 설립자입니다 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 Microsoft 웹 기술을 사용 하 여 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는 [ *Sams 설명 직접 ASP.NET 2.0 24 시간 동안의*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 그에 도달할 수 있습니다 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com) 찾을 수 있는 저자의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자 Burnadette Leigh, S ren Jacob Lauritsen Teresa Murphy 및 Hilton Geisenow 되었습니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](working-with-computed-columns-vb.md)
> [다음](protecting-connection-strings-and-other-configuration-information-vb.md)
