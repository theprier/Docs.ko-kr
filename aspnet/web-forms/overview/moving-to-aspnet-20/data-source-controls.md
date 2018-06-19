---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: 데이터 소스 컨트롤 | Microsoft Docs
author: microsoft
description: DataGrid 컨트롤 1.x asp.net에서 웹 응용 프로그램에서 데이터 액세스에서 크게 개선으로 표시 합니다. 그러나 되었을 수 처럼 친숙 않았습니다 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: b1ac7fb62767d61c97fe00338bc0f5087f4863b5
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
ms.locfileid: "28885897"
---
<a name="data-source-controls"></a>데이터 소스 제어
====================
by [Microsoft](https://github.com/microsoft)

> DataGrid 컨트롤 1.x asp.net에서 웹 응용 프로그램에서 데이터 액세스에서 크게 개선으로 표시 합니다. 그러나 되었을 수 처럼 친숙 않았습니다. 여전히 상당한 양의에서 많은 유용한 기능을 가져오기 위해 코드를 필요 합니다. 예: 1.x에서 모든 데이터 액세스 노력에서 모델입니다.


DataGrid 컨트롤 1.x asp.net에서 웹 응용 프로그램에서 데이터 액세스에서 크게 개선으로 표시 합니다. 그러나 되었을 수 처럼 친숙 않았습니다. 여전히 상당한 양의에서 많은 유용한 기능을 가져오기 위해 코드를 필요 합니다. 예: 1.x에서 모든 데이터 액세스 노력에서 모델입니다.

ASP.NET 2.0이 문제를 해결 된 일부 데이터 소스 컨트롤과 합니다. ASP.NET 2.0의 데이터 소스 제어, 데이터를 검색 하 고, 데이터를 표시 하 고, 데이터 편집에 대 한 선언적 모델 개발자에 게 제공 합니다. 데이터 소스 컨트롤의 목적은 이러한 데이터의 소스와 데이터 바인딩된 컨트롤에 데이터의 일관 된 표현을 제공 하는 것입니다. ASP.NET 2.0의 데이터 소스 제어의 핵심에는 데이터 소스 제어 추상 클래스입니다. 데이터 원본 컨트롤 클래스 IDataSource 인터페이스 및 후자는 할당할 수 있도록 데이터 소스 제어 (새 DataSourceId 속성을 통해 데이터 바인딩된 컨트롤의 데이터 원본으로 IListSource 인터페이스의 기본 구현을 제공합니다 나중에 설명) 및 그 안에 목록으로 데이터를 노출 합니다. DataSourceView 개체 데이터 소스 컨트롤에서 데이터의 각 목록 표시 됩니다. DataSourceView 인스턴스에 대 한 액세스는 IDataSource 인터페이스에서 제공 됩니다. 예를 들어 여기서 메서드는 특정 데이터 소스 제어와 관련 된는 DataSourceViews를 열거할 수 있습니다는 ICollection 및 영역의 GetView 메서드 이름으로 특정 DataSourceView 인스턴스에 액세스할 수 있습니다를 반환 합니다.

데이터 소스 제어는 사용자 인터페이스가 없습니다. 원하는 경우 페이지 상태에 액세스할 수 있는 있도록 및 선언적 구문을 지원할 수 있도록 서버 컨트롤로 구현 됩니다. 데이터 소스 제어 클라이언트에 HTML 태그를 렌더링 하지 않습니다.

> [!NOTE]
> 나중에 볼 수 있듯이 없습니다도 캐싱하며 데이터 소스 제어를 사용 하 여 얻은 이점입니다.


## <a name="storing-connection-strings"></a>연결 문자열 저장

보고 데이터 소스 제어를 구성 하는 방법에 들어가기 전에 우리는 연결 문자열에 대 한 ASP.NET 2.0의 새로운 기능인을 다루어야 합니다. ASP.NET 2.0에서는 런타임에 동적으로 읽을 수 있는 연결 문자열을 쉽게 저장할 수 있는 구성 파일의 새 섹션을 소개 합니다. &lt;connectionStrings&gt; 섹션을 사용 하면 쉽게 연결 문자열을 저장 합니다.

아래 코드 조각에는 새 연결 문자열을 추가합니다.

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> 과 마찬가지로 &lt;appSettings&gt; 섹션은 &lt;connectionStrings&gt; 외부의 섹션이 나타납니다는 &lt;system.web&gt; 구성 파일의 섹션입니다.


이 연결 문자열을 사용 하려면 서버 컨트롤의 ConnectionString 특성을 설정 하는 경우 다음 구문을 사용할 수 있습니다.

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

&lt;connectionStrings&gt; 중요 한 정보가 노출 되지 않도록 섹션을 암호화할 수도 있습니다. 해당 기능이 이후 단원에서 설명 합니다.

## <a name="caching-data-sources"></a>데이터 원본 캐싱

캐싱; 구성에 대 한 네 가지 속성을 제공 하는 각 데이터 소스 제어 EnableCaching, CacheDuration, CacheExpirationPolicy, 및 CacheKeyDependency 합니다.

## <a name="enablecaching"></a>EnableCaching

EnableCaching은 데이터 소스 제어를 사용 캐싱 여부를 결정 하는 부울 속성입니다.

## <a name="cacheduration-property"></a>CacheDuration 속성

CacheDuration 속성 캐시 유효한 상태를 유지 하는 시간 (초)을 설정 합니다. 이 속성을 설정 **0** 캐시가 명시적으로 무효화 될 때까지 유효 합니다.

## <a name="cacheexpirationpolicy-property"></a>CacheExpirationPolicy Property

CacheExpirationPolicy 속성 중 하나로 **절대** 또는 **슬라이딩**합니다. 데이터가 캐시 되는 최대 기간 CacheDuration 속성에 지정 된 시간 (초)의 수에 절대 방법을로 설정 합니다. 슬라이딩을 설정 하 여 각 작업이 수행 될 때 만료 시간이 재설정 됩니다.

## <a name="cachekeydependency-property"></a>CacheKeyDependency 속성

문자열 값을 CacheKeyDependency 속성에 대해 지정 하는 경우 ASP.NET에서는 해당 문자열을 기반으로 새 캐시 종속성을 설정 합니다. 이 옵션을 사용 하면 단순히 변경 하거나는 CacheKeyDependency를 제거 하 여 명시적으로 캐시를 무효화 수 있습니다.

**중요 한**: 데이터 소스 및/또는 콘텐츠 데이터의 클라이언트 id를 기반으로 가장 사용 하 고에 대 한 액세스, 캐싱 EnableCaching False로 설정 하 여 사용할 수 없도록 하는 것이 좋습니다. 이 시나리오에서는 캐싱이 설정 되어 원래 데이터를 요청한 사용자 이외의 사용자는 요청을 실행 하는 경우에 데이터 원본에 대 한 권한 부여 적용 되지 않습니다. 데이터는 단순히 캐시에서 처리 됩니다.

## <a name="the-sqldatasource-control"></a>SqlDataSource 컨트롤

SqlDataSource 컨트롤 개발자를 ADO.NET 지원 되는 관계형 데이터베이스에 저장 된 데이터를 액세스할 수 있습니다. System.Data.SqlClient 공급자는 SQL Server 데이터베이스, System.Data.OleDb 공급자, System.Data.Odbc 공급자 또는 Oracle에 액세스 하도록 System.Data.OracleClient 공급자에 액세스 하는 데 사용할 수 있습니다. 따라서 SqlDataSource은 확실히 사용 되지 않습니다만 SQL Server 데이터베이스의 데이터에 액세스 하기 위한.

SqlDataSource를 사용 하려면 단순히 ConnectionString 속성에 대 한 값을 제공와 SQL 명령을 지정 하십시오. 또는 저장 프로시저입니다. SqlDataSource 컨트롤 기본 ADO.NET 아키텍처를 사용 하 여 처리를 담당 합니다. 연결, 데이터 소스를 쿼리 또는 저장된 프로시저를 실행, 데이터를 반환을 열고 사용자에 대 한 연결을 닫습니다.

> [!NOTE]
> 데이터 원본 컨트롤 클래스 수에 대 한 연결을 자동으로 종료, 때문에 누수 데이터베이스 연결에 의해 생성 된 고객 호출 수를 줄여야 합니다.


아래 코드 조각 SqlDataSource 컨트롤 위에 표시 된 것과 같이 구성 파일에 저장 된 연결 문자열을 사용 하 여 DropDownList 컨트롤을 바인딩합니다.

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

위에서 설명한 대로 SqlDataSource의 DataSourceMode 속성은 데이터 원본에 대 한 모드를 지정 합니다. 위의 예에서 DataSourceMode DataReader로 설정 됩니다. 이 경우 SqlDataSource 정방향 및 읽기 전용 커서를 사용 하 여 IDataReader 개체를 반환 합니다. 지정 된 형식의 반환 되는 개체는 사용 되는 공급자에 의해 제어 됩니다. System.Data.SqlClient 공급자 사용 하 고에 지정 된 경우에 &lt;connectionStrings&gt; web.config 파일의 섹션입니다. 따라서 반환 되는 개체는 SqlDataReader 형식의 수 있습니다. 데이터 집합의 DataSourceMode 값을 지정 하 여 서버에 있는 데이터 집합에 데이터를 저장할 수 있습니다. 이 모드에서는 정렬, 페이징 등 등의 기능을 추가할 수 있습니다. 데이터 바인딩 있었다면 GridView 컨트롤에 SqlDataSource I 선택 했 데이터 집합 모드입니다. 그러나 한 DropDownList의 경우 DataReader 모드는 올바른 좋습니다.

> [!NOTE]
> SqlDataSource 또는 AccessDataSource를 캐시할 때 DataSourceMode 속성 데이터 집합으로 설정 되어야 합니다. DataReader DataSourceMode 캐싱을 사용 하도록 설정 하면 예외가 발생 합니다.


## <a name="sqldatasource-properties"></a>SqlDataSource 속성

다음은 SqlDataSource 컨트롤의 속성 중 일부입니다.

### <a name="cancelselectonnullparameter"></a>CancelSelectOnNullParameter

매개 변수 중 하나가 null 인 경우 select 명령 취소 되었는지를 지정 하는 부울 값입니다. 기본적으로 true입니다.

### <a name="conflictdetection"></a>ConflictDetection

여기서 여러 사용자가 업데이트할 수 데이터 원본을 한 번에 한 경우 ConflictDetection 속성 SqlDataSource 컨트롤의 동작을 결정 합니다. 이 속성은 ConflictOptions 열거형의 값 중 하나를 평가합니다. 이러한 값은 **CompareAllValues** 및 **OverwriteChanges**합니다. 경우 overwritechanges, 마지막으로 데이터 원본에 데이터를 쓸 사용자 집합에는 모든 이전 변경 내용을 덮어씁니다. 경우 ConflictDetection 속성이 CompareAllValues로 설정 되 면 매개 변수는 SelectCommand에서 반환 되는 열에 대해 작성 수 있으며 이러한 각 열에 SqlDataSource 허용에 원래 값을 보유할 만들어집니다 매개 변수 값이 SelectCommand 실행 된 후 변경 되었는지 여부를 결정 합니다.

### <a name="deletecommand"></a>DeleteCommand

데이터베이스에서 행을 삭제할 때 사용 되는 SQL 문자열을 가져오거나 설정 합니다. 이 수는 SQL 쿼리 또는 저장된 프로시저 이름을 입력 합니다.

### <a name="deletecommandtype"></a>DeleteCommandType

설정 하거나 SQL 쿼리 (텍스트) 또는 저장된 프로시저 (StoredProcedure) 하거나 delete 명령의 유형을 가져옵니다.

### <a name="deleteparameters"></a>DeleteParameters

SqlDataSource 컨트롤와 관련 된 SqlDataSourceView 개체 DeleteCommand에서 사용 되는 매개 변수를 반환 합니다.

### <a name="oldvaluesparameterformatstring"></a>OldValuesParameterFormatString

이 속성은 사용 하 여 CompareAllValues를 ConflictDetection 속성이 설정 되어 있는 경우에는 원래 값 매개 변수 형식을 지정할 수 있습니다. 기본값은 {0} 원래 값 매개 변수 이름이 같은 원래 매개 변수를 취할 됩니다. 즉, 필드 이름이 EmployeeID 인 경우의 원래 값 매개 변수를 지정할 @EmployeeID합니다.

### <a name="selectcommand"></a>SelectCommand

데이터베이스에서 데이터를 검색 하는 데 사용 되는 SQL 문자열을 가져오거나 설정 합니다. 이 수는 SQL 쿼리 또는 저장된 프로시저 이름을 입력 합니다.

### <a name="selectcommandtype"></a>SelectCommandType

설정 하거나 SQL 쿼리 (텍스트) 또는 저장된 프로시저 (StoredProcedure) 하거나 select 명령의 유형을 가져옵니다.

### <a name="selectparameters"></a>SelectParameters

SqlDataSource 컨트롤와 관련 된 SqlDataSourceView 개체 SelectCommand에서 사용 되는 매개 변수를 반환 합니다.

### <a name="sortparametername"></a>SortParameterName

데이터 정렬 검색 될 때 데이터 소스 제어에서 사용 되는 저장된 프로시저 매개 변수의 이름을 가져오거나 설정 합니다. SelectCommandType StoredProcedure로 설정 된 경우에 유효 합니다.

### <a name="sqlcachedependency"></a>SqlCacheDependency

데이터베이스 및 SQL Server 캐시 종속성에 사용 되는 테이블을 지정 하는 세미콜론으로 구분 된 문자열입니다. (SQL 캐시 종속성은 이후 단원 살펴봅니다.)

### <a name="updatecommand"></a>UpdateCommand

데이터베이스의에서 데이터를 업데이트할 때 사용 되는 SQL 문자열을 가져오거나 설정 합니다. 이 수는 SQL 쿼리 또는 저장된 프로시저 이름을 입력 합니다.

### <a name="updatecommandtype"></a>UpdateCommandType

설정 하거나 SQL 쿼리 (텍스트) 또는 저장된 프로시저 (StoredProcedure) 하거나 업데이트 명령 유형을 가져옵니다.

### <a name="updateparameters"></a>UpdateParameters

SqlDataSource 컨트롤와 관련 된 SqlDataSourceView 개체 UpdateCommand에서 사용 되는 매개 변수를 반환 합니다.

## <a name="the-accessdatasource-control"></a>AccessDataSource 컨트롤

AccessDataSource 컨트롤 SqlDataSource 클래스에서 파생 되며 데이터에 바인딩할 Microsoft Access 데이터베이스에 사용 됩니다. AccessDataSource 컨트롤에 대 한 연결 문자열 속성은 읽기 전용 속성입니다. ConnectionString 속성을 사용 하는 대신 데이터 파일 속성은 아래와 같이 Access 데이터베이스를 가리키도록 사용 됩니다.

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

AccessDataSource는 항상 기본 SqlDataSource ProviderName로 설정 System.Data.OleDb Microsoft.Jet.OLEDB.4.0 OLE DB 공급자를 사용 하 여 데이터베이스에 연결 합니다. AccessDataSource 컨트롤 암호로 보호 된 Access 데이터베이스에 연결 하는 데 사용할 수 없습니다. 암호로 보호 된 데이터베이스에 연결 해야 할 경우 SqlDataSource 컨트롤을 사용 해야 합니다.

> [!NOTE]
> 응용 프로그램에 웹 사이트 내에 저장 된 access 데이터베이스를 배치 해야\_데이터 디렉터리입니다. ASP.NET 탐색할이 디렉터리의 파일을 허용 하지 않습니다. 프로세스 계정에 응용 프로그램에 대 한 읽기 및 쓰기 권한을 부여 해야 합니다\_Access 데이터베이스를 사용 하는 경우 데이터 디렉터리입니다.


## <a name="the-xmldatasource-control"></a>XmlDataSource 컨트롤

XmlDataSource는 데이터-bind XML 데이터를 데이터 바인딩된 컨트롤에 사용 됩니다. DataFile 속성을 사용 하 여 XML 파일에 바인딩할 수 또는 데이터 속성을 사용 하는 XML 문자열에 바인딩할 수 있습니다. XmlDataSource는 바인딩 가능한 필드도 XML 특성을 노출합니다. 특성으로 표현 되지 않는 값에 바인딩 해야 하는 경우에 XSL 변환을 사용 해야 합니다. 필터 XML 데이터에 대 한 XPath 식을 사용할 수도 있습니다.

다음 XML 파일을 고려 합니다.

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

XmlDataSource의 XPath 속성에서는 */사람과* 를 기준으로 필터링 하기 위해 테이블만 &lt;사람&gt; 노드. DropDownList 다음 DataTextField 속성을 사용 하 여 LastName 특성으로 데이터 바인딩합니다.

XmlDataSource 컨트롤은 주로 읽기 전용 XML 데이터에 데이터 바인딩하는 동안에 XML 데이터 파일을 편집할 수 있습니다. 이러한 경우 자동으로 삽입, 업데이트 및 삭제의 XML 파일에 대 한 정보는 이루어지지 자동으로 다른 데이터 소스 컨트롤에서와 마찬가지로 note 합니다. 대신, XmlDataSource 컨트롤의 다음 메서드를 사용 하 여 데이터를 수동으로 편집 하는 코드를 작성 해야 합니다.

### <a name="getxmldocument"></a>GetXmlDocument

XmlDataSource에서 검색할 XML 코드를 포함 하는 XmlDocument 개체를 검색 합니다.

### <a name="save"></a>저장

데이터 소스에 다시 메모리에 XmlDocument를 저장합니다.

다음 두 조건이 충족 되 면 Save 메서드만 작동 하는지 실현 하려면 반드시:

1. XmlDataSource는 메모리에 XML 데이터에 바인딩할 데이터 속성 대신 XML 파일에 바인딩할 DataFile 속성을 사용 중입니다.
2. 변환이 변환 또는 TransformFile 속성을 통해 지정 됩니다.

또한 note Save 메서드가 동시에 여러 사용자가 직접 호출할 때 예기치 않은 결과 얻을 수 있습니다.

## <a name="the-objectdatasource-control"></a>ObjectDataSource 컨트롤

이 시점까지 설명 했습니다 있는 데이터 소스 컨트롤은 데이터 소스 제어의 데이터 저장소에 직접 통신 하는 위치 2 계층 응용 프로그램에 대 한 뛰어난 선택 합니다. 그러나 많은 실제 응용 프로그램 데이터 계층과 통신 하는 비즈니스 개체와 통신 하도록 데이터 소스 제어는 해야는 다층 계층 응용 프로그램. 이러한 경우에는 ObjectDataSource 원활 하 게 청구서를 채웁니다. ObjectDataSource는 소스 개체와 함께에서 작동합니다. 개체의 정적 (Visual Basic의 경우 Shared) 메서드 대신 인스턴스 메서드 ObjectDataSource 컨트롤 소스 개체, 지정된 된 메서드를 호출 및 dispose 단일 요청 범위 내에서 모든 개체 인스턴스의 인스턴스를 만들어집니다. 따라서 개체는 상태 비저장 이어야 합니다. 즉, 개체가 획득 하 고 단일 요청 범위 내에서 필요한 모든 리소스를 해제 해야 합니다. ObjectDataSource 컨트롤의 ObjectCreating 이벤트를 처리 하 여 소스 개체를 만드는 하는 방법을 제어할 수 있습니다. 원본 개체의 인스턴스를 만들 수 있으며 해당 인스턴스에 ObjectDataSourceEventArgs 클래스의 ObjectInstance 속성을 설정 합니다. ObjectDataSource 컨트롤에는 자체 인스턴스를 만드는 대신 ObjectCreating 이벤트에서 생성 된 인스턴스를 사용 합니다.

ObjectDataSource 컨트롤에 대 한 원본 개체에서 검색 하 고 데이터를 수정 하기 위해 호출할 수 있는 공용 정적 메서드 (Visual Basic의 경우 Shared)을 노출 하는 경우 ObjectDataSource 컨트롤 이러한 메서드를 직접 호출 됩니다. ObjectDataSource 컨트롤 소스 개체의 인스턴스 메서드 호출을 수행 하기 위해를 만들어야 하는 경우 개체 매개 변수를 사용 하는 공용 생성자에 포함 되어야 합니다. ObjectDataSource 컨트롤 소스 개체의 새 인스턴스를 만들 때이 생성자를 호출 합니다.

원본 개체는 매개 변수가 없는 public 생성자를 포함 하지 않습니다, ObjectDataSource 컨트롤 ObjectCreating 이벤트에 의해 사용 될 원본 개체의 인스턴스를 만들 수 있습니다.

## <a name="specifying-object-methods"></a>개체 메서드 지정

ObjectDataSource 컨트롤에 대 한 소스 개체 선택, 삽입, 업데이트 하는 데 사용 되는 메서드가 여러 개를 포함 하거나 데이터를 삭제할 수 있습니다. ObjectDataSource 컨트롤의 SelectMethod, InsertMethod, UpdateMethod 또는 DeleteMethod 속성을 사용 하 여 식별 한 대로 이러한 메서드는 메서드의 이름을 기반으로 ObjectDataSource 컨트롤에 의해 호출 됩니다. 원본 개체에는 데이터 원본에 있는 개체의 총 수의 개수를 반환 하는 SelectCountMethod 속성을 사용 하 여 ObjectDataSource 컨트롤에 의해 식별 되는 선택적 SelectCount 메서드가 포함할 수도 수 있습니다. ObjectDataSource 컨트롤 페이징 하는 경우 사용 하기 위해 데이터 소스에서 레코드의 총 수를 검색 하는 Select 메서드가 호출 된 후 SelectCount 메서드를 호출 합니다.

## <a name="lab-using-data-source-controls"></a>데이터 소스 제어를 사용 하 여 랩

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>연습 1-SqlDataSource 컨트롤을 사용 하 여 데이터 표시

다음 연습에서는 Northwind 데이터베이스에 연결 하는 데 SqlDataSource 컨트롤을 사용 합니다. SQL Server 2000 인스턴스에서 Northwind 데이터베이스에 액세스할 수 있다고 가정 합니다.

1. 새 ASP.NET 웹 사이트를 만듭니다.
2. Web.config 파일을 추가 합니다.

    1. 솔루션 탐색기에서 프로젝트 단추로 클릭 하 고 새 항목 추가 클릭 합니다.
    2. 템플릿 목록에서 웹 구성 파일을 선택 하 고 추가 클릭 합니다.
3. 편집 된 &lt;connectionStrings&gt; 다음과 같은 섹션: 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. 코드 보기로 전환 하 고 연결 문자열 특성 및 SelectCommand 특성을 추가 &lt;asp: SqlDataSource&gt; 다음과 같이 제어: 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. 디자인 뷰에서 새 GridView 컨트롤을 추가 합니다.
6. GridView 작업 메뉴에서 데이터 소스 선택 드롭다운 목록에서 SqlDataSource1를 선택 합니다.
7. Default.aspx 단추로 클릭 하 고 메뉴에서 브라우저에서 보기를 선택 합니다. 저장할지 묻는 메시지가 나타나면 예를 클릭 합니다.
8. GridView는 Products 테이블에서 데이터를 표시합니다.

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>연습 2-SqlDataSource 컨트롤을 사용 하 여 데이터 편집

다음 연습은 방법을 보여 주는 데이터 바인딩을 위해 DropDownList 선언 구문을 사용 하 여 제어할 DropDownList 컨트롤에 표시 되는 데이터를 편집할 수 있습니다.

1. 디자인 보기에서 Default.aspx에서 GridView 컨트롤을 삭제 합니다. 

    **중요 한**: 페이지에서 SqlDataSource 컨트롤을 그대로 둡니다.
2. Default.aspx로 DropDownList 컨트롤을 추가 합니다.
3. 소스 뷰로 전환 합니다.
4. DataSourceId, DataTextField, 및 DataValueField 특성을 추가 &lt;asp: DropDownList&gt; 다음과 같이 제어: 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. Default.aspx를 저장 하 고 브라우저에서 보기. 참고 DropDownList 모든 Northwind 데이터베이스에서 제품을 포함 합니다.
6. 브라우저를 닫습니다.
7. Default.aspx의 소스 뷰에서 DropDownList 컨트롤 아래에 새 TextBox 컨트롤을 추가 합니다. TextBox의 ID 속성 txtProductName로 변경 합니다.
8. TextBox 컨트롤에서 새 단추 컨트롤을 추가 합니다. 단추의 ID 속성을 btnUpdate, 텍스트 속성을 변경 **업데이트 제품 이름**합니다.
9. Default.aspx의 소스 뷰에서 UpdateCommand 속성 및 두 개의 새 UpdateParameters SqlDataSource 태그를 다음과 같이 추가. 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > Note 된다고 두 업데이트 및 매개 변수 (ProductName ProductID)이이 코드에 추가 합니다. 이러한 매개 변수 txtProductName 입력란의 텍스트 속성 및 ddlProducts DropDownList의 SelectedValue 속성에 매핑됩니다.
10. 디자인 뷰로 전환 하 고 이벤트 처리기를 추가 하는 단추 컨트롤을 두 번 클릭 합니다.
11. 다음 코드는 btnUpdate를 추가\_코드를 클릭 합니다. 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. Default.aspx 단추로 클릭 하 고 브라우저에서 보기를 선택 합니다. 모든 변경 내용을 저장 하 라는 메시지가 나타나면 예를 클릭 합니다.
13. ASP.NET 2.0 런타임에 컴파일에 대 한 partial 클래스를 사용 합니다. 참조 코드 변경 내용을 적용 하려면 응용 프로그램을 빌드할 필요는 없습니다.
14. 드롭다운 목록에서 제품을 선택 합니다.
15. 텍스트 상자에 선택한 제품에 대 한 새 이름을 입력 한 다음 업데이트 단추를 클릭 합니다.
16. 제품 이름은 데이터베이스에서 업데이트 됩니다.

## <a name="exercise-3-using-the-objectdatasource-control"></a>ObjectDataSource 컨트롤을 사용 하 여 3 연습

이 연습에서는 Northwind 데이터베이스와 상호 작용할 수 ObjectDataSource 컨트롤 및 원본 개체를 사용 하는 방법을 보여 줍니다.

1. 솔루션 탐색기에서 프로젝트 단추로 클릭 하 고 새 항목 추가 클릭 합니다.
2. 템플릿 목록에서 Web Form을 선택 합니다. 이름을 object.aspx로 변경 하 고 추가 클릭 합니다.
3. 솔루션 탐색기에서 프로젝트 단추로 클릭 하 고 새 항목 추가 클릭 합니다.
4. 템플릿 목록에서 클래스를 선택 합니다. 클래스의 이름을 NorthwindData.cs로 변경 하 고 추가 클릭 합니다.
5. 응용 프로그램에 클래스를 추가 하 라는 메시지가 나타나면 예를 클릭\_코드 폴더입니다.
6. NorthwindData.cs 파일에 다음 코드를 추가 합니다. 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. 다음 코드 object.aspx의 소스 뷰를 추가 합니다. 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. 모든 파일을 저장 하 고 object.aspx를 찾습니다.
9. 세부 정보 보기, 편집 직원, 직원을 추가 및 직원 삭제는 인터페이스와 상호 작용 합니다.
