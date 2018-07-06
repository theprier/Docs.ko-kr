---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
title: 일시적인 오류 처리 (Azure 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드 앱 빌드 Azure 전자책을 사용 하 여 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴과 그을 수 있는 방법을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 11/03/2015
ms.assetid: 7ead83bc-c08c-4b26-8617-00e07292e35c
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
msc.type: authoredcontent
ms.openlocfilehash: e67f3106f060d52f90ba56d6684af64779009e39
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37823380"
---
<a name="transient-fault-handling-building-real-world-cloud-apps-with-azure"></a>일시적인 오류 처리 (Azure 사용 하 여 실제 클라우드 앱 빌드)
====================
하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 합니다 **실제 세계 클라우드 앱 빌드 Azure** 전자책 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴 설명 하 고 도움이 될 수 있는 사례 성공적인 클라우드를 위한 웹 앱을 개발할 수 있습니다. 전자책에 대 한 정보를 참조 하세요 [첫 번째 장에서](introduction.md)합니다.


실제 클라우드 앱을 디자인할 때 일시적으로 서비스 중단을 처리 하는 방법을 고려해 야 하는 항목 중 하나입니다. 이 문제는 네트워크 연결과 외부 서비스에 종속 되므로 이므로 클라우드 앱에서 고유 하 게 중요 합니다. 사소 하지만 자동 복구 일반적으로 얻을 수 있습니다 하 고 고객에 게 잘못 된 환경에서 인해에서는 아니라면 지능적으로 처리할 수 있도록 준비 합니다.

## <a name="causes-of-transient-failures"></a>일시적인 오류의 원인

클라우드 환경에서 실패 하 고 삭제 된 데이터베이스 연결에 주기적으로 발생할 알려드립니다. 하려는 온-프레미스 환경에 비해 더 많은 load balancer를 통해 웹 서버와 데이터베이스 서버에 있는 직접 실제 연결 때문에 일부입니다. 또한 다중 테 넌 트 서비스에 종속 하는 경우에 따라 크게 도달는 사람에 게 서비스를 사용 하기 때문에 서비스 느려집니다 또는 시간 초과에 대 한 호출 표시 됩니다. 다른 경우에 사용자가 너무 자주 서비스에 도달할 수 있습니다 하 고 서비스가 의도적으로 제한 – 연결 거부 – 하면 서비스의 다른 테 넌 트에 나쁜 영향을 주지 않도록 하기 위해.

## <a name="use-smart-retryback-off-logic-to-mitigate-the-effect-of-transient-failures"></a>일시적인 오류의 영향을 완화 하기 위해 스마트 재시도/백오프 논리를 사용 합니다.

예외를 throw 하 고 고객에 게 사용할 수 없음 또는 오류 페이지를 표시 하는 대신 일반적으로 일시적인 오류를 인식할 수 있습니다 하 고 자동으로에서 오류를 발생 시킨 작업을 다시 시도 위해 하려고 하는 긴 수 성공 하기 전에 합니다. 대부분의 작업, 두 번째 시도에 성공 하 고 문제가 발생 했음을 인식 된 적이 고객 없이 오류 로부터 복구할 수 있습니다.

여러 가지 방법으로 스마트 재시도 논리를 구현할 수 있습니다.

- Microsoft Patterns &amp; 사례 그룹에는 [일시적인 오류 처리 응용 프로그램 블록](https://msdn.microsoft.com/library/dn440719(v=pandp.60).aspx) 하는 모든 작업을 수행 하기 없습니다 (Entity Framework)를 통해 SQL Database 액세스에 대 한 ADO.NET을 사용 하는 경우. 다시 시도-쿼리를 다시 시도 횟수에 대 한 정책을 설정 또는 명령 및 대기 시간을 시도 – 사이의 줄 바꿈 SQL 코드가 *를 사용 하 여* 블록입니다.

    [!code-csharp[Main](transient-fault-handling/samples/sample1.cs)]

    TFH 수도 [Azure In-role Cache](https://msdn.microsoft.com/library/windowsazure/dn386103.aspx) 하 고 [Service Bus](https://azure.microsoft.com/services/service-bus/)합니다.
- Entity Framework를 사용 하는 경우 일반적으로 작업 하지 않는 SQL 연결을 통해 직접이 Patterns and Practices 패키지를 사용할 수 없지만 Entity Framework 6 프레임 워크에 이러한 종류의 재시도 논리를 작성 하도록 합니다. 다시 시도 전략을 지정 하는 비슷한 방식으로 하 고 데이터베이스에 액세스할 때마다 EF 해당 전략을 사용 하는 다음 키를 누릅니다.

    Fix It 응용 프로그램에서이 기능을 사용 하려면 작업을 수행 해야 됩니다에서 파생 된 클래스를 추가 *DbConfiguration* 재시도 논리를 켭니다.

    [!code-csharp[Main](transient-fault-handling/samples/sample2.cs)]

    표시 된 코드는 일반적으로 일시적인 오류를 식별 하는 프레임 워크는 예외를 SQL Database에 대 한 재시도 사이의 최대 지연 시간을 5 초 동안 지 수 백오프 지연이 발생 된 작업을 최대 3 회 다시 시도 하는 EF를 지시 합니다. 지 수 백오프는 실패 한 각 다시 시도 후 대기 다시 시도 하기 전에 더 긴 기간을 의미 합니다. 행에 3 번의 시도 실패 하면 예외가 throw 됩니다. 회로 차단기에 대 한 다음 섹션에서는 지 수 백오프 하 고 다시 시도 횟수를 제한 된 이유를 설명 합니다.

    Fix It 응용 프로그램은 blob의 경우와 동일한 종류의 논리를 이미 구현 하는.NET 저장소 클라이언트 API에는 Azure Storage 서비스를 사용 하는 경우 비슷한 문제가 있을 수 있습니다. 다시 시도 정책에만 지정할 또는 기본 설정에 만족 하는 경우 수행할 필요가 없습니다.

<a id="circuitbreakers"></a>
## <a name="circuit-breakers"></a>회로 차단기

오랜 기간 동안 너무 여러 번 다시 시도 하지 않을 이유는 여러 가지가 있습니다.

- 영구적으로 실패 한 요청을 다시 시도 하는 너무 많은 사용자가 다른 사용자의 환경이 저하 될 수 있습니다. 수백만 명의 사용자는 반복을 수행 하는 모든 요청을 다시 시도 수 수 IIS 디스패치 큐를 확보할를 처리 하는 것이 고, 그렇지 못했습니다 성공적으로 요청을 서비스에서 앱을 방지 합니다.
- 모든 사용자가 다시 시도 하 고 있는 서비스 오류로 인해 수 너무 많은 요청 큐에서 대기 하는 경우 복구를 시작할 때 서비스가 플 러 딩을 가져옵니다.
- 제한으로 인해 오류가 발생 한 것 이며 시간 제한에 대 한 서비스를 사용 하 여 창에 있는 경우 계속된 다시 시도 창 밖으로 이동을 계속 하려면 제한이 발생할 수 있습니다.
- 렌더링 하는 웹 페이지에 대 한 대기 중인 사용자가 있을 수 있습니다. 너무 긴 만들기 사용자 대기는 비교적 빠르게 확인 하 라는 나중에 다시 시도 하도록 더 성가신 수 수 있습니다.

지 수 백오프 재시도 서비스 응용 프로그램에서 가져올 수의 빈도 제한 하 여 이러한 문제 중 일부를 해결 합니다. 또한 해야 하지만 *회로 차단기*: 즉, 특정에 다시 시도 앱을 다시 시도 중지 하 고 다음 중 하 나와 같은 다른 작업을 수행 하는 임계값:

- 사용자 지정 대체 (fallback) 합니다. 주가 Reuters에서 확인할 수 없는 경우 아마도 가져올 수 있습니다 Bloomberg;에서 또는 데이터베이스에서 데이터를 가져올 수 없을 경우 아마도에서 가져올 수 있습니다이 캐시 합니다.
- 자동 실패 합니다. 서비스에서 필요한 앱에 대 한 이것 아니면 저것 인 아니면만 null을 반환 데이터를 가져올 수 없습니다. Fix It 작업을 표시 하는 경우 Blob service에 응답 하지 않는 이미지 없이 작업 세부 정보를 표시할 수 있습니다.
- 페일 패스트 합니다. 사용 하 여 서비스를 방지 하려면 사용자는 오류 제한 기간을 확장 하거나 다른 사용자에 대 한 서비스 중단을 일으킬 수 있는 요청을 다시 시도 하세요. 친숙 한 "나중에 다시 시도" 메시지를 표시할 수 있습니다.

모든 상황에 맞는 재시도 정책이 없는 경우 여러 번 재시도 응답에 대 한 사용자를 기다리고 있는 동기 웹 앱에서 수행 하는 것 보다는 비동기 백그라운드 작업자 프로세스에서 더 이상 대기 합니다. 기다릴 수 있습니다 더 이상 관계형 데이터베이스 서비스에 대해 재시도 간에 캐시 서비스에 대 한 것 보다. 권장 되는 일부 샘플 숫자가 다를 수 있습니다 하는 방법의 아이디어를 제공 하는 정책을 다시 시도 다음과 같습니다. ("빠른 첫 번째" 의미 첫 번째 재시도 전에 지연 되지 않습니다.

![다시 시도 정책 예제](transient-fault-handling/_static/image1.png)

SQL Database 다시 시도 정책 지침은 [일시적인 오류 및 SQL Database에 연결 오류 문제 해결](https://azure.microsoft.com/documentation/articles/sql-database-connectivity-issues/)합니다.

## <a name="summary"></a>요약

다시 시도/백오프 전략을 수 있도록 임시 오류 보이지 않는 고객에 게 대부분의 시간 및 Microsoft ADO.NET, Entity Framework 또는 Azure를 사용 하든지 전략을 구현 하 여 작업을 최소화 하는 데 사용할 수 있는 프레임 워크를 제공 합니다. 저장소 서비스입니다.

에 [다음 장에서](distributed-caching.md), 성능을 향상 시키는 방법 살펴보겠습니다 및 사용 하 여 안정성 분산 캐싱입니다.

## <a name="resources"></a>자료

자세한 내용은 다음 리소스를 참조하세요.

설명서

- [Azure Cloud Services에서 대규모 서비스 설계를 위한 모범 사례](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)합니다. Mark Simms 및 Michael Thomassy 백서입니다. 비슷하지만 Failsafe 시리즈 자세한 방법 세부 정보로 이동 합니다. 원격 분석 및 진단 섹션을 참조 하세요.
- [Failsafe: 복원 력 있는 클라우드 아키텍처 지침](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)합니다. Marc Mercuri, Ulrich Homann 및 Andrew Townhill 백서입니다. FailSafe 동영상 시리즈의 웹 페이지 버전입니다.
- [Microsoft Patterns and Practices-Azure 지침](https://msdn.microsoft.com/library/dn568099.aspx)합니다. 참조 다시 시도 패턴, Scheduler 에이전트 감독자 패턴입니다.
- [Azure SQL Database의 내결함성](https://blogs.msdn.com/b/windowsazure/archive/2012/07/30/fault-tolerance-in-windows-azure-sql-database.aspx)합니다. Tony Petrossian 블로그 게시물입니다.
- [Entity Framework-연결 복구 / 재시도 논리](https://msdn.microsoft.com/data/dn456835)합니다. 사용 하 여 일시적인 오류 처리 Entity Framework 6의 기능을 사용자 지정 하는 방법입니다.
- [연결 복원 력 및 명령 인터 셉 션 ASP.NET MVC 응용 프로그램에서 Entity Framework 사용 하 여](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)입니다. 네 번째 9 부 자습서 시리즈에서는 SQL Database에 대 한 EF 6 연결 복원 력 기능을 설정 하는 방법을 보여 줍니다.

비디오

- [FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는 데](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms에서 9 부 시리즈입니다. 고급 개념 및 아키텍처 원칙으로 실제 고객의 Microsoft 고객 자문 팀 (CAT) 환경에서 가져온 스토리를 사용 하 여 액세스 가능 하 고 흥미로운 방식으로 표시 합니다. 에피소드 3 40:55부터에서 회로 차단기의 설명을 참조 하세요.
- [빌드 큰: Azure 고객에 게-부에서에서 Lessons learned](https://channel9.msdn.com/Events/Build/2012/3-030)합니다. 일시적인 오류에 대 한 설계에 대 한 Mark Simms 통신을 처리 하 고 모든 계측 오류입니다.

코드 샘플

- [Azure에서 서비스 기본 사항 클라우드](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)합니다. Microsoft Azure 고객 자문 팀 사용 하는 방법을 보여 주는에서 만든 응용 프로그램 예제는 [Enterprise Library 일시적인 오류 처리 블록](http://nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/) (TFH). 자세한 내용은 [클라우드 서비스의 기본 데이터 액세스 계층 – 일시적인 오류 처리](https://social.technet.microsoft.com/wiki/contents/articles/18665.cloud-service-fundamentals-data-access-layer-transient-fault-handling.aspx)합니다. (사용 하지 않고 직접 Entity Framework) ADO.NET을 사용 하 여 데이터베이스 액세스를 위한 TFH 것이 좋습니다.

> [!div class="step-by-step"]
> [이전](monitoring-and-telemetry.md)
> [다음](distributed-caching.md)
