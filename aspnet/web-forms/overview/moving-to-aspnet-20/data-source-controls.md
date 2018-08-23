---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: 데이터 소스 컨트롤 | Microsoft Docs
author: microsoft
description: DataGrid 컨트롤을 ASP.NET 1.x 웹 응용 프로그램에서 데이터 액세스에서 크게 개선 표시 합니다. 그러나 되었을 수 있습니다 하는 대로 친숙 않았습니다...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: ba00024e93beba6eab226dd0d381d8734061e095
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41836736"
---
<a name="data-source-controls"></a>데이터 소스 컨트롤
====================
[Microsoft](https://github.com/microsoft)

> DataGrid 컨트롤을 ASP.NET 1.x 웹 응용 프로그램에서 데이터 액세스에서 크게 개선 표시 합니다. 그러나 되지 않은 것으로 사용자에 게 친숙 대로 되었을 수 있습니다. 여전히 상당한 양의 코드가에서 많은 유용한 기능을 가져오는 데 필요 합니다. 등에서 모든 데이터 액세스 1.x의 모델입니다.


DataGrid 컨트롤을 ASP.NET 1.x 웹 응용 프로그램에서 데이터 액세스에서 크게 개선 표시 합니다. 그러나 되지 않은 것으로 사용자에 게 친숙 대로 되었을 수 있습니다. 여전히 상당한 양의 코드가에서 많은 유용한 기능을 가져오는 데 필요 합니다. 등에서 모든 데이터 액세스 1.x의 모델입니다.

ASP.NET 2.0이 문제를 해결 된 일부 데이터 소스 컨트롤을 사용 하 여 합니다. ASP.NET 2.0에서 데이터 소스 컨트롤이 데이터 검색, 데이터, 데이터 표시 및 편집에 대 한 선언적 모델을 개발자에 게 제공 합니다. 데이터 소스 컨트롤의 목적은 이러한 데이터 소스에 관계 없이 데이터 바인딩된 컨트롤에 데이터의 일관 된 표현을 제공 하는 것입니다. ASP.NET 2.0의 데이터 소스 컨트롤의 핵심 DataSourceControl 추상 클래스가입니다. DataSourceControl 클래스에는 IDataSource 인터페이스 및 데이터 소스 컨트롤 (새 DataSourceId 속성을 통해 데이터 바인딩된 컨트롤의 DataSource로 할당할 수는 있습니다 IListSource 인터페이스의 기본 구현을 제공합니다 뒷부분에서 설명)을 목록으로 든 막론 하 고 데이터를 노출 합니다. 데이터 소스 컨트롤에서 데이터의 각 목록 DataSourceView 개체로 노출 됩니다. DataSourceView 인스턴스에 대 한 액세스는 IDataSource 인터페이스를 통해 제공 됩니다. 예를 들어, 특정 데이터 소스 컨트롤과 연결 된 DataSourceViews를 열거할 수 있도록 ICollection 및 GetView 메서드 이름으로 특정 DataSourceView 인스턴스에 액세스할 수 있습니다 GetViewNames 메서드를 반환 합니다.

데이터 소스 컨트롤의 사용자 인터페이스가 없는 경우 서버 컨트롤 선언 구문 지원할 수 있도록 및 필요한 경우 페이지 상태에 액세스할 수 있는 있도록 구현 됩니다. 데이터 소스 컨트롤은 클라이언트에 HTML 태그를 렌더링 하지 않습니다.

> [!NOTE]
> 나중에 알게 있습니다도 캐시 하는 데이터 소스 컨트롤을 사용 하 여 가져온 혜택.


## <a name="storing-connection-strings"></a>연결 문자열 저장

데이터 소스 컨트롤을 구성 하는 방법, 시작 하기 전에 연결 문자열에 관한 ASP.NET 2.0의 새로운 기능을 적용 해야 합니다. ASP.NET 2.0에서는 런타임에 동적으로 읽을 수 있는 연결 문자열을 쉽게 저장할 수 있는 구성 파일에 새 섹션을 소개 합니다. 합니다 &lt;connectionStrings&gt; 섹션 쉽게 연결 문자열을 저장 합니다.

아래 코드 조각에는 새 연결 문자열을 추가합니다.

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> 와 마찬가지로 &lt;appSettings&gt; 섹션을 &lt;connectionStrings&gt; 외부 섹션이 나타납니다는 &lt;system.web&gt; 구성 파일의 섹션.


이 연결 문자열을 사용 하려면 서버 컨트롤의 ConnectionString 특성을 설정 하는 경우 다음 구문을 사용할 수 있습니다.

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

합니다 &lt;connectionStrings&gt; 중요 한 정보가 노출 되지 않도록 섹션을 암호화할 수도 있습니다. 이 기능은 이후 단원에서 설명 합니다.

## <a name="caching-data-sources"></a>데이터 원본 캐싱

캐싱; 구성에 대 한 네 가지 속성을 제공 하는 각 데이터 소스 제어 EnableCaching, CacheDuration, CacheExpirationPolicy, 및 CacheKeyDependency 합니다.

## <a name="enablecaching"></a>EnableCaching

EnableCaching은 데이터 소스 컨트롤에 대 한 캐시 여부를 결정 하는 부울 속성을 사용 하도록 설정할지입니다.

## <a name="cacheduration-property"></a>CacheDuration 속성

CacheDuration 속성 캐시에 유효한 상태로 남아 있는 시간 (초) 수를 설정 합니다. 이 속성을 설정 **0** 캐시가 명시적으로 무효화 될 때까지 유효한 상태로 유지 됩니다.

## <a name="cacheexpirationpolicy-property"></a>CacheExpirationPolicy 속성

CacheExpirationPolicy 속성 중 하나로 **절대** 하거나 **슬라이딩**합니다. 데이터 캐시 되는 최대 기간 CacheDuration 속성으로 지정 하는 시간 (초)입니다 절대 즉으로 설정 합니다. 슬라이딩을 설정 하면 각 작업이 수행 될 때 만료 시간이 재설정 됩니다.

## <a name="cachekeydependency-property"></a>CacheKeyDependency 속성

CacheKeyDependency 속성을 문자열 값을 지정 하는 경우 ASP.NET은 해당 문자열을 기반으로 새 캐시 종속성을 설정 합니다. 이 옵션을 사용 하면 명시적으로 간단히 변경 하거나는 CacheKeyDependency를 제거 하 여 캐시를 무효화할 수 있습니다.

**중요 한**: 가장 사용 되 고 액세스 하는 경우 데이터 원본 및/또는 데이터의 콘텐츠를 클라이언트 id를 기반으로, 캐싱 EnableCaching False로 설정 하 여 사용할 수 없도록 하는 것이 좋습니다. 이 시나리오에서 캐싱이 설정 되어 요청을 발급 하는 원래 데이터를 요청한 사용자 이외의 사용자를 권한 부여 데이터 원본에 적용 되지 않습니다. 데이터는 단순히 캐시에서 처리 됩니다.

## <a name="the-sqldatasource-control"></a>SqlDataSource 컨트롤

SqlDataSource 컨트롤 개발자를 ADO.NET을 지 원하는 모든 관계형 데이터베이스에 저장 된 데이터에 액세스를 수 있습니다. SQL Server 데이터베이스, System.Data.OleDb 공급자, System.Data.Odbc 공급자 또는 System.Data.OracleClient 공급자 Oracle 액세스를 액세스할 수 System.Data.SqlClient 공급자를 사용할 수 있습니다. 따라서 SqlDataSource 분명 하지 않습니다만 사용 됩니다 SQL Server 데이터베이스의 데이터에 액세스 하기 위해.

SqlDataSource를 사용 하려면 단순히 ConnectionString 속성에 대 한 값을 제공와 지정 된 SQL 명령 또는 저장 프로시저. SqlDataSource 컨트롤 기본 ADO.NET 아키텍처를 사용 하 여 업무를 담당 합니다. 연결, 데이터 소스를 쿼리 또는 저장된 프로시저를 실행, 데이터를 반환을 열고 연결을 닫습니다.

> [!NOTE]
> DataSourceControl 클래스에는 자동으로 연결을 닫습니다, 때문에 데이터베이스 연결 누수에서 생성 된 고객 호출 수를 줄여야 합니다.


아래 코드 조각 SqlDataSource 컨트롤 위에 표시 된 대로 구성 파일에 저장 된 연결 문자열을 사용 하 여 DropDownList 컨트롤을 바인딩합니다.

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

위에서 볼 수 있듯이, SqlDataSource의 DataSourceMode 속성을 데이터 원본에 대 한 모드를 지정 합니다. 위의 예제에는 DataSourceMode DataReader로 설정 됩니다. 이 경우 SqlDataSource 정방향 전용 및 읽기 전용 커서를 사용 하 여 IDataReader 개체를 반환 합니다. 지정된 된 형식의 반환 되는 개체는 사용 되는 공급자에 의해 제어 됩니다. System.Data.SqlClient 공급자를 사용 하 고에 지정 된 대로 경우에 &lt;connectionStrings&gt; web.config 파일의 섹션입니다. 따라서 반환 되는 개체 형식이 SqlDataReader 됩니다. 데이터 집합의 DataSourceMode 값을 지정 하 여 서버에서 데이터 집합의 데이터를 저장할 수 있습니다. 이 모드에서는 정렬, 페이징 등와 같은 기능을 추가할 수 있습니다. 데이터 바인딩 있었다면 GridView 컨트롤에 SqlDataSource에는 선택 했습니다 데이터 집합 모드입니다. 단, DropDownList, DataReader 모드 경우 적합 합니다.

> [!NOTE]
> SqlDataSource 또는 AccessDataSource를 캐시 하는 경우 데이터 집합에 DataSourceMode 속성을 설정 해야 합니다. DataReader의 DataSourceMode 캐싱을 사용 하도록 설정 하면 예외가 발생 합니다.


## <a name="sqldatasource-properties"></a>SqlDataSource 속성

다음은 SqlDataSource 컨트롤의 속성 중 일부입니다.

### <a name="cancelselectonnullparameter"></a>CancelSelectOnNullParameter

Select 명령 매개 변수 중 하나가 null 인 경우 취소가 있는지 여부를 지정 하는 부울 값입니다. 기본적으로 true입니다.

### <a name="conflictdetection"></a>ConflictDetection

여기서 여러 사용자가 업데이트할 수 있습니다 데이터 원본을 한 번에 상황에서는 ConflictDetection 속성 SqlDataSource 컨트롤의 동작을 결정 합니다. 이 속성 ConflictOptions 열거형의 값 중 하나를 평가 합니다. 이러한 값은 **CompareAllValues** 하 고 **OverwriteChanges**합니다. 경우 OverwriteChanges 마지막으로 데이터 원본에 데이터를 쓸 사용자로 이전 내용을 덮어씁니다. 하는 경우 ConflictDetection 속성 CompareAllValues로 SelectCommand에서 반환 되는 열에 대 한 매개 변수 생성 고 SqlDataSource를 허용 하는 이러한 열 각각에 원래 값을 보유할 만들어집니다 매개 변수 SelectCommand가 실행 되므로 값이 변경 되었는지 여부를 결정 합니다.

### <a name="deletecommand"></a>DeleteCommand

데이터베이스에서 행을 삭제할 때 사용 하는 SQL 문자열을 가져오거나 설정 합니다. 이 SQL 쿼리 또는 저장된 프로시저 이름을 하거나 수 있습니다.

### <a name="deletecommandtype"></a>DeleteCommandType

설정 하거나 SQL 쿼리 (텍스트) 또는 저장된 프로시저 (StoredProcedure) 하거나 삭제 명령의 형식을 가져옵니다.

### <a name="deleteparameters"></a>DeleteParameters

SqlDataSource 컨트롤을 사용 하 여 연결 SqlDataSourceView 개체의 DeleteCommand에서 사용 되는 매개 변수를 반환 합니다.

### <a name="oldvaluesparameterformatstring"></a>OldValuesParameterFormatString

이 속성은 사용 하 여 CompareAllValues를 ConflictDetection 속성이 설정 되어 있는 경우에서 원래 값 매개 변수의 형식을 지정 합니다. 기본값은 {0} 즉, 원래 값 매개 변수 이름이 같은 원래 매개 변수는 걸립니다. 즉, 필드 이름을 EmployeeID 인 경우 원래의 값 매개 변수 것 @EmployeeID입니다.

### <a name="selectcommand"></a>SelectCommand

데이터베이스에서 데이터를 검색 하는 데 사용 되는 SQL 문자열을 가져오거나 설정 합니다. 이 SQL 쿼리 또는 저장된 프로시저 이름을 하거나 수 있습니다.

### <a name="selectcommandtype"></a>SelectCommandType

설정 하거나 SQL 쿼리 (텍스트) 또는 저장된 프로시저 (StoredProcedure) 하거나 select 명령의 형식을 가져옵니다.

### <a name="selectparameters"></a>SelectParameters

SqlDataSource 컨트롤을 사용 하 여 연결 SqlDataSourceView 개체의 SelectCommand에서 사용 되는 매개 변수를 반환 합니다.

### <a name="sortparametername"></a>SortParameterName

데이터 소스 컨트롤에서 검색 데이터를 정렬할 때 사용 되는 저장된 프로시저 매개 변수의 이름을 가져오거나 설정 합니다. SelectCommandType StoredProcedure로 설정 된 경우에 유효 합니다.

### <a name="sqlcachedependency"></a>SqlCacheDependency

데이터베이스 및 SQL Server 캐시 종속성에 사용 되는 테이블을 지정 하는 세미콜론으로 구분 된 문자열입니다. (SQL 캐시 종속성은 이후 단원 살펴봅니다.)

### <a name="updatecommand"></a>UpdateCommand

데이터베이스의 데이터를 업데이트할 때 사용 되는 SQL 문자열을 가져오거나 설정 합니다. 이 SQL 쿼리 또는 저장된 프로시저 이름을 하거나 수 있습니다.

### <a name="updatecommandtype"></a>UpdateCommandType

설정 하거나 SQL 쿼리 (텍스트) 또는 저장된 프로시저 (StoredProcedure) 하거나 업데이트 명령의 형식을 가져옵니다.

### <a name="updateparameters"></a>UpdateParameters

SqlDataSource 컨트롤을 사용 하 여 연결 SqlDataSourceView 개체의 UpdateCommand에서 사용 되는 매개 변수를 반환 합니다.

## <a name="the-accessdatasource-control"></a>AccessDataSource 컨트롤

AccessDataSource 컨트롤 SqlDataSource 클래스에서 파생 되 고 Microsoft Access 데이터베이스에 데이터 바인딩할 사용 됩니다. AccessDataSource 컨트롤에 대 한 ConnectionString 속성에는 읽기 전용 속성이입니다. ConnectionString 속성을 사용 하는 대신 데이터 파일 속성은 아래와 같이 Access 데이터베이스를 가리키도록 사용 됩니다.

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

AccessDataSource는 항상 기본 SqlDataSource의 ProviderName System.Data.OleDb로 설정 됩니다 및 Microsoft.Jet.OLEDB.4.0 OLE DB 공급자를 사용 하 여 데이터베이스에 연결 합니다. AccessDataSource 컨트롤을 사용 하 여 암호로 보호 된 Access 데이터베이스에 연결할 수 없습니다. 암호로 보호 된 데이터베이스에 연결 해야 할 경우 SqlDataSource 컨트롤을 사용 해야 합니다.

> [!NOTE]
> 앱에서 웹 사이트 내에 저장 된 access 데이터베이스를 배치할\_데이터 디렉터리입니다. ASP.NET이이 디렉터리를 찾을 수에 있는 파일을 허용 하지 않습니다. 프로세스 계정에 앱에 읽기 및 쓰기 권한을 부여 해야\_Access 데이터베이스를 사용 하는 경우 데이터 디렉터리입니다.


## <a name="the-xmldatasource-control"></a>XmlDataSource 컨트롤

XML 데이터를 데이터 바인딩된 컨트롤에 데이터 바인딩하는 XmlDataSource가 됩니다. 데이터 파일 속성을 사용 하 여 XML 파일에 바인딩할 수 있습니다 또는 데이터 속성을 사용 하 여 XML 문자열을 바인딩할 수 있습니다. 고 XmlDataSource 바인딩할 수 있는 필드와 XML 특성을 노출합니다. 특성으로 표현 되지 않는 값에 바인딩할 해야 하는 경우에 XSL 변환을 사용 해야 합니다. XML 데이터를 필터링 하는 XPath 식을 사용할 수도 있습니다.

다음 XML 파일을 고려 합니다.

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

고 XmlDataSource의 XPath 속성은 사용 하 여 */사람이* 필터링 하기 위해 요소만 &lt;Person&gt; 노드. DropDownList 다음 DataTextField 속성을 사용 하 여 LastName 특성에 데이터 바인딩합니다.

XmlDataSource 컨트롤은 읽기 전용 XML 데이터에 데이터 바인딩하는 데 주로, XML 데이터 파일을 편집 하는 것이 같습니다. 이러한 경우에 자동으로 삽입, 업데이트 및 삭제 정보는 XML 파일에 자동으로 이루어지지는지 않습니다 다른 데이터 소스 컨트롤에서와 마찬가지로 note 합니다. 대신 수동으로 XmlDataSource 컨트롤의 다음 메서드를 사용 하 여 데이터를 편집 하려면 코드를 작성 해야 합니다.

### <a name="getxmldocument"></a>GetXmlDocument

고 XmlDataSource에서 검색 하는 XML 코드를 포함 하는 XmlDocument 개체를 검색 합니다.

### <a name="save"></a>저장

메모리의 XmlDocument 데이터 소스에 다시 저장합니다.

다음 두 조건이 충족 되 면 Save 메서드 에서만 작동 됩니다 실현 하는 것이 반드시:

1. 고 XmlDataSource 메모리 내 XML 데이터에 바인딩할 데이터 속성 대신 XML 파일에 바인딩할 데이터 파일 속성을 사용 하는 합니다.
2. 변환이 변환 또는 변형 파일 속성을 통해 지정 됩니다.

Save 메서드를 동시에 여러 사용자가 호출 될 때 예기치 않은 결과가 생성 수는 또한 note 합니다.

## <a name="the-objectdatasource-control"></a>ObjectDataSource 컨트롤

이 지점까지 살펴 봤는 데이터 소스 컨트롤 데이터 소스 컨트롤이 데이터 저장소에 직접 통신 하는 위치 2 계층 응용 프로그램에 대 한 훌륭한 선택 됩니다. 그러나 많은 실제 응용 프로그램 데이터 소스 컨트롤 데이터 계층과 통신 하는 비즈니스 개체와 통신 하도록 해야 할 수 있는 다중 계층 응용 프로그램입니다. 이러한 상황에서는 ObjectDataSource 원활 하 게 청구서를 채웁니다. ObjectDataSource가 소스 개체와 함께에서 작동합니다. 개체의 인스턴스 메서드 대신 정적 메서드 (Visual Basic에서는 Shared) ObjectDataSource 컨트롤 소스 개체, 지정된 된 메서드를 호출 및 dispose 단일 요청의 범위 내에서 모든 개체 인스턴스의 인스턴스를 만들어집니다. 따라서 개체는 상태 비저장 이어야 합니다. 즉, 개체 획득 하 고 단일 요청 범위 내에서 모든 필요한 리소스를 해제 해야 합니다. ObjectDataSource 컨트롤의 ObjectCreating 이벤트를 처리 하 여 원본 개체를 만드는 방법을 제어할 수 있습니다. 원본 개체의 인스턴스를 만들고 속성을 설정 합니다 ObjectInstance ObjectDataSourceEventArgs 클래스의 해당 인스턴스에 수 있습니다. ObjectDataSource 컨트롤 자체의 인스턴스를 만드는 대신 ObjectCreating 이벤트에서 만든 인스턴스를 사용 합니다.

ObjectDataSource 컨트롤 소스 개체를 검색 및 데이터를 수정 하기 위해 호출할 수 있는 공용 정적 메서드 (Visual Basic에서는 Shared)를 노출 하는 경우 ObjectDataSource 컨트롤을 해당 메서드를 직접 호출 됩니다. ObjectDataSource 컨트롤을 메서드 호출을 수행 하기 위해 원본 개체의 인스턴스를 만들어야 하는, 개체 매개 변수가 없는 public 생성자를 포함 해야 합니다. ObjectDataSource 컨트롤 소스 개체의 새 인스턴스를 만들 때이 생성자를 호출 합니다.

원본 개체에 매개 변수가 없는 public 생성자를 찾을 수 없는 경우에 ObjectDataSource 컨트롤 ObjectCreating 이벤트에 의해 사용 될 원본 개체의 인스턴스를 만들 수 있습니다.

## <a name="specifying-object-methods"></a>개체 메서드 지정

ObjectDataSource 컨트롤 소스 개체는 여러 개의 선택, 삽입, 업데이트 하는 데 사용 되는 메서드를 포함 하거나 데이터를 삭제할 수 있습니다. 이러한 메서드는 ObjectDataSource 컨트롤의 SelectMethod, InsertMethod, UpdateMethod, 또는 DeleteMethod 속성을 사용 하 여 식별 되는 메서드의 이름을 기반으로 ObjectDataSource 컨트롤에서 호출 됩니다. 원본 개체는 ObjectDataSource 컨트롤 데이터 소스의 개체의 총 개수를 반환 하는 SelectCountMethod 속성을 사용 하 여 식별 되는 선택적 SelectCount 메서드를 포함할 수도 수 있습니다. ObjectDataSource 컨트롤 페이징 하는 경우 사용 하기 위해 데이터 원본에서 레코드의 총 수를 검색 하는 Select 메서드를 호출한 후 SelectCount 메서드를 호출 합니다.

## <a name="lab-using-data-source-controls"></a>데이터 소스 컨트롤을 사용 하 여 랩

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>연습 1-SqlDataSource 컨트롤을 사용 하 여 데이터 표시

다음 연습에서는 Northwind 데이터베이스에 연결할 SqlDataSource 컨트롤을 사용 합니다. SQL Server 2000 인스턴스에서 Northwind 데이터베이스에 액세스할 수 있다고 가정 합니다.

1. 새 ASP.NET 웹 사이트를 만듭니다.
2. 새 web.config 파일을 추가 합니다.

    1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 새 항목 추가 클릭 합니다.
    2. 템플릿 목록에서 웹 구성 파일을 선택 하 고 추가 클릭 합니다.
3. 편집 된 &lt;connectionStrings&gt; 다음과 같은 섹션: 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. 코드 뷰로 전환 및 ConnectionString 특성 및 SelectCommand 특성을 추가 합니다 &lt;asp: SqlDataSource&gt; 다음과 같이 제어 합니다. 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. 디자인 뷰에서 새 GridView 컨트롤을 추가 합니다.
6. GridView 작업 메뉴에서 데이터 소스 선택 드롭다운 목록에서 SqlDataSource1를 선택 합니다.
7. Default.aspx 단추로 클릭 하 고 메뉴에서 브라우저에서 보기를 선택 합니다. 저장 하 라는 메시지가 나타나면 예를 클릭 합니다.
8. GridView는 Products 테이블에서 데이터를 표시합니다.

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>연습 2-SqlDataSource 컨트롤을 사용 하 여 데이터 편집

다음 연습은 방법을 보여 주는 데이터 바인딩할 DropDownList 선언적 구문을 사용 하 여 제어 DropDownList 컨트롤에서 표시 되는 데이터를 편집할 수 있습니다.

1. 디자인 뷰에서 Default.aspx에서 GridView 컨트롤을 삭제 합니다. 

    **중요 한**: 페이지의 SqlDataSource 컨트롤을 그대로 둡니다.
2. DropDownList 컨트롤을 Default.aspx 추가 합니다.
3. 원본 뷰로 전환 합니다.
4. DataSourceId를 DataTextField, DataValueField 특성을 추가 합니다 &lt;asp: DropDownList&gt; 다음과 같이 제어 합니다. 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. Default.aspx를 저장 하 고 브라우저에서 보기. 참고 DropDownList 모든 Northwind 데이터베이스에서 제품을 포함 합니다.
6. 브라우저를 닫습니다.
7. Default.aspx의 소스 뷰에서 DropDownList 컨트롤 아래에 새 텍스트 상자 컨트롤을 추가 합니다. TxtProductName를 TextBox의 ID 속성을 변경 합니다.
8. TextBox 컨트롤에서 새 단추 컨트롤을 추가 합니다. BtnUpdate 및 Text 속성을 단추의 ID 속성 변경 **업데이트 제품 이름을**입니다.
9. Default.aspx의 소스 뷰에서 UpdateCommand 속성 및 두 개의 새 UpdateParameters SqlDataSource 태그 같이 추가 합니다. 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > 이 코드에 추가 된 매개 변수 (ProductID 및 ProductName)를 업데이트 하는 두 개의 있는지 note 합니다. 이러한 매개 변수 ddlProducts DropDownList의 SelectedValue 속성과 txtProductName TextBox의 Text 속성에 매핑됩니다.
10. 디자인 뷰로 전환한 이벤트 처리기를 추가 하는 단추 컨트롤을 두 번 클릭 합니다.
11. 다음 코드는 btnUpdate 추가할\_코드를 클릭 합니다. 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. Default.aspx 단추로 클릭 하 고 브라우저에서 보기를 선택 합니다. 모든 변경 내용을 저장 하 라는 메시지가 나타나면 예를 클릭 합니다.
13. ASP.NET 2.0 런타임 시 컴파일에 대 한 partial 클래스를 사용 합니다. 코드 변경 내용이 적용 확인 하기 위해 응용 프로그램을 빌드하는 데 필요한 것입니다.
14. 드롭다운 목록에서 제품을 선택 합니다.
15. 텍스트 상자에 선택한 제품에 대 한 새 이름을 입력 하 고 [업데이트] 단추를 클릭 합니다.
16. 제품 이름은 데이터베이스에서 업데이트 됩니다.

## <a name="exercise-3-using-the-objectdatasource-control"></a>연습 3 ObjectDataSource 컨트롤 사용

이 연습에서는 Northwind 데이터베이스를 조작할 ObjectDataSource 컨트롤 및 원본 개체를 사용 하는 방법을 보여 줍니다.

1. 솔루션 탐색기에서 프로젝트 단추로 클릭 하 고 새 항목 추가 클릭 합니다.
2. 템플릿 목록에서 웹 폼을 선택 합니다. Object.aspx 이름을 변경 하 고 추가 클릭 합니다.
3. 솔루션 탐색기에서 프로젝트 단추로 클릭 하 고 새 항목 추가 클릭 합니다.
4. 템플릿 목록에서 클래스를 선택 합니다. NorthwindData.cs 클래스의 이름을 변경 하 고 추가 클릭 합니다.
5. 앱에 클래스를 추가 하 라는 메시지가 나타나면 예 클릭\_코드 폴더입니다.
6. NorthwindData.cs 파일에 다음 코드를 추가 합니다. 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. Object.aspx의 원본 뷰에 다음 코드를 추가 합니다. 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. 모든 파일을 저장 하 고 object.aspx를 찾습니다.
9. 세부 정보를 보는, 직원을 편집 하 고, 직원을 추가 하 고 직원을 삭제 하 여 인터페이스와 상호 작용 합니다.
