---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
title: 분산 캐싱 (실제 클라우드 앱 빌드 azure) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드 앱 빌드 Azure 전자책을 사용 하 여 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴과 그을 수 있는 방법을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 07/20/2015
ms.assetid: 406518e9-3817-49ce-8b90-e82bc461e2c0
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/distributed-caching
msc.type: authoredcontent
ms.openlocfilehash: a165c789ae656025934bc5e3ed8e8caef1c21787
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37821621"
---
<a name="distributed-caching-building-real-world-cloud-apps-with-azure"></a>분산 캐싱 (실제 클라우드 앱 빌드 Azure 사용 하 여)
====================
하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 합니다 **실제 세계 클라우드 앱 빌드 Azure** 전자책 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴 설명 하 고 도움이 될 수 있는 사례 성공적인 클라우드를 위한 웹 앱을 개발할 수 있습니다. 전자책에 대 한 정보를 참조 하세요 [첫 번째 장에서](introduction.md)합니다.


이전 장에서 일시적인 오류 처리를 살펴보고 하 고 회로 차단기 전략으로 캐시를 언급 합니다. 이 장에서 캐싱, 하는 방법에 대 한 자세한 배경 정보 사용에 대 한 일반적인 패턴 사용 하는 경우를 포함 하 여 Azure에서 구현 하는 방법입니다.

## <a name="what-is-distributed-caching"></a>분산 캐싱는 무엇입니까

캐시는 메모리에 데이터를 저장 하 여 높은 처리량, 자주 액세스 하는 응용 프로그램 데이터에 대 한 대기 시간이 짧은 액세스를 제공 합니다. 클라우드 앱에 대 한 가장 유용한 유형의 캐시는 데이터는 개별 웹 서버의 메모리에 있지만 다른 클라우드 리소스에 저장 되지 않으며 캐시 된 데이터에 사용할 수 있는 모든 응용 프로그램의 웹 서버는 분산된 캐시 (또는 다른 클라우드 Vm는 ar e 응용 프로그램에서 사용)입니다.

![동일한 캐시 서버에 액세스 하는 여러 웹 서버를 보여 주는 다이어그램](distributed-caching/_static/image1.png)

추가 하거나 서버를 제거 하 여 응용 프로그램의 확장성 때나 서버 업그레이드 또는 오류 인해 바뀝니다 때 캐시 된 데이터를 응용 프로그램을 실행 하는 모든 서버에 액세스할 수 있는 상태로 유지 됩니다.

영구 데이터 저장소의 높은 대기 시간 데이터 액세스를 방지 하 여 캐싱 크게 향상할 수 응용 프로그램 응답성. 예를 들어, 캐시에서 데이터를 검색 하는 관계형 데이터베이스에서 검색할 때 보다 훨씬 빠릅니다.

Caching의 부수적인 혜택 감소 영구 데이터 저장소에 대 한 요금이 청구 트래픽을 영구 데이터 저장소에 데이터 송신 경우 비용 절감 될 수 있습니다.

## <a name="when-to-use-distributed-caching"></a>분산 캐싱을 사용 하는 경우

캐싱 작동 데이터를 쓰는 것 보다 더 많은 읽기를 수행 하 고 데이터 모델 캐시에서 데이터 저장 및 검색을 사용 하는 키/값 조직을 지원 하는 경우 응용 프로그램 워크 로드에 가장 적합 합니다. 것도 유용한 응용 프로그램 사용자는 많은 일반적인 데이터를 공유 하는 경우 예를 들어 캐시는 각 사용자 일반적으로 해당 사용자에 게 고유한 데이터를 검색 하는 경우 많은 이점을 제공 하지 않습니다. 캐시 될 수 있는 매우 유용한 예로 제품 카탈로그를 이므로 데이터가 자주 변경 되지 않습니다 하 고 모든 고객에 게 동일한 데이터를 보고 합니다.

캐싱의 혜택 수 점점 측정 가능한 보다는 응용 프로그램의 확장성, 처리량 제한 및 영구 데이터 저장소의 대기 시간이 지연 될 전체 응용 프로그램 성능에 대 한 제한을 많이 있습니다. 그러나 다른 이유로 성능이 보다 캐싱을 구현할 수 있습니다. 사용자에 게 표시 될 때 완벽 하 게 최신 상태로 유지할 수 없는 데이터에 대 한 영구 데이터 저장소에 응답 하지 않거나 사용할 수 없는 경우 캐시 액세스에 대 한 회로 차단기를 사용할 수 있습니다.

## <a name="popular-cache-population-strategies"></a>인기 있는 캐시 채우기 전략

캐시에서 데이터를 검색할 수 있도록 저장할 수 있는 먼저 지정 해야 합니다. 캐시에 필요한 데이터를 가져오기 위한 몇 가지 전략을 가지 있습니다.

- 주문형 / Aside 캐시

    응용 프로그램이 캐시에서 데이터를 검색 하려고 하 고이 사용할 수 있도록 다음에 응용 프로그램의 캐시에 데이터를 저장 캐시 데이터 (한 "miss")가 없는 경우. 응용 프로그램에서 동일한 데이터를 가져오려고 다음에 무엇을 찾고 있는지 ("적중") 캐시에서 찾습니다. 데이터베이스에서 변경 된 캐시 된 데이터를 페치를 방지 하려면 데이터 저장소로 변경 하는 경우 캐시를 무효화 합니다.
- 백그라운드 데이터 푸시

    백그라운드 서비스 데이터를 푸시할 캐시는 정기적으로 응용 프로그램에 항상 풀 캐시에서. 이 방법은 작동 잘 항상 있습니다 필요 하지 않은 대기 시간이 긴 데이터 원본에는 최신 데이터를 반환 합니다.
- 회로 차단기

    응용 프로그램은 일반적으로 영구 데이터 저장소와 직접 통신 하지만 영구 데이터 저장소에 가용성 문제가 될 때 응용 프로그램이 캐시에서 데이터를 검색 합니다. 데이터 캐시를 따로 또는 백그라운드 데이터 푸시 전략 중 하나를 사용 하 여 캐시에 배치 된 될 수 있습니다. 성능 향상 전략 대신 전략을 처리 하는 오류입니다.

현재 캐시에 데이터 유지를 위해 응용 프로그램 생성, 업데이트, 또는 데이터를 삭제 하는 경우 관련 된 캐시 항목을 삭제할 수 있습니다. 인 경우 이제 약간 오래 된 데이터를 가져올 경우에 따라 응용 프로그램에 대 한 오래 된 캐시 데이터 수에 제한을 설정 하려면 구성 가능한 만료 시간을 사용할 수 있습니다.

절대 만료 (양의 캐시 항목을 만든 후 시간) 또는 상대 만료 (마지막으로 캐시 항목을 액세스 한 이후에 시간 간격)을 구성할 수 있습니다. 절대 만료를 데이터가 너무 부실 해지지 않도록 하는 캐시 만료 메커니즘에 좌우 되는 경우에 사용 됩니다. Fix It 앱에서 부실 캐시 항목을 수동으로 제거 됩니다 것을 상대 (sliding) 만료 사용 하 여 캐시의 최신 데이터를 유지 합니다. 선택 하면 만료 정책에 관계 없이 캐시 캐시의 메모리 제한에 도달 하면 가장 오래 된 (가장 최근에 사용한 또는 LRU) 항목을 제거 자동으로 됩니다.

## <a name="sample-cache-aside-code-for-fix-it-app"></a>Fix It 응용 프로그램에 대 한 캐시 배제 코드 샘플

다음 샘플 코드에서에서는 캐시를 먼저 확인 Fix It 작업을 검색 하는 경우. 작업 캐시에 있으면, 반환 찾을 수 없는 경우, 데이터베이스에서 가져와야 하 고 캐시에 저장 합니다. 변경에 캐싱을 추가 하려면를 `FindTaskByIdAsync` 메서드 강조 표시 됩니다.

[!code-csharp[Main](distributed-caching/samples/sample1.cs?highlight=5,9-11,13-15,19)]

Fix It 작업을 삭제 하거나 업데이트할 때 캐시 된 (제거) 작업을 무효화 해야 합니다. 이 고, 그렇지 미래 작업은 계속 해 서 이전 데이터를 캐시에서 읽기를 시도 합니다.

[!code-csharp[Main](distributed-caching/samples/sample2.cs?highlight=7)]

다음은 간단한 캐싱 코드를 보여 주기 위해 샘플 다운로드 가능한 Fix It 프로젝트의 캐싱을 구현 되지 않았습니다.

## <a name="azure-caching-services"></a>Azure caching 서비스

Azure는 다음과 같은 캐싱 서비스를 제공 합니다. [Azure Redis Cache](https://msdn.microsoft.com/library/dn690523.aspx) 및 [Azure 관리 된 캐시](https://msdn.microsoft.com/library/dn386094.aspx)합니다. Azure Redis cache는 기반으로 널리 사용 되 [오픈 소스 Redis Cache](http://redis.io/) 및 시나리오 캐싱 대부분에 대 한 첫 번째 선택 합니다.

<a id="sessionstate"></a>
## <a name="aspnet-session-state-using-a-cache-provider"></a>ASP.NET 세션 상태 캐시 공급자를 사용 하 여

에 설명 된 대로 합니다 [웹 개발 모범 사례 장](web-development-best-practices.md), 세션 상태를 사용 하지 않는 것이 좋습니다. 응용 프로그램 세션 상태에 필요한 다음 모범 사례 경우 확장 (웹 서버의 여러 인스턴스)를 사용 하도록 설정 하지는 때문에 기본 메모리 내 공급자를 방지 합니다. ASP.NET SQL Server 세션 상태 공급자를 세션 상태를 사용 하 여 여러 웹 서버에서 실행 되는 사이트를 사용 하도록 설정 하지만 메모리 내 공급자에 비해 높은 대기 시간 비용이 발생 합니다. 세션 상태를 사용 해야 할 경우 가장 좋은 것 같은 캐시 공급자를 사용 하는 [Azure 캐시용 세션 상태 제공자](https://msdn.microsoft.com/library/windowsazure/gg185668.aspx)합니다.

## <a name="summary"></a>요약

어떻게 Fix It 응용 프로그램 데이터베이스를 사용할 수 없는 경우 읽기 작업에 대 한 응답 수를 계속 하려면 앱을 사용 하도록 설정 하 고 응답 시간 및 확장성을 개선 하기 위해 캐싱을 구현할 수 살펴보았습니다. 에 [다음 장에서](queue-centric-work-pattern.md) 더 확장성을 향상 하 고 쓰기 작업에 대 한 응답을 계속 앱을 확인 하는 방법을 살펴보겠습니다.

## <a name="resources"></a>자료

캐싱에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

설명서

- [Azure 캐시](https://msdn.microsoft.com/library/gg278356.aspx)합니다. Azure의 캐싱에서 공식 MSDN 설명서입니다.
- [Microsoft Patterns and Practices-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx)합니다. 캐싱 지침과 캐시 배제 패턴을 참조 하세요.
- [Failsafe: 복원 력 있는 클라우드 아키텍처 지침](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)합니다. Marc Mercuri, Ulrich Homann 및 Andrew Townhill 백서입니다. Caching에서 섹션을 참조 합니다.
- [Azure Cloud Services에서 대규모 서비스 설계를 위한 모범 사례](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)합니다. W. Mark Simms 및 Michael Thomassy 백서입니다. 분산 캐싱 섹션을 참조 합니다.
- [분산 캐싱 확장성에 대 한 경로에서](https://msdn.microsoft.com/magazine/dd942840.aspx)합니다. 이전 버전 (2009) MSDN Magazine 기사 이지만 명확 하 게 작성 된 분산 캐싱 일반적; 소개 FailSafe 및 모범 사례 백서 캐싱 섹션 보다 더 심층적으로 이동합니다.

비디오

- [FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는 데](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms에서 9 부 시리즈입니다. 클라우드 앱을 설계 하는 방법의 400 수준 보기를 표시 합니다. 이 시리즈 이론에 집중 하 고 이유; 자세한 방법에 대 한 Mark Simms 하 여 빌드 큰 시리즈를 참조 합니다. 1시 24분: 14에서 시작 하는 에피소드 3 캐싱 설명을 참조 하세요.
- [빌드 큰: Azure 고객에 게-부에서 Lessons learned](https://channel9.msdn.com/Events/Build/2012/3-029)합니다. Simon Davies 분산 캐싱부터 46:00 설명 합니다. 비슷하지만 Failsafe 시리즈 자세한 방법 세부 정보로 이동 합니다. 프레젠테이션은 2013에 도입 된 Azure App Service에서 Web Apps의 캐싱 서비스를 다루지 않습니다 있도록 2012 년 10 월 31 일 제공 되었습니다.

코드 샘플

- [Azure에서 서비스 기본 사항 클라우드](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)합니다. 분산 캐싱을 구현 하는 샘플 응용 프로그램입니다. 함께 제공 되는 블로그 게시물을 참조 하세요 [클라우드 서비스 기본 사항 – 기본 캐싱](https://blogs.msdn.com/b/windowsazure/archive/2013/10/03/cloud-service-fundamentals-caching-basics.aspx)합니다.

> [!div class="step-by-step"]
> [이전](transient-fault-handling.md)
> [다음](queue-centric-work-pattern.md)
