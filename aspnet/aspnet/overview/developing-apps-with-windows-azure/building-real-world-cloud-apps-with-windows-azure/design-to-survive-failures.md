---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
title: "실패 (Azure로 응용 프로그램 빌딩 실제 클라우드)를 디자인 | Microsoft Docs"
author: MikeWasson
description: "실제 세계 클라우드로 응용 프로그램 빌딩 Azure 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴 및 그을 수 있는 방법에 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: 364ce84e-5af8-4e08-afc9-75a512b01f84
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
msc.type: authoredcontent
ms.openlocfilehash: a0ee790da07c99cdb1279a6bca637a4ce8076e84
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="design-to-survive-failures-building-real-world-cloud-apps-with-azure"></a>에 오류가 발생 했습니다 (Azure로 응용 프로그램 빌딩 실제 클라우드)에 동등한 존속 디자인
====================
여 [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **실제 세계 클라우드로 응용 프로그램 빌딩 Azure** 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴에 설명 하 고 사례 수 있는 클라우드에 대 한 웹 앱을 개발 성공적으로 수행 되어야 합니다. 전자책에 대 한 정보를 참조 하십시오. [첫 번째 장](introduction.md)합니다.


모든 종류의 응용 프로그램을 사용할 수 있지만 특히 있는 많은 사용자는 사용, 클라우드에서 실행 될를 작성 하는 경우에 대해 신경쓸 필요가 작업 중 하나는 오류 처리 고 가치를 제공 하는 계속 정상적으로 수 있도록 앱을 디자인 하는 방법으로 가능한 합니다. 충분 한 시간이 주어, 진행 상황 모든 환경 또는 모든 소프트웨어 시스템에서 잘못 된 이동입니다. 어떻게 화가 고객에 게는 표시 되며 시간 결정 앱 이러한 상황을 어떻게 처리 하는지 분석 하 고 문제 해결을 소비 해야 합니다.

## <a name="types-of-failures"></a>오류 유형

다르게 처리 하려고 할 수 있는 오류의 두 가지 기본 범주가 있습니다.

- 임시 자체 일시적인 네트워크 연결 문제와 같은 오류를 복구 합니다.
- 해결 해야 하는 원칙은 오랫동안 지속 실패 합니다.

일시적 오류에 대 한 해당 대부분의 응용 프로그램을 자동으로 복구 시간을 확인 하는 재시도 정책을 구현할 수 있습니다. 고객이 약간 더 긴 응답 시간을 알 수 있지만 그렇지 않은 경우 이러한 영향을 받지 않습니다. 이러한 오류를 처리 하는 몇 가지 보여 주 겠지만 [일시적인 오류 처리 장](transient-fault-handling.md)합니다.

오류 지속에 대 한 모니터링 및 로깅 신속 하 게 되 면 알려줍니다 문제가 발생 하 고 근본 원인 분석을 용이 하 게 하는 기능을 구현할 수 있습니다. 이러한 종류의 오류를 파악할 수 있도록 몇 가지 방법을 보여 주 겠지만 [모니터링 및 원격 분석 장](monitoring-and-telemetry.md)합니다.

## <a name="failure-scope"></a>오류 범위

있습니다 – 실패 범위에 대해 생각 하는 단일 컴퓨터에 영향을, SQL 데이터베이스 또는 저장소 또는 전체 영역 등의 전체 서비스입니다.

![오류 범위](design-to-survive-failures/_static/image1.png)

### <a name="machine-failures"></a>컴퓨터 오류

Azure에서 오류가 발생 한 서버는 자동으로 새 식으로 대체 하 고 자동으로 고 신속 하 게 잘 설계 된 클라우드 앱이이 종류의 오류에서 복구 합니다. 상태 비저장 웹 계층의 확장성 이점을 스트레스 우리는 이전 및 실패 한 서버에서 복구의 용이성은 비저장의 또 다른 이점은 합니다. 복구의 용이성은 또한 SQL 데이터베이스 및 Azure 앱 서비스 웹 앱 같은 플랫폼으로-서비스 (PaaS) 기능의 이점 중 하나입니다. 하드웨어 오류 드물지만 이러한 서비스를 처리 하는 자동으로 발생할 때 도 이러한 서비스 중 하나를 사용 하는 경우 컴퓨터 오류를 처리 하는 코드를 작성할 필요가 없습니다.

### <a name="service-failures"></a>서비스 오류

클라우드 앱은 일반적으로 여러 서비스를 사용합니다. 예를 들어 수정 응용 프로그램에 SQL 데이터베이스 서비스, 저장소 서비스를 사용 하 여 및 웹 앱은 Azure 앱 서비스에 배포 합니다. 응용 프로그램 수행할 작업에 의존 하는 서비스 중 하나가 실패할 경우? 일부 서비스 오류 친숙 한 "죄송 하지만 나중에 다시 시도" 메시지에 가장 적합 한 작업을 수행할 수 수 있습니다. 하지만 대부분의 시나리오에서 잘 할 수 있습니다. 예를 들어 백 엔드 데이터 저장소 다운 되는 경우 사용자 입력을 허용, "요청이 수신 되기"를 표시 및 저장할 수 있습니다 다른 곳의 입력 일시적으로; 그런 다음 필요한 서비스를 다시 작동 되어 입력을 검색 하 고 처리 합니다.

[큐 중심 작업 패턴](queue-centric-work-pattern.md) 장이이 시나리오를 처리 하는 방법을 보여 줍니다. 수정 앱 SQL 데이터베이스에서 작업을 저장 하지만 SQL 데이터베이스 다운 되었을 때 작업을 취소 하려면 필요 하지 않습니다. 이 장에서 큐에 작업에 대 한 사용자 입력을 저장 하 고 큐를 읽고 작업을 업데이트 하는 작업자 프로세스를 사용 하는 방법을 살펴보겠습니다. 수정 작업을 만들 수 있습니다; 영향을 받지 않습니다 SQL 다운 되는 경우 작업자 프로세스가 기다렸다가 SQL 데이터베이스를 사용할 수 있는 경우 새 작업을 처리할 수 있습니다.

### <a name="region-failures"></a>영역 장애

전체 지역이 실패할 수 있습니다. 자연 재해 데이터 센터 손상 될 수 있습니다, 그리고을 해제 하십시오. 여 평면화 얻을 수 있습니다, 그리고 매장 backhoe 등과 함께 cow farmer 하 여 데이터 센터에 트렁크 줄을 줄일 수 없습니다. 앱 stricken 데이터 센터에서 호스트 될 경우????????????? 다른 영역에서 실행을 계속 하나에 재해가 발생 하는 경우, 여러 영역에서 동시에 실행 하도록 Azure에 응용 프로그램이를 설정 하는 것이 불가능 합니다. 이러한 오류는 거의 발생 하 고 대부분의 응용 프로그램은 이러한 종류의 오류를 통해 중단 없이 서비스를 확인 하는 데 필요한 쉽지를 통해 이동 하지 않습니다. 영역 오류 통해서도 사용할 수 있는 앱을 유지 하는 방법에 대 한 내용은 장의 끝 부분에 리소스 섹션을 참조 합니다.

Azure의 목표 처리 모두 이러한 종류의 오류가 훨씬 쉽게 확인 하 고 방법을 수행 되는 작업 하는 다음 장에서 몇 가지 예제를 볼 수 있습니다.

## <a name="slas"></a>Sla

클라우드 환경에서 서비스 수준 계약 (Sla)에 대 한 사용자 종종 듣고 합니다. 기본적으로 서비스는 신뢰할 수 있는 방법에 대 한 회사 있도록 약속입니다. SLA를 의미 하는 99.9% 99.9%의 시간 동안 제대로 작동 하려면 서비스를 예상 해야 합니다. SLA에 대 한 매우 일반적인 값 기능이 며 매우 높은 번호를 말 좋지만 작동 중단 시간이 얼마나 사실을 모를 수 있습니다. 1%가 실제로 금액을 합니다. 다음은 다양 한 SLA 백분율 1 년, 월 및 주 통해으로 해석 얼마나 많은 가동 중지 시간을 표시 하는 테이블입니다.

![SLA 테이블](design-to-survive-failures/_static/image2.png)

따라서 1 년 또는 한 달 43.2 분 SLA 의미 서비스는 99.9% 만큼 아래로 수 있습니다. 더 작동 중단 시간 보다는 대부분의 사람들이 실현 됩니다. 않으므로 개발자는 어느 정도의 가동 중지 시간이 수 있다는 점에 유의 하 고 정상적인 방식으로 처리 해야 할 수도 있습니다. 특정 시점에이 분명히 응용 프로그램을 사용 하 고 서비스가 다운 된 것 이며 고객에 해당 부정적인 영향을 최소화 해야 합니다.

SLA에 대해 알아야 할 한 가지 참조 하는 시간 프레임은: 않습니다 시계가 다시 설정 될 매주, 매월 또는 매년? Azure에서 다시 설정 클록 연간 SLA는 일련의 좋은 개월 오프셋을 적용 하 여 나쁜 달을 숨길 수 있으므로 보다 연간 SLA는 매월 합니다.

물론에서는 항상의 목표 SLA; 보다 더 잘 수행 일반적으로 보다 훨씬 적은 다운 됩니다. 프라미스는 우리가 적이 다운 가동 중지 시간이 최대 길이 보다 오랫동안 경우 환불을 요청할 수 있습니다. 얻게 아마도 금액이 완전히 보상 경우 작동 중단 시간을 초과의 비즈니스 영향에 대 한 하지만 그러한 측면 SLA의 적용 정책 되며는 म 않습니다 라인 매우 심각 하 게 알 수 있습니다.

### <a name="composite-slas"></a>복합 Sla

Sla 보고 하는 경우에 대해 생각 하는 중요 한 점은 응용 프로그램의 여러 서비스를 사용 하 여 별도 SLA에 있는 각 서비스에 미치는 영향을 사용 하는 것입니다. 예를 들어 수정 앱 Azure 앱 서비스 웹 앱, Azure 저장소 및 SQL 데이터베이스를 사용합니다. 다음은이 전자책, 2013 년 12 월에에서 기록 되는 날짜를 기준으로 해당 SLA 번호입니다.

![SLA 웹 사이트, 저장소, SQL 데이터베이스](design-to-survive-failures/_static/image3.png)

가동 중지 시간이 예상 서비스 Sla에 따라 앱에 대 한 최대 무엇입니까? 프로그램 작동 중단 시간이 수 있다고 최악의 SLA 백분율 또는 99.9%가 경우를 생각할 수 있습니다. 되는 true 세 서비스에 모두 같은 시간에 항상 실패 했지만 반드시 실제로 이렇게 하는 경우. 각 서비스 실패할 수 있습니다 하지 독립적으로 서로 다른 시간에 개별 SLA 숫자를 곱하여 복합 SLA를 계산할 필요가 있습니다.

![복합 SLA](design-to-survive-failures/_static/image4.png)

응용 프로그램 종료 될 뿐 아니라 43.2 분 한 달에 있지만 해당 크기 보다 3 배 한 달 – 108 분 하 고 여전히 Azure SLA 제한 내에서 사용할 수 없습니다.

이 문제를 Azure에 고유 하지 않습니다. 실제로 최상의 클라우드를 사용할 수 있는 클라우드 서비스의 Sla를 제공 하 고 모든 공급 업체의 클라우드 서비스를 사용 하는 경우를 다루는 데 비슷한 문제가 해야 합니다. 고객이 나 사용자에 영향을 줄 수 만큼 자주 발생할 수 있으므로 불가피 한 서비스 오류를 정상적으로, 처리 응용 프로그램을 디자인할 수 어떻게 생각의 중요성은이 강조 표시 합니다.

### <a name="cloud-slas-compared-to-enterprise-down-time-experience"></a>엔터프라이즈 다운 타임 환경에 비해 클라우드 Sla

사람 경우가 예를 들어, "엔터프라이즈 응용 프로그램 내에서 없었던 이러한 문제." 한 달 작동 중단 시간이 얼마나 요청할 경우 실제로 있는 일반적으로, 이제 ", 클러스터가 가끔 있습니다." 이러한 사실을 인정 얼마나 자주 요청 하 고 "경우가를 백업 하거나 새 서버 또는 update 소프트웨어를 설치할 필요가 있습니다." 물론, 하는 작동 중단 시간으로 계산 합니다. 대부분의 엔터프라이즈 응용 프로그램 특히 중요 한 있지 않은 경우 실제로 다운 우리의 서비스 Sla에서 허용 되는 기간 보다 그 이상입니다. 하지만 중단 시간이 덜 angst에 대 한 느껴야 하는 경향이 있는 경우 서버 및 인프라 및 제어에 대 한 책임을 합니다. 클라우드 환경에서 다른 사람의 종속를 알 수 없는 진행 되는 상황을 가져오는 것 더 신경을 경향이 수 있도록 합니다.

엔터프라이즈 클라우드 SLA에서에서 받아야 하는 보다 큰 가동 시간 백분율을 얻을 수 때 하드웨어에 훨씬 더 많은 비용을 소비 하 여 수행할 수 있습니다. 클라우드 서비스에서 수행할 수 있지만 해당 서비스에 대 한 더 많은 요금을 청구 해야 합니다. 대신, 비용 효율적인 서비스 활용 및 불가피 한 오류를 고객에 게 최소 중단 되도록 소프트웨어를 디자인 합니다. 클라우드 응용 프로그램 디자이너를 사용 하는 작업 재해 방지에 대 한 오류를 방지 하기 위해 수많은 아니며 하드웨어에 없는 소프트웨어에 집중 하 여 그렇게 합니다. 엔터프라이즈 응용 프로그램 오류 간 평균 시간을 최대화 하기 위해 노력을 하지만 클라우드 응용 프로그램을 복구 하는 평균 시간을 최소화 하기 위해 노력 합니다.

### <a name="not-all-cloud-services-have-slas"></a>Sla를 보유할 모든 클라우드 서비스

주의 모든 클라우드 서비스에도 SLA 있습니다. 응용 프로그램을 가동 시간 다 사용 하 여 서비스에 종속 된 경우 생각 보다 훨씬 더 오래 종료 될 수 없습니다. 예를 들어 Facebook 또는 Twitter와 같은 소셜 공급자를 사용 하 여 사이트에 로그인 사용, 한 SLA는 고 하셨습니까 알게 될 수 있습니다를 확인 하려면 서비스 공급자와 함께 확인 가지 없습니다. 하지만 고객에 게 앱이 잠글 인증 서비스 작동이 중단 요청을 받고 해당 볼륨을 지원할 수 없는 경우. 이상 (일) 동안 다운 되었을 수 있습니다. 하나의 새 응용 프로그램의 작성자 억 다운로드 하 고 종속성 Facebook 인증-을 갖고 하는데 너무 늦 라이브 및 검색을 진행 하기 전에 Facebook와 통신 하지 않았습니다 해당 서비스에 대 한 SLA를 제공 하지 했음을 합니다.

### <a name="not-all-downtime-counts-toward-slas"></a>Sla까지 일부만 가동 중지 시간 계산

일부 클라우드 서비스 응용 프로그램에서 과도 하 게 사용 하는 경우에 의도적으로 서비스를 거부할 수 있습니다. 이 라고 *제한*합니다. 서비스 SLA 있으면는 제한 될 수 있습니다, 고 응용 프로그램 디자인 해야 이러한 상황이 발생 하지 않게 발생 하는 제한에 적절 하 게 반응 조건을 내용이 표시 되어야 합니다. 예를 들어 서비스에 대 한 요청을 특정 수 / 초를 초과 했을 때 실패 하기 시작 하려는 경우 자동 다시 시도를 계속 하면 제한이 발생 하기 너무 빨리 문제가 발생 하지 않도록 확인 합니다. 제한에 대해 자세히 되 겠는 [일시적인 오류 처리 장](transient-fault-handling.md)합니다.

## <a name="summary"></a>요약

이 장에서 실제 클라우드 앱을 오류를 적절 하 게 유지 되도록 설계에 이유를 실현할 수 있도록 시도 했습니다. 부터는 [다음 장에서](monitoring-and-telemetry.md), 그렇게 하는 데 몇 가지 전략에 대 한 좀 더 자세히 논의할이 시리즈의 나머지 패턴:

- 양호가 [모니터링 및 원격 분석](monitoring-and-telemetry.md)의 개입을 필요로 하는 오류에 대 한 신속 하 게 확인 하 고이 문제를 해결 하는 데 충분 한 정보가 있는 있도록, 합니다.
- [일시적인 오류 처리](transient-fault-handling.md) 수 및로 대체 때 앱을 자동으로 복구 되도록 지능형 다시 시도 논리를 구현 하 여 [회로 차단기](transient-fault-handling.md#circuitbreakers) 논리 표시할 수 없는 경우.
- 사용 하 여 [분산 캐싱](distributed-caching.md) 데이터베이스 액세스 권한이 있는 처리량, 대기 시간 및 연결 문제를 최소화 하기 위해 합니다.
- 느슨한 결합을 통해 구현 된 [큐 중심 작업 패턴](queue-centric-work-pattern.md)응용 프로그램 프런트 엔드는 백 엔드 다운 되었을 때 작업을 계속할 수 있도록 합니다.

## <a name="resources"></a>리소스

자세한 내용은이 전자책 (영문) 및 다음 리소스의 뒷부분을 참조 하십시오.

설명서:

- [Failsafe: 복원 력 있는 클라우드 아키텍처에 대 한 지침](https://msdn.microsoft.com/en-us/library/windowsazure/jj853352.aspx)합니다. 백서: Marc Mercuri, Ulrich Homann 및 Andrew Townhill 합니다. FailSafe 비디오 시리즈의 웹 페이지 버전입니다.
- [Azure 클라우드 서비스에서 대규모 서비스를 디자인에 대 한 유용한](https://msdn.microsoft.com/en-us/library/windowsazure/jj717232.aspx)합니다. 백서: Mark Simms 및 Michael Thomassy 합니다.
- [Azure 비즈니스 연속성 기술 지침](https://msdn.microsoft.com/en-us/library/windowsazure/hh873027.aspx)합니다. 백서: Patrick Wickline 및 Jason Roth 합니다.
- [Azure 응용 프로그램에 대 한 고가용성 및 재해 복구](https://msdn.microsoft.com/en-us/library/windowsazure/dn251004.aspx)합니다. Michael McKeown, Hanu Kommalapati, 및 Jason Roth 백서에 나와 있습니다.
- [Microsoft Patterns and Practices-Azure 지침](https://msdn.microsoft.com/en-us/library/dn568099.aspx)합니다. 회로 차단기 패턴을 여러 데이터 센터 배포 지침을 참조 하십시오.
- [Azure 지원-서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)합니다.
- [Azure SQL 데이터베이스의 비즈니스 연속성](https://msdn.microsoft.com/en-us/library/windowsazure/hh852669.aspx)합니다. SQL 데이터베이스 높은 가용성 및 재해 복구 기능에 대 한 설명서입니다.
- [고가용성 및 재해 복구 Azure 가상 컴퓨터에서 SQL Server에 대 한](https://msdn.microsoft.com/en-us/library/windowsazure/jj870962.aspx)합니다.

비디오:

- [FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms 하 여 시리즈를 9 개 부분으로 구성 합니다. 고급 개념 및 아키텍처 원칙 매우 액세스 가능 하 고 흥미로운 방법으로 스토리 실제 고객과 Microsoft 고객 자문 팀 (CAT) 환경에서 가져온 것으로 표시 합니다. 1에서 8 에피소드 깊이에 실패 하는 클라우드 앱을 디자인 하기 위한 이유도 이동 합니다. 49:57, 오류 지점과 오류 모드 56:05에서 시작 하는 2 에피소드의 토론 및 회로 차단기 40:55에서 시작 하는 3 에피소드에 대 한 설명에서 시작 하는 2 에피소드 제한에 대 한 추가 설명은 참조 하십시오.
- [건물 큰: Azure 고객-2 부에서에서 확인 된 사항을](https://channel9.msdn.com/Events/Build/2012/3-030)합니다. Mark Simms 실패에 대 한 디자인 하 고 모든 항목을 계측 하는 방법에 대 한 설명입니다. 유사 Failsafe 시리즈 하지만 방법 더 세부적으로 이동 합니다.

>[!div class="step-by-step"]
[이전](unstructured-blob-storage.md)
[다음](monitoring-and-telemetry.md)
