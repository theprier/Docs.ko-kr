---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: 캐싱 | Microsoft Docs
author: microsoft
description: 캐싱의 이해가 성능이 뛰어난 ASP.NET 응용 프로그램에 대 한 중요 합니다. ASP.NET 캐싱;에 대 한 3 가지 옵션을 제공 하는 1.x 출력 캐싱을 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: 90faaae75cc85585efa05e6e50eabe8c990d076e
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="caching"></a>캐싱
====================
by [Microsoft](https://github.com/microsoft)

> 캐싱의 이해가 성능이 뛰어난 ASP.NET 응용 프로그램에 대 한 중요 합니다. ASP.NET 캐싱;에 대 한 3 가지 옵션을 제공 하는 1.x 출력 캐싱, 부분 캐싱 및 캐시 API입니다.


캐싱의 이해가 성능이 뛰어난 ASP.NET 응용 프로그램에 대 한 중요 합니다. ASP.NET 캐싱;에 대 한 3 가지 옵션을 제공 하는 1.x 출력 캐싱, 부분 캐싱 및 캐시 API입니다. ASP.NET 2.0은 다음이 방법 중 세 가지를 모두 제공 하지만 일부 중요 한 기능을 추가 합니다. 몇 가지 새로운 캐시 종속성 있으며 개발자가 만드는 사용자 지정 캐시 종속성도 옵션을 만들었습니다. 캐싱 구성도 상당히 향상 되었습니다 ASP.NET 2.0.

## <a name="new-features"></a>새 기능

## <a name="cache-profiles"></a>캐시 프로필

캐시 프로필을 사용 하면 개발자가 특정 캐시 설정을 정의 하 여 개별 페이지에 적용할 수 있습니다. 예를 들어, 12 시간 후 캐시에서 만료 되어야 하는 일부 페이지를 사용 하도록 설정한 경우 해당 페이지에 적용할 수 있는 캐시 프로필을 쉽게 만들 수 있습니다. 새 캐시 프로필을 추가 하려면 사용 된 &lt;outputCacheSettings&gt; 구성 파일의 섹션입니다. 구성을 호출 하는 캐시 프로필의 예를 들어 다음은 *twoday* 12 시간 캐시 기간을 구성 하는입니다.

[!code-xml[Main](caching/samples/sample1.xml)]

이 캐시 프로필의 특정 페이지를 적용 하려면 아래와 같이 @ OutputCache 지시문의 CacheProfile 특성을 사용 합니다.

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>사용자 지정 캐시 종속성

사용자 지정 캐시 종속성에 대 한 ASP.NET 1.x 개발자 cried 합니다. ASP.NET에서 1.x CacheDependency 클래스에서 고유한 클래스를 파생 금지 개발자가 봉인 되어 있습니다. ASP.NET 2.0에서는 이러한 제한 사항이 제거 되 고 개발자는 자신의 사용자 지정 캐시 종속성을 개발 하 합니다. CacheDependency 클래스 파일, 디렉터리 또는 캐시 키를 기반으로 하는 사용자 지정 캐시 종속성을 만들 수 있도록 합니다.

예를 들어 아래 코드는 웹 응용 프로그램의 루트에 있는 stuff.xml 라는 파일에 따라 새 사용자 지정 캐시 종속성을 만듭니다.

[!code-csharp[Main](caching/samples/sample3.cs)]

이 시나리오에서는 stuff.xml 파일이 변경 될 때 캐시 된 항목이 무효화 됩니다.

캐시 키를 사용 하 여 사용자 지정 캐시 종속성을 만들 수 이기도 합니다. 이 메서드를 사용 하 여 캐시 키를 제거 하 고 캐시 된 데이터를 무효화 됩니다. 다음 예제는 이러한 과정을 보여 줍니다.

[!code-csharp[Main](caching/samples/sample4.cs)]

위에 삽입 된 항목을 무효화 하는 캐시 키 역할을 위해 캐시에 삽입 된 항목을 제거 하면 됩니다.

[!code-csharp[Main](caching/samples/sample5.cs)]

참고 캐시 키의 배열에 추가 된 값과 같으면 캐시 키 역할을 하는 항목의 키 여야 합니다.

## <a name="polling-based-sql-cache-dependenciesemalso-called-table-based-dependenciesem"></a>SQL 캐시 종속성 폴링을 기반<em>(테이블 기반 종속성이 라고도 함)</em>

SQL Server 7 및 2000 SQL 캐시 종속성에 대 한 폴링 기반 모델을 사용합니다. 폴링 기반 모델은 테이블의에서 데이터를 변경할 때 트리거되는 데이터베이스 테이블에 트리거를 사용 합니다. 업데이트를 트리거하는 **changeId** 필드 ASP.NET 주기적으로 검사 하는 알림 테이블에 있습니다. 경우는 **changeId** 필드가 업데이트 되었습니다, ASP.NET 알고 데이터 변경 및 캐시 된 데이터를 무효화 합니다.

> [!NOTE]
> SQL Server 2005 폴링 기반 모델을 사용할 수도 있지만 폴링 기반 모델은 가장 효율적인 모델을 없기 때문에 SQL Server 2005 (나중에 설명)는 쿼리 기반 모델을 사용 하는 것이 좋습니다.


폴링 기반 모델을 사용 하 여 제대로 작동 하려면 SQL 캐시 종속성에 대 한 순서로 테이블 알림이 활성화 되어 있어야 합니다. 이 위해서는 SqlCacheDependencyAdmin 클래스를 사용 하 여 프로그래밍 방식으로 또는 aspnet를 사용 하 여\_regsql.exe 유틸리티입니다.

다음 명령줄 라는 SQL Server 인스턴스에 있는 Northwind 데이터베이스의 Products 테이블 등록 *dbase* SQL에 대 한 종속성을 캐시 합니다.

[!code-console[Main](caching/samples/sample6.cmd)]

다음은 위의 명령에 사용 되는 명령줄 스위치에 대해 설명 합니다.

| **명령줄 스위치** | **용도** |
| --- | --- |
| -S *server* | 서버 이름을 지정합니다. |
| -ed | SQL 캐시 종속성에 대 한 데이터베이스를 사용 해야 한다고 지정 합니다. |
| -d *database\_name* | SQL 캐시 종속성을 사용 하도록 설정 하는 데이터베이스 이름을 지정 합니다. |
| -E | 해당 aspnet 지정\_regsql 데이터베이스에 연결할 때 Windows 인증을 사용 해야 합니다. |
| -et | SQL 캐시 종속성에 대 한 데이터베이스 테이블 설정 하는 것을 지정 합니다. |
| -t *table\_name* | SQL 캐시 종속성을 사용할 수 있도록 데이터베이스 테이블의 이름을 지정 합니다. |

> [!NOTE]
> Aspnet에 사용할 수 있는 다른 스위치는\_regsql.exe 합니다. 전체 목록은 실행 aspnet\_regsql.exe-? 명령줄입니다.


이 명령은 실행 하는 경우에 SQL Server 데이터베이스에 다음과 같은 변경 내용이:

- **AspNet\_SqlCacheTablesForChangeNotification** 테이블이 추가 됩니다. 이 테이블에는 SQL 캐시 종속성 활성화 된 데이터베이스의 각 테이블에 한 행씩을 포함 합니다.
- 다음 저장된 프로시저는 데이터베이스 내부에 생성 됩니다.


| AspNet\_SqlCachePollingStoredProcedure | AspNet 쿼리\_SqlCacheTablesForChangeNotification 테이블 SQL 캐시 종속성과 changeId 각 테이블에 대 한 값에 대해 설정 된 모든 테이블을 반환 합니다. 이 저장된 프로시저는 데이터 변경 되었는지 여부를 확인 하려면 폴링에 사용 됩니다. |
| --- | --- |
| AspNet\_SqlCacheQueryRegisteredTablesStoredProcedure | AspNet를 쿼리하여 SQL 캐시 종속성에 대해 설정 된 테이블의 모든 반환\_SqlCacheTablesForChangeNotification 테이블 및 모든 테이블은 SQL에 사용할 반환 종속성을 캐시 합니다. |
| AspNet\_SqlCacheRegisterTableStoredProcedure | 알림 테이블에 필요한 항목을 추가 하 여 SQL 캐시 종속성에 대 한 테이블을 등록 하 고 트리거를 추가 합니다. |
| AspNet\_SqlCacheUnRegisterTableStoredProcedure | 알림 테이블에 항목을 제거 하 여 SQL 캐시 종속성에 대 한 테이블의 등록을 취소 하 고 트리거를 제거 합니다. |
| AspNet\_SqlCacheUpdateChangeIdStoredProcedure | 변경된 된 테이블에 대 한 changeId 증가 하 여 알림 테이블을 업데이트 합니다. ASP.NET이이 값을 사용 하 여 데이터 변경 되었는지 여부를 결정 합니다. 아래에 표시 된 대로이 저장된 프로시저는 테이블을 설정할 때 만든 트리거에 의해 실행 됩니다. |


- SQL Server 트리거를 호출 ***테이블\_이름 *\_AspNet\_SqlCacheNotification\_트리거** 테이블에 대해 생성 됩니다. 이 트리거가 실행 AspNet\_SqlCacheUpdateChangeIdStoredProcedure는 INSERT, UPDATE 또는 DELETE는 테이블에서 수행 하는 경우.
- SQL Server 역할 이라는 **aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** 데이터베이스에 추가 합니다.

**aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** SQL Server 역할 권한이 EXEC AspNet\_SqlCachePollingStoredProcedure 합니다. Aspnet에 프로세스 계정을 추가 해야 하는 제대로 작동 하려면 폴링 모델에 대 한 순서로\_ChangeNotification\_ReceiveNotificationsOnlyAccess 역할입니다. Aspnet\_regsql.exe 도구에서 하지 이렇게 합니다.

### <a name="configuring-polling-based-sql-cache-dependencies"></a>폴링 기반 SQL 캐시 종속성을 구성

SQL 캐시 종속성 폴링을 기반을 구성 하는 데 필요한 몇 가지 단계가 있습니다. 데이터베이스 및 위에서 언급 한 대로 테이블을 사용 하도록 설정 하는 첫 번째 단계가입니다. 단계가 완료 되 면 구성의 나머지는 다음과 같습니다.

- ASP.NET 구성 파일을 구성 합니다.
- SqlCacheDependency를 구성합니다.

### <a name="configuring-the-aspnet-configuration-file"></a>ASP.NET 구성 파일을 구성합니다.

파일을 이전 모듈에 설명 된 대로 연결 문자열을 추가할 뿐 아니라 구성도 해야는 &lt;캐시&gt; 인 요소는 &lt;sqlCacheDependency&gt; 아래와 같이 요소:

[!code-xml[Main](caching/samples/sample7.xml)]

이 구성에서 SQL 캐시 종속성을 사용 하도록 설정 된 *pubs* 데이터베이스입니다. pollTime 특성이 참고는 &lt;sqlCacheDependency&gt; 요소 기본값 60000 밀리초로 또는 1 분입니다. (이 값 500 밀리초 미만 이어야 합니다.) 이 예제는 &lt;추가&gt; 요소는 새 데이터베이스를 추가 하 고 9000000 밀리초로 설정 하 고 pollTime를 재정의 합니다.

#### <a name="configuring-the-sqlcachedependency"></a>SqlCacheDependency를 구성합니다.

다음 단계는 SqlCacheDependency를 구성 하는 것입니다. 이 수행 하는 가장 쉬운 방법은 @ Outcache 지시문에서 SqlDependency 특성에 대 한 값을 다음과 같이 지정 하는 것:

[!code-aspx[Main](caching/samples/sample8.aspx)]

SQL 캐시 종속성에 대해 구성 된 위의 @ OutputCache 지시문에는 *작성자* 테이블에 *pubs* 데이터베이스입니다. 세미콜론으로 구분 하 여 여러 종속성을 구성할 수 있습니다 같이:

[!code-aspx[Main](caching/samples/sample9.aspx)]

SqlCacheDependency를 구성 하는 또 다른 방법은 프로그래밍 방식으로 그러려면 됩니다. 다음 코드에 대 한 새 SQL 캐시 종속성을 만듭니다는 *작성자* 테이블에 *pubs* 데이터베이스입니다.

[!code-csharp[Main](caching/samples/sample10.cs)]

SQL 캐시 종속성을 프로그래밍 방식으로 정의할의 이점 중 하나는 발생할 수 있는 모든 예외를 처리할 수 있습니다. 예를 들어, 알림에 대 한 설정 되어 있지 않은 데이터베이스에 대 한 SQL 캐시 종속성을 정의 하는 **DatabaseNotEnabledForNotificationException** 예외가 throw 됩니다. 이 경우 알림에 대 한 데이터베이스 호출 하 여 활성화를 시작할 수 있습니다는 **SqlCacheDependencyAdmin.EnableNotifications** 메서드 및 데이터베이스 이름을 전달 합니다.

마찬가지로, 알림의 경우 설정 되어 있지 않은 테이블에 대해 SQL 캐시 종속성을 정의 하는 경우는 **TableNotEnabledForNotificationException** throw 됩니다. 호출할 수 있습니다는 **SqlCacheDependencyAdmin.EnableTableForNotifications** 데이터베이스 이름 및 테이블 이름을 전달 합니다.

다음 코드 샘플에는 SQL 캐시 종속성을 구성 하는 경우 예외 처리 구성 하는 방법을 보여 줍니다.

[!code-csharp[Main](caching/samples/sample11.cs)]

추가 정보: [https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>쿼리 기반 SQL 캐시 종속성 (SQL Server 2005만)

SQL 캐시 종속성에 대 한 SQL Server 2005를 사용할 때 폴링 기반 모델은 필요한있지 않습니다. SQL 캐시 종속성 (추가 구성은 필요 하지 않습니다) SQL Server 인스턴스에 대 한 SQL 연결을 통해 직접 통신 사용 되 면 SQL Server 2005, SQL Server 2005 쿼리 알림 사용 합니다.

가장 간단한 방법은 쿼리 기반 알림을 사용 하도록 설정 하 여 선언적으로 작업을 수행 하는 **SqlCacheDependency** 를 데이터 원본 개체의 특성 **CommandNotification** 는 설정**EnableCaching** 특성을 **true**합니다. 이 메서드를 사용 하 여 코드는 필요 없습니다. 명령의 결과 대해 실행 데이터 원본 변경 내용을 데이터 캐시는 무효화 합니다.

다음 예제에서는 SQL 캐시 종속성에 대 한 데이터 소스 제어를 구성합니다.

[!code-aspx[Main](caching/samples/sample12.aspx)]

이 경우에 쿼리에 지정 된 경우에 **SelectCommand** 다른 결과 보다가 원래 반환 결과 캐시를 무효화 됩니다. 합니다.

모든 데이터 소스를 사용 한다고 SQL 캐시 종속성에 대해 설정 하 여 지정할 수도 있습니다는 **SqlDependency** 특성에는 **@ OutputCache** 지시문을 **CommandNotification** . 다음 예제에서는이 보여 줍니다.

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> SQL Server 2005에서 쿼리 알림에 대 한 자세한 내용은 SQL Server 온라인 설명서를 참조 합니다.


쿼리 기반 SQL 캐시 종속성을 구성 하는 또 다른 방법은 SqlCacheDependency 클래스를 사용 하 여 프로그래밍 방식으로 작업을 수행 하는 합니다. 다음 코드 예제에서는 이것은 수행 하는 방법을 보여 줍니다.

[!code-csharp[Main](caching/samples/sample14.cs)]

추가 정보: [https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>캐시 후 대체

캐싱 페이지는 웹 응용 프로그램의 성능을 크게 향상 시킬 수 있습니다. 그러나 경우에 따라 동적으로 페이지 내에서 캐시 될 페이지의 대부분 및 일부 조각 해야 합니다. 예를 들어는 전적으로 정적 설정된 기간에 대 한 뉴스 기사 페이지를 만들면 전체 페이지를 캐시 하도록 설정할 수 있습니다. 모든 페이지 요청에서 변경 하는 회전 광고 배너를 포함 하려는 경우 동적으로 보급 알림을 포함 하는 페이지의 일부 필요 합니다. 에 페이지를 캐시 하지만 일부 콘텐츠를 동적으로 대체할 수 있도록 하려면 asp를 사용할 수 있습니다. 캐시 후 대체 전체 페이지 캐시할 수 없는 특정 부분으로 표시 되며 광고 배너 예제에서는 AdRotator 제어를 사용 하면 광고 하 고 각 페이지 새로 고침에 대 한 각 사용자에 대해 동적으로 생성 되도록 캐시 후 대체 활용할 수 있습니다.

캐시 후 대체를 구현 하는 방법은 세 가지가 있습니다.

- 대체 컨트롤 사용 하 여 선언적으로 정의 합니다.
- 대체 제어 API에서 사용 하 여 프로그래밍 방식으로 합니다.
- AdRotator 컨트롤을 암시적으로 사용.

### <a name="substitution-control"></a>대체 컨트롤

ASP.NET 대체 컨트롤은 동적으로 생성 하지 않고 캐시는 캐시 된 페이지의 섹션을 지정 합니다. 페이지에 동적 콘텐츠를 나타낼 위치에 대체 컨트롤을 배치 합니다. 런타임 시 대체 컨트롤 MethodName 속성으로 지정 하는 메서드를 호출 합니다. 이 메서드는 대체 컨트롤의 내용을 대체 하는 문자열을 반환 해야 합니다. 메서드는 정적 메서드를 포함 하는 Page 또는 UserControl 컨트롤 이어야 합니다. 대체 컨트롤을 사용 하 여 클라이언트 쪽 cacheability 서버 캐시 가능성으로 변경 해야이 하면 페이지가 클라이언트에서 캐시 되지 것입니다. 이렇게 하면 페이지에 앞으로 요청 다시 동적 콘텐츠를 생성 하는 메서드를 호출 하 합니다.

### <a name="substitution-api"></a>대체 API

캐시 된 페이지에 대 한 동적 콘텐츠를 프로그래밍 방식으로 만들려면 호출할 수 있습니다는 [WriteSubstitution](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx) 메서드 페이지 코드에서 메서드 이름을 매개 변수로 전달 합니다. 동적 콘텐츠의 생성을 처리 하는 메서드는 단일 [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) 매개 변수는 문자열을 반환 합니다. 반환 문자열은 지정된 된 위치에서 대체 되는 콘텐츠. 대체 컨트롤에 선언적으로 사용 하는 대신 WriteSubstitution 메서드를 호출 하는 경우의 이점은 Page 또는 UserControl 개체의 정적 메서드를 호출 하는 것이 아니라 임의의 개체 메서드를 호출할 수 있습니다.

WriteSubstitution 메서드를 호출 하면 클라이언트 쪽 캐시 가능성이 서버 캐시 가능성으로 변경 되므로 클라이언트에서의 페이지 캐시 되지 것입니다. 이렇게 하면 페이지에 앞으로 요청 다시 동적 콘텐츠를 생성 하는 메서드를 호출 하 합니다.

### <a name="adrotator-control"></a>AdRotator 컨트롤

서버 컨트롤 구현 AdRotator 내부적으로 캐시 후 대체에 대 한 지원. 페이지에 있는 AdRotator 컨트롤을 배치 하는 경우에 부모 페이지의 캐시 여부에 관계 없이 각 요청에 대해 고유한 광고를 렌더링 합니다. 결과적으로, AdRotator 컨트롤을 포함 하는 페이지만 캐시 된 서버-측면입니다.

## <a name="controlcachepolicy-class"></a>ControlCachePolicy 클래스

ControlCachePolicy 클래스 사용자 정의 컨트롤을 사용 하 여 캐싱 조각의 프로그래밍 방식으로 제어할 수 있습니다. ASP.NET에서 사용자 정의 컨트롤을 포함 한 [BasePartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx) 인스턴스. BasePartialCachingControl 클래스에 출력 캐싱을 사용 하도록 설정 하는 사용자 정의 컨트롤을 나타냅니다.

액세스 하는 경우는 [BasePartialCachingControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx) 속성은 [PartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx) 컨트롤을 올바른 ControlCachePolicy 개체를 항상 표시 됩니다. 그러나 액세스 하는 경우는 [UserControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx) 속성은 [UserControl](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx) 컨트롤을 받게 유효한 ControlCachePolicy 개체가 사용자 정의 컨트롤에서 래핑된 이미 있는 경우에는 BasePartialCachingControl 컨트롤입니다. 래핑되지 않은 ControlCachePolicy 개체의 속성에서 반환 되는 관련된 BasePartialCachingControl 없기 때문에 조작 하려고 할 때 예외를 throw 합니다. 를 UserControl 인스턴스 예외를 생성 하지 않고 캐싱을 지원 하는지 확인 하려면 검사는 [SupportsCaching](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx) 속성입니다.

ControlCachePolicy 클래스를 사용 하 여 출력 캐시를 사용 하는 여러 가지 방법 중 하나입니다. 다음 목록에서는 출력 캐싱을 사용 하도록 설정 하는 방법은 설명 합니다.

- 사용 하 여는 [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) 지시문 사용할 수 있도록 출력 선언적 시나리오에서 캐시 합니다.
- 사용 하 여는 [PartialCachingAttribute](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx) 특성을 코드 숨김 파일에서 사용자 정의 컨트롤에 대 한 캐싱을 사용 합니다.
- 사용 하는 앞의 두 방법 중 하나를 사용 하 여 캐시 활성화 되 고는 를사용하여동적으로로드된BasePartialCachingControl인스턴스프로그래밍시나리오에서캐시설정을지정하려면ControlCachePolicy클래스를사용하여[System.Web.UI.TemplateControl.LoadControl](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx) 메서드.

ControlCachePolicy 인스턴스 제어 수명 주기의 Init 및 PreRender 단계 사이만 성공적으로 조작할 수 있습니다. PreRender 단계 이후에 ControlCachePolicy 개체를 수정 하는 경우 컨트롤이 렌더링 되 면 후 변경한 모든 내용은 캐시 설정 (컨트롤 렌더링 단계 동안 캐시 됨)에 실제로 영향을 줄 수 없습니다 ASP.NET 예외를 throw 합니다. 마지막으로, 사용자 정의 컨트롤 인스턴스 (및 따라서 ControlCachePolicy 개체)은 프로그래밍 방식으로 조작에 사용할 수 있는 경우에는 실제로 렌더링 합니다.

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>캐싱 구성-변경는 &lt;캐싱&gt; 요소

ASP.NET 2.0에서 캐싱 구성에 몇 가지 변경 사항이 있습니다. &lt;캐싱&gt; 요소 ASP.NET 2.0의 새로운 기능 및 구성 파일에서 캐싱 구성을 변경할 수 있습니다. 다음 특성을 사용할 수 있습니다.

| **요소** | **설명** |
| --- | --- |
| **cache** | 선택적 요소입니다. 전역 응용 프로그램 캐시 설정을 정의합니다. |
| **outputCache** | 선택적 요소입니다. 응용 프로그램 수준 출력 캐시 설정을 지정합니다. |
| **outputCacheSettings** | 선택적 요소입니다. 응용 프로그램의 페이지에 적용할 수 있는 출력 캐시 설정을 지정 합니다. |
| **sqlCacheDependency** | 선택적 요소입니다. ASP.NET 응용 프로그램에 대 한 SQL 캐시 종속성을 구성합니다. |

### <a name="the-ltcachegt-element"></a>&lt;캐시&gt; 요소

다음 특성에서 사용할 수 있는 &lt;캐시&gt; 요소:

| **특성** | **설명** |
| --- | --- |
| **disableMemoryCollection** | 선택적 **부울** 특성입니다. 컴퓨터의 메모리가 부족할 때 발생 하는 캐시 메모리 컬렉션 되지 않는지 여부를 나타내는 값을 가져오거나 설정 합니다. |
| **disableExpiration** | 선택적 **부울** 특성입니다. 캐시 만료 되지 않는지 여부를 나타내는 값을 가져오거나 설정 합니다. 캐시 된 항목이 만료 되지 않고 비활성화 및 만료 된 캐시 항목의 배경 청소 발생 하지 않습니다. |
| **privateBytesLimit** | 선택적 **Int64** 특성입니다. 메모리를 회수 하는 동안 만료 된 항목 플러시를 시작 하기 전에 응용 프로그램의 전용 바이트의 최대 크기를 나타내는 값을 가져오거나 설정 합니다. 이 제한으로 캐시에서 사용 되는 메모리의에서 일반적인 메모리 오버 실행 중인 응용 프로그램을 포함 합니다. 0으로 설정 ASP.NET를 시작 메모리를 회수 하는 시기를 결정 하기 위한 자체 추론을 사용 함을 나타냅니다. |
| **percentagePhysicalMemoryUsedLimit** | 선택적 **Int32** 특성입니다. 이 메모리 사용도 캐시에서 사용 하는 두 메모리를 포함 하는 메모리를 회수 하는 동안 만료 된 항목 플러시를 시작 하기 전에 응용 프로그램에서 사용할 수 있는 컴퓨터의 실제 메모리의 최대 백분율을 나타내는 값을 가져오거나 설정 합니다. 실행 중인 응용 프로그램의 일반적인 메모리 사용 합니다. 0으로 설정 ASP.NET를 시작 메모리를 회수 하는 시기를 결정 하기 위한 자체 추론을 사용 함을 나타냅니다. |
| **privateBytesPollTime** | 선택적 **TimeSpan** 특성입니다. 응용 프로그램의 전용 바이트 메모리 사용에 대 한 폴링 간의 시간 간격을 나타내는 값을 가져오거나 설정 합니다. |

### <a name="the-ltoutputcachegt-element"></a>&lt;outputCache&gt; 요소

다음 특성은 사용할 수는 &lt;outputCache&gt; 요소입니다.


|       <strong>특성</strong>        |                                                                                                                                                                                                                                                       <strong>설명</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>enableOutputCache</strong>    |                                                                                                                                                          선택적 <strong>부울</strong> 특성입니다. 페이지 출력 캐시를 설정/해제합니다. 사용 하지 않을 경우 프로그래밍 방식으로 또는 선언적 설정에 관계 없이 페이지가 캐시 됩니다. 기본값은 <strong>true</strong>합니다.                                                                                                                                                           |
|  <strong>enableFragmentCache</strong>   |                                                선택적 <strong>부울</strong> 특성입니다. 응용 프로그램 부분 캐시를 설정/해제합니다. 비활성화 하면 페이지가 없는에 관계 없이 캐시 된 [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) 지시문 또는 캐싱을 사용 하는 프로필입니다. 업스트림 프록시 서버는 물론 브라우저 클라이언트 페이지 출력 캐시를 시도 하지 않아야 표시 하는 캐시 제어 헤더를 포함 합니다. 기본값은 <strong>false</strong>합니다.                                                 |
| <strong>sendCacheControlHeader</strong> |                                                                                                                                                      선택적 <strong>부울</strong> 특성입니다. 나타내는 값을 가져오거나 여부는 <strong>캐시-control: private</strong> 출력 캐시 모듈에 의해 기본적으로 헤더를 보냅니다. 기본값은 <strong>false</strong>합니다.                                                                                                                                                      |
|      <strong>omitVaryStar</strong>      | 선택적 <strong>부울</strong> 특성입니다. Http 전송 사용 가능/불가능 "<strong>달라질 수 있습니다: \<g ><em>" 응답에서 헤더입니다. 기본 설정인 false, 사용 된 "</em>* 달라질 수 있습니다: \* <strong>" 출력 캐시 된 페이지에 대 한 헤더를 보냅니다. Vary 헤더를 보낼 때 수에 대 한 서로 다른 버전을 캐싱하지 Vary 헤더에 지정 된 내용에 따라 합니다. 예를 들어 <em>Vary: 사용자-에이전트</em> 요청을 실행 하는 사용자 에이전트에 따라 페이지의 여러 버전을 저장 합니다. 기본값은 * * false</strong>합니다. |

### <a name="the-ltoutputcachesettingsgt-element"></a>&lt;outputCacheSettings&gt; 요소

&lt;outputCacheSettings&gt; 요소 앞에서 설명한 대로 캐시 프로필을 만들 수 있도록 합니다. 에 대 한 유일한 자식 요소는 &lt;outputCacheSettings&gt; 요소는는 &lt;outputCacheProfiles&gt; 요소 캐시 프로필을 구성 합니다.

### <a name="the-ltsqlcachedependencygt-element"></a>&lt;sqlCacheDependency&gt; 요소

다음 특성은 사용할 수는 &lt;sqlCacheDependency&gt; 요소입니다.

| **특성** | **설명** |
| --- | --- |
| **enabled** | 필요한 **부울** 특성입니다. 변경 내용 폴링 하는지 여부를 나타냅니다. |
| **pollTime** | 선택적 **Int32** 특성입니다. SqlCacheDependency 된 변경에 대 한 데이터베이스 테이블을 폴링하는 빈도 설정 합니다. 이 값은 연속적인 폴링 간격 (밀리초)의 수에 해당합니다. 500 밀리초 미만에 설정할 수 없습니다. 기본값은 1 분입니다. |

### <a name="more-information"></a>추가 정보

있어야 하는 인식 캐시 구성과 관련 된 일부 추가 정보가 있습니다.

- 작업자 프로세스가 전용 바이트 제한 설정 되어 있지 않으면 캐시는 다음과 같은 제한이 중 하나를 사용 합니다. 

    - x86 2 GB: 800 MB 또는 실제 RAM의 60% 더 작은
    - x86 3 g B: 1800 MB 또는 실제 RAM의 60% 더 작은
    - x 64: 1 테라바이트까지 또는 실제 RAM의 60% 더 작은
- 두 작업자 프로세스 전용 바이트 제한 및 &lt;privateBytesLimit 캐시 /&gt; 는 설정, 캐시 두의 최소값을 사용 합니다.
- 마찬가지로 1.x에서는 캐시 항목을 삭제 하 고 GC를 호출 합니다. 두 가지 이유로 수집 합니다. 

    - 전용 바이트 제한에 근접 하는 매우
    - 사용 가능한 메모리가 10% 보다 작거나 near
- 효과적으로 트림을 사용 하지 않도록 설정 하 고 설정 하 여 사용 가능한 메모리 부족 상태에 대 한 캐시 수 &lt;percentagePhysicalMemoryUseLimit 캐시 /&gt; 100입니다.
- 1.x와 달리 2.0에서 일시 중단 trim 및 수집 호출 마지막 gc가 있습니다. 수집 전용 바이트 메모리 제한 (캐시)의 1% 개 이상의 관리 되는 힙의 크기 또는 줄어들지 않습니다.

## <a name="lab1-custom-cache-dependencies"></a>Lab1: 사용자 지정 캐시 종속성

1. 새 웹 사이트를 만듭니다.
2. Cache.xml 라는 새 XML 파일을 추가 하 고 웹 응용 프로그램의 루트에 저장 합니다.
3. 페이지에 다음 코드를 추가\_default.aspx의 코드 숨김의 메서드를 로드 합니다. 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. 소스 뷰에서 default.aspx의 맨 위에 다음을 추가 합니다. 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. Default.aspx를 찾습니다. 시간의 않습니다 말합니다?
6. 브라우저를 새로 고칩니다. 시간의 않습니다 말합니다?
7. Cache.xml 열고 다음 코드를 추가 합니다. 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. Cache.xml를 저장 합니다.
9. 브라우저를 새로 고치십시오. 시간의 않습니다 말합니다?
10. 이전에 캐시 된 값을 표시 하는 대신 시간을 업데이트 하는 이유를 설명 합니다.

## <a name="lab-2-using-polling-based-cache-dependencies"></a>랩 2:를 사용 하 여 폴링 기반 캐시 종속성

이 랩에서 GridView 및 DetailsView 컨트롤을 통해 Northwind 데이터베이스의 데이터를 편집할 수 있는 이전 모듈에서 만든 프로젝트를 사용 합니다.

1. Visual Studio 2005에서 프로젝트를 엽니다.
2. Aspnet 실행\_Products 테이블 및 데이터베이스를 사용 하도록 설정 하려면 Northwind 데이터베이스에 대해 regsql 유틸리티입니다. Visual Studio 명령 프롬프트에서 다음 명령을 사용 합니다. 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. Web.config 파일에 다음을 추가 합니다. 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. Showdata.aspx 라는 새 webform를 추가 합니다.
5. @ Outputcache 지시문 다음 showdata.aspx 페이지에 추가 합니다. 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. 페이지에 다음 코드를 추가\_showdata.aspx의 로드: 

    [!code-html[Main](caching/samples/sample21.html)]
7. 새 SqlDataSource 컨트롤 showdata.aspx을 추가 하 고 Northwind 데이터베이스 연결을 사용 하도록 구성 합니다. 다음을 클릭 합니다.
8. ProductID 및 ProductName 확인란을 선택 하 고 클릭 합니다.
9. 마침을 클릭 합니다.
10. 새 GridView showdata.aspx 페이지에 추가 합니다.
11. SqlDataSource1 드롭다운 목록에서 선택 합니다.
12. 저장 하 고 showdata.aspx를 찾습니다. 표시 된 시간을 기록해 둡니다.
