---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
title: "일시적인 오류 처리 (Azure 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs"
author: MikeWasson
description: "실제 세계 클라우드로 응용 프로그램 빌딩 Azure 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴 및 그을 수 있는 방법에 설명..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 11/03/2015
ms.topic: article
ms.assetid: 7ead83bc-c08c-4b26-8617-00e07292e35c
ms.technology: 
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling
msc.type: authoredcontent
ms.openlocfilehash: 3caeeb83e4c074ae0ffc30f035d793a821eb6be2
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="transient-fault-handling-building-real-world-cloud-apps-with-azure"></a>일시적인 오류 처리 (Azure 사용 하 여 실제 클라우드 앱 빌드)
====================
여 [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **실제 세계 클라우드로 응용 프로그램 빌딩 Azure** 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴에 설명 하 고 사례 수 있는 클라우드에 대 한 웹 앱을 개발 성공적으로 수행 되어야 합니다. 전자책에 대 한 정보를 참조 하십시오. [첫 번째 장](introduction.md)합니다.


실제 클라우드 앱을 디자인할 때 일시적인 서비스 중단을 처리 하는 방법에 대해 신경쓸 필요가 작업 중 하나입니다. 이 문제는 네트워크 연결 및 외부 서비스에 종속 되므로 이기 때문에 클라우드 응용 프로그램의 고유 하 게 중요 합니다. 자주 사소 하지만 자체 복구 일반적으로 가져오고 지능적으로 처리 하기 위한 준비 하지 않은 경우 합니다 초래할 있습니다 잘못 된 환경을 고객에 대 한 합니다.

## <a name="causes-of-transient-failures"></a>일시적인 오류의 원인

클라우드 환경에서 실패 했으며 연결 정기적으로 발생 하는 데이터베이스를 삭제 하는 값을 찾을 수 있습니다. 즉, 거 온-프레미스 환경에 비해 더 많은 부하 분산 장치를 통해 웹 서버와 데이터베이스 서버가 직접 실제 연결 되어 있기 때문 이기도 합니다. 또한 다중 테 넌 트 서비스에 종속 하는 경우에 과도 하 게 도달는 서비스를 사용 하는 다른 사용자 때문에 느린 서비스 get 또는 시간 초과에 대 한 호출을 표시 됩니다. 다른 경우에는 서비스에 너무 자주 도달는 사용자 수 있으며 서비스 의도적으로 스로틀 – 연결 거부 – 하면 서비스의 다른 테 넌 트에 부정적인 영향을 하지 않도록 하려면.

## <a name="use-smart-retryback-off-logic-to-mitigate-the-effect-of-transient-failures"></a>스마트 재시도/백오프 논리를 사용 하 여 일시적인 오류의 영향을 완화 하기

예외를 throw 하 고 고객에 게 사용할 수 없음 또는 오류 페이지를 표시 하는 대신 오류는 일반적으로 일시적인를 인식할 수 있습니다 및 자동으로 오류를 발생 시킨 작업을 다시 시도에서는 나중에 찾아낸 하 긴 수 성공 하기 전에. 대부분의 작업, 두 번째 시도에 성공 하 고 문제가 했음을 인식 된 적이 고객 없이 오류 로부터 복구할 수 있습니다.

여러 가지 방법으로 스마트 재시도 논리를 구현할 수 있습니다.

- Microsoft Patterns &amp; 사례 그룹에는 [일시적인 오류 처리 응용 프로그램 블록](https://msdn.microsoft.com/en-us/library/dn440719(v=pandp.60).aspx) 하는 모든 작업을 수행 하면에 대 한 (Entity Framework) 통해서가 아니라 SQL 데이터베이스 액세스를 위해 ADO.NET을 사용 하는 경우. 다시 시도-는 쿼리를 다시 시도 횟수에 대 한 정책을 설정 하기만 또는 명령 및 대기 시간을 시도-줄 바꿈 사이의 SQL 코드가 *를 사용 하 여* 블록입니다.

    [!code-csharp[Main](transient-fault-handling/samples/sample1.cs)]

    TFH도 지원 [Azure 역할 내 캐시](https://msdn.microsoft.com/en-us/library/windowsazure/dn386103.aspx) 및 [서비스 버스](https://azure.microsoft.com/services/service-bus/)합니다.
- Entity Framework를 사용 하는 경우 일반적으로 작동 하지 SQL 연결을 직접 사용 되므로이 Patterns and Practices 패키지를 사용할 수 없습니다. 그러나 Entity Framework 6 프레임 워크에 바로 이러한 종류의 재시도 논리를 작성 합니다. 다시 시도 전략 비슷하게에서 지정 하 고 데이터베이스에 액세스할 때마다 EF 해당 전략을 사용 하는 다음 합니다.

    수정 응용 프로그램에서이 기능을 사용 하려면 하기만 하면는에서 파생 된 클래스를 추가 *DbConfiguration* 한 재시도 논리를 켭니다.

    [!code-csharp[Main](transient-fault-handling/samples/sample2.cs)]

    표시 된 코드 프레임 워크는 일반적으로 일시적인 오류도 식별 하는 SQL 데이터베이스 예외에 대 한 작업을 다시 최대 3 회 다시 시도 시간 사이 5 초의 최대 지연 시간 지 수 백오프 지연이 발생 된 EF에 지시 합니다. 지 수 백오프는 실패 한 각 다시 시도 후 기다리는 다시 시도 하기 전에 더 긴 기간을 의미 합니다. 행에 3 회 실패할 경우 예외가 throw 됩니다. 회로 차단기에 대 한 다음 섹션 지 수 백오프 하 고 제한 된 수의 재시도 이유를 설명 합니다.

    .NET 저장소 클라이언트 API에는 이미 동일한 종류의 논리가 구현 하 고 수정 앱은 blob의 경우에 Azure 저장소 서비스를 사용 하는 경우 비슷한 문제가 있을 수 있습니다. 재시도 정책을 지정 하거나 기본 설정을 사용 하 여 만족 했으면 경우 그렇게도 없는 합니다.

<a id="circuitbreakers"></a>
## <a name="circuit-breakers"></a>회로 차단기

너무 긴 기간 동안 여러 번 다시 시도 하지 않을 이유는 여러 가지가 있습니다.

- 너무 많은 사용자가 영구적으로 실패 한 요청을 다시 시도 다른 사용자의 환경이 저하 될 수 있습니다. 수백만의 사람들이 반복을 만드는 모든 요청을 다시 시도 되 면 있습니다 될 수 있습니다 제한 된 IIS 디스패치 큐 고 것 그렇지 않은 경우 처리할 수 있는 성공적으로 요청을 처리에서 앱을 방지 합니다.
- 모든 사용자가 다시 시도해도 문제가 있는 서비스 오류로 인해 수 수 너무 많은 요청 큐에서 대기 하는 서비스를 복구 하기 시작할 때 서비스 장애 유발 가져옵니다.
- 제한으로 인해 오류는 경우는 제한에 대 한 서비스를 사용 하는 기간 계속된 다시 시도 해당 창 밖으로 이동 되 고 계속 조정이 수 없습니다.
- 렌더링 하는 웹 페이지에 대 한 대기 중인 사용자를 할 수 있습니다. 만들기 사람 대기 너무 깁니다 해당 상대적으로 신속 하 게 확인 하 라는 나중에 다시 시도 하도록 더까지 될 수 있습니다.

지 수 백오프 응용 프로그램에서 서비스를 가져올 수 재시도 빈도 제한 하 여 이러한 문제 중 일부를 해결 합니다. 또한가 필요 하지만 *회로 차단기*:이 특정에 다시 시도 응용 프로그램을 다시 시도 중지 하 고 다음 중 하 나와 같은 다른 작업을 수행 하는 임계값을 의미 합니다.

- 사용자 지정 대체 합니다. 주식 시세 Reuters에서 가져올 수 없습니다, 하는 경우 이전 있습니다에서 구할 수 Bloomberg; 또는 경우 데이터베이스에서 데이터를 가져올 수 없습니다, 어쩌면 있습니다에서 구할 수 캐시 합니다.
- 자동 실패 합니다. 서비스에서 필요 없는 경우 앱에 대 한 완전히만 null을 반환 데이터를 가져올 수 없습니다. 수정 작업을 표시 하는 경우 Blob 서비스가 응답 하지 않으면 이미지 없이 작업 세부 정보를 표시할 수 있습니다.
- 빠른 실패 합니다. 사용 하 여 서비스의 폭주를 방지 하려면 사용자 오류 제한 기간을 확장 하거나 다른 사용자에 대 한 서비스 중단을 일으킬 수 있는 요청을 다시 시도 하십시오. 친숙 한 "나중에 다시 시도" 메시지를 표시할 수 있습니다.

적합 한 다시 시도 정책이 없으면 있습니다. 번 더 다시 시도 수 있으며 사용자가 응답을 기다리고 있는 동기 웹 응용 프로그램에서 사용 하는 것 보다는 비동기 백그라운드 작업자 프로세스에서 더 이상 대기 수 있습니다. 대기할 수 있습니다 더 이상 관계형 데이터베이스 서비스에 대 한 다시 시도 대기 중 캐시 서비스에 대 한 보다. 권장 하는 몇 가지 샘플 재시도 정책 알 수 있는 숫자 다를 수 있습니다 어떻게의 다음과 같습니다. ("빠른 첫 번째" 의미 첫 번째 다시 시도 하기 전에 지연 되지 않습니다.

![예제 다시 시도 정책](transient-fault-handling/_static/image1.png)

SQL 데이터베이스 다시 시도 정책 지침 참조 [일시적인 오류 및 SQL 데이터베이스에 연결 오류 해결](https://azure.microsoft.com/documentation/articles/sql-database-connectivity-issues/)합니다.

## <a name="summary"></a>요약

Microsoft는 ADO.NET, Entity Framework 또는 Azure를 사용 하는 전략을 구현 하 여 작업을 최소화 하는 데 사용할 수 있는 프레임 워크를 제공 하 고 다시 시도/백오프 전략을 고객에 게 임시 오류 보이지 않는 대부분의 경우 시킬 수 있습니다. 저장소 서비스입니다.

에 [다음 장에서](distributed-caching.md), 성능을 개선 하는 방법을 살펴보겠습니다 및 사용 하 여 안정성 분산 캐싱 합니다.

## <a name="resources"></a>리소스

자세한 내용은 다음 리소스를 참조하세요.

설명서

- [Azure 클라우드 서비스에서 대규모 서비스를 디자인에 대 한 유용한](https://msdn.microsoft.com/en-us/library/windowsazure/jj717232.aspx)합니다. 백서: Mark Simms 및 Michael Thomassy 합니다. 유사 Failsafe 시리즈 하지만 방법 더 세부적으로 이동 합니다. 원격 분석 및 진단 섹션을 참조 하십시오.
- [Failsafe: 복원 력 있는 클라우드 아키텍처에 대 한 지침](https://msdn.microsoft.com/en-us/library/windowsazure/jj853352.aspx)합니다. 백서: Marc Mercuri, Ulrich Homann 및 Andrew Townhill 합니다. FailSafe 비디오 시리즈의 웹 페이지 버전입니다.
- [Microsoft Patterns and Practices-Azure 지침](https://msdn.microsoft.com/en-us/library/dn568099.aspx)합니다. 참조 재시도 패턴, 스케줄러 에이전트 감독자 패턴입니다.
- [Azure SQL 데이터베이스의 내결함성](https://blogs.msdn.com/b/windowsazure/archive/2012/07/30/fault-tolerance-in-windows-azure-sql-database.aspx)합니다. Tony Petrossian 하 여 블로그 게시물입니다.
- [Entity Framework-연결 복원 력 재시도 논리 /](https://msdn.microsoft.com/en-us/data/dn456835)합니다. 사용 및 일시적인 오류 처리 Entity Framework 6의 기능을 사용자 지정 하는 방법.
- [연결 복원 력 및 ASP.NET MVC 응용 프로그램에서 Entity Framework와 함께 명령 인터 셉 션](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)합니다. 네 번째 9 개 부분으로 이루어진 자습서 시리즈의 SQL 데이터베이스의 EF 6 연결 복원 력 기능은를 설정 하는 방법을 보여 줍니다.

비디오

- [FailSafe: 복원 력 있는 확장 가능한 클라우드 서비스를 만드는](https://channel9.msdn.com/Series/FailSafe)합니다. Marc Mercuri, Ulrich Homann, Mark Simms 하 여 시리즈를 9 개 부분으로 구성 합니다. 고급 개념 및 아키텍처 원칙 매우 액세스 가능 하 고 흥미로운 방법으로 스토리 실제 고객과 Microsoft 고객 자문 팀 (CAT) 환경에서 가져온 것으로 표시 합니다. 회로 차단기 40:55에서 시작 하는 3 에피소드 설명을 참조 하십시오.
- [건물 큰: Azure 고객-2 부에서에서 확인 된 사항을](https://channel9.msdn.com/Events/Build/2012/3-030)합니다. 일시적인 오류에 대 한 설계에 대 한 토론 Mark Simms, 처리 및 모든 항목이 계측 오류.

코드 샘플

- [클라우드 서비스 기본 사항 Azure에서](https://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)합니다. Microsoft Azure 고객 자문 팀 사용 하는 방법을 보여 주는 하 여 만든 응용 프로그램 예제는 [엔터프라이즈 라이브러리 일시적인 오류 처리 블록](http://nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/) (TFH). 자세한 내용은 참조 [클라우드 서비스 기초 데이터 액세스 계층-일시적인 오류 처리](https://social.technet.microsoft.com/wiki/contents/articles/18665.cloud-service-fundamentals-data-access-layer-transient-fault-handling.aspx)합니다. TFH (사용 하지 않고 직접 Entity Framework) ADO.NET을 사용 하 여 데이터베이스 액세스를 위한 것이 좋습니다.

>[!div class="step-by-step"]
[이전](monitoring-and-telemetry.md)
[다음](distributed-caching.md)
