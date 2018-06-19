---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-vb
title: 데이터 액세스 계층 연결 및 명령 수준 설정 (VB) 구성 | Microsoft Docs
author: rick-anderson
description: 자동으로 입력 데이터 집합 내에서 Tableadapter 데이터베이스에 연결, 명령, 발급 및 결과 DataTable을 채우는 처리 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 08/03/2007
ms.topic: article
ms.assetid: d57dfa2b-d627-45cb-b5b1-abbf3159d770
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-vb
msc.type: authoredcontent
ms.openlocfilehash: b73c6113e84e290025e5835781fa2f85587289b1
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30877179"
---
<a name="configuring-the-data-access-layers-connection--and-command-level-settings-vb"></a>데이터 액세스 계층 연결 및 명령 수준 설정 (VB) 구성
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_72_VB.zip) 또는 [PDF 다운로드](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/datatutorial72vb1.pdf)

> 자동으로 입력 데이터 집합 내에서 Tableadapter 데이터베이스에 연결, 명령, 발급 및 결과 DataTable을 채우는 주의 합니다. TableAdapter에 데이터베이스 연결 및 명령 수준 설정에 액세스 하는 방법을 배울 스스로 이러한 세부 정보 및이 자습서에서는 처리 하려는 경우 있지만 경우가 있습니다.


## <a name="introduction"></a>소개

자습서 시리즈 전체 가이드의 계층화 된 아키텍처의 비즈니스 개체 및 데이터 액세스 계층 구현 하기 위해 형식화 된 데이터 집합 사용 했습니다. 에 설명 된 대로 [첫 번째 자습서](../introduction/creating-a-data-access-layer-vb.md), 형식화 된 데이터 집합 s TableAdapters가 검색 하 고 기본 데이터를 수정할 데이터베이스와 통신 하는 래퍼를 프록시로 반면 데이터의 리포지토리로 사용 되는 Datatable입니다. Tableadapter는 데이터베이스 작업에 관련 된 복잡성을 캡슐화 하 고 데이터베이스에 연결, 명령 실행 또는 DataTable에 결과 채우는 코드를 작성 하지 않아도 구성할 필요가 있습니다.

그러나 TableAdapter의 안쪽으로 은신처 고 ADO.NET 개체와 직접 통신 하는 코드를 작성 해야 경우 경우가 있습니다. 에 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md) 자습서에서는 예를 들어 추가 메서드를 시작, 커밋 및 ADO.NET 트랜잭션 롤백에 대 한 합니다. 이러한 메서드는 내부 사용 수동으로 만든 `SqlTransaction` TableAdapter s에 할당 된 개체 `SqlCommand` 개체입니다.

이 자습서는 TableAdapter의 데이터베이스 연결 및 명령 수준 설정에 액세스 하는 방법을 살펴보겠습니다. 특히, 기능을 추가 합니다는 `ProductsTableAdapter` 수 있도록 내부 연결 문자열에 대 한 액세스 및 명령 제한 시간 설정 합니다.

## <a name="working-with-data-using-adonet"></a>ADO.NET을 사용 하 여 데이터 작업

Microsoft.NET Framework는 다량의 데이터와 함께 작동 하도록 특별히 설계 된 클래스를 포함 합니다. 내에 있는이 클래스는 [ `System.Data` 네임 스페이스](https://msdn.microsoft.com/library/system.data.aspx)는 라고 하는 *ADO.NET* 클래스입니다. 특정에 연결 된 일부 ADO.NET 포괄적인 아래 클래스 *데이터 공급자*합니다. 데이터 공급자의 정보는 ADO.NET 클래스 및 기본 데이터 저장소 간에 전달 될 수 있는 통신 채널으로 생각할 수 있습니다. 특정 데이터베이스 시스템에 대해 특별히 고안 된 공급자 뿐만 아니라 OleDb는 ODBC와 같은 일반화 된 공급자가 있습니다. 예를 들어 ole Db 공급자를 사용 하 여 Microsoft SQL Server 데이터베이스에 연결할 수 있지만 SqlClient 공급자는 훨씬 더 효율적을 설계 하 고 SQL Server에 대해 특히 최적화.

데이터를 프로그래밍 방식으로 액세스할 때 다음 패턴은 일반적으로 사용 됩니다.

1. 데이터베이스에 대 한 연결을 설정 합니다.
2. 명령을 실행 합니다.
3. 에 대 한 `SELECT` 쿼리 결과 레코드를 사용 합니다.

이러한 각 단계를 수행 하기 위한 별도 ADO.NET 클래스가 있습니다. SqlClient 공급자를 사용 하는 데이터베이스에 연결할 사용 예를 들어는 [ `SqlConnection` 클래스](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection(VS.80).aspx)합니다. 문제에는 `INSERT`, `UPDATE`, `DELETE`, 또는 `SELECT` 명령을 사용 하 여 데이터베이스에는 [ `SqlCommand` 클래스](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.aspx)합니다.

제외 하 고는 [트랜잭션 내에서 데이터베이스 수정 내용을 래핑](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md) 자습서에서는 발생 하지 Tableadapter 자동 생성 된 코드는 데 필요한 기능을 포함 하기 때문에 직접 하위 수준 ADO.NET 코드 작성 데이터베이스에 연결 명령을 실행 데이터를 검색 및 Datatable에 해당 데이터를 채웁니다. 그러나 이러한 하위 수준 설정을 사용자 지정 해야 우리는 경우가 있을 수 있습니다. 다음 몇 단계를 통해 Tableadapter에서 내부적으로 사용 하는 경우 ADO.NET 개체에 간단 하는 방법을 살펴보겠습니다.

## <a name="step-1-examining-with-the-connection-property"></a>1 단계: 연결 속성 검토

각 TableAdapter 클래스에는 `Connection` 데이터베이스 연결 정보를 지정 하는 속성입니다. 이 속성의 데이터 형식 및 `ConnectionString` 값 TableAdapter 구성 마법사에서 선택 내용에 따라 결정 됩니다. 회수는 형식화 된 데이터 집합에 TableAdapter를 처음 추가할 때이 마법사에서는 데이터베이스에 대 한 원본 (그림 1 참조). 이 첫 번째 단계에서 드롭 다운 목록에 서버 탐색기의 데이터 연결의에서 다른 데이터베이스를 비롯 하 여 구성 파일에 지정 된 해당 데이터베이스에 포함 됩니다. 사용 하려는 데이터베이스 드롭 다운 목록에 없는 경우 새 연결 단추를 클릭 하 고 필요한 연결 정보를 제공 하 여 새 데이터베이스 연결을 지정할 수 있습니다.


[![TableAdapter 구성 마법사의 첫 번째 단계](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image2.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image1.png)

**그림 1**: TableAdapter 구성 마법사의 첫 번째 단계 ([전체 크기 이미지를 보려면 클릭](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image3.png))


Let s 보십시오 TableAdapter s에 대 한 코드 검사 `Connection` 속성입니다. 설명한 것 처럼는 [데이터 액세스 계층을 만들려면](../introduction/creating-a-data-access-layer-vb.md) 자습서, 클래스 뷰 창으로 이동 하 고 적절 한 클래스에 액세스 한 다음 멤버 이름을 두 번 클릭 하 여 자동으로 생성 된 TableAdapter 코드 볼 수 있습니다.

보기 메뉴를 이동 하 고 클래스 뷰를 선택 하 여 (또는 Ctrl + Shift + C를 입력 하 여) 클래스 뷰 창으로 이동 합니다. 클래스 뷰 창 상단에서 드릴 다운 하는 `NorthwindTableAdapters` 네임 스페이스를 선택 하 고는 `ProductsTableAdapter` 클래스입니다. 이 표시 됩니다는 `ProductsTableAdapter`의 멤버 아래에 있는 그림 2에 나와 있는 것 처럼 클래스 뷰의 절반입니다. 두 번 클릭 하 여 `Connection` 속성을 동시에 코드를 참조 하십시오.


![해당 자동 생성 된 코드를 보려면 클래스 뷰의 연결 속성을 두 번 클릭](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image4.png)

**그림 2**: 해당 자동 생성 된 코드를 보려면 클래스 뷰의 연결 속성을 두 번 클릭


TableAdapter의 `Connection` 속성 및 기타 연결 관련 코드 다음과:


[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample1.vb)]

TableAdapter 클래스의 인스턴스가 만들어질 때, 멤버 변수 `_connection` 같으면 `Nothing`합니다. 경우는 `Connection` 속성에 액세스 하는 먼저 확인 하는 경우는 `_connection` 멤버 변수를 인스턴스화해야 합니다. 그렇지 않은 경우는 `InitConnection` 인스턴스화하는 메서드가 호출 되 `_connection` 설정 하 고 해당 `ConnectionString` 속성 TableAdapter 구성 마법사 s 첫 번째 단계에서 지정 된 연결 문자열 값을 합니다.

`Connection` 속성에 할당할 수도 있습니다는 `SqlConnection` 개체입니다. 새 연결 이렇게 `SqlConnection` TableAdapter s의 각 개체 `SqlCommand` 개체입니다.

## <a name="step-2-exposing-connection-level-settings"></a>2 단계: 노출 연결 수준 설정

연결 정보는 TableAdapter 내에서 캡슐화 된 상태로 유지 하 고 응용 프로그램 아키텍처의 다른 계층에 액세스할 수 없어야 해야 합니다. 그러나 TableAdapter의 연결 수준 정보에 액세스할 수 없거나 쿼리, 사용자 또는 ASP.NET 페이지에 대 한 사용자 지정 가능한 해야 할 때 시나리오 있을 수 있습니다.

확장 s는 `ProductsTableAdapter` 에 `Northwind` 포함 하도록 데이터 집합을 `ConnectionString` 속성을 읽거나 TableAdapter에서 사용 하는 연결 문자열을 변경 하는 비즈니스 논리 계층으로 사용할 수 있는 합니다.

> [!NOTE]
> A *연결 문자열* 데이터베이스, 인증 자격 증명 및 기타 데이터베이스 관련 설정의 위치를 사용 하려면 공급자와 같은 데이터베이스 연결 정보를 지정 하는 문자열입니다. 목록이 다양 한 데이터 저장소 및 공급자에서 사용 되는 연결 문자열 패턴에 대 한 참조 [ConnectionStrings.com](http://www.connectionstrings.com/)합니다.


에 설명 된 대로 [데이터 액세스 계층을 만들려면](../introduction/creating-a-data-access-layer-vb.md) 자습서에서는 형식화 된 데이터 집합의 자동 생성 된 클래스는 partial 클래스를 사용 하 여 확장할 수 있습니다. 먼저 라는 프로젝트에서 새 하위 폴더를 만듭니다 `ConnectionAndCommandSettings` 아래에서 `~/App_Code/DAL` 폴더입니다.


![ConnectionAndCommandSettings 라는 하위 폴더를 추가 합니다.](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image5.png)

**그림 3**: 라는 하위 폴더를 추가 합니다. `ConnectionAndCommandSettings`


라는 새 클래스 파일 추가 `ProductsTableAdapter.ConnectionAndCommandSettings.vb` 다음 코드를 입력 합니다.


[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample2.vb)]

이 partial 클래스에 추가 `Public` 라는 속성이 `ConnectionString` 에 `ProductsTableAdapter` 읽거나 업데이트 기본 연결이 TableAdapter s에 대 한 연결 문자열 내의 어느 계층을 허용 하는 클래스입니다.

이 partial 클래스와 (저장)를 만들고 엽니다는 `ProductsBLL` 클래스입니다. 기존 메서드 중 하나로 이동에 입력 `Adapter` 후 IntelliSense를 불러오는 마침표 키를 누릅니다. 새 나타나야 `ConnectionString` 속성을 의미 하거나 수 있는 프로그래밍 방식으로 읽을 BLL에서이 값을 조정 IntelliSense에서 사용할 수 있습니다.

## <a name="exposing-the-entire-connection-object"></a>전체 연결 개체를 노출합니다.

이 partial 클래스를 기본 연결 개체의 속성을 하나만 노출: `ConnectionString`합니다. 전체 연결 개체를 TableAdapter의 범위를 벗어나면 사용할 수 있도록 하려는 경우 변경할 수 있습니다 또는 `Connection` 속성의 보호 수준입니다. TableAdapter s는 1 단계에서에서 검사 했습니다 자동 생성 코드가 보인 `Connection` 속성이으로 표시 되 `Friend`는 수만 액세스할 수 있기 동일한 어셈블리의 클래스를 의미 합니다. 그러나이 변경할 수 있습니다, TableAdapter s 통해 `ConnectionModifier` 속성입니다.

열기는 `Northwind` 데이터 집합을 클릭 하는 `ProductsTableAdatper` 디자이너에서 속성 창으로 이동 합니다. 여기에서 `ConnectionModifier` 해당 기본값으로 설정 `Assembly`합니다. 있도록는 `Connection` 변경 형식의 DataSet의 어셈블리 외부에서 사용할 수 있는 속성은 `ConnectionModifier` 속성을 `Public`합니다.


[![연결 속성 s 액세스 가능성 수준 ConnectionModifier 속성을 통해 구성할 수 있습니다.](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image7.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image6.png)

**그림 4**:는 `Connection` 통한 속성 액세스 수준을 구성할 수 있습니다 s는 `ConnectionModifier` 속성 ([전체 크기 이미지를 보려면 클릭](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image8.png))


데이터 집합을 저장 한 다음으로 돌아가려면는 `ProductsBLL` 클래스입니다. 이전에 기존 방법 중 하나로 이동에 입력 하는 대로 `Adapter` 후 IntelliSense를 불러오는 마침표 키를 누릅니다. 목록에 포함 해야는 `Connection` 속성에는 이제 프로그래밍 방식으로 읽거나 있습니다 BLL에서 모든 연결 수준의 설정은 할당을 의미 합니다.

## <a name="step-3-examining-the-command-related-properties"></a>3 단계: 명령 관련 속성 검사

기본적으로는 자동으로 생성 하는 주 쿼리의 TableAdapter 구성 `INSERT`, `UPDATE`, 및 `DELETE` 문. 이 주 쿼리 s `INSERT`, `UPDATE`, 및 `DELETE` 문을 통해 ADO.NET 데이터 어댑터 개체로 TableAdapter의 코드에서 구현 됩니다는 `Adapter` 속성입니다. 와 함께 해당 `Connection` 속성에는 `Adapter`의 속성 데이터 형식이 사용 되는 데이터 공급자에 의해 결정 됩니다. 이 자습서에는 SqlClient 공급자를 사용 하므로 `Adapter` 형식의 속성은 [ `SqlDataAdapter` ](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter(VS.80).aspx)합니다.

TableAdapter s `Adapter` 속성에는 세 가지 속성 형식의 `SqlCommand` 위해 사용 하는 문제는 `INSERT`, `UPDATE`, 및 `DELETE` 문:

- `InsertCommand`
- `UpdateCommand`
- `DeleteCommand`

A `SqlCommand` 개체를 데이터베이스에 특정 쿼리를 보내는 같은 속성이: [ `CommandText` ](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtext.aspx), 임시 SQL 문 또는 저장된 프로시저는 실행를 포함 하 고 [ `Parameters` ](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.parameters.aspx)의 컬렉션인 `SqlParameter` 개체입니다. 다시에서 설명한 것 처럼는 [데이터 액세스 계층을 만들려면](../introduction/creating-a-data-access-layer-vb.md) 자습서에서는이 명령은 속성 창을 통해 개체를 사용자 지정할 수 있습니다.

TableAdapter의 주 쿼리에서 외에도 다양 한 수의 메서드를 포함할 수는 호출 되 면 데이터베이스에 지정된 된 명령을 디스패치합니다. 주 쿼리의 명령 개체 및 모든 추가 방법에 대해 명령 개체는 tableadapter에 저장 됩니다 `CommandCollection` 속성입니다.

Let s 보십시오에 의해 생성 된 코드는 `ProductsTableAdapter` 에 `Northwind` 이러한 두 속성 및 해당 멤버 변수를 지원 및 도우미 메서드에 대 한 데이터 집합:


[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample3.vb)]

에 대 한 코드는 `Adapter` 및 `CommandCollection` 속성에는 항목을 최대한 가깝게 모방는 `Connection` 속성입니다. 속성에 의해 사용 되는 개체를 포함 하는 멤버 변수는. 속성 `Get` 접근자 해당 멤버 변수 인지 확인 하 여 시작 `Nothing`합니다. 이 경우 초기화 메서드는 멤버 변수의 인스턴스를 만들고 핵심 명령 관련 속성을 할당 하 라고 합니다.

## <a name="step-4-exposing-command-level-settings"></a>4 단계: 노출 명령 수준 설정

이상적으로 명령 수준 정보는 데이터 액세스 계층 내에서 캡슐화 된 유지 되어야 합니다. 그러나이 정보는 아키텍처의 다른 계층에 필요 하지 않습니다, 노출할 수 있지만 부분 클래스를 통해와 마찬가지로 연결 수준 설정으로 합니다.

TableAdapter는 단일은만 되므로 `Connection` 속성을 연결 수준의 설정은 노출 하기 위한 코드는 매우 간단 합니다. TableAdapter에 여러 개의 명령 개체-있을 수 있으므로 명령 수준 설정을 수정 하는 경우 작업은 조금 더 복잡 한 `InsertCommand`, `UpdateCommand`, 및 `DeleteCommand`, 가변 개수의의 명령 개체와 함께 `CommandCollection` 속성입니다. 명령 수준 설정으로 업데이트할 때 이러한 설정은 모든 명령 개체에 전파 해야 합니다.

예를 들어, 실행 하는 특별 한 오랜 시간이 걸린 TableAdapter에 특정 쿼리 내용이 한다고 가정 합니다. TableAdapter를 사용 하 여 해당 쿼리 중 하나를 실행할를 우리 늘려야 할 수 명령 개체 s [ `CommandTimeout` 속성](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtimeout.aspx)합니다. 이 속성 명령이 실행 될 때까지 기다리는 시간 (초)의 수를 지정 하 고 기본값은 30입니다.

허용 하는 `CommandTimeout` 는 BLL으로 조정 해야 하는 속성에 다음 추가 `Public` 메서드를는 `ProductsDataTable` 2 단계에서에서 만든 partial 클래스 파일을 사용 하 여 (`ProductsTableAdapter.ConnectionAndCommandSettings.vb`):


[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample4.vb)]

이 메서드는 해당 TableAdapter 인스턴스에서 모든 명령 문제에 대해 명령 제한 시간을 설정 하려면 BLL 또는 프레젠테이션 계층에서 호출 수 없습니다.

> [!NOTE]
> `Adapter` 및 `CommandCollection` 속성으로 표시 된 `Private`, 즉 TableAdapter 내의 코드에서 액세스할 수만 있습니다. 와 달리는 `Connection` 속성을 이러한 액세스 한정자는 구성할 수 없습니다. 따라서 다른 계층 아키텍처를 명령 수준 속성을 노출 하는 경우 제공 하려면 위에서 설명한 partial 클래스 방법을 사용 해야 합니다는 `Public` 메서드 또는 속성을 읽거나 쓸는 `Private` 명령 개체입니다.


## <a name="summary"></a>요약

형식화 된 데이터 집합 내에서 Tableadapter 캡슐화 데이터 액세스 세부 정보 및 복잡성을 제공 합니다. Tableadapter를 사용 하 여 우리 필요가 없습니다를 데이터베이스에 연결, 명령, 발급 하거나 결과 DataTable를 채우는 ADO.NET 코드를 작성 하는 방법에 대 한 중요 합니다. 모든 처리 자동으로을 수행해 줍니다.

그러나 연결 문자열 또는 기본 연결 또는 명령 시간 제한 값을 변경 하는 등 낮은 수준의 ADO.NET 고유 정보를 사용자 지정 해야 우리는 경우가 있을 수 있습니다. TableAdapter에 자동으로 생성 된 `Connection`, `Adapter`, 및 `CommandCollection` 있지만 속성은 `Friend` 또는 `Private`, 기본적으로 합니다. 이 내부 정보를 포함 하도록 partial 클래스를 사용 하 여 TableAdapter를 확장 하 여 노출 될 수 있습니다 `Public` 메서드 또는 속성입니다. Tableadapter 또는 `Connection` TableAdapter s 통해 속성 액세스 한정자를 구성할 수 있습니다 `ConnectionModifier` 속성입니다.

만족도 매우 프로그래밍!

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다. 에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [ http://ScottOnWriting.NET ](http://ScottOnWriting.NET)합니다.

## <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Burnadette Leigh, S ren 야곱의 Lauritsen Teresa 머피 및 Hilton Geisenow 했습니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](working-with-computed-columns-vb.md)
> [다음](protecting-connection-strings-and-other-configuration-information-vb.md)
