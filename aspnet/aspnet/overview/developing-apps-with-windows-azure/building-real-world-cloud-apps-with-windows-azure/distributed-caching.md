---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: 분산 캐싱 (Azure로 응용 프로그램 빌딩 실제 클라우드) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드로 응용 프로그램 빌딩 Azure 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴 및 그을 수 있는 방법에 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/20/2015
ms.topic: article
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: 3600200f9bb705ccf66c859547668bdf8e89d97a
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>분산 캐싱 (실제 클라우드로 응용 프로그램 빌딩 Azure)
====================
여 [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **실제 세계 클라우드로 응용 프로그램 빌딩 Azure** 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴에 설명 하 고 사례 수 있는 클라우드에 대 한 웹 앱을 개발 성공적으로 수행 되어야 합니다. 전자책에 대 한 정보를 참조 하십시오. [첫 번째 장](introduction.md)합니다.


이전 장 일시적인 오류 처리에 검토 하 고 캐싱 회로 차단기 전략으로 언급 합니다. 이 장에서 캐싱, 하는 방법에 대 한 자세한 배경을 알고 싶으면이를 사용 하기 위한 일반적인 패턴을 사용 하는 경우를 포함 하 고 Azure에서 구현 하는 방법입니다.

## <a name="what-is-distributed-caching"></a>분산 캐싱는 기능

캐시는 메모리에 데이터를 저장 하 여 높은 처리량, 낮은 대기 시간 자주 사용 되는 응용 프로그램 데이터에 대 한 액세스를 제공 합니다. 클라우드 앱에 대 한 가장 유용한 유형의 캐시는 개별 웹 서버의 메모리에 있지만 다른 클라우드 리소스에는 데이터는 저장 되지 않으며 캐시 된 데이터를 제공할 모든 응용 프로그램의 웹 서버에 분산된 캐시 (또는 해당 ar Vm 클라우드 다른 e 응용 프로그램에서 사용)입니다.

![같은 캐시 서버에 액세스 하는 여러 웹 서버를 보여 주는 다이어그램](distributed-caching/_static/image1.png)

추가 하거나 서버를 제거 하 여 응용 프로그램의 확장성 또는 서버 업그레이드 또는 결함으로 인해 바꾸면 캐시 된 데이터는 응용 프로그램을 실행 하는 모든 서버에 액세스할 수 있는 상태로 유지 됩니다.

영구 데이터 저장소의 대기 시간이 긴 데이터 액세스를 방지 하 여 캐싱 크게 향상 시킬 수 응용 프로그램의 응답성. 예를 들어, 캐시에서 데이터를 검색 하는 관계형 데이터베이스에서 검색할 때 보다 훨씬 빠릅니다.

캐싱 경우의 부수적인 혜택 감소 데이터 유출을 경우 비용 절감에 발생할 수 있습니다.은 영구 데이터 저장소에 대 한 트래픽을 영구 데이터 저장소에 대 한 요금이 청구 합니다.

## <a name="when-to-use-distributed-caching"></a>분산 캐시를 사용 하는 경우

캐싱 동작을의 데이터를 쓰는 것 보다 더 많은 읽기를 수행 하 고 데이터 모델은 캐시에 데이터 저장 및 검색을 사용 하는 키/값 조직을 지원 하는 경우 응용 프로그램 작업 부하에 가장 적합 합니다. 것도 더 유용 하 게 응용 프로그램 사용자가 많은 일반적인 데이터; 공유 하는 경우 예를 들어 캐시는 각 사용자 일반적으로 해당 사용자에 게 고유 데이터를 검색 하는 경우 많은 이점을 제공 하지 않습니다. 캐시 될 수 있는 유익함 예는 데이터가 자주 변경 되지 않는 모든 고객이 동일한 데이터에서 원하는 하기 때문에 제품 카탈로그입니다.

Caching의 이점은 수 점점 더 측정 가능한 더는 응용 프로그램의 확장성, 처리량 제한 및 영구 데이터 저장소의 대기 시간이 지연 될 전반적인 응용 프로그램 성능에 대 한 제한을 중 있습니다. 그러나 다른 이유로 성능이 보다 캐싱 구현할 수 있습니다. 사용자에 게 표시 될 때 완벽 하 게 최신 상태가 될 필요가 없는 데이터에 대 한 캐시 액세스 영구 데이터 저장소는 응답 하지 않거나 사용할 수 없는 경우에 대 한 회로 차단기 될 수 있습니다.

## <a name="popular-cache-population-strategies"></a>인기 있는 캐시 채우기 전략

캐시에서 데이터를 검색할 수 있도록 저장 있습니다 먼저 해야 합니다. 캐시에 필요한 데이터를 가져오기 위한 하는 방법은 여러 가지가 있습니다.

- 필요에 따라 / Aside 캐시

    응용 프로그램 캐시에서 데이터를 검색 하려고 시도 하 고 캐시 데이터 ("누락")가 응용 프로그램 데이터가 저장 캐시에 사용할 수 있습니다 다음에 있도록 합니다. 응용 프로그램이 동일한 데이터를을 가져오려고 하면 다음에 찾을 대상을 대 한 캐시 ("적중")에서 찾습니다. 데이터베이스에서 변경 된 캐시 된 데이터를 페치를 방지 하려면 데이터 저장소에 변경할 때 캐시를 무효화 합니다.
- 배경 데이터 푸시

    백그라운드 서비스 데이터를 푸시 캐시는 정기적으로 및 응용 프로그램에 항상 끌어오는 소스 캐시에서 합니다. 이 접근 방식을 works 좋은 항상 있습니다 요구 하지 않는 높은 대기 시간 데이터 원본과 최신 데이터를 반환 합니다.
- 회로 차단기

    일반적으로 응용 프로그램은 영구 데이터 저장소와 직접 통신 하 하지만 응용 프로그램은 영구 데이터 저장소에 가용성 문제가 있는 경우 캐시에서 데이터를 검색 합니다. 데이터가 캐시를 따로 또는 백그라운드 데이터 밀어넣기 전략을 사용 하 여 캐시에 노출 될 수 있습니다. 이 성능 향상 전략 보다는 전략을 처리 하는 오류입니다.

현재 캐시에 데이터 유지를 위해 응용 프로그램 업데이트를 만들거나 데이터를 삭제 하는 경우 관련 된 캐시 항목을 삭제할 수 있습니다. 인 경우 네 약간 오래 된 데이터를 가져올 경우에 따라 응용 프로그램에 대 한 오래 된 캐시 데이터를 수에 대 한 제한을 설정 하려면 구성 가능한 만료 시간에 사용할 수 있습니다.

절대 만료 (양의 캐시 항목이 생성 된 이후 경과 시간) 또는 상대 만료 (마지막으로 캐시 항목 액세스 한 이후에 시간의 양)을 구성할 수 있습니다. 절대 만료 너무 부실에서 데이터를 방지 하기 위해 캐시 만료 메커니즘에 좌우 되는 경우에 사용 됩니다. 수정 응용 프로그램에서 오래 된 캐시 항목을 수동으로 제거할 수 있습니다 및 캐시에 최신 데이터를 보존 하도록 이면 슬라이딩 만료가 사용 합니다. 선택한 만료 정책에 관계 없이 캐시 캐시의 메모리 제한에 도달 하면 가장 오래 된 (가장 최근에 사용한 또는 LRU) 항목을 제거 자동으로 됩니다.

## <a name="sample-cache-aside-code-for-fix-it-app"></a>수정 응용 프로그램에 대 한 캐시 배제 코드 샘플

다음 샘플 코드에서에서는 캐시를 먼저 확인 수정 작업을 검색할 때. 작업은 캐시에서 발견 되 면 하는 경우, 반환 이 파일이 없으면 데이터베이스에서 가져오기 하 고 캐시에 저장 합니다. 변경 내용은에 캐싱을 추가 하려면는 `FindTaskByIdAsync` 메서드 강조 표시 됩니다.

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

수정 작업을 삭제 하거나 업데이트할 때 캐시 된 (제거) 작업을 무효화할 해야 합니다. 그렇지 않으면 이후 캐시에서 오래 된 데이터를 가져오려면 해당 작업은 계속 읽으려고 시도 합니다.

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

다음은 간단한 캐싱 코드; 설명 하기 위해 샘플 다운로드 가능한 수정 프로젝트에 캐싱을 구현 되지 않았습니다.

## <a name="azure-caching-services"></a>Azure caching 서비스

Azure는 다음과 같은 캐싱 서비스 제공: [Azure Redis Cache](https://msdn.microsoft.com/library/dn690523.aspx) 및 [Azure 관리 캐시](https://msdn.microsoft.com/library/dn386094.aspx)합니다. Azure Redis 캐시는 인기 있는에 따라 [오픈 소스 Redis 캐시](http://redis.io/) 및 시나리오 캐싱 대부분에 대 한 첫 번째 선택 합니다.

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>ASP.NET 세션 상태 캐시 공급자를 사용 하 여

설명한 것 처럼는 [웹 개발 모범 사례 장](web-development-best-practices.md), 세션 상태를 사용 하지 않도록 하는 것이 좋습니다. 응용 프로그램 세션 상태를 해야 하는 경우에 다음 모범 사례 (웹 서버의 여러 인스턴스)에 확장을 사용 하도록 설정 하지 않습니다는 있으므로 기본 메모리 내 공급자를 사용 하지 않는 것입니다. 세션 상태를 사용 하는 여러 웹 서버에서 실행 되는 사이트를 사용 하는 SQL Server ASP.NET 세션 상태 공급자 있지만 메모리 내 공급자에 비해 높은 대기 시간이 비용을 발생 시킵니다. 와 같은 캐시 공급자를 사용 하는 세션 상태를 사용 해야 할 경우 가장 적합 한 솔루션의 [Azure 캐시용 세션 상태 공급자](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx)합니다.

## <a name="summary"></a>요약

캐싱 응용 프로그램에서 계속 해 서 데이터베이스를 사용할 수 없는 경우 읽기 작업에 대해 응답할 수 있도록 및 응답 시간 및 확장성을 개선 하기 위해 수정 앱 수 구현 방법을 살펴보았습니다. 에 [다음 장에서](queue-centric-work-pattern.md) 더욱 확장성이 개선 하 고 앱 계속 쓰기 작업에 대해 응답할 수 있도록 하는 방법을 보여줍니다.

## <a name="resources"></a>자료

캐싱에 대 한 자세한 내용은 다음 리소스를 참조 합니다.

설명서

- [Azure 캐시](https://msdn.microsoft.com/library/gg278356.aspx)합니다. Azure의 캐싱에 대 공식 MSDN 설명서입니다.
- [Microsoft Patterns and Practices-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx)합니다. 캐싱 지침 및 캐시 배제 패턴을 참조 하십시오.
- [Failsafe: 복원 력 있는 클라우드 아키텍처에 대 한 지침](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)합니다. 백서: Marc Mercuri, Ulrich Homann 및 Andrew Townhill 합니다. Caching에서 섹션을 참조 하십시오.
- [Azure 클라우드 서비스에서 대규모 서비스를 디자인에 대 한 유용한](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)합니다. W. 백서: Mark Simms 및 Michael Thomassy 합니다. 분산 캐싱 섹션을 참조 하십시오.
- [배포 확장성에 대 한 경로 대 한 캐싱을](https://msdn.microsoft.com/magazine/dd942840.aspx)합니다. 이전 버전 (2009) MSDN Magazine 문서 하지만 분산 캐싱 일반적;에 대 한 명확 하 게 작성 된 소개 FailSafe 및 모범 사례 백서의 캐싱 섹션 보다 좀 더 깊이에 저장합니다.

비디오

- [FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms 하 여 시리즈를 9 개 부분으로 구성 합니다. 클라우드 응용 프로그램을 설계 하는 방법의 400 수준 보기를 표시 합니다. 이 시리즈 이론 중점적으로 다루며 이유; 자세히 사용 방법에 대 한 Mark Simms 하 여 큰 문서를 참조 합니다. 1시 24분: 14에서 시작 하는 3 에피소드 캐싱 설명을 참조 하십시오.
- [건물 큰:-1 부 Azure 고객 으로부터 얻은](https://channel9.msdn.com/Events/Build/2012/3-029)합니다. Simon Davies 46:00에서 분산 캐싱 시작을 설명 합니다. 유사 Failsafe 시리즈 하지만 방법 더 세부적으로 이동 합니다. 프레젠테이션의는 2013에 도입 된 Azure 앱 서비스의 웹 응용 프로그램의 캐싱 서비스를 포함 하지 않을 하므로 2012 년 10 월 31 일이 지정 되었습니다.

코드 샘플

- [클라우드 서비스 기본 사항 Azure에서](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)합니다. 분산 캐시를 구현 하는 샘플 응용 프로그램 관련 블로그 게시물을 참조 [클라우드 서비스 기본 사항 – 기본 사항 캐싱](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx)합니다.

> [!div class="step-by-step"]
> [이전](transient-fault-handling.md)
> [다음](queue-centric-work-pattern.md)
