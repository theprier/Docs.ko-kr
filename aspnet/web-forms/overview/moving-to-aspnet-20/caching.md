---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: 캐싱 | Microsoft Docs
author: microsoft
description: 캐싱의 이해가 우수한 ASP.NET 응용 프로그램에 대 한 중요 합니다. ASP.NET 1.x 캐싱;에 대 한 세 가지 다른 옵션 제공 캐싱, 출력 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: 4f52a88680db54de6271b17bd52cbdace66425e9
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37387701"
---
<a name="caching"></a>캐싱
====================
[Microsoft](https://github.com/microsoft)

> 캐싱의 이해가 우수한 ASP.NET 응용 프로그램에 대 한 중요 합니다. ASP.NET 1.x 캐싱;에 대 한 세 가지 다른 옵션 제공 출력 캐싱, 부분 캐싱 및 캐시 API.


캐싱의 이해가 우수한 ASP.NET 응용 프로그램에 대 한 중요 합니다. ASP.NET 1.x 캐싱;에 대 한 세 가지 다른 옵션 제공 출력 캐싱, 부분 캐싱 및 캐시 API. ASP.NET 2.0은 모든 세 가지이 방법이 제공 하지만 몇 가지 중요 한 기능을 추가 합니다. 몇 가지 새 캐시 종속성 및 개발자는 이제 사용자 지정 캐시 종속성도 만들 수 있습니다. 캐싱 구성도 크게 향상 되었습니다 ASP.NET 2.0의 합니다.

## <a name="new-features"></a>새 기능

## <a name="cache-profiles"></a>캐시 프로필

캐시 프로필 개별 페이지에 다음 적용할 수 있는 특정 캐시 설정을 정의 하는 개발자를 수 있습니다. 예를 들어, 12 시간 후 캐시에서 만료 되어야 하는 일부 페이지에 있는 경우 해당 페이지에 적용할 수 있는 캐시 프로필을 쉽게 만들 수 있습니다. 새 캐시 프로필을 추가 하려면 사용 합니다 &lt;outputCacheSettings&gt; 구성 파일의 섹션입니다. 예를 들어, 다음은 호출 하는 캐시 프로필의 구성 *twoday* 12 시간의 캐시 기간을 구성 합니다.

[!code-xml[Main](caching/samples/sample1.xml)]

이 캐시 프로필의 특정 페이지에 적용 하려면 아래와 같이 @ OutputCache 지시문의 CacheProfile 특성을 사용 합니다.

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>사용자 지정 캐시 종속성

ASP.NET 1.x 개발자는 사용자 지정 캐시 종속성에 대 한 cried 합니다. Asp.net에서 1.x에서는 CacheDependency 클래스는 자체 클래스에서 파생 될 방지-개발자가 봉인 되었습니다. ASP.NET 2.0에서는 해당 제한 사항이 제거 되었습니다 및 개발자는 자신의 사용자 지정 캐시 종속성을 개발 합니다. 에서는 CacheDependency 클래스 파일, 디렉터리 또는 캐시 키에 따라 사용자 지정 캐시 종속성을 만들 수 있습니다.

예를 들어, 아래 코드는 웹 응용 프로그램의 루트에 있는 stuff.xml 라는 파일을 기반으로 새 사용자 지정 캐시 종속성을 만듭니다.

[!code-csharp[Main](caching/samples/sample3.cs)]

이 시나리오에서는 stuff.xml 파일이 변경 되 면 캐시 된 항목이 무효화 됩니다.

캐시 키를 사용 하 여 사용자 지정 캐시 종속성을 만들 수 이기도 합니다. 이 방법을 사용 하 여 캐시 키의 제거 캐시 된 데이터를 무효화 됩니다. 다음 예제는 이러한 과정을 보여 줍니다.

[!code-csharp[Main](caching/samples/sample4.cs)]

위에 삽입 된 항목을 무효화 하는 캐시 키 역할을 캐시에 삽입 된 항목을 제거 하면 됩니다.

[!code-csharp[Main](caching/samples/sample5.cs)]

참고 캐시 키 배열에 추가 하는 값과 같은 캐시 키로 사용 되는 항목의 키 여야 합니다.

## <a name="polling-based-sql-cache-dependenciesemalso-called-table-based-dependenciesem"></a>SQL 캐시 종속성 폴링 기반<em>(테이블 기반 종속성이 라고도 함)</em>

SQL Server 7 및 2000 SQL 캐시 종속성에 대 한 폴링 기반 모델을 사용 합니다. 폴링 기반 모델은 테이블의에서 데이터를 변경할 때 트리거되는 데이터베이스 테이블에서 트리거를 사용 합니다. 업데이트를 트리거하는 한 **changeId** ASP.NET 주기적으로 확인 하는 알림 테이블의 필드입니다. 경우는 **changeId** 필드가 업데이트 되었습니다, ASP.NET 인식 데이터를 변경 하 고 캐시 된 데이터를 무효화 합니다.

> [!NOTE]
> SQL Server 2005 폴링 기반 모델을 사용할 수도 있지만 폴링 기반 모델은 가장 효율적인 모델을 없는 이므로 SQL Server 2005를 사용 하 여 나중에 설명 하는 쿼리 기반 모델을 사용 하는 것이 좋습니다.


폴링 기반 모델을 사용 하 여 제대로 작동 하려면 SQL 캐시 종속성에 대 한 순서로 테이블 알림 기능이 설정 되어 있어야 합니다. 프로그래밍 방식으로 SqlCacheDependencyAdmin 클래스를 사용 하 여 수행할 수 있습니다 또는 aspnet를 사용 하 여\_regsql.exe 유틸리티입니다.

다음 명령줄 라는 SQL Server 인스턴스에 있는 Northwind 데이터베이스의 Products 테이블을 등록 *dbase* SQL에 대 한 종속성을 캐시 합니다.

[!code-console[Main](caching/samples/sample6.cmd)]

다음은 위의 명령에 사용 되는 명령줄 스위치의 설명입니다.

| **명령줄 스위치** | **용도** |
| --- | --- |
| -S *server* | 서버 이름을 지정합니다. |
| -ed | SQL 캐시 종속성에 대 한 데이터베이스를 사용 해야를 지정 합니다. |
| -d *database\_name* | SQL 캐시 종속성을 사용 하도록 설정 해야 하는 데이터베이스 이름을 지정 합니다. |
| -E | 해당 aspnet 지정\_regsql 데이터베이스에 연결할 때 Windows 인증을 사용 해야 합니다. |
| -et | SQL 캐시 종속성에 대 한 데이터베이스 테이블을 사용 하는 것을 지정 합니다. |
| -t *table\_name* | SQL 캐시 종속성을 사용할 수 있도록 데이터베이스 테이블의 이름을 지정 합니다. |

> [!NOTE]
> Aspnet에 사용할 수 있는 다른 스위치는\_regsql.exe 합니다. 전체 목록을 실행 aspnet\_regsql.exe-? 명령줄입니다.


이 명령을 실행 하는 경우 SQL Server 데이터베이스를 다음 변경 내용은 적용 됩니다.

- **AspNet\_SqlCacheTablesForChangeNotification** 테이블이 추가 됩니다. 이 테이블에는 각 데이터베이스의 테이블에는 SQL 캐시 종속성을 사용 하도록 설정한 행당 하나씩 포함 합니다.
- 다음 저장된 프로시저를 데이터베이스 내부에 만들어집니다.


| AspNet\_SqlCachePollingStoredProcedure | AspNet 쿼리\_SqlCacheTablesForChangeNotification 테이블 changeId 각 테이블에 대 한 값과 SQL 캐시 종속성에 대해 설정 된 모든 테이블을 반환 합니다. 이 저장된 프로시저는 데이터 변경 되었는지 여부를 확인 하려면 폴링에 사용 됩니다. |
| --- | --- |
| AspNet\_SqlCacheQueryRegisteredTablesStoredProcedure | AspNet를 쿼리하여 SQL 캐시 종속성에 대 한 설정 된 테이블의 모든 반환\_SqlCacheTablesForChangeNotification 테이블과 반환 모든 테이블에 설정 된 SQL 캐시 종속성입니다. |
| AspNet\_SqlCacheRegisterTableStoredProcedure | 알림 테이블에 필요한 항목을 추가 하 여 SQL 캐시 종속성에 대 한 테이블을 등록 하 고 트리거를 추가 합니다. |
| AspNet\_SqlCacheUnRegisterTableStoredProcedure | 알림 테이블에 항목을 제거 하 여 SQL 캐시 종속성에 대 한 테이블을 등록 취소 하 고 트리거를 제거 합니다. |
| AspNet\_SqlCacheUpdateChangeIdStoredProcedure | 변경된 테이블에 대 한 changeId 증가 시켜 알림 테이블을 업데이트 합니다. ASP.NET은 데이터 변경 되었는지 여부를 확인 하려면이 값을 사용 합니다. 아래와 같이이 저장된 프로시저는 테이블에 활성화 될 때 생성 된 트리거에 의해 실행 됩니다. |


- SQL Server 트리거를 호출 ***테이블\_이름 *\_AspNet\_SqlCacheNotification\_트리거** 테이블에 대해 만들어집니다. 이 트리거가 실행 AspNet\_SqlCacheUpdateChangeIdStoredProcedure 삽입, 업데이트 또는 삭제 테이블에서 수행 될 때입니다.
- SQL Server 역할을 호출 **aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** 데이터베이스에 추가 됩니다.

합니다 **aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** SQL Server 역할 권한이 EXEC AspNet\_SqlCachePollingStoredProcedure 합니다. 제대로 작동 하려면 폴링 모델에 대 한 순서로 프로세스 계정의을 더해야 aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess 역할입니다. Aspnet\_regsql.exe 도구는 이렇게 하지 있습니다.

### <a name="configuring-polling-based-sql-cache-dependencies"></a>폴링 기반 SQL 캐시 종속성 구성

SQL 캐시 종속성 폴링 기반을 구성 하는 데 필요한 여러 단계가 있습니다. 첫 번째 단계는 데이터베이스 및 테이블 위에서 설명한 것 처럼 사용할 수 있도록 합니다. 해당 단계가 완료 되 면 구성의 나머지는 다음과 같습니다.

- ASP.NET 구성 파일을 구성 합니다.
- SqlCacheDependency를 구성합니다.

### <a name="configuring-the-aspnet-configuration-file"></a>ASP.NET 구성 파일 구성

연결 문자열에는 이전 단원에서 설명한 대로 추가 하는 것 외에도 구성도 해야 합니다는 &lt;캐시&gt; 요소를 &lt;sqlCacheDependency&gt; 아래와 같이 요소:

[!code-xml[Main](caching/samples/sample7.xml)]

이 구성에서 SQL 캐시 종속성을 사용 하도록 설정 합니다 *pubs* 데이터베이스입니다. pollTime 특성에 &lt;sqlCacheDependency&gt; 요소 기본값 60000 밀리초로 또는 1 분입니다. (이 값 500 밀리초 미만 이어야 합니다.) 이 예제는 &lt;추가&gt; 요소는 새 데이터베이스를 추가 하 고 9000000 밀리초로 설정 된 pollTime 재정의 합니다.

#### <a name="configuring-the-sqlcachedependency"></a>SqlCacheDependency를 구성합니다.

다음 단계는 SqlCacheDependency를 구성 하는 것입니다. 작업을 수행 하는 가장 쉬운 방법은 다음과 같습니다. 다음과 같이 @ Outcache 지시문에 SqlDependency 특성에 대 한 값을 지정 하려면

[!code-aspx[Main](caching/samples/sample8.aspx)]

SQL 캐시 종속성에 대해 구성 된 위의 @ OutputCache 지시문에 *작성자* 테이블에 *pubs* 데이터베이스입니다. 세미콜론으로 구분 하 여 여러 종속성을 구성할 수 있습니다 다음과 같이 합니다.

[!code-aspx[Main](caching/samples/sample9.aspx)]

SqlCacheDependency를 구성 하는 다른 방법은 프로그래밍 방식으로 수행 하는 것입니다. 다음 코드를 새 SQL 캐시 종속성을 만듭니다.는 *작성자* 테이블에 *pubs* 데이터베이스입니다.

[!code-csharp[Main](caching/samples/sample10.cs)]

프로그래밍 방식으로 SQL 캐시 종속성을 정의 하는 이점 중 하나는 발생할 수 있는 모든 예외를 처리할 수 있습니다. 예를 들어 알림의 경우 활성화 되지 않은 데이터베이스에 대 한 SQL 캐시 종속성을 정의 하는 **DatabaseNotEnabledForNotificationException** 예외가 throw 됩니다. 이 경우 알림에 대 한 데이터베이스 호출 하 여 활성화를 시작할 수 있습니다 합니다 **SqlCacheDependencyAdmin.EnableNotifications** 메서드 및 데이터베이스 이름을 전달 합니다.

마찬가지로 알림의 경우 활성화 되지 않은 테이블에 대 한 SQL 캐시 종속성을 정의 하려는 경우는 **TableNotEnabledForNotificationException** throw 됩니다. 호출할 수 있습니다 합니다 **SqlCacheDependencyAdmin.EnableTableForNotifications** 메서드 테이블 이름과 데이터베이스 이름을 전달 합니다.

다음 코드 샘플에서는 SQL 캐시 종속성을 구성 하는 경우 예외 처리를 제대로 구성 하는 방법을 보여 줍니다.

[!code-csharp[Main](caching/samples/sample11.cs)]

자세한 정보: [https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>쿼리 기반 SQL 캐시 종속성 (SQL Server 2005만)

SQL 캐시 종속성에 대 한 SQL Server 2005를 사용 하는 경우 폴링 기반 모델은 필요한 아닙니다. SQL 캐시 종속성 (추가 구성은 필요 하지 않습니다) SQL Server 인스턴스에 대 한 SQL 연결을 통해 직접 통신 사용 되 면 SQL Server 2005, SQL Server 2005 쿼리 알림 사용 합니다.

가장 간단한 방법은 쿼리 기반 알림을 사용 하도록 설정 하 여 선언적으로 수행 하는 것은 **SqlCacheDependency** 데이터 원본 개체의 특성 **CommandNotification** 설정과 합니다 **EnableCaching** 특성을 **true**합니다. 이 메서드를 사용 하 여 코드가 필요 하지 않습니다. 명령의 결과 대해 실행 데이터 원본 변경 내용 캐시 데이터는 무효화 합니다.

다음 예제에서는 SQL 캐시 종속성에 대 한 데이터 소스 컨트롤을 구성합니다.

[!code-aspx[Main](caching/samples/sample12.aspx)]

이 경우에 지정 된 쿼리를 **SelectCommand** 보다 다른 결과 원래 않았습니다 반환 결과 캐시를 무효화 됩니다. 합니다.

모든 데이터 원본이 사용할 SQL 캐시 종속성에 대 한 설정 하 여 지정할 수도 있습니다는 **SqlDependency** 특성을 **@ OutputCache** 지시문을 **CommandNotification** . 아래 예제에서는이 설명 합니다.

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> SQL Server 2005의 쿼리 알림에 대 한 자세한 내용은 SQL Server 온라인 설명서를 참조 합니다.


쿼리 기반 SQL 캐시 종속성을 구성 하는 다른 방법은 SqlCacheDependency 클래스를 사용 하 여 프로그래밍 방식으로 이렇게 하는 것입니다. 다음 코드 샘플에서는 이렇게 하는 방법을 보여 줍니다.

[!code-csharp[Main](caching/samples/sample14.cs)]

자세한 정보: [https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>캐시 후 대체

캐싱 페이지는 웹 응용 프로그램의 성능을 크게 향상 시킬 수 있습니다. 그러나 일부 경우 동적 페이지 내에서 대부분의 캐시할 페이지 및 일부 조각 해야 합니다. 예를 들어은 전적으로 정적 설정된 기간에 대 한 뉴스 기사 페이지를 만드는 경우 전체 페이지를 캐시 하도록 설정할 수 있습니다. 페이지 요청 마다 변경 하는 회전 ad 배너를 포함 하려는 경우 동적으로 보급 알림을 포함 하는 페이지의 부분을 해야 합니다. 페이지를 캐시 하지만 일부 콘텐츠를 동적으로 대체할 수 있도록, ASP.NET 캐시 후 대체를 사용할 수 있습니다. 캐시 후 대체를 사용 하 여 전체 페이지 출력 캐싱에서 제외로 표시 하는 특정 파트와 캐시 됩니다. 광고 배너 예에서 AdRotator 컨트롤을 사용 하면 각 페이지 새로 고침 및 각 사용자에 대 한 동적으로 만들었으므로 광고 캐시 후 대체 활용할 수 있습니다.

캐시 후 대체를 구현 하는 방법은 세 가지가 있습니다.

- 대체 컨트롤을 선언적으로 사용 합니다.
- 프로그래밍 방식으로 대체 컨트롤 API를 사용 합니다.
- AdRotator 컨트롤을 암시적으로 사용 합니다.

### <a name="substitution-control"></a>대체 제어

ASP.NET 대체 컨트롤은 동적으로 생성 하지 않고 캐시는 캐시 된 페이지의 섹션을 지정 합니다. 동적 콘텐츠를 표시 하려는 페이지의 위치에 대체 컨트롤을 추가 합니다. 런타임 시 대체 컨트롤 MethodName 속성으로 지정 하는 메서드를 호출 합니다. 메서드는 다음 대체 컨트롤의 콘텐츠를 대체 하는 문자열을 반환 해야 합니다. 메서드를 포함 하는 페이지 또는 UserControl 컨트롤에 정적 메서드여야 합니다. 대체 컨트롤 사용 하면 클라이언트 쪽 캐시 가능성 서버 캐시 가능성을 변경할 페이지 클라이언트에서 캐시 되지 않을 수 있도록 합니다. 페이지에 대 한 향후 요청 동적 콘텐츠 생성을 다시 메서드를 호출 하는 것이 이렇게 합니다.

### <a name="substitution-api"></a>대체 API

캐시 된 페이지에 대 한 동적 콘텐츠를 프로그래밍 방식으로 만들려면 호출할 수 있습니다는 [WriteSubstitution](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx) 메서드 페이지 코드에서 메서드 이름을 매개 변수로 전달 합니다. 동적 콘텐츠 생성을 처리 하는 메서드는 단일 [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) 매개 변수는 문자열을 반환 합니다. 반환 문자열은 콘텐츠를 지정된 된 위치에서 대체 됩니다. 대체 컨트롤을 선언적으로 사용 하는 대신 WriteSubstitution 메서드를 호출 하는 장점은 페이지 또는 UserControl 개체의 정적 메서드를 호출 하는 것이 아니라 임의의 개체 메서드를 호출할 수 있습니다.

WriteSubstitution 메서드를 호출 하면 클라이언트 쪽 캐시 가능성 서버 캐시 가능성으로 변경 되므로 클라이언트에서 페이지 캐시 되지 않을. 페이지에 대 한 향후 요청 동적 콘텐츠 생성을 다시 메서드를 호출 하는 것이 이렇게 합니다.

### <a name="adrotator-control"></a>AdRotator 컨트롤

서버 컨트롤 구현 AdRotator는 내부적으로 캐시 후 대체를 지원 합니다. 페이지에는 AdRotator 컨트롤을 배치 하는 경우 부모 페이지의 캐시 여부에 관계 없이 각 요청에 대해 고유한 광고 렌더링 합니다. 결과적으로, AdRotator 컨트롤을 포함 하는 페이지는만 캐시 서버 쪽입니다.

## <a name="controlcachepolicy-class"></a>ControlCachePolicy 클래스

ControlCachePolicy 클래스는 사용자 정의 컨트롤을 사용 하 여 캐싱용 조각의 프로그래밍 방식으로 제어할 수 있습니다. ASP.NET 사용자 컨트롤 내에서 포함 된 [BasePartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx) 인스턴스. BasePartialCachingControl 클래스에 출력 캐싱을 사용 하도록 설정 하는 사용자 컨트롤을 나타냅니다.

액세스 하는 경우는 [BasePartialCachingControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx) 의 속성을 [PartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx) 컨트롤 올바른 ControlCachePolicy 개체를 항상 표시 됩니다. 그러나 액세스 하는 경우는 [UserControl.CachePolicy](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx) 의 속성을 [UserControl](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx) 컨트롤 받게 올바른 ControlCachePolicy 개체가 사용자 정의 컨트롤 이미 래핑되는 경우에을 BasePartialCachingControl 컨트롤입니다. 래핑되지 않은 경우 ControlCachePolicy 개체 속성에서 반환 하는 연결된 BasePartialCachingControl 없으므로 조작 하려고 할 때 예외가 throw 됩니다. UserControl 인스턴스를 예외 생성 없이 캐시를 지원 하는지 여부를 결정할 검사 합니다 [SupportsCaching](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx) 속성입니다.

ControlCachePolicy 클래스를 사용 하는 여러 가지 방법으로 출력 캐싱을 사용할 수 있습니다. 다음 목록에서는 출력 캐싱을 사용 하도록 설정 하 여 메서드를 설명 합니다.

- 사용 된 [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) 활성화 하는 지시문에서에서 출력 캐싱을 선언적 시나리오입니다.
- 사용 된 [PartialCachingAttribute](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx) 특성을 코드 숨김 파일에 사용자 정의 컨트롤에 대 한 캐싱을 사용 하도록 설정 합니다.
- ControlCachePolicy 클래스를 사용 하 여 이전 방법 중 하나를 사용 하 여 캐시 활성화 되었으며 를사용하여동적으로로드하는BasePartialCachingControl인스턴스와작업은프로그래밍시나리오에서캐시설정을지정[System.Web.UI.TemplateControl.LoadControl](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx) 메서드.

컨트롤 주기의 Init 및 PreRender 단계 사이만 ControlCachePolicy 인스턴스를 성공적으로 조작할 수 있습니다. PreRender 단계 후 ControlCachePolicy 개체를 수정 하면 ASP.NET 컨트롤 렌더링 된 후 변경 실제로 (컨트롤을 렌더링 단계 동안 캐시 된) 캐시 설정에 영향을 줄 수 없습니다 때문에 예외가 throw 됩니다. 마지막으로, 사용자 컨트롤 인스턴스 (및 따라서 ControlCachePolicy 개체)에 제공 됩니다 프로그래밍 방식으로 조작 실제로 렌더링 될 때입니다.

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>캐싱 구성-변경 된 &lt;캐싱&gt; 요소

ASP.NET 2.0에서 캐싱 구성에 여러 변경 내용이 있습니다. 합니다 &lt;캐싱&gt; 요소는 ASP.NET 2.0의 새로운 기능 및 구성 파일에서 캐싱 구성을 변경할 수 있습니다. 다음 특성을 사용할 수 있습니다.

| **요소** | **설명** |
| --- | --- |
| **cache** | 선택적 요소입니다. 전역 응용 프로그램 캐시 설정을 정의합니다. |
| **outputCache** | 선택적 요소입니다. 응용 프로그램 수준 출력 캐시 설정을 지정합니다. |
| **outputCacheSettings** | 선택적 요소입니다. 응용 프로그램의 페이지에 적용할 수 있는 출력 캐시 설정을 지정 합니다. |
| **sqlCacheDependency** | 선택적 요소입니다. ASP.NET 응용 프로그램에 대 한 SQL 캐시 종속성을 구성합니다. |

### <a name="the-ltcachegt-element"></a>합니다 &lt;캐시&gt; 요소

다음 특성에서 사용할 수는 &lt;캐시&gt; 요소:

| **특성** | **설명** |
| --- | --- |
| **disableMemoryCollection** | 선택적 **부울** 특성입니다. 컴퓨터의 메모리가 부족할 때 발생 하는 캐시 메모리 수집이 비활성화 되었는지 여부를 나타내는 값을 가져오거나 설정 합니다. |
| **disableExpiration** | 선택적 **부울** 특성입니다. 캐시 만료가 비활성화 되었는지 여부를 나타내는 값을 가져오거나 설정 합니다. 를 사용할 수 없을 때 캐시 된 항목이 만료 되지 않습니다 및 만료 된 캐시 항목의 백그라운드 청소 발생 하지 않습니다. |
| **privateBytesLimit** | 선택적 **Int64** 특성입니다. 메모리를 회수 하는 동안 만료 된 항목을 캐시 플러시를 시작 하기 전에 응용 프로그램의 전용 바이트의 최대 크기를 나타내는 값을 가져오거나 설정 합니다. 이 제한으로 캐시에서 사용 되는 메모리 오버 헤드를 실행 중인 응용 프로그램에서에서 일반적인 메모리를 포함 합니다. 0으로 설정 ASP.NET를 메모리를 회수를 시작 하는 시기를 결정 하기 위한 자체 추론을 사용 함을 나타냅니다. |
| **percentagePhysicalMemoryUsedLimit** | 선택적 **Int32** 특성입니다. 캐시도 사용 하는 두 메모리를 포함 하는 메모리 사용이 메모리를 회수 하는 동안 만료 된 항목을 캐시 플러시를 시작 하기 전에 응용 프로그램에서 사용할 수 있는 컴퓨터의 실제 메모리의 최대 비율을 나타내는 값을 가져오거나 설정 합니다. 실행 중인 응용 프로그램의 일반 메모리 사용량입니다. 0으로 설정 ASP.NET를 메모리를 회수를 시작 하는 시기를 결정 하기 위한 자체 추론을 사용 함을 나타냅니다. |
| **privateBytesPollTime** | 선택적 **TimeSpan** 특성입니다. 응용 프로그램의 전용 바이트 메모리 사용량에 대 한 폴링 간의 시간 간격을 나타내는 값을 가져오거나 설정 합니다. |

### <a name="the-ltoutputcachegt-element"></a>합니다 &lt;outputCache&gt; 요소

다음 특성은 사용할 수는 &lt;outputCache&gt; 요소입니다.


|       <strong>특성</strong>        |                                                                                                                                                                                                                                                       <strong>설명</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>enableOutputCache</strong>    |                                                                                                                                                          선택적 <strong>부울</strong> 특성입니다. 페이지 출력 캐시를 사용 하거나 사용 하지 않습니다. 사용 하지 않으면 페이지가 없는 프로그래밍 방식으로 또는 선언적 설정과 관계 없이 캐시 됩니다. 기본값은 <strong>true</strong>합니다.                                                                                                                                                           |
|  <strong>enableFragmentCache</strong>   |                                                선택적 <strong>부울</strong> 특성입니다. 응용 프로그램 부분 캐시를 사용 하거나 사용 하지 않습니다. 페이지가 없습니다에 관계 없이 캐시는 사용 하지 않으면 합니다 [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) 지시문 또는 사용 하는 프로필을 캐시 합니다. 브라우저 클라이언트 뿐만 아니라 업스트림 프록시 서버 캐시 페이지 출력 하지 말아야 나타내는 캐시 제어 헤더를 포함 합니다. 기본값은 <strong>false</strong>합니다.                                                 |
| <strong>sendCacheControlHeader</strong> |                                                                                                                                                      선택적 <strong>부울</strong> 특성입니다. 나타내는 값을 가져오거나 여부는 <strong>캐시-control: private</strong> 헤더는 기본적으로 출력 캐시 모듈에 의해 전송 됩니다. 기본값은 <strong>false</strong>합니다.                                                                                                                                                      |
|      <strong>omitVaryStar</strong>      | 선택적 <strong>부울</strong> 특성입니다. Http 전송 사용 가능/불가능 "<strong>달라질 수 있습니다: \</s o n ><em>" 헤더를 응답 합니다. False로 기본값을 사용 하 여는 "</em>* 달라질 수 있습니다: \* <strong>" 출력 캐시 된 페이지에 대 한 헤더를 보냅니다. Vary 헤더를 보낼 때 수 있도록 다양 한 버전을 캐시할 Vary 헤더에 지정 된 내용에 따라 합니다. 예를 들어 <em>달라질 수 있습니다: 사용자-에이전트</em> 요청을 실행 한 사용자 에이전트에 따라 페이지의 다른 버전을 저장 합니다. 기본값은 * * false</strong>합니다. |

### <a name="the-ltoutputcachesettingsgt-element"></a>합니다 &lt;outputCacheSettings&gt; 요소

합니다 &lt;outputCacheSettings&gt; 요소 앞에서 설명한 대로 캐시 프로필을 만들 수 있도록 합니다. 유일한 자식 요소를 &lt;outputCacheSettings&gt; 요소는를 &lt;outputCacheProfiles&gt; 캐시 프로필을 구성 하는 것에 대 한 요소입니다.

### <a name="the-ltsqlcachedependencygt-element"></a>합니다 &lt;sqlCacheDependency&gt; 요소

다음 특성은 사용할 수는 &lt;sqlCacheDependency&gt; 요소입니다.

| **특성** | **설명** |
| --- | --- |
| **enabled** | 필요한 **부울** 특성입니다. 변경 내용에 대 한 폴링 하는지 여부를 나타냅니다. |
| **pollTime** | 선택적 **Int32** 특성입니다. SqlCacheDependency 있는 변경 내용에 대 한 데이터베이스 테이블을 폴링하는 빈도 설정 합니다. 이 값은 연속적인 폴링 간격 (밀리초)의 수에 해당합니다. 500 개 미만의 시간 (밀리초)을 설정할 수 없습니다. 기본값은 1 분입니다. |

### <a name="more-information"></a>추가 정보

알아야의 캐시 구성에 대 한 추가 정보가 있습니다.

- 작업자 프로세스 전용 바이트 제한이 설정 되어 있지 않으면 캐시는 다음과 같은 제한이 중 하나를 사용 됩니다. 

    - x86 2 GB: 800 MB 또는 실제 RAM의 60% 더 작은
    - x86 3 GB: 1800 MB 또는 실제 RAM의 60% 더 작은
    - 64: 1 테라바이트 또는 실제 RAM의 60% 더 작은
- 두 작업자 프로세스 전용 바이트 제한 하 고 &lt;privateBytesLimit 캐시 /&gt; 캐시는 두 개를 사용 하 여 설정 됩니다.
- 마찬가지로 1.x에서 캐시 항목을 삭제 하 고 GC를 호출 합니다. 두 가지 이유로 수집 합니다. 

    - 전용 바이트 제한에 가까워 진 매우는
    - 사용 가능한 메모리가 10% 보다 작거나 거의
- 효과적으로 trim을 사용 하지 않도록 설정 하 고 설정 하 여 사용 가능한 메모리가 부족 조건에 대 한 캐시 수 &lt;percentagePhysicalMemoryUseLimit 캐시 /&gt; 100입니다.
- 1.x와 달리 2.0에서 일시 중단 trim 및 수집 호출을 마지막 GC 합니다. 수집 전용 바이트 또는 메모리 제한 (캐시)의 1%를 초과 하 여 관리 되는 힙 크기는 줄어들지 않습니다 않았습니다.

## <a name="lab1-custom-cache-dependencies"></a>Lab1: 사용자 지정 캐시 종속성

1. 새 웹 사이트를 만듭니다.
2. Cache.xml 이라는 새 XML 파일을 추가 하 고 웹 응용 프로그램의 루트에 저장 합니다.
3. 페이지에 다음 코드를 추가\_default.aspx의 코드 숨김의 메서드를 로드 합니다. 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. 소스 뷰에서 default.aspx의 맨 위에 다음을 추가 합니다. 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. Default.aspx를 찾습니다. 에 않다고 하는 무엇입니까?
6. 브라우저를 새로 고칩니다. 에 않다고 하는 무엇입니까?
7. Cache.xml를 열고 다음 코드를 추가 합니다. 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. Cache.xml를 저장 합니다.
9. 브라우저를 새로 고칩니다. 에 않다고 하는 무엇입니까?
10. 이전에 캐시 된 값을 표시 하는 대신 시간을 업데이트 하는 이유를 설명 합니다.

## <a name="lab-2-using-polling-based-cache-dependencies"></a>랩 2:를 사용 하 여 폴링 기반 캐시 종속성

이 랩에서 GridView 및 DetailsView 컨트롤을 통해 Northwind 데이터베이스의에서 데이터를 편집할 수 있는 이전 모듈에서 만든 프로젝트를 사용 합니다.

1. Visual Studio 2005에서 프로젝트를 엽니다.
2. Aspnet 실행\_Products 테이블 및 데이터베이스를 사용 하도록 설정 하려면 Northwind 데이터베이스에 대해 regsql 유틸리티입니다. Visual Studio 명령 프롬프트에서 다음 명령을 사용 합니다. 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. Web.config 파일에 다음을 추가 합니다. 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. 새 webform showdata.aspx 호출을 추가 합니다.
5. @ Outputcache 지시문 다음 showdata.aspx 페이지에 추가 합니다. 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. 페이지에 다음 코드를 추가\_showdata.aspx 로드 합니다. 

    [!code-html[Main](caching/samples/sample21.html)]
7. Showdata.aspx 새 SqlDataSource 컨트롤을 추가 하 고 Northwind 데이터베이스 연결을 사용 하도록 구성 합니다. 다음을 클릭 합니다.
8. ProductID 및 ProductName 확인란을 선택 하 고 클릭 합니다.
9. 마침을 클릭 합니다.
10. 새로운 GridView showdata.aspx 페이지에 추가 합니다.
11. SqlDataSource1 드롭다운 목록에서 선택 합니다.
12. 저장 하 고 showdata.aspx를 찾습니다. 표시 된 시간을 기록해 둡니다.
