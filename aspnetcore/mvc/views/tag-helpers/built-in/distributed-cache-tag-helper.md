---
title: ASP.NET Core의 분산 캐시 태그 도우미
author: pkellner
description: 캐시 태그 도우미 사용 방법 소개
ms.author: riande
ms.date: 02/14/2017
uid: mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper
ms.openlocfilehash: d33c22802030eb9bc77baa64b83c9bbd7e902195
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36275177"
---
# <a name="distributed-cache-tag-helper-in-aspnet-core"></a>ASP.NET Core의 분산 캐시 태그 도우미

작성자: [Peter Kellner](http://peterkellner.net) 

분산 캐시 태그 도우미는 콘텐츠를 분산 캐시 원본에 캐싱하여 ASP.NET Core 앱 성능을 획기적으로 개선하는 기능을 제공합니다.

분산 캐시 태그 도우미는 캐시 태그 도우미와 동일한 기본 클래스에서 상속합니다. 캐시 태그 도우미와 연결된 모든 특성은 분산 태그 도우미에서도 작동합니다.

분산 캐시 태그 도우미는 **생성자 주입**이라고도 하는 **명시적 종속성 원칙**을 따릅니다. 특히 `IDistributedCache` 인터페이스 컨테이너는 분산 캐시 태그 도우미의 생성자에 전달됩니다. `IDistributedCache`의 구체적인 구현이 `ConfigureServices`에 생성되지 않은 경우(주로 startup.cs에서 발견됨) 분산 캐시 태그 도우미는 동일한 메모리 내 공급자를 사용하여 캐시된 데이터를 기본 캐시 태그 도우미로 저장합니다.

## <a name="distributed-cache-tag-helper-attributes"></a>분산 캐시 태그 도우미 특성

- - -

### <a name="enabled-expires-on-expires-after-expires-sliding-vary-by-header-vary-by-query-vary-by-route-vary-by-cookie-vary-by-user-vary-by-priority"></a>설정된 expires-on expires-after expires-sliding vary-by-header vary-by-query vary-by-route vary-by-cookie vary-by-user vary-by priority

정의는 캐시 태그 도우미를 참조하세요. 분산 캐시 태그 도우미는 캐시 태그 도우미와 동일한 클래스에서 상속하므로 이 모든 특성이 캐시 태그 도우미에서 공통입니다.

- - -

### <a name="name-required"></a>이름(필수)

| 특성 유형    | 예제 값     |
|----------------   |----------------   |
| string    | "my-distributed-cache-unique-key-101"     |

필수 `name` 특성은 분산 캐시 태그 도우미의 각 인스턴스에 대해 저장된 캐시의 키로 사용됩니다. razor 페이지의 Razor 페이지 이름 및 태그 도우미 위치를 기준으로 각 캐시 태그 도우미 인스턴스에 키를 할당하는 기본 캐시 태그 도우미와는 달리, 분산 캐시 태그 도우미는 `name` 특성의 키만을 기준으로 합니다.

사용 예제:

```cshtml
<distributed-cache name="my-distributed-cache-unique-key-101">
    Time Inside Cache Tag Helper: @DateTime.Now
</distributed-cache>
```

## <a name="distributed-cache-tag-helper-idistributedcache-implementations"></a>분산 캐시 태그 도우미 IDistributedCache 구현

ASP.NET Core에 두 가지 `IDistributedCache` 구현이 기본적으로 제공됩니다. 하나는 SQL Server 기반이고 다른 하나는 Redis 기반입니다. 이러한 구현의 세부 정보는 <xref:performance/caching/distributed>에서 찾을 수 있습니다. 두 구현 모두 ASP.NET Core의 *Startup.cs*에서 `IDistributedCache` 인스턴스를 설정해야 합니다.

특정 `IDistributedCache` 구현 사용과 특별히 관련된 태그 특성은 없습니다.

## <a name="additional-resources"></a>추가 자료

* <xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper>
* <xref:fundamentals/dependency-injection#service-lifetimes-and-registration-options>
* <xref:performance/caching/distributed>
* <xref:performance/caching/memory>
* <xref:security/authentication/identity>
