---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
title: (실제 클라우드 앱 빌드 azure) 장애를 견딜 수 디자인 | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드 앱 빌드 Azure 전자책을 사용 하 여 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴과 그을 수 있는 방법을 설명 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: 364ce84e-5af8-4e08-afc9-75a512b01f84
ms.technology: ''
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/design-to-survive-failures
msc.type: authoredcontent
ms.openlocfilehash: db7398cfd9ed51d716cb595d977b482fd0da131e
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37372464"
---
<a name="design-to-survive-failures-building-real-world-cloud-apps-with-azure"></a>(실제 클라우드 앱 빌드 azure) 장애를 견딜 수 디자인
====================
하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 합니다 **실제 세계 클라우드 앱 빌드 Azure** 전자책 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴 설명 하 고 도움이 될 수 있는 사례 성공적인 클라우드를 위한 웹 앱을 개발할 수 있습니다. 전자책에 대 한 정보를 참조 하세요 [첫 번째 장에서](introduction.md)합니다.


응용 프로그램을 사용할 수 있지만 특히 있는 많은 사람이 사용할 클라우드에서 실행 될 모든 유형의 작성 하는 경우 고려해 야 하는 중 하나는 정상적으로 오류를 처리 하 고 가치를 계속 수 있도록 앱을 디자인 하는 방법 만큼 가능 합니다. 충분 한 시간을 지정 합니다 작업 하려는 모든 환경이 나 모든 소프트웨어 시스템에서 문제가 발생 합니다. 어떻게 화가 고객에 게 받 및 시간을 결정 앱에서 이러한 상황을 처리 하는 방법을 분석 하 고 문제를 해결 해야 합니다.

## <a name="types-of-failures"></a>실패 유형

가지 오류를 다르게 처리 해야 하는 두 가지 기본 범주가 있습니다.

- 일시적이 지, 자체 일시적인 네트워크 연결 문제와 같은 오류를 복구 합니다.
- 다각적인 오류 개입입니다.

일시적인 오류에 대 한 대부분의 앱을 신속 하 고 자동으로 복구 하는 시간을 확인 하는 재시도 정책을 구현할 수 있습니다. 고객에 게 약간 긴 응답 시간을 확인할 수 있지만 그렇지 않은 경우 이러한 영향을 받지 않습니다. 이러한 오류를 처리 하는 몇 가지 방법을 살펴보겠습니다 합니다 [일시적인 오류 처리 장](transient-fault-handling.md)합니다.

비전과 오류에 대 한 모니터링 및 로깅 알려 주는 신속 하 게 문제가 발생 하 고 근본 원인 분석을 용이 하 게 하는 기능을 구현할 수 있습니다. 이러한 종류의 오류를 기반으로 유지할 수 있도록 몇 가지 측면을 살펴보겠습니다 합니다 [모니터링 및 원격 분석 장](monitoring-and-telemetry.md)합니다.

## <a name="failure-scope"></a>오류 범위

또한 고려해 야 – 오류 범위에 대 한 단일 컴퓨터에 영향을 주며 여부를 SQL 데이터베이스 또는 저장소 등 전체 지역 전체 서비스입니다.

![오류 범위](design-to-survive-failures/_static/image1.png)

### <a name="machine-failures"></a>컴퓨터 오류

Azure에서 새 대시보드를 여는 실패 한 서버는 자동으로 대체 하 고 빠르고 자동으로 잘 설계 된 클라우드 앱이이 종류의 오류 복구 됩니다. 이전 상태 비저장 웹 계층의 확장성 이점의 강조한 것 이며 실패 한 서버에서 복구 편의성 또 다른 이점은 상태 비저장입니다. 복구의 간편한 SQL Database 및 Azure App Service Web Apps 같은 플랫폼-as a service (PaaS) 기능의 이점 중 하나 이기도합니다. 하드웨어 오류는 흔치 않지만 이러한 서비스가 자동으로 처리할 발생 시기 도 이러한 서비스 중 하나를 사용 하는 경우 컴퓨터 오류를 처리 하는 코드를 작성할 필요가 없습니다.

### <a name="service-failures"></a>서비스 오류

클라우드 앱은 일반적으로 여러 서비스를 사용합니다. 예를 들어 Fix It 응용 프로그램에서는 SQL Database 서비스를 저장소 서비스를 사용 하 고 Azure App Service에 웹 앱 배포 됩니다. 가 앱 수행할 신뢰할 수 있는 서비스 중 하나가 실패할 경우? 일부 서비스 실패 친숙 한 "죄송 합니다. 나중에 다시 시도" 할 수 있는 최상의 메시지가 될 수 있습니다. 하지만 대부분의 시나리오에서 잘 할 수 있습니다. 예를 들어, 백 엔드 데이터 저장소에 다운 되 면 사용자 입력을 허용, "요청을 받은" 표시 및 저장할 수 있습니다 다른 임의의 위치 입력 일시적으로; 필요한 서비스를 다시 작동 되 면 다음 입력을 검색 하 고 처리할 수 있습니다.

합니다 [큐 중심 작업 패턴](queue-centric-work-pattern.md) 장이이 시나리오를 처리 하는 방법을 보여 줍니다. Fix It 응용 프로그램 SQL Database에서 작업을 저장 하지만 SQL Database 종료 되는 경우 작업을 종료 하지 않아도 됩니다. 내용, 큐에 있는 작업에 대 한 사용자 입력을 저장 하 고 큐를 읽고 작업을 업데이트 하는 작업자 프로세스를 사용 하는 방법을 살펴보겠습니다. Fix It 작업을 만들 수는 영향을 받는; SQL 다운 된 경우 작업자 프로세스는 대기 하 고 SQL 데이터베이스를 사용할 수 있는 경우 새 작업을 처리할 수 있습니다.

### <a name="region-failures"></a>지역 장애

전체 지역 실패할 수 있습니다. 자연 재해는 데이터 센터가 손상 될 수 있습니다 하 고는 meteor 하 여 평면화 가져올 수 있습니다 하 고, 데이터 센터에 트렁크 줄 등 backhoe 구독만 매장을 농부에서 차단 될 수 있습니다. 앱 stricken 데이터 센터에서 호스팅되는 경우 어떻게 해야 하나요? 하나에서 재해가 발생 하는 경우 다른 지역에서 실행 되는 것이 할 수 있도록 여러 지역에서 동시에 실행 하도록 Azure에서 앱을 설정 하는 것이 가능 합니다. 이러한 오류는 매우 드물게 발생 하 고 대부분의 앱이이 종류의 오류를 통해 중단 없이 서비스를 확인 하는 데 필요한 강화를 통해 이동 하지 않습니다. 지역 장애를 통해서도 사용할 수 있는 앱을 유지 하는 방법에 대 한 내용은 장의 끝 리소스 섹션을 참조 합니다.

Azure의 목표를 훨씬 쉽게 오류의 이러한 종류의 모든 처리 되도록 이며 있으시면는 다음 챕터에서 몇 가지 예가 표시 됩니다.

## <a name="slas"></a>Sla

사용자는 종종 클라우드 환경에서 서비스 수준 계약 (Sla)에 대해 알아보세요. 기본적으로 이들은 어떻게 신뢰할 수 있는 해당 서비스에 대 한 회사는 약속입니다. 99.9 %SLA 의미 하는 99.9%의 시간 동안 제대로 작동 하는 서비스를 예상 해야 합니다. SLA에 대 한 매우 일반적인 값 및 매우 높게 처럼 보인다는 것 이지만 얼마나 많은 가동 중지 시간을 알 수 없습니다. %1에 실제로 금액입니다. 가동 중지 시간을 1 년, 월 및 주를 통해 amount는 다양 한 SLA 백분율을 보여 주는 테이블이 다음과 같습니다.

![SLA 테이블](design-to-survive-failures/_static/image2.png)

따라서 1 년 또는 달 43.2 분에 서비스를 의미 하는 SLA 99.9 %8.76 시간 아래로 수 있습니다. 이것이 더 가동 중지 시간이 사람들이 실현 하는 것입니다. 개발자로 서 않으므로 어느 정도의 가동 중지 시간이 가능한 임을 인식 하 고 정상적인 방식으로 처리 해야 할 수도 있습니다. 시점에서 누군가 앱을 사용 하 고 서비스를 중지 하려는 고객에는 부정적인 영향을 최소화 하려는 경우.

SLA에 대해 알아야 할 것은 어떤 시간 프레임을 가리킵니다: 클록 재설정 되지 매주, 매월 또는 매년? Azure 연간 SLA 좋은 개월 계열을 사용 하 여이 오프셋 하 여 나쁜 달을 가릴 수 있으므로 보다는 매년 SLA는 매월 클록을 재설정 했습니다.

물론 우리가 항상 목표로 SLA; 보다 더 잘 수행 일반적으로 이보다 훨씬 적은 축소 됩니다. 프라미스가 다운 된 것 적이 가동 중지 시간이 최대 이상에 대 한 환불을 요청할 수 있습니다. 받게 것은 금액 않습니다 보상이 중단 시간이 과도 한 비즈니스 영향에 대 한 하지만 SLA의 이러한 측면은 적용 정책의 역할는 우리가 수행 가져갈 매우 심각 하 게 알려줍니다.

### <a name="composite-slas"></a>복합 Sla

Sla에서 보고 있는 경우에 대해 생각 하는 중요 한 점은 앱에서 여러 서비스를 사용 하 여 각 서비스는 별도 SLA를 사용 하 여 영향 사용 하는 것입니다. 예를 들어 Fix It 앱을 Azure App Service Web Apps, Azure Storage 및 SQL Database를 사용합니다. 이 전자책은 2013 년 12 월에에서 기록 되는 날짜를 기준으로 SLA 번호는 다음과 같습니다.

![웹 사이트, Storage, SQL Database SLA](design-to-survive-failures/_static/image3.png)

이러한 서비스 Sla에 따라 앱에 대 한 예상 시간 아래로 최대 란? 같아야 하는 가동 중지 시간에는 가장 낮은 SLA 백분율 또는 99.9%가 경우 생각할 수 있습니다. 세 가지 서비스 모두에서 동시에 항상 실패 했지만 반드시 실제로 무엇이 발생 하는 경우 사실일 것입니다. 각 서비스가 실패할 수 하지 독립적으로 서로 다른 시간에 개별 SLA 숫자를 곱하여 복합 SLA를 계산 해야 합니다.

![복합 SLA](design-to-survive-failures/_static/image4.png)

따라서 앱 다운 될 뿐 아니라 43.2 분 한 달에 있지만 해당 크기 3 번 달 – 108 분 및 Azure SLA 제한 내에서 수 없습니다.

이 문제를 Azure에 고유 하지 않습니다. 에서는 실제로 최적인 클라우드를 사용할 수 있는 클라우드 서비스의 Sla를 제공 하 고 비슷한 문제는 공급 업체의 클라우드 서비스를 사용 하는 경우 처리 해야 합니다. 고객이 나 사용자에 영향을 줄 만큼 자주 발생할 수 있으므로 피할 수 없는 서비스 오류를 정상적으로 처리 하도록 앱을 디자인할 수 있습니다 하는 방법에 대 한 생각의 중요성은이 강조 표시 합니다.

### <a name="cloud-slas-compared-to-enterprise-down-time-experience"></a>엔터프라이즈 하위 타임 환경에 비해 클라우드 Sla

사람들이 때로는 예를 들어 "내 엔터프라이즈 앱에 되지 문제가이 있습니다." 한 달에 얼마나 많은 가동 중지 시간을 요청 하면 실제로 있으면 일반적으로 밝히는 "사실 이것이 가끔." 이러한 사실을 인정 빈도 요청 하 고 "백업 하거나 새 서버 또는 update 소프트웨어를 설치할 필요가 경우가 있습니다." 물론, 작동 중단 시간으로 계산 하는 합니다. 대부분의 엔터프라이즈 앱 특히 중요 아닌 실제로 다운 된 서비스가 Sla에서 허용 하는 시간 보다 더 합니다. 하지만 서버 및 인프라 및 제어에 대 한 책임을 하다 보면 중단 시간이 덜 다에 대 한 생각 합니다. 클라우드 환경에서 다른 사용자에 따라 달라 집니다 이며 모르는, 것이 더 신경을 가져오기 경향이 수 있도록 합니다.

엔터프라이즈가 SLA는 클라우드에서 것 보다 큰 가동 시간 비율을 달성 하는 경우 해당 하는 것 하드웨어에서 훨씬 더 많은 비용을 지출 한도입니다. 클라우드 서비스는 수행할 수 있으 나 등 해당 서비스에 대 한 요금을 청구 해야 합니다. 대신, 비용 효율적인 서비스를 활용 하 고 오류를 피할 수 없는 고객에 게 최소 중단 되도록 소프트웨어를 디자인 합니다. 클라우드 앱 디자이너를 사용 하는 작업 재해 방지에 대 한 오류를 방지 하려면 많지 아니며 하드웨어에 없는 소프트웨어에 집중 하 여 그렇게 합니다. 엔터프라이즈 앱 오류 간 평균 시간을 최대화 하기 위해 노력을 하는 반면 클라우드 앱 복구 시간을 최소화 하기 위해 노력 합니다.

### <a name="not-all-cloud-services-have-slas"></a>모든 클라우드 서비스 Sla를 보유

모든 클라우드 서비스에도 SLA가에 주의 수입니다. 앱을 가동 시간 보장 없이 서비스에 종속 된 경우 생각 보다 훨씬 더 종료 될 수 없습니다. 예를 들어 로그인 Facebook 또는 Twitter 같은 소셜 공급자를 사용 하 여 사이트를 사용 하는 경우는 SLA가 있고 알게 될 것도 아닌 알아보려면 서비스 공급자를 사용 하 여 확인 합니다. 하지만 고객에 게 앱 잠긴 인증 서비스 중단 또는 볼륨에서 throw 하는 요청을 지원할 수 없는 경우. 일 이상 종료 될 수 있습니다. 하나의 새 앱 작성자가 수백 개의 수백만 회의 다운로드를 예상 및 Facebook 인증-에서 종속성을 갖고 있지만 라이브 및 검색 된를 너무 늦게 진행 하기 전에 Facebook에 호환 되지 않는 경우가 했습니다. 해당 서비스에 대 한 SLA가 없습니다.

### <a name="not-all-downtime-counts-toward-slas"></a>일부 가동 중지 시간 수에 합산 Sla

일부 클라우드 서비스 앱에서 과도 하 게 사용 하는 경우에 의도적으로 서비스를 거부할 수 있습니다. 이 이라고 *제한*합니다. 서비스는 SLA가 하는 경우는 제한 될 수 있습니다, 그리고 및 앱 디자인 해야 이러한 상황이 발생 하지 않게 제한이 발생 하는 경우에 적절 하 게 반응 조건을 내용이 표시 되어야 합니다. 예를 들어, 서비스에 요청을 초당 특정 횟수를 초과 하면 실패 하기 시작 하려는 경우 자동 재시도 계속 제한이 발생 하기 너무 빨리 발생 하지 않는지 확인 합니다. 제한에 대 한 더 마련 합니다 [일시적인 오류 처리 장](transient-fault-handling.md)합니다.

## <a name="summary"></a>요약

이 장에서 실제 클라우드 앱을 정상적으로 장애를 견딜 수 디자인에 이유를 누릴 수 하려고 했습니다. 로 시작 합니다 [다음 장에서](monitoring-and-telemetry.md),이 시리즈의 나머지 패턴은 작업을 수행 하 여 몇 가지 전략에 대 한 자세한 정보로 이동:

- 가 좋은 [모니터링 및 원격 분석](monitoring-and-telemetry.md)개입을 필요로 하는 오류에 대 한 신속 하 게 확인 하 고 문제를 해결 하기에 충분 한 정보가 있습니다 있도록 합니다.
- [일시적인 오류 처리](transient-fault-handling.md) 수 및 대체 경우 앱을 자동으로 복구 되도록 지능형 다시 시도 논리를 구현 하 여 [회로 차단 기가](transient-fault-handling.md#circuitbreakers) 논리 수 없는 경우.
- 사용 하 여 [분산 캐싱](distributed-caching.md) 데이터베이스 액세스를 사용 하 여 처리량, 대기 시간 및 연결 문제를 최소화 하기 위해.
- 느슨한 연결을 통해 구현 된 [큐 중심 작업 패턴](queue-centric-work-pattern.md)앱의 프런트 엔드에서 백 엔드로 종료 되는 경우를 작업을 계속할 수 있도록 합니다.

## <a name="resources"></a>자료

자세한 내용은 다음 리소스를이 전자책에 이후 장을 참조 하세요.

설명서:

- [Failsafe: 복원 력 있는 클라우드 아키텍처 지침](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)합니다. Marc Mercuri, Ulrich Homann 및 Andrew Townhill 백서입니다. FailSafe 동영상 시리즈의 웹 페이지 버전입니다.
- [Azure Cloud Services에서 대규모 서비스 설계를 위한 모범 사례](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)합니다. Mark Simms 및 Michael Thomassy 백서입니다.
- [Azure 비즈니스 연속성 기술 지침](https://msdn.microsoft.com/library/windowsazure/hh873027.aspx)합니다. Patrick Wickline 및 Jason Roth 백서입니다.
- [Azure 응용 프로그램에 대 한 고가용성 및 재해 복구](https://msdn.microsoft.com/library/windowsazure/dn251004.aspx)합니다. Michael McKeown, Hanu Kommalapati 및 Jason Roth 백서입니다.
- [Microsoft Patterns and Practices-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx)합니다. 여러 데이터 센터 배포 지침, 회로 차단기 패턴을 참조 하세요.
- [Azure 지원-서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)합니다.
- [Azure SQL Database의 비즈니스 연속성](https://msdn.microsoft.com/library/windowsazure/hh852669.aspx)합니다. SQL Database 높은 가용성 및 재해 복구 기능에 대 한 설명서입니다.
- [고가용성 및 재해 복구 Azure Virtual Machines의 SQL Server에 대 한](https://msdn.microsoft.com/library/windowsazure/jj870962.aspx)합니다.

비디오:

- [FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는 데](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms에서 9 부 시리즈입니다. 고급 개념 및 아키텍처 원칙으로 실제 고객의 Microsoft 고객 자문 팀 (CAT) 환경에서 가져온 스토리를 사용 하 여 액세스 가능 하 고 흥미로운 방식으로 표시 합니다. 에피소드 1에서 8 방어에서 오류에서 존속 하는 클라우드 앱 디자인에 대 한 이유를 이동 합니다. 에피소드 2 49:57, 오류 지점과 오류 모드 56:05에서 시작 하는 에피소드 2의 대 한 에피소드 3 40:55부터에서 회로 차단기에 대 한 설명부터의 제한에 대 한 추가 설명은 참조 하세요.
- [빌드 큰: Azure 고객에 게-부에서에서 Lessons learned](https://channel9.msdn.com/Events/Build/2012/3-030)합니다. Mark Simms 실패에 대 한 디자인 및 모든 계측에 대해 설명 합니다. 비슷하지만 Failsafe 시리즈 자세한 방법 세부 정보로 이동 합니다.

> [!div class="step-by-step"]
> [이전](unstructured-blob-storage.md)
> [다음](monitoring-and-telemetry.md)
