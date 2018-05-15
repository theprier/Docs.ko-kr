---
title: ASP.NET Core에서 분산 캐시 사용하기
author: ardalis
description: 특히 클라우드나 서버 팜 환경에서 ASP.NET Core의 분산 캐시를 사용하여 응용 프로그램의 성능 및 확장성을 개선하는 방법을 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 02/14/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: performance/caching/distributed
ms.openlocfilehash: d9c7c1c3b2c052ba11f9ea5eaaa424d69bc43eb2
ms.sourcegitcommit: 48beecfe749ddac52bc79aa3eb246a2dcdaa1862
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="work-with-a-distributed-cache-in-aspnet-core"></a>ASP.NET Core에서 분산 캐시 사용하기

작성자: [Steve Smith](https://ardalis.com/)

분산 캐시는 ASP.NET Core 응용 프로그램이 특히 클라우드나 서버 팜 환경에서 호스팅될 때 성능 및 확장성을 개선할 수 있습니다. 이 문서에서는 ASP.NET Core가 기본으로 제공하는 분산 캐시 추상화 및 구현의 사용 방법을 설명합니다.

[예제 코드 살펴보기 및 다운로드](https://github.com/aspnet/Docs/tree/master/aspnetcore/performance/caching/distributed/sample) ([다운로드 방법](xref:tutorials/index#how-to-download-a-sample))

## <a name="what-is-a-distributed-cache"></a>분산 캐시란

분산 캐시는 여러 응용 프로그램 서버에서 공유됩니다([캐시 기본 사항](memory.md#caching-basics) 참조). 캐시에 저장된 정보는 개별 웹 서버의 메모리에 저장되지 않으며, 캐시된 데이터는 모든 응용 프로그램의 서버에 사용할 수 있습니다. 이는 몇 가지 이점을 제공합니다.

1. 캐시된 데이터가 모든 웹 서버에서 일관적입니다. 어떤 서버가 사용자의 요청을 처리하는지에 따라 다른 결과를 표시하거나 하지 않습니다.

2. 캐시된 데이터는 웹 서버가 재시작되거나 배포된 후에도 유지됩니다. 캐시에 영향을 주지 않고 개별 웹 서버를 제거하거나 추가할 수 있습니다.

3. 원본 데이터 저장소에 대한 요청 회수가 줄어듭니다(다수의 메모리 내 캐시를 사용하거나 캐시를 전혀 사용하지 않는 경우 보다).

> [!NOTE]
> SQL Server 분산 캐시를 사용하는 경우 이런 장점 중 일부는 응용 프로그램의 원본 데이터와 다른 캐시 전용 데이터베이스 인스턴스를 사용하는 경우에만 적용됩니다.

다른 모든 캐시와 마찬가지로, 대부분 관계형 데이터베이스(또는 웹 서비스)에서 조회하는 것보다 캐시에서 데이터를 훨씬 빠르게 조회할 수 있기 때문에 분산 캐시도 응용 프로그램의 응답성을 획기적으로 향상시킵니다.

캐시 구성은 구현에 따라 다릅니다. 이 문서에서는 Redis 및 SQL Server 분산 캐시를 구성하는 두 가지 방법을 모두 설명합니다. 어떤 구현을 선택하던지 응용 프로그램은 공통 `IDistributedCache` 인터페이스를 사용해서 캐시와 상호 작용합니다.

## <a name="the-idistributedcache-interface"></a>IDistributedCache 인터페이스

`IDistributedCache` 인터페이스는 동기 및 비동기 메서드를 포함하고 있습니다. 이 인터페이스를 사용하면 분산 캐시 구현에 항목을 추가하고, 검색하고, 제거할 수 있습니다. `IDistributedCache` 인터페이스는 다음과 같은 메서드를 포함하고 있습니다.

**Get, GetAsync**

문자열 키를 전달받아서 캐시에 항목이 존재할 경우 `byte[]`로 캐시 항목을 조회합니다.

**Set, SetAsync**

문자열 키를 사용해서 (`byte[]`로) 캐시에 항목을 추가합니다.

**Refresh, RefreshAsync**

키를 기반으로 캐시 항목을 새로 고치고, 캐시 항목의 슬라이딩 만료 시간 제한을 재설정합니다(필요한 경우).

**Remove, RemoveAsync**

키를 기반으로 캐시 항목을 제거합니다.

`IDistributedCache` 인터페이스를 사용하려면:

   1. 프로젝트 파일에 필요한 NuGet 패키지를 추가합니다.

   2. `Startup` 클래스의 `ConfigureServices` 메서드에서 `IDistributedCache`의 특정 구현을 구성하고 컨테이너에 추가합니다.

   3. 응용 프로그램의 [미들웨어](xref:fundamentals/middleware/index)나 MVC 컨트롤러 클래스의 생성자에서 `IDistributedCache`의 인스턴스를 요청합니다. 인스턴스는 [종속성 주입](../../fundamentals/dependency-injection.md)(DI)을 통해서 제공됩니다.

> [!NOTE]
> `IDistributedCache` 인스턴스를 Singleton이나 Scoped 수명으로 사용할 필요는 없습니다(적어도 기본 구현일 경우). 필요할 때마다 인스턴스를 생성할 수도 있지만([종속성 주입](../../fundamentals/dependency-injection.md)을 사용하는 대신), 그럴 경우 코드를 테스트하기가 어려워지고 [명시적 종속성 원칙](http://deviq.com/explicit-dependencies-principle/)을 위반하게 됩니다.

다음 예제는 간단한 미들웨어 구성 요소에서 `IDistributedCache`의 인스턴스를 사용하는 방법을 보여줍니다.

[!code-csharp[](./distributed/sample/src/DistCacheSample/StartTimeHeader.cs?highlight=15,18,21,27,28,29,30,31)]

위의 코드는 캐시된 값을 읽기만 하고 작성하지는 않습니다. 이 예제에서 값은 오직 서버가 시작될 때만 설정하고 변경되지 않습니다. 다중 서버 시나리오에서는 가장 최근에 시작된 서버가 다른 서버에 의해 설정된 기존의 모든 값을 덮어쓰게 됩니다. 그리고 `Get` 및 `Set` 메서드는 `byte[]` 형식을 사용합니다. 따라서 문자열 값은 `Encoding.UTF8.GetString`(`Get`을 사용할 때) 또는 `Encoding.UTF8.GetBytes`(`Set`을 사용할 때)를 사용해서 변환해야 합니다.

다음 코드는 *Startup.cs*에서 값이 설정되고 있는 부분을 보여줍니다.

[!code-csharp[](./distributed/sample/src/DistCacheSample/Startup.cs?highlight=2,4,5,6&range=58-66)]

> [!NOTE]
> `ConfigureServices` 메서드에서 `IDistributedCache`가 구성되고 나면 이를 `Configure` 메서드의 매개 변수로 전달할 수 있습니다. 이렇게 매개 변수로 추가하면 DI를 통해서 구성된 인스턴스가 제공됩니다.

## <a name="using-a-redis-distributed-cache"></a>Redis 분산 캐시 사용하기

[Redis](https://redis.io/)는 분산 캐시로 흔히 사용되는 오픈 소스 메모리 내 데이터 저장소입니다. 로컬에서 사용할 수도 있고 Azure에서 호스팅되는 응용 프로그램에 대한 [Azure Redis Cache](https://azure.microsoft.com/services/cache/)를 구성할 수도 있습니다. ASP.NET Core 응용 프로그램은 `RedisDistributedCache`의 인스턴스를 사용해서 캐시 구현을 구성합니다.

`ConfigureServices`에서 Redis 구현을 구성한 다음 응용 프로그램 코드에서 `IDistributedCache`의 인스턴스를 요청하여 이에 접근합니다(위의 코드 참조).

예제 코드에서는 서버가 `Staging` 환경으로 구성될 때 `RedisCache` 구현이 사용됩니다. 따라서 `ConfigureStagingServices` 메서드에서 `RedisCache`를 구성합니다.

[!code-csharp[](./distributed/sample/src/DistCacheSample/Startup.cs?highlight=8,9,10,11,12,13&range=27-40)]

> [!NOTE]
> Redis를 로컬 컴퓨터에 설치하려면 chocolatey 패키지 [https://chocolatey.org/packages/redis-64/](https://chocolatey.org/packages/redis-64/)를 설치하고 명령 프롬프트에서 `redis-server`를 실행합니다.

## <a name="using-a-sql-server-distributed-cache"></a>SQL Server 분산 캐시 사용하기

SqlServerCache 구현을 사용하면 SQL Server 데이터베이스를 백업 저장소로 이용해서 분산 캐시를 사용할 수 있습니다. 지정한 이름 및 스키마로 테이블을 생성하는 도구인 sql-cache 도구를 이용해서 SQL Server 테이블을 생성할 수 있습니다.

sql-cache 캐시 도구를 사용하려면 *.csproj* 파일의 `<ItemGroup>` 요소에 `SqlConfig.Tools`를 추가하고 dotnet restore를 실행합니다.

[!code-xml[](./distributed/sample/src/DistCacheSample/DistCacheSample.csproj?range=23-25)]

다음 명령을 실행하면 SqlConfig.Tools를 테스트 할 수 있습니다.

```none
C:\DistCacheSample\src\DistCacheSample>dotnet sql-cache create --help
   ```

그러면 sql-cache 도구가 사용 방법, 옵션 및 명령 도움말을 출력하며, 이제 "sql-cache create" 명령을 실행하여 Sql Server에 테이블을 생성할 수 있습니다.

```none
C:\DistCacheSample\src\DistCacheSample>dotnet sql-cache create "Data Source=(localdb)\v11.0;Initial Catalog=DistCache;Integrated Security=True;" dbo TestCache
   info: Microsoft.Extensions.Caching.SqlConfig.Tools.Program[0]
       Table and index were created successfully.
   ```

생성된 테이블은 다음과 같은 스키마를 갖고 있습니다.

![SqlServer 캐시 테이블](distributed/_static/SqlServerCacheTable.png)

다른 모든 캐시 구현과 마찬가지로, 응용 프로그램은 `SqlServerCache`가 아니라 `IDistributedCache`의 인스턴스를 사용해서 캐시 값을 읽고 설정해야 합니다. 예제에서는 `Production` 환경에서 `SqlServerCache`를 구현하고 있습니다(그래서 `ConfigureProductionServices`에 설정되어 있습니다).

[!code-csharp[](./distributed/sample/src/DistCacheSample/Startup.cs?highlight=7,8,9,10,11,12&range=42-56)]

> [!NOTE]
> 일반적으로 `ConnectionString`은 (그리고 필요한 경우 `SchemaName` 및 `TableName`은) 자격 증명이 포함되어 있을 수도 있기 때문에 소스 제어 외부에 (UserSecrets 같은) 저장되어야 합니다.

## <a name="recommendations"></a>권장 사항

응용 프로그램에 적합한 `IDistributedCache`의 구현을 결정할 때는 기존 인프라와 환경, 성능 요구 사항 및 팀의 경험을 감안하여 Redis와 SQL Server 중 하나를 선택해야 합니다. Redis로 작업하는 것이 더 편안한 팀이라면 탁월한 선택입니다. 팀이 SQL Server를 선호한다면 해당 구현에도 확신을 가질 수 있습니다. 기존의 캐싱 솔루션은 데이터를 메모리 내에 저장하기 때문에 데이터를 빠르게 조회할 수 있다는 점에 주의하시기 바랍니다. 공통적으로 사용되는 데이터는 캐시에 저장하고 전체 데이터를 SQL Server 또는 Azure Storage 같은 백엔드 영구 저장소에 저장해야 합니다. Redis 캐시는 SQL 캐시와 비교하여 높은 처리량과 낮은 대기 시간을 제공하는 캐싱 솔루션입니다.

## <a name="additional-resources"></a>추가 자료

* [Azure Redis Cache](https://azure.microsoft.com/documentation/services/redis-cache/)
* [Azure SQL Database](https://azure.microsoft.com/documentation/services/sql-database/)
* [메모리 내 캐시](xref:performance/caching/memory)
* [변경 토큰을 이용해서 변경 감지하기](xref:fundamentals/primitives/change-tokens)
* [응답 캐싱](xref:performance/caching/response)
* [응답 캐싱 미들웨어](xref:performance/caching/middleware)
* [캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)
* [분산 캐시 태그 도우미](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)
