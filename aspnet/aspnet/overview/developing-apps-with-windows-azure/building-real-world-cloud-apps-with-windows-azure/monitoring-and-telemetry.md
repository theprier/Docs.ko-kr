---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: "모니터링 및 원격 분석 (Azure로 응용 프로그램 빌딩 실제 클라우드) | Microsoft Docs"
author: MikeWasson
description: "실제 세계 클라우드로 응용 프로그램 빌딩 Azure 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴 및 그을 수 있는 방법에 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 07/09/2015
ms.topic: article
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: dfb0158ec05c890ecf80571d95b22d8c791ba7fc
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>모니터링 및 원격 분석 (Azure로 응용 프로그램 빌딩 실제 클라우드)
====================
여 [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **실제 세계 클라우드로 응용 프로그램 빌딩 Azure** 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴에 설명 하 고 사례 수 있는 클라우드에 대 한 웹 앱을 개발 성공적으로 수행 되어야 합니다. 전자책에 대 한 정보를 참조 하십시오. [첫 번째 장](introduction.md)합니다.


많은 사람들이 해당 응용 프로그램 중지 되는 경우 알 수 있도록 하는 고객에 의존 합니다. 하는 실제로 가장 좋은 방법은 어디에서 든 지 고 특히 클라우드에 없습니다. 빠른 알림 보장 되지 않으며 무슨 상황이 발생 하는 방법에 대 한 최소 수준 이거나 잘못 된 데이터를 통보 가져오기 수행 얻을 경우가 많기 때문입니다. 좋은 원격 분석 및 응용 프로그램 및 특정 상황이 발생할 때의 진행 상황을 확인할 수 로깅 시스템 발생할 바로 확인 하 고 유용한 문제 해결 정보는 실행 되도록 합니다.

## <a name="buy-or-rent-a-telemetry-solution"></a>구매 또는 임대는 원격 분석 솔루션

> [!NOTE]
> 하기 전에이 문서가 작성 된 [Application Insights](https://azure.microsoft.com/services/application-insights/) 릴리스 되었습니다. Application Insights는 Azure에서 원격 분석 솔루션에 대 한 기본 설정된 방법입니다. 참조 [ASP.NET 웹 사이트에 대 한 Application Insights 설정](https://docs.microsoft.com/azure/application-insights/app-insights-asp-net) 자세한 정보에 대 한 합니다.


클라우드 환경에 대 한 뛰어난 것 중 하나을 구매 또는 승리 하 임대 못해도 손쉽게 된다는 점입니다. 원격 분석 예입니다. 많은 노력 없이 최대 및 실행, 경제적으로 매우 정말로 우수한 원격 분석 시스템을 가져올 수 있습니다. Azure와 통합 하는 뛰어난 파트너의 많은 있고 그 중 일부를 무료 계층으로 때문 nothing에 대 한 기본 원격 분석을 가져올 수 있습니다. Azure에서 현재 사용할 수 있는 몇 가지는 것 같습니다.

- [New Relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

2015 년 3 월을 기준으로 [Visual Studio Online 용 Application Insights Microsoft](https://azure.microsoft.com/en-us/documentation/articles/app-insights-get-started/) 아직 해제 되지 않습니다 되지만를 사용해 미리 보기에서 사용할 수 있습니다. [Microsoft System Center](http://www.petri.co.il/microsoft-system-center-introduction.htm#) 도 모니터링 기능을 포함 합니다.

New Relic을 얼마나 쉬운지는 것이 원격 분석 시스템을 사용 하도록 표시 하도록 설정 하 여 신속 하 게 살펴보겠습니다.

Azure 관리 포털에서 서비스에 등록 합니다. 클릭 **새로**, 클릭 하 고 **저장소**합니다. **추가 기능 선택** 대화 상자가 나타납니다. 아래로 스크롤하여 클릭 **New Relic**합니다.

![추가 기능 선택](monitoring-and-telemetry/_static/image1.png)

오른쪽 화살표를 클릭 하 고 원하는 서비스 계층을 선택 합니다. 이 데모에서는 무료 계층을 사용 합니다.

![추가 기능을 개인 설정](monitoring-and-telemetry/_static/image2.png)

오른쪽 화살표를 클릭 하 고 "구입" 확인 New Relic에 포털에서 추가 기능으로 참석 이제 합니다.

![구매를 검토 합니다.](monitoring-and-telemetry/_static/image3.png)

![관리 포털에서 새 Relic 추가 기능](monitoring-and-telemetry/_static/image4.png)

클릭 **연결 정보입니다.**, 라이선스 키를 복사 합니다.

![연결 정보입니다.](monitoring-and-telemetry/_static/image5.png)

로 이동는 **구성** 탭에 포털에서 웹 앱 설정 **성능 모니터링** 를 **추가 기능**를 설정 하 고는 **추가 기능 선택** 드롭 다운 목록 **New Relic**합니다. 클릭 **저장**합니다.

![구성 탭에서 새 Relic](monitoring-and-telemetry/_static/image6.png)

Visual Studio에서 응용 프로그램에서 새 Relic NuGet 패키지를 설치 합니다.

![개발자 분석 구성 탭에서](monitoring-and-telemetry/_static/image7.png)

Azure에 응용 프로그램을 배포 하 고 사용을 시작 합니다. 모니터링할 New Relic에 대 한 몇 가지 활동을 제공 하는 몇 수정 작업을 만듭니다.

다음 돌아가서는 **New Relic** 페이지에 **추가 기능** 포털 및 클릭 탭 **관리**합니다. 포털을 사용 하 여 single sign on 인증에 대 한 자격 증명을 다시 입력 하는 것이 없는 New Relic 관리 포털로 보냅니다. 개요 페이지는 다양 한 성능 통계를 표시합니다. (개요 페이지의 전체 크기를 표시 하려면 이미지를 클릭 합니다.)

[![새 Relic 모니터링 탭](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

다음은 몇 가지 통계를 볼 수입니다.

- 하루 중 서로 다른 시간에 평균 응답 시간입니다.

    ![응답 시간](monitoring-and-telemetry/_static/image10.png)
- 하루 중 서로 다른 시간에 처리량 속도 (분당 요청)에서.

    ![처리량](monitoring-and-telemetry/_static/image11.png)
- 다른 HTTP 요청을 처리 하는 데 걸린 서버 CPU 시간입니다.

    ![웹 트랜잭션 제한 시간](monitoring-and-telemetry/_static/image12.png)
- 응용 프로그램 코드의 다른 부분에 소요 된 CPU 시간:

    ![추적 세부 정보](monitoring-and-telemetry/_static/image13.png)
- 성능 기록 통계입니다.

    ![성능 기록](monitoring-and-telemetry/_static/image14.png)
- Blob 서비스 및 신뢰할 수 있는 방법과 응답에 대 한 통계와 같은 외부 서비스에 대 한 호출 서비스가 되었습니다.

    ![외부 서비스](monitoring-and-telemetry/_static/image15.png)

    ![외부 서비스](monitoring-and-telemetry/_static/image16.png)

    ![외부 서비스](monitoring-and-telemetry/_static/image17.png)
- 미국 web app에서 트래픽을 가져온 원본 위치에서 또는 전 세계에 있는 위치에 대 한 정보입니다.

    ![지리](monitoring-and-telemetry/_static/image18.png)

보고서 및 이벤트를 설정할 수 있습니다. 예를 들어 오류 재빨리 언제 든 지를 발생 하는 문제 경고 지원 담당자에 게는 전자 메일 수 있습니다.

![보고서](monitoring-and-telemetry/_static/image19.png)

New Relic 원격 분석 시스템;의 한 예는 여러 서비스에서 이러한 모든 데이터를 가져올 수 있습니다. 클라우드의 장점은 있는 모든 코드를 작성할 필요 없이 용 최소 하거나 없는 경비 갑자기 얻을 수 있습니다 응용 프로그램 사용 방법 및 고객에 게 실제로 발생 무엇에 대 한 다양 한 추가 정보입니다.

<a id="log"></a>
## <a name="log-for-insight"></a>통찰력에 대 한 로그

원격 분석 패키지 좋은 첫 번째 단계는 있지만 사용자 고유의 코드를 계측 하 합니다. 원격 분석 서비스를 알려는 문제가 있을 때 대상을 지정 하 고 고객을 발생 하지만 하지을 줄 수 많은 코드에서의 진행 상황에 대 한 정보입니다.

앱이 수행 하는 참조를 프로덕션 서버에 원격에 않으려는 합니다. 한 서버를가지고 있지만 수백 대의 서버에는 크기가 조정 된 및로 원격 해야 할 것을 알 수 없는 경우에 어떻게 실용적인 상태일 수 있습니까? 로깅이 필요가 원격 분석 및 디버그 하는 프로덕션 서버에 충분 한 정보를 제공 해야 문제입니다. 하면 로그를 통해서만 문제를 격리할 수 있도록 충분 한 정보를 로깅 수 해야 합니다.

### <a name="log-in-production"></a>프로덕션에 로그인

많은 사람들이 문제가 있습니다. 디버깅 하려는 경우에 프로덕션에서 추적을 켤 합니다. 이 항목에 대 한 유용한 문제 해결 정보를 얻을 시간과 문제를 인식 하는 시간 사이 상당한 지연 시간을 발생할 수 있습니다. 얻을 수 있는 정보를 일시적인 오류에 대 한 유용할 수 있습니다.

저장 비용은 저렴 클라우드 환경에서 권장 사항는 항상 상태로 두는 프로덕션 환경에 로그온 합니다. 이미 있는 로그에 기록 하 고 수 있는 기록 데이터가 있는 오류가 발생 하는 경우 이런 방식으로 시간이 지나면서 또는 서로 다른 시간에 정기적으로 수행 하는 문제를 분석 합니다. 이전 로그를 삭제 하려면 제거 프로세스를 자동화 수 있지만 로그를 유지 하는 것 보다 이러한 프로세스를 설정 하는 비용이 많이 드는 임을 알게 될 수 있습니다.

로깅 추가 비용은 시간과 비용을 모두 필요한 문제가 발생 하는 경우 이미 사용할 수 있는 정보 여 절약할 수 문제 해결에 비해 간단 합니다. 그런 다음 나타나면 사람이 가졌던 임의 오류가 잠시 약 8:00 어젯밤, 하지만 오류를 기억 하지 못하는 것을 확인할 수 있습니다 쉽게 문제를 합니다.

4 달러에 대 한 한 달에 가까이 50gb의 로그를 유지할 수 있습니다 및 로깅의 성능 영향은 간단으로 염두-성능 병목 현상을 방지, 로깅 라이브러리 비동기 인지 확인 하기 위해 한 가지를 유지 합니다.

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>작업을 필요로 하는 로그에서 알려주는 로그를 구분 합니다.

로그는 INFORM (주세요를 아는) 또는 ACT (주세요 하다가) 되어야 합니다. 만 순전히 조치를 취할 사람 또는 자동화 된 프로세스를 필요로 하는 문제에 대 한 ACT 로그를 쓸 수 주의 해야 합니다. 너무 많은 ACT 로그 노이즈를 통해 모든 정품 문제를 찾을 수를 조사 하 여 너무 많은 작업이 필요한 만들어집니다. 고 ACT 로그 직원을 지원 하기 위해 메일을 보내는 것과 같은 작업을 자동으로 트리거를 하는 경우 등의 작업을 사용 하는 천 단위는 단일 문제로 인해 트리거될 수 있으므로 하지 마십시오.

.NET System.Diagnostics 추적에서 로그 오류, 경고, 정보 및 디버그/자세한 정보 표시 수준을 할당할 수 있습니다. ACT 로그에 대 한 오류 수준을 예약 하 고 INFORM 로그에 대 한 하위 수준을 사용 하 여 INFORM 로그에서 ACT를 쉽게 구분할 수 있습니다.

![로깅 수준](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>런타임 시 로깅 수준을 구성합니다

프로덕션 환경에서 항상 로깅을 좋은지를 이지만, 또 다른 최선의 실행 시 다시 배포 하거나 응용 프로그램을 다시 시작 하지 않고, 로그인 하는 정보의 수준을 조정할 수 있습니다 하는 로깅 프레임 워크를 구현 하는 것입니다. 예를 사용 하는 경우에 추적 기능 `System.Diagnostics` 디버그/자세히 로그에 기록 및 오류, 경고, 정보를 만들 수 있습니다. 항상 오류, 경고를 기록 하 고 프로덕션 환경에서 정보를 기록 하 고 디버그/자세한 정보 표시 로깅 상황별으로에서 문제 해결을 위한 동적으로 추가할 수 있게 되기를 하려면 것이 좋습니다.

Azure 앱 서비스의 웹 앱은 쓰기에 대 한 기본 제공 지원 `System.Diagnostics` 파일 시스템, 테이블 저장소 또는 Blob 저장소에 로깅합니다. 각 저장소 대상에 대 한 서로 다른 로깅 수준을 선택한 응용 프로그램을 다시 시작할 필요 없이 즉석에서 로깅 수준을 변경할 수 있습니다. Blob 저장소 지원 더 쉽게 실행 하려면 [HDInsight](https://docs.microsoft.com/azure/hdinsight/) HDInsight Blob 저장소에서 직접 작업 하는 방법을 알기 때문에 응용 프로그램 로그에 작업 분석 합니다.

### <a name="log-exceptions"></a>로그 예외

구현 하지 않는 *예외입니다. Tostring ()* 로깅 코드에 있습니다. 컨텍스트 정보를 유지합니다. SQL 오류가 발생 한 경우 SQL 오류 번호 남깁니다. 모든 예외에 대 한 컨텍스트 정보, 예외, 자체 및 문제 해결을 위해 수행 해야 하는 제공 된 모든 내부 예외를 포함 합니다. 예를 들어, 서버 이름, 트랜잭션 식별자 및 사용자 이름 (하지만 하지 암호 또는 비밀이!) 컨텍스트 정보 포함 될 수 있습니다.

각 개발자가 로깅 예외를 사용 하 여 올바른 작업을 수행할 수에 의존 하는 경우 그 중 일부만 않습니다. 것 가져옵니다 했는지 오른쪽 항상을 보장 하려면 예외로 거 인터페이스에 바로 처리 빌드:로 거 클래스에 자체 예외 개체를 전달 하 고로 거 클래스에서 제대로 예외 데이터를 기록 합니다.

### <a name="log-calls-to-services"></a>서비스에 대 한 로그 호출

데이터베이스 또는 REST API 또는 외부 서비스에 인지 응용 프로그램 서비스를 호출할 때마다 로그를 작성 하는 것이 좋습니다. 성공 또는 실패 하지만 각 요청 걸린 표시 뿐만 아니라 로그에 포함 됩니다. 클라우드 환경에서 완전 중단 보다는 시간이 오래 걸리지에 관련 된 문제를 자주 표시 됩니다. 갑자기 초 작성을 시작 수 일반적으로 10 밀리초를 사용 하는 것입니다. 나타나면 사용자 응용 프로그램 속도가 느린, New Relic에서 찾을 수 있게 되기를 원하는 또는 느린 하는 이유에 대 한 세부 정보로 이동 하려면 로그를 되 찾을 수 있게 되기를 원하는 경험, 한 다음 모든 원격 분석 서비스 하 고 유효성을 검사 합니다.

### <a name="use-an-ilogger-interface"></a>ILogger 인터페이스를 사용 하 여

권장 되는 방식이 프로덕션 응용 프로그램을 만들 때 수행 하는 간단한을 만드는 것입니다 *ILogger* 인터페이스와 몇 가지 방법을에 집중 합니다. 이렇게 하면 쉽게 로깅 구현을 나중에 변경 하 여 모든 코드를 진행할 필요가 없습니다. 사용할 수 있습니다는 `System.Diagnostics.Trace` 수정 응용 프로그램 전체에서 클래스 하지만 대신 사용 구현 하는 로깅 클래스에서 내부적 *ILogger*, 하도록 및 *ILogger* 전체에서 메서드 호출 응용 프로그램입니다.

이런 방식으로 로깅을 보다 다양 하 고 확인 하려는 경우 바꾸면 [ `System.Diagnostics.Trace` ](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs) 원하는 로깅 메커니즘을 사용 합니다. 예를 들어 앱이 늘어남에 수도 있습니다와 같은 보다 포괄적인 로깅 패키지를 사용 하려면 [NLog](http://nlog-project.org/) 또는 [Enterprise Library 로깅 응용 프로그램 블록](https://msdn.microsoft.com/en-us/library/dn440731(v=pandp.60).aspx)합니다. ([Log4Net](http://logging.apache.org/log4net/) 다른 인기 있는 로깅 프레임 워크 이지만 비동기 로깅을 수행 하지 않습니다.)

NLog 등의 프레임 워크를 사용 하기 위한 한 가지 가능한 이유는 별도 대용량 및 우선 순위가 높은 데이터 저장소에 로그 출력을 나누는 용이 것입니다. 효율적으로 많은 양의 ACT 데이터에 대 한 빠른 액세스를 유지 하면서,에 대 한 빠른 쿼리를 실행할 필요가 없는 INFORM 데이터를 저장할 수 있습니다.

### <a name="semantic-logging"></a>의미 체계 로깅

보다 유용한 진단 정보를 생성할 수 있는 로깅 작업을 수행 하는 비교적 새로운 방법을 참조 하세요. [엔터프라이즈 라이브러리 의미 체계 로깅 응용 프로그램 블록 (조각)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)합니다. 조각에 사용 하 여 [Windows 용 이벤트 추적](https://msdn.microsoft.com/en-us/library/windows/desktop/bb968803.aspx) (ETW) 및 [EventSource](https://msdn.microsoft.com/en-us/library/system.diagnostics.tracing.eventsource.aspx) 구조화 되 고 쿼리할 수에 대 한 더 많은 로그를 만들 수 있도록.NET 4.5를 지원 합니다. 각 유형의 작성 정보를 사용자 지정할 수 있는 로그, 이벤트에 대 한 다른 메서드를 정의 합니다. 예를 들어, 호출할 수 있는 SQL 데이터베이스 오류를 기록 하는 `LogSQLDatabaseError` 메서드. 해당 유형의 예외에 대 한 주요 정보는 오류 번호 메서드 시그니처의 오류 번호 매개 변수를 포함 하 고 작성 하는 로그 레코드의 필드로 별도 오류 번호를 기록 수 있도록 하는 것이 알아보았습니다. 별도의 필드 번호는 하므로 보다는 메시지 문자열에 오류 번호를 방금 연결 된 경우에 SQL 오류 번호를 기반으로 보고서 보다 쉽고 안정적으로 얻을 수 있습니다.

## <a name="logging-in-the-fix-it-app"></a>수정 프로그램에 로깅 응용 프로그램

### <a name="the-ilogger-interface"></a>ILogger 인터페이스

다음은 *ILogger* 수정 응용 프로그램에 대 한 인터페이스입니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

이러한 메서드를 사용 하면에서 지 원하는 같은 네 가지 수준에서 로그를 쓰지 *System.Diagnostics*합니다. TraceApi 메서드 외부 서비스 호출 대기 시간에 대 한 정보를 사용 하 여 로깅에 대 한는입니다. 디버그/자세한 정보 표시 수준에 대 한 메서드의 집합을 추가할 수도 있습니다.

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>ILogger 인터페이스의로 거 구현

인터페이스의 구현을 매우 간단 합니다. 기본적으로 바로 호출 표준으로 *System.Diagnostics* 메서드. 다음 코드 조각 정보 방법 중 세 가지 모두와 각 하나는 다른 인스턴스의 보여 줍니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>ILogger 메서드 호출

호출 될 때마다 된 예외를 catch 하는 수정 앱에서 코드를 있는 *ILogger* 예외 세부 정보를 기록 하는 메서드. 및 데이터베이스, Blob 서비스 또는 REST API에 대 한 호출을 수행할 때마다 호출 전에 스톱 워치 시작, 서비스가 반환 될 때 초시계를 중지 하 고 성공 또는 실패에 대 한 정보와 함께 경과 시간을 기록 합니다.

로그 메시지 클래스 이름과 메서드 이름에 포함 되도록 확인 합니다. 로그 메시지는 응용 프로그램 코드의 어떤 부분이 작성 식별 하는지 확인 하는 것이 좋습니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

이제 수정 앱 SQL 데이터베이스에 대 한 호출을 수행한 때마다에 대 한 메서드를 호출한 호출을 확인할 수 있습니다 및 걸린 시간을 얼마나 정확 하 게 합니다.

![로그에 SQL 데이터베이스 쿼리](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

로그를 통해 찾아보기 이동 하려는 경우 데이터베이스 호출을 수행 하는 시간 변수 인지 확인할 수 있습니다. 정보가 유용할 수 있습니다: 앱이 모든 로그 때문에 시간이 지남에 따라 데이터베이스 서비스는 수행 하는 방식에 과거의 추세를 분석할 수 있습니다. 예를 들어, 대부분의 경우 이러한 서비스를 빠른 될 수 있지만 요청 실패 하거나 하루 중 특정 시간에 응답이 느려질 수 있습니다.

될 때마다 새 파일을 업로드 하는 응용 프로그램 로그에는 하 고 각 파일을 업로드 하는 데 걸린 시간 방식을 정확 하 게 확인할 수 있습니다에 대 한 Blob 서비스 –에 대해 동일한 작업을 수행할 수 있습니다.

![Blob 업로드 로그](monitoring-and-telemetry/_static/image23.png)

양의 코드를 작성 하는 서비스를 호출할 필요 하며 이제 랐 문제 라고 표시 누군가가 때마다 정확히 문제 였습니까, 또는 느리게 실행 하기만 하는 경우에 오류가 발생 했는지 여부가 때마다 몇 줄은 원격 서버에 필요 없이 문제의 원인을 파악할 수도 있고 후 오류가 발생 하 고 다시 만들어야 하 여 로깅을 설정할 수 있습니다.

## <a name="dependency-injection-in-the-fix-it-app"></a>종속성 주입 수정 프로그램에이 응용 프로그램

위에 나와 있는 예제에서 리포지토리 생성자를 가져오는 방식이 결정로 거 인터페이스 구현 지 궁금할 수도 있습니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

응용 프로그램 구현에 인터페이스를 연결 하기 위해 사용 [종속성 주입](http://en.wikipedia.org/wiki/Dependency_injection)(DI)와 [AutoFac](http://autofac.org/)합니다. DI를 사용 하면 여러 위치에 코드 전체의 인터페이스에 따라 개체를 사용 하 고을 한 곳에서 인터페이스를 인스턴스화할 때 사용 되는 구현을 지정 수 있습니다. 이렇게 하면 구현을 변경 쉽게: 예를 들어 System.Diagnostics로 거는 NLog로 거로 대체 수 있습니다. 또는 자동화 된 테스트에 대 한로 거 모의 버전으로 대체 하려는 수 있습니다.

수정 응용 프로그램의 모든 컨트롤러 및 모든 저장소는 DI를 사용합니다. 컨트롤러 클래스의 생성자를 가져오기는 *ITaskRepository* 인터페이스 동일한 방식으로 저장소로 거 인터페이스를 가져옵니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

응용 프로그램을 자동으로 제공할 AutoFac DI 라이브러리를 사용 하 여 *TaskRepository* 및 *로 거* 이러한 생성자에 대 한 인스턴스.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

이 코드는 기본적으로 아무 곳 이나 생성자가 필요 함을 표시는 *ILogger* 인터페이스의 인스턴스를 전달는 *로 거* 클래스와 필요한 때마다는 *IFixItTaskRepository*인터페이스의 인스턴스를 전달는 *FixItTaskRepository* 클래스입니다.

[AutoFac](http://autofac.org/) 사용할 수 있는 많은 종속성 주입 프레임 워크 중 하나입니다. 다른 인기 있는 트랜잭션이 [Unity](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx), 권장 하며 Microsoft Patterns and Practices에서 지원 합니다.

## <a name="built-in-logging-support-in-azure"></a>Azure의 기본 제공 로깅 지원

Azure 지원 다음과 같은 종류의 [Azure 앱 서비스에서 웹 앱에 대 한 로깅을](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio):

- System.Diagnostics 추적 (설정 및 해제 하 고 설정할 수 수준 즉석에서 사이트를 다시 시작 하지 않고).
- Windows 이벤트입니다.
- IIS 로그 (HTTP/FREB)입니다.

Azure 지원 다음과 같은 종류의 [클라우드 서비스에서 로깅](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics):

- System.Diagnostics 추적 합니다.
- 성능 카운터입니다.
- Windows 이벤트입니다.
- IIS 로그 (HTTP/FREB)입니다.
- 사용자 지정 디렉터리를 모니터링 합니다.

수정 응용 프로그램에서는 System.Diagnostics 추적을 사용 합니다. 포털에서 스위치를 대칭 이동 또는 REST API를 호출 하는 웹 앱에 로그인 하는 System.Diagnostics를 사용 하도록 설정 하기 위해 수행 해야 됩니다. 포털에서 클릭는 **구성** 사이트에 대 한 탭을 보기 위해 아래로 스크롤해야는 **Application Diagnostics** 섹션. 로깅을 설정 하거나 해제 하 고 원하는 로깅 수준을 선택할 수 있습니다. 저장소 계정 또는 파일 시스템에 로그를 작성 하는 Azure를 사용할 수 있습니다.

![App 진단 및 사이트 진단 구성 탭에](monitoring-and-telemetry/_static/image24.png)

Azure에 로그인을 활성화 한 후에 만들어지는 경우 Visual Studio 출력 창에서 로그를 볼 수 있습니다.

![스트리밍 로그 메뉴](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/en-us/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![스트리밍 로그 메뉴](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/en-us/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

수 또한 로그를 저장소 계정에 기록 하 고 보기 있는 도구 하나를 사용 하 여 Azure 저장소 테이블 서비스에 같은 액세스할 수 **서버 탐색기** Visual Studio에서 또는 [Azure 저장소 탐색기](https://azure.microsoft.com/features/storage-explorer/)합니다.

![서버 탐색기에서 로그](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/en-us/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>요약

정말 간단 하 게 기본적으로 원격 분석 시스템을 구현, 로그인 사용자 코드를 계측 하 고 Azure에서 로깅 구성 됩니다. 및 프로덕션 문제를 사용 하는 경우 원격 분석 시스템 및 사용자 지정 로그의 조합 하면이 고객에 대 한 중요 한 문제를 해지기 전에 문제를 신속 하 게 해결 합니다.

에 [다음 장에서](transient-fault-handling.md) 프로덕션 문제를 조사 해야 할 수 있는 상태가 하지 않는 일시적인 오류를 처리 하는 방법을 살펴보겠습니다.

## <a name="resources"></a>리소스

자세한 내용은 다음 리소스를 참조하세요.

원격 분석에 대 한 주로 설명서:

- [Microsoft Patterns and Practices-Azure 지침](https://msdn.microsoft.com/en-us/library/dn568099.aspx)합니다. 계측 및 원격 분석 지침, 지침 서비스 계량, 상태 끝점 모니터링 패턴 및 런타임 재구성 패턴을 참조 하십시오.
- [클라우드에서 모으는 금액: New Relic 성능 Azure 웹 사이트에 대 한 모니터링을 사용 하도록 설정](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx)합니다.
- [Azure 클라우드 서비스에서 대규모 서비스를 디자인에 대 한 유용한](https://msdn.microsoft.com/en-us/library/windowsazure/jj717232.aspx)합니다. 백서: Mark Simms 및 Michael Thomassy 합니다. 원격 분석 및 진단 섹션을 참조 하십시오.
- [Application Insights 사용한 개발 Next-generation](https://msdn.microsoft.com/en-us/magazine/dn683794.aspx)합니다. MSDN Magazine 문서입니다.

로깅에 대 한 주로 설명서:

- [의미 체계 로깅 응용 프로그램 블록 (조각)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)합니다. Neil Mackenzie 조각 된 의미 체계 로깅에 대 한 사례를 표시합니다.
- [의미 체계 로깅을 사용 하 여 구조화 되 고 의미 있는 로그 만들기](https://channel9.msdn.com/Events/Build/2013/3-336)합니다. (비디오) 율리우스력 Dominguez 조각 된 의미 체계 로깅에 대 한 사례를 표시합니다.
- [EF6 SQL 로깅-1 부: 간단한 로깅](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/)합니다. Arthur Vickers EF 6에서 Entity Framework에서 실행 되는 쿼리를 기록 하는 방법을 보여 줍니다.
- [연결 복원 력 및 ASP.NET MVC 응용 프로그램에서 Entity Framework와 함께 명령 인터 셉 션](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)합니다. 네 번째 9 개 부분으로 이루어진 자습서 시리즈의 Entity Framework에서 데이터베이스에 전송 되는 SQL 명령을 기록 하도록 EF 6 명령 인터 셉 션 기능을 사용 하는 방법을 보여 줍니다.
- [C# 5.0 호출자 정보 특성을 사용 하 여 로깅을 향상](http://www.dotnetcurry.com/showarticle.aspx?ID=972)합니다. 쉽게에 하드 코딩 것 리터럴 또는 수동으로 가져오도록 하는 데 리플렉션을 사용 하지 않고 호출 메서드의 이름의 기록 하는 방법.

문제 해결에 대 한 주로 설명서:

- [Azure 문제 해결 &amp; 블로그 디버깅](https://blogs.msdn.com/b/kwill/)합니다.
- [AzureTools –는 진단 유틸리티는 Azure 개발자 지원 팀에서 사용 하는](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true)합니다. 소개 하 고 다운로드 하 고 다양 한 모니터링 및 진단 도구를 실행 하는 Azure VM에서 사용할 수 있는 도구에 대 한 다운로드 링크를 제공 합니다. 특정 VM에 대 한 문제를 진단 해야 하는 경우 유용 합니다.
- [Visual Studio를 사용 하 여 Azure 앱 서비스의 웹 앱의 문제를 해결](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)합니다. System.Diagnostics 추적 및 원격 디버깅 시작 하기 위한 단계별 자습서입니다.

비디오:

- [FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms 하 여 시리즈를 9 개 부분으로 구성 합니다. 고급 개념 및 아키텍처 원칙 매우 액세스 가능 하 고 흥미로운 방법으로 스토리 실제 고객과 Microsoft 고객 자문 팀 (CAT) 환경에서 가져온 것으로 표시 합니다. 4-9 에피소드는 모니터링 및 원격 분석입니다. 9 에피소드 MetricsHub, AppDynamics, New Relic 및 PagerDuty 서비스 모니터링의 개요를 포함 합니다.
- [건물 큰: Azure 고객-2 부에서에서 확인 된 사항을](https://channel9.msdn.com/Events/Build/2012/3-030)합니다. Mark Simms 실패에 대 한 디자인 하 고 모든 항목을 계측 하는 방법에 대 한 설명입니다. 유사 Failsafe 시리즈 하지만 방법 더 세부적으로 이동 합니다.

코드 샘플:

- [클라우드 서비스 기본 사항 Azure에서](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)합니다. Microsoft Azure 고객 자문 팀에서 만든 샘플 응용 프로그램입니다. 다음 문서에 설명 된 대로 원격 분석 및 로깅 사례를 모두 보여 줍니다. 이 샘플은 응용 프로그램 로깅을 사용 하 여 구현 [NLog](http://nlog-project.org/)합니다. 관련된 문서에 대 한 참조는 [일련의 원격 분석 및 로깅에 대 한 TechNet wiki 문서를 4 개의](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon)합니다.

>[!div class="step-by-step"]
[이전](design-to-survive-failures.md)
[다음](transient-fault-handling.md)
