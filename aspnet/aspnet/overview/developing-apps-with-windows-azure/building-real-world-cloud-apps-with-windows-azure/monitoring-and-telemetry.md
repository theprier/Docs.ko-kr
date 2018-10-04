---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
title: 모니터링 및 원격 분석 (실제 클라우드 앱 빌드 azure) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드 앱 빌드 Azure 전자책을 사용 하 여 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴과 그을 수 있는 방법을 설명 하는 중...
ms.author: riande
ms.date: 07/09/2015
ms.assetid: 7e986ab5-6615-4638-add7-4614ce7b51db
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry
msc.type: authoredcontent
ms.openlocfilehash: f4dae827627103e5cfb9981b6c3b9342cdc34c13
ms.sourcegitcommit: 7b4e3936feacb1a8fcea7802aab3e2ea9c8af5b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48578005"
---
<a name="monitoring-and-telemetry-building-real-world-cloud-apps-with-azure"></a>모니터링 및 원격 분석 (Azure 사용 하 여 빌드 실제 클라우드 앱)
====================
하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 합니다 **실제 세계 클라우드 앱 빌드 Azure** 전자책 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴 설명 하 고 도움이 될 수 있는 사례 성공적인 클라우드를 위한 웹 앱을 개발할 수 있습니다. 전자책에 대 한 정보를 참조 하세요 [첫 번째 장에서](introduction.md)합니다.


많은 사람들이 자신의 응용 프로그램 종료 되는 경우 알 수 있도록 하는 고객에 게 사용 합니다. 실제로 모범 사례 없는 섹션과 어디서 나 클라우드에서입니다. 빠른 알림 보장이 및 종종 내용에 대 한 최소 또는 잘못 된 데이터를 가져올 때 알림을 받을 수행 수에 합니다. 분석과 로깅 시스템이 수 있습니다 것의 경우 및 앱을 사용 하 여 문제가 발생할 바로 확인 하 고 유용한 문제 해결 정보를 사용 하 여 합니다.

## <a name="buy-or-rent-a-telemetry-solution"></a>구입 또는 원격 분석 솔루션도 임대

> [!NOTE]
> 이 문서에서는 되기 전에 작성 된 [Application Insights](/azure/application-insights/app-insights-overview) 출시 되었습니다. Application Insights는 Azure에서 원격 분석 솔루션에 대 한 기본 방법입니다. 참조 [ASP.NET 웹 사이트에 대 한 Application Insights 설정](/azure/application-insights/app-insights-asp-net) 자세한 내용은 합니다.


클라우드 환경에 대 한 훌륭한 것 중 하나는 쉽게 구입 하거나 임대 승리 하는 것입니다. 원격 분석은 예제입니다. 많은 노력 없이 작동 및 실행, 비용 효율적으로 매우 좋은 원격 분석 시스템을 가져올 수 있습니다. Azure와 통합 되는 뛰어난 파트너는 여러 있고 일부는 무료 계층으로 아무 작업도 수행에 대 한 기본 원격 분석을 얻을 수 있습니다. Azure에서 현재 사용할 수 중 일부에 불과합니다가 같습니다.

- [New Relic](http://newrelic.com/)
- [AppDynamics](http://www.appdynamics.com/)
- [Dynatrace](https://datamarket.azure.com/application/b4011de2-1212-4375-9211-e882766121ff)

[Microsoft System Center](http://www.petri.co.il/microsoft-system-center-introduction.htm#) 도 모니터링 기능을 포함 합니다.

New Relic 얼마나 수 있는지는 원격 분석 시스템을 사용 하 여 표시할 설정를 신속 하 게 살펴보겠습니다.

Azure 관리 포털에서 서비스에 등록 합니다. 클릭 **새로 만들기**를 클릭 하 고 **스토어**합니다. 합니다 **추가 기능 선택** 대화 상자가 나타납니다. 아래로 스크롤하여 클릭 **New Relic**합니다.

![추가 기능 선택](monitoring-and-telemetry/_static/image1.png)

오른쪽 화살표를 클릭 하 고 서비스 계층을 선택 합니다. 이 데모에 대 한 무료 계층을 사용 하겠습니다.

![추가 기능 개인 설정](monitoring-and-telemetry/_static/image2.png)

오른쪽 화살표를 클릭 하 고 "구매"를 확인 합니다. New Relic 이제 포털에서 추가 기능으로 나타납니다.

![구입 검토](monitoring-and-telemetry/_static/image3.png)

![관리 포털에서 새 Relic 추가 기능](monitoring-and-telemetry/_static/image4.png)

클릭 **연결 정보**, 라이선스 키를 복사 합니다.

![연결 정보입니다.](monitoring-and-telemetry/_static/image5.png)

로 이동 합니다 **구성** 포털에서 웹 앱 설정에 대 한 탭 **성능 모니터링** 에 **추가 기능**, 설정 및 합니다 **추가 기능 선택** 드롭다운 목록을 **New Relic**합니다. 누른 **저장할**합니다.

![구성 탭에서 새 Relic](monitoring-and-telemetry/_static/image6.png)

Visual Studio에서 앱에서 New Relic NuGet 패키지를 설치 합니다.

![구성 탭에서 개발자 분석](monitoring-and-telemetry/_static/image7.png)

Azure에 앱을 배포 하 고 사용 하 여 시작 합니다. New Relic 모니터링에 대 한 몇 가지 작업을 제공 하는 몇 가지 Fix It 작업을 만듭니다.

로 다시 이동 합니다 **New Relic** 페이지에 **추가 기능** 탭 포털을 클릭 **관리**. 포털을 사용 하 여 single sign on 인증에 대 한 자격 증명을 다시 입력 하지 않아도 되므로 New Relic 관리 포털로 전송 합니다. 개요 페이지는 다양 한 성능 통계를 표시합니다. (개요 페이지 전체 크기로 보려면 이미지를 클릭 합니다.)

[![새 Relic 모니터링 탭](monitoring-and-telemetry/_static/image9.png)](monitoring-and-telemetry/_static/image8.png)

다음은 몇 가지 통계를 볼 수 있습니다.

- 하루 중 서로 다른 시간에 대 한 평균 응답 시간입니다.

    ![응답 시간](monitoring-and-telemetry/_static/image10.png)
- 하루 중 서로 다른 시간에 처리량 속도 (분당 요청 수)에 있습니다.

    ![처리량](monitoring-and-telemetry/_static/image11.png)
- 다른 HTTP 요청을 처리 하는 데 걸린 서버 CPU 시간입니다.

    ![웹 트랜잭션 제한 시간](monitoring-and-telemetry/_static/image12.png)
- 응용 프로그램 코드의 다른 부분에 소요 된 CPU 시간:

    ![추적 세부 정보](monitoring-and-telemetry/_static/image13.png)
- 성능 기록 통계입니다.

    ![성능 기록](monitoring-and-telemetry/_static/image14.png)
- Blob service 및 신뢰할 수 있는 방법과 응답에 대 한 통계와 같은 외부 서비스에 대 한 호출 서비스가 되었습니다.

    ![외부 서비스](monitoring-and-telemetry/_static/image15.png)

    ![외부 서비스](monitoring-and-telemetry/_static/image16.png)

    ![외부 서비스](monitoring-and-telemetry/_static/image17.png)
- 세계 지도나 미국 웹 앱에서 트래픽이 발생 한 위치에서 위치에 대 한 정보입니다.

    ![지리](monitoring-and-telemetry/_static/image18.png)

보고서 및 이벤트를 설정할 수 있습니다. 예를 들어, 오류를 표시 하는 것이 먼저 언제 든 지 말할 하, 문제에 대 한 경고 지원부에 전자 메일을 보낼 수 있습니다.

![보고서](monitoring-and-telemetry/_static/image19.png)

New Relic은 원격 분석 시스템;의 한 예 다른 서비스에서이 모든 데이터를 가져올 수 있습니다. 클라우드에서의 장점은 모든 코드를 작성 하지 않고도 한 최소 없는 비용 갑자기 가져올 수도 있고 응용 프로그램이 어떻게 사용 되 고 새로운 고객에 게 실제로 발생 하는 방법에 대 한 다양 한 추가 정보.

<a id="log"></a>
## <a name="log-for-insight"></a>로그에서 insight

원격 분석 패키지는 첫 단계로 유용 하지만 여전히 사용자 고유의 코드를 계측 해야 합니다. 원격 분석 서비스를 알려는 문제가 발생할 때 대상을 지정 하 고 고객을 발생 하지만 하지을 줄 수는 많은 코드에서 것에 대 한 정보입니다.

앱 수행 하는 참조를 프로덕션 서버에 원격 않아도 원하지입니다. 될 수 있는 실용적인 하나의 서버 적지 하지만 수백 대의 서버에 크기를 조정한 및를 원격으로 연결 해야 하는 것을 알 수 없는 경우에 어떨까요? 로깅이 필요가 원격 분석 및 디버그를 프로덕션 서버에는 충분 한 정보를 제공 해야 문제입니다. 해야 로깅하려 충분 한 정보 로그를 통해서만 문제를 격리할 수 있도록 합니다.

### <a name="log-in-production"></a>프로덕션 환경에 로그인

많은 사람들이 문제가 발생 하 고 디버그 하려는 경우에 프로덕션 환경에서 추적을 설정 합니다. 이 문제를 알고 시간과 대 한 유용한 문제 해결 정보를 표시 하는 시간 사이 상당한 지연이 발생할 수 있습니다. 및 표시 정보를 일시적인 오류에 대 한 도움이 되지 않을 수 있습니다.

저장소는 저렴 한 클라우드 환경에서 권장 사항는 항상 그대로 두는 프로덕션 환경에 로그온 합니다. 시간이 지남에 따라 개발 하거나 서로 다른 시간에 정기적으로 발생 하는 문제를 분석 하면 이미 기록 하 고 도움이 되는 기록 데이터가 있는 오류가 발생 한 경우 이렇게 합니다. 이전 로그를 삭제 하려면 제거 프로세스를 자동화할 수 있지만 로그를 유지 하는 것 보다 이러한 프로세스를 설정 하는 데 더 임을 볼 수 있습니다.

로깅의 비용 추가 시간과 비용을 모두 필요한 문제가 발생 하는 경우 이미 사용할 수 있는 정보를 포함 하 여 저장할 수 있습니다 문제 해결에 비해 간단 합니다. 그런 다음 나타나면 사용자가 가졌던 임의 오류가 잠시 약 8:00 어젯밤, 하지만 오류를 기억 하지 못하는 것을 확인할 수 있습니다 쉽게 문제를 확인 합니다.

$ 4 보다 작거나 한편으로 50gb의 로그를 유지할 수 있습니다 하 고 로깅 성능에 미치는 간단 염두-성능 병목 현상을 방지 하려면 로깅 라이브러리 비동기 인지 확인 한 것을 유지 하기만 합니다.

### <a name="differentiate-logs-that-inform-from-logs-that-require-action"></a>작업을 필요로 하는 로그에서 제공 하는 로그를 구분

로그는 게 (하겠습니다 알고) 또는 ACT (원하는 작업을 수행할 수 있습니다) 것입니다. 정말로 작업을 수행 하는 사람 또는 자동화 된 프로세스를 필요로 하는 문제에 대 한 작업 로그를 기록 하는 주의 해야 합니다. ACT 로그 너무 많은 노이즈를 통해 모든 정품 문제를 찾을 수를 조사 하 여 너무 많은 작업이 필요한 만들어집니다. 및 ACT 로그 지원 팀에 전자 메일을 보내는 등 일부 작업에 자동으로 트리거하는 경우 등의 작업을 사용 하는 수천 개의 단일 문제로 인해 트리거될 수 있도록 되지 않도록 합니다.

System.Diagnostics 추적에서 로그 오류, 경고, 정보 및 디버그/Verbose 수준을 할당할 수 있습니다. ACT 로그에 대 한 오류 수준을 예약 게 로그에 대 한 하위 수준을 사용 하 여 게 로그에서 ACT를 쉽게 구분할 수 있습니다.

![로깅 수준](monitoring-and-telemetry/_static/image20.png)

### <a name="configure-logging-levels-at-run-time"></a>런타임 시 로깅 수준 구성

살펴볼 가치가 있습니다 로그온 항상 프로덕션에 있지만, 다른 모범 사례 런타임 시 다시 배포 하거나 응용 프로그램을 다시 시작 하지 않고, 로깅하려는 정보의 수준을 조정할 수 있도록 로깅 프레임 워크를 구현 하는 것입니다. 추적 기능을 사용 하면 예를 들어 `System.Diagnostics` 디버그/자세한 정보 표시 로그 및 오류, 경고, 정보를 만들 수 있습니다. 항상 오류, 경고, 로그 및 프로덕션 환경에서 정보를 기록에서 상황별으로 문제 해결에 대 한 디버그/자세한 정보 표시 로깅을 동적으로 추가할 수 하려는 것이 좋습니다.

Azure App Service에서 웹 앱에 작성에 대 한 지원이 기본 제공 `System.Diagnostics` 파일 시스템, 테이블 저장소 또는 Blob storage에 로그 합니다. 각 저장소 대상에 대 한 다양 한 로깅 수준을 선택할 수 있으며 응용 프로그램을 다시 시작할 필요 없이 즉석에서 로깅 수준을 변경할 수 있습니다. Blob 저장소 지원 쉽게 실행 [HDInsight](https://docs.microsoft.com/azure/hdinsight/) HDInsight는 Blob 저장소를 직접 사용 하는 방법을 알고 있기 때문에 분석 응용 프로그램 로그에서 작업 합니다.

### <a name="log-exceptions"></a>예외 기록

방금 두지 *예외입니다. Tostring ()* 로깅 코드에 있습니다. 컨텍스트 정보는 유지합니다. SQL 오류의 경우 SQL 오류 번호 남깁니다. 모든 예외에 대 한 컨텍스트 정보, 자체 예외 및 문제 해결을 위해 필요한 모든 제공 된 되도록 내부 예외를 포함 합니다. 예를 들어, 서버 이름, 트랜잭션 식별자를 및 사용자 이름 (하지만 하지 암호 또는 암호!) 컨텍스트 정보가 포함 될 수 있습니다.

로깅 예외를 사용 하 여 올바른 작업을 수행 하 여 각 개발자가 의존 하는 경우 그 중 일부에 없습니다. 수행 되는지 함께 볼까요 오른쪽 방식으로 모든 시간을 보장 하려면 예외로 거 인터페이스에 바로 처리 빌드:로 거 클래스 자체 예외 개체를 전달 하 고로 거 클래스의 예외 데이터를 제대로 기록 합니다.

### <a name="log-calls-to-services"></a>서비스에 대 한 로그 호출

데이터베이스 또는 REST API 또는 외부 서비스 인지 앱 서비스에 호출 될 때마다 로그를 작성 하는 것이 좋습니다. 성공 또는 실패 하지만 각 요청에 걸린 표시 뿐 아니라 로그에 포함 됩니다. 클라우드 환경에서 전체 중단 하지 않고 시간이 오래 걸리지와 관련 된 문제를 종종 표시 됩니다. 갑자기 초당 수행을 시작할 수 일반적으로 10 시간 (밀리초)을 사용 하는 것입니다. 사용자가 앱이 알려 느린, New Relic에서 검색할 수 있게 되기를 원하는 때나 사용자 고유의 로그가 느린 이유의 세부 정보에 자세히 알아보기를 검색할 수 있게 되기를 원하는 경험, 한 다음 모든 원격 분석 서비스가 있고의 유효성을 검사 합니다.

### <a name="use-an-ilogger-interface"></a>ILogger 인터페이스를 사용 합니다.

간단한을 만들 때 권장 되는 방식이 프로덕션 응용 프로그램을 만들 때 수행 *ILogger* 인터페이스 및 그 안에 몇 가지 메서드를 그대로 유지 합니다. 이렇게 하면 쉽게 나중의 로깅 구현을 변경 하 고 작업을 수행 하 여 모든 코드를 통해 이동 하지 않아도 됩니다. 우리가 사용 하는 `System.Diagnostics.Trace` Fix It 앱 전체에서 클래스 하지만 대신 사용 하 고이 구현 하는 로깅 클래스에서 내부적 *ILogger*, 하며 *ILogger* 전체 메서드를 호출 앱입니다.

이런 방식으로 로깅을 풍부 하며 확인 하려는 경우 바꾸면 [ `System.Diagnostics.Trace` ](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio#apptracelogs) 원하는 모든 로깅 메커니즘을 사용 하 여 합니다. 예를 들어 앱이 커지면 수도 있습니다와 같은 보다 포괄적인 로깅 패키지를 사용 하려는 [NLog](http://nlog-project.org/) 하거나 [엔터프라이즈 라이브러리 Logging Application Block](https://msdn.microsoft.com/library/dn440731(v=pandp.60).aspx)합니다. ([Log4Net](http://logging.apache.org/log4net/) 다른 인기 있는 로깅 프레임 워크 이지만 비동기 로깅을 수행 하지 않습니다.)

NLog와 같은 프레임 워크를 사용 하는 것이 원인 나누는 것 별도 높은 볼륨 및 높은 가치의 데이터 저장소에 로그 출력을 용이 하 게 됩니다. 효율적으로 볼륨이 큰 ACT 데이터에 대 한 빠른 액세스를 유지 하면서 빠른 쿼리를 실행할 필요가 없는 게 데이터를 저장할 수 있습니다.

### <a name="semantic-logging"></a>의미 체계 로깅

유용한 진단 정보를 생성할 수 있는 로깅 작업을 수행 하는 비교적 새로운 방식으로 참조 [엔터프라이즈 라이브러리 의미 체계 로깅 응용 프로그램 블록 (SLAB)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)합니다. SLAB 사용 [Windows 이벤트 추적에 대 한](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) 및 [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) 구조화 및 쿼리할 수에 대 한 더 많은 로그를 만들 수 있도록.NET 4.5에서를 지원 합니다. 각 유형의 기록한 정보를 사용자 지정할 수 있는 로그를 이벤트에 대 한 다양 한 메서드를 정의 합니다. 예를 들어, 호출할 수 있습니다 하는 SQL Database 오류를 기록 하는 `LogSQLDatabaseError` 메서드. 해당 유형의 예외에 대 한 주요 정보는 오류 번호를 메서드 시그니처에 오류 번호 매개 변수를 포함 하 고 오류 번호를 작성 하는 로그 레코드를 별도 필드로 기록 수 있도록 알 수 있습니다. 수 있는 별도 필드 이므로 보고서 메시지 문자열에 오류 번호를 방금 연결 된 경우 보다 SQL 오류 번호에 따라 더 쉽고 안정적으로 가져올 수 있습니다.

## <a name="logging-in-the-fix-it-app"></a>수정 프로그램에 로깅 앱

### <a name="the-ilogger-interface"></a>ILogger 인터페이스

다음은 *ILogger* Fix It 응용 프로그램의 인터페이스입니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample1.cs)]

이러한 메서드를 사용 하면 지 같은 네 가지 수준에서 로그에 쓸 *System.Diagnostics*합니다. TraceApi 방법이 외부 서비스 호출 대기 시간에 대 한 정보를 사용 하 여 로깅에 대 한 합니다. 디버그/Verbose 수준에 대 한 메서드 집합을 추가할 수도 있습니다.

### <a name="the-logger-implementation-of-the-ilogger-interface"></a>ILogger 인터페이스의로 거 구현

인터페이스의 구현은 매우 간단 합니다. 기본적으로 바로 호출 표준으로 *System.Diagnostics* 메서드. 다음 코드 조각은 세 정보 메서드 중 하나를 각 다른 보여 줍니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample2.cs)]

### <a name="calling-the-ilogger-methods"></a>ILogger 메서드를 호출합니다.

호출 될 때마다 예외를 catch 하는 Fix It 응용 프로그램의 코드에는 *ILogger* 메서드 예외 세부 정보를 기록 합니다. 및 데이터베이스, Blob 서비스 또는 REST API에 대 한 호출을 수행할 때마다 호출 전에 스톱 워치를 시작, 서비스는 반환 될 때 워치를 중지 하 고 성공 또는 실패 하는 방법에 대 한 정보와 함께 경과 된 시간을 기록 합니다.

로그 메시지가 포함 된 클래스 이름과 메서드 이름을 알 수 있습니다. 로그 메시지 작성 응용 프로그램 코드의 어느 부분을 식별 하는지 확인 하는 것이 좋습니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample3.cs?highlight=6,14,20-21,25)]

Fix It 응용 프로그램에 SQL Database에 대 한 호출을 수행 될 때마다, 이제에 대 한 호출을 호출 하는 메서드를 볼 수 있습니다 및 데 걸린 시간 얼마나 정확 하 게 합니다.

![로그에 SQL Database 쿼리](monitoring-and-telemetry/_static/image21.png)

![](monitoring-and-telemetry/_static/image22.png)

로그를 통해 찾아보기 이동 하려는 경우 데이터베이스 호출 소요 시간은 변수는 확인할 수 있습니다. 정보를 유용할 수 있습니다: 앱이 모든 로그 때문에 시간이 지남에 따라 데이터베이스 서비스의 성능을 기록 추세를 분석할 수 있습니다. 예를 들어 대부분의 이러한 서비스를 빨리 처리할 수 있지만 요청이 실패할 수 있습니다 또는 응답 하루 중 특정 시간에 느려질 수 있습니다.

때마다 새 파일을 업로드 하는 앱에서 로그에는 각 파일을 업로드 하는 데 소요 된 시간 정확 하 게 볼 수 있습니다에 대 한 Blob service –에 대해 동일한 작업을 수행할 수 있습니다.

![Blob 업로드 로그](monitoring-and-telemetry/_static/image23.png)

단 두 개의 추가 될 때마다 서비스를 호출 했으며 이제 누군가가 라는 문제에 실행 될 때마다 정확히 어떤 문제를 인지에 관계 없이 오류가 발생 하거나 느리게 실행만 하는 경우에 쓸 코드 줄 것입니다. 원격으로 서버를 연결 하지 않고도 문제의 근원을 수도 있고 오류가 발생 하 고 다시 만들어야 하는 후 로깅을 설정할 수 있습니다.

## <a name="dependency-injection-in-the-fix-it-app"></a>수정 프로그램에 종속성 주입이 앱

위의 예제에서 리포지토리 생성자를 가져오는 방법을 거 인터페이스 구현 궁금할 수 있습니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample4.cs?highlight=6)]

사용 하 여 앱 구현에 인터페이스를 연결 하는 데 [종속성 주입](http://en.wikipedia.org/wiki/Dependency_injection)(DI) 사용 하 여 [AutoFac](http://autofac.org/)합니다. DI를 사용 하면 코드 전체에서 여러 위치에서 인터페이스를 기반으로 개체를 사용 하 고 한 곳에서 인터페이스를 인스턴스화할 때 사용 되는 구현을 지정 수 있습니다. 이 쉽게 구현을 변경: 예를 들어, NLog로 거를 사용 하 여 System.Diagnostics로 거를 대체 수 있습니다. 또는 자동화 된 테스트 하려는 경우을 모의 버전의로 거를 대체 합니다.

Fix It 응용 프로그램의 모든 컨트롤러 및 모든 저장소는 DI를 사용합니다. 컨트롤러 클래스의 생성자를 가져오기는 *ITaskRepository* 인터페이스 동일한 방식으로 저장소로 거 인터페이스를 가져옵니다.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample5.cs?highlight=5)]

앱을 자동으로 제공할 AutoFac DI 라이브러리를 사용 *TaskRepository* 하 고 *로 거* 이러한 생성자에 대 한 인스턴스.

[!code-csharp[Main](monitoring-and-telemetry/samples/sample6.cs?highlight=8,10)]

이 코드는 기본적으로 아무 곳 이나 생성자 해야 라는 *ILogger* 인터페이스의 인스턴스에 전달 합니다 합니다 *로 거* 클래스와 필요할 때마다는 *IFixItTaskRepository*인터페이스를 인스턴스에 전달 합니다 *FixItTaskRepository* 클래스입니다.

[AutoFac](http://autofac.org/) 사용할 수 있는 많은 종속성 주입 프레임 워크 중 하나입니다. 또 다른 인기 있는 것 [Unity](https://blogs.msdn.com/b/agile/archive/2013/08/20/new-guide-dependency-injection-with-unity.aspx)를 권장 하 고 Microsoft Patterns and Practices에서 지원 합니다.

## <a name="built-in-logging-support-in-azure"></a>Azure의 기본 제공 로깅 지원

Azure 지원 다음과 같은 종류의 [Azure App Service에서 웹 앱에 대 한 로깅](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio):

- System.Diagnostics 추적 (설정 및 해제 하 고 설정할 수 수준 즉석에서 사이트를 다시 시작 하지 않고).
- Windows 이벤트입니다.
- IIS 로그 (HTTP/FREB)입니다.

Azure 지원 다음과 같은 종류의 [Cloud Services의 로깅](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics):

- System.Diagnostics 추적 합니다.
- 성능 카운터입니다.
- Windows 이벤트입니다.
- IIS 로그 (HTTP/FREB)입니다.
- 사용자 지정 디렉터리를 모니터링 합니다.

Fix It 앱 System.Diagnostics 추적을 사용합니다. 포털에서 스위치를 대칭 이동 또는 REST API를 호출할 웹 앱 로그인 System.Diagnostics를 사용 하도록 설정 하기 위해 수행 해야 됩니다. 포털에서 클릭 합니다 **구성** 사이트에 대 한 탭을 보려면 아래로 스크롤하여 합니다 **Application Diagnostics** 섹션. 로깅 켜기 / 끄기 수 있으며 원하는 로깅 수준을 선택할 수 있습니다. 저장소 계정 또는 파일 시스템에 로그를 작성 하는 Azure를 사용할 수 있습니다.

![앱 진단 및 구성 탭에서 사이트 진단](monitoring-and-telemetry/_static/image24.png)

Azure 로그인을 활성화 한 후에 만들 때 Visual Studio 출력 창에서 로그를 볼 수 있습니다.

![스트리밍 로그 메뉴](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-viewlogsmenu.png)

![스트리밍 로그 메뉴](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-nologsyet.png)

저장소 계정에 기록 된 로그도 있을 수 있으며 뷰는 도구 하나를 사용 하 여 Azure Storage Table service를 같은 액세스할 수 있습니다 **서버 탐색기** Visual Studio에서 또는 [Azure Storage 탐색기](https://azure.microsoft.com/features/storage-explorer/)합니다.

![서버 탐색기에서 로그](http://wacomdpsstorage.blob.core.windows.net/articlesmedia/content-ppe.windowsazure.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/20140115062810/tws-storagelogs.png)

## <a name="summary"></a>요약

실제로,의 기본 원격 분석 시스템을 구현 하 고, 사용자 고유의 코드에서 로깅 계측 하 고, Azure에서 로깅 구성 하는 것이 간단 합니다. 및 프로덕션 문제 경우 원격 분석 시스템 및 사용자 지정 로그의 조합에서는 고객에 게 중요 한 문제를 해지기 전에 문제를 신속 하 게 해결 합니다.

에 [다음 장에서](transient-fault-handling.md) 프로덕션 문제를 조사 해야 할 수 있는 상태가 없는 일시적인 오류를 처리 하는 방법을 살펴보겠습니다.

## <a name="resources"></a>자료

자세한 내용은 다음 리소스를 참조하세요.

원격 분석에 대 한 주로 설명서:

- [Microsoft Patterns and Practices-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx)합니다. 계측 및 원격 분석 지침, 서비스 계량 지침, 상태 끝점 모니터링 패턴 및 런타임 재구성 패턴을 참조 하세요.
- [클라우드에서 펴서 무장관: 새 Relic 성능 Azure Websites에서 모니터링을 사용 하도록 설정 하면](http://www.hanselman.com/blog/PennyPinchingInTheCloudEnablingNewRelicPerformanceMonitoringOnWindowsAzureWebsites.aspx)합니다.
- [Azure Cloud Services에서 대규모 서비스 설계를 위한 모범 사례](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)합니다. Mark Simms 및 Michael Thomassy 백서입니다. 원격 분석 및 진단 섹션을 참조 하세요.
- [Application Insights 사용 하 여 차세대 개발](https://msdn.microsoft.com/magazine/dn683794.aspx)합니다. MSDN Magazine 기사입니다.

주로 로깅에 대 한 설명서:

- [응용 프로그램 블록 의미 체계 로깅 (SLAB)](http://convective.wordpress.com/2013/08/12/semantic-logging-application-block-slab/)합니다. Neil Mackenzie SLAB 사용 하 여 의미 체계 로깅에 대 한 사례를 제공합니다.
- [의미 체계 로깅을 사용 하 여 구조화 된 하 고 의미 있는 로그를 만드는](https://channel9.msdn.com/Events/Build/2013/3-336)합니다. (비디오) 율리우스력 Dominguez SLAB 사용 하 여 의미 체계 로깅에 대 한 사례를 제공합니다.
- [EF6 SQL 로깅-1 부: 간단한 로깅](http://blog.oneunicorn.com/2013/05/08/ef6-sql-logging-part-1-simple-logging/)합니다. Arthur Vickers EF 6에서 Entity Framework에서 실행 되는 쿼리를 기록 하는 방법을 보여 줍니다.
- [연결 복원 력 및 명령 인터 셉 션 ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)입니다. 네 번째 9 부 자습서 시리즈에서는 EF 6 명령 인터 셉 션 기능을 사용 하 여 Entity Framework에서 데이터베이스에 전송 하는 SQL 명령을 기록 하는 방법을 보여 줍니다.
- [C# 5.0 호출자 정보 특성을 사용 하 여 로깅을 개선](http://www.dotnetcurry.com/showarticle.aspx?ID=972)합니다. 에 하드 코딩 하 리터럴 또는 리플렉션을 사용 하 여 수동으로 되도록 하지 않고 호출 메서드의 이름을 쉽게 로깅할 방법입니다.

문제 해결에 대 한 주로 설명서:

- [Azure 문제 해결 &amp; 블로그를 디버깅](https://blogs.msdn.com/b/kwill/)합니다.
- [AzureTools – 진단 유틸리티를 Azure 개발자 지원 팀에서 사용 하는](https://blogs.msdn.com/b/kwill/archive/2013/08/26/azuretools-the-diagnostic-utility-used-by-the-windows-azure-developer-support-team.aspx?Redirected=true)합니다. 소개 하 고 다운로드 하 고 다양 한 모니터링 및 진단 도구를 실행 하는 Azure VM에서 사용할 수 있는 도구에 대 한 다운로드 링크를 제공 합니다. 특정 VM의 문제를 진단 해야 하는 경우 유용 합니다.
- [Visual Studio를 사용 하 여 Azure App Service에서 웹 앱 문제 해결](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)합니다. System.Diagnostics 추적 및 원격 디버깅을 시작 하기 위한 단계별 자습서입니다.

비디오:

- [FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는 데](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms에서 9 부 시리즈입니다. 고급 개념 및 아키텍처 원칙으로 실제 고객의 Microsoft 고객 자문 팀 (CAT) 환경에서 가져온 스토리를 사용 하 여 액세스 가능 하 고 흥미로운 방식으로 표시 합니다. 4-9 에피소드는 모니터링 및 원격 분석 하려고 합니다. 9 에피소드 MetricsHub, AppDynamics, New Relic 및 PagerDuty 서비스 모니터링의 개요를 포함 합니다.
- [빌드 큰: Azure 고객에 게-부에서에서 Lessons learned](https://channel9.msdn.com/Events/Build/2012/3-030)합니다. Mark Simms 실패에 대 한 디자인 및 모든 계측에 대해 설명 합니다. 비슷하지만 Failsafe 시리즈 자세한 방법 세부 정보로 이동 합니다.

코드 샘플:

- [Azure에서 서비스 기본 사항 클라우드](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)합니다. Microsoft Azure 고객 자문 팀에서 만든 샘플 응용 프로그램입니다. 다음 문서에 설명 된 대로 원격 분석 및 로깅 사례를 보여 줍니다. 샘플을 사용 하 여 응용 프로그램 로깅 구현 [NLog](http://nlog-project.org/)합니다. 관련된 설명서에 대 한 참조를 [일련의 원격 분석 및 로깅에 대 한 네 가지 TechNet wiki 문서](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx#Telemetry_coming_soon)합니다.

> [!div class="step-by-step"]
> [이전](design-to-survive-failures.md)
> [다음](transient-fault-handling.md)
