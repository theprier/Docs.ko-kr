---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
title: 연속 통합 및 지속적인 업데이트 (실제 클라우드 앱 빌드 azure) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드 앱 빌드 Azure 전자책을 사용 하 여 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴과 그을 수 있는 방법을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 06/12/2014
ms.assetid: eaece9f5-f80c-428b-b771-5db66d275b7d
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
msc.type: authoredcontent
ms.openlocfilehash: 40687c490fdfb7764ac9ca8af6fffd054362d552
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37819421"
---
<a name="continuous-integration-and-continuous-delivery-building-real-world-cloud-apps-with-azure"></a>연속 통합 및 지속적인 업데이트 (Azure 사용 하 여 빌드 실제 클라우드 앱)
====================
하 여 [Mike Wasson](https://github.com/MikeWasson)하십시오 [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> 합니다 **실제 세계 클라우드 앱 빌드 Azure** 전자책 Scott Guthrie를 개발한 프레젠테이션을 기반으로 합니다. 13 패턴 설명 하 고 도움이 될 수 있는 사례 성공적인 클라우드를 위한 웹 앱을 개발할 수 있습니다. 전자책에 대 한 정보를 참조 하세요 [첫 번째 장에서](introduction.md)합니다.


처음 두 개발 프로세스 패턴 된 하는 것이 좋습니다 [모든 자동화](automate-everything.md) 및 [소스 제어](source-control.md), 세 번째 프로세스 패턴을 결합 합니다. CI (지속적인 통합)는 개발자가 소스 리포지토리에 코드에 체크 인하면, 때마다 빌드를 자동으로 트리거됩니다 의미 합니다. 지속적인 업데이트 (CD)은이 한 단계 더: 자동화 된 단위 테스트 및 빌드를 성공한 후 자동으로 응용 프로그램을 배포한 환경 자세한 철저 한 테스트를 수행할 수 있습니다.

클라우드를 사용 하면만 요금을 지급 하므로 환경 리소스를 사용 하는 테스트 환경 유지 관리 비용을 최소화할 수 있습니다. 필요 하 고 완료 되 면 환경 아래로 수행할 수 있는 경우 CD 프로세스 테스트 환경을 설정할 수 테스트 합니다.

## <a name="continuous-integration-and-continuous-delivery-workflow"></a>연속 통합 및 지속적인 업데이트 워크플로

일반적으로 개발 및 스테이징 환경에 지속적인 업데이트를 수행 하는 것이 좋습니다. Microsoft에도 대부분의 팀은 프로덕션 배포에 대 한 수동 검토 및 승인 프로세스를 필요합니다. 프로덕션 배포 하는지 확인 하려는 개발 팀에서 사용자를 키 지원의 경우 또는 트래픽이 낮은 기간 동안 사용할 수 있을 때 발생 합니다. 이지만 되도록 개발자가 체크 인을 변경 하 고 환경 개발 및 테스트 환경을 완전히 자동화할 수 없도록 nothing 승인 테스트에 대 한 설정입니다.

다음에서 다이어그램 [는 Microsoft Patterns and Practices 전자책 지속적인 업데이트에 대 한](http://aka.ms/ReleasePipeline) 일반적인 워크플로 보여 줍니다. 원래 컨텍스트의 전체 크기 이미지를 표시를 클릭 합니다.

[![연속 배달 워크플로](continuous-integration-and-continuous-delivery/_static/image1.png)](https://msdn.microsoft.com/library/dn449955.aspx)

## <a name="how-the-cloud-enables-cost-effective-ci-and-cd"></a>클라우드 비용 효율적인 CI 및 CD를 사용 하는 방법을

Azure에서 이러한 프로세스를 자동화 하는 것은 쉽습니다. 를 실행 중인 모든 클라우드에 있으므로 구입 하거나 빌드 또는 테스트 환경에 대 한 서버를 관리할 필요가 없습니다. 및 테스트에 사용할 수 있도록 서버를 기다릴 필요가 없습니다. 수행 하는 모든 빌드를 사용 하 여 automation 스크립트, 실행된 승인 테스트 또는 한 심도 있는 더 많은 테스트를 사용 하 여 Azure에서 테스트 환경을 스핀업 하 고 방금 완료 되 면 중단할 수 있습니다. 이며만 2 시간 8 시간 또는 하루에 해당 서버를 실행 하면에 대 한 요금을 지불 해야 할 금액 최소화 하기 때문에 컴퓨터를 실제로 실행 되는 시간에만 지불 합니다. 예를 들어, 환경에 필요한 수정 프로그램 응용 프로그램 기본적으로 비용이 시간당 약 1% 무료 수준에서 한 계층을 이동 하는 경우. 한 달에 걸쳐 한 번에 한 시간 환경만 실행 하는 경우 테스트 환경의 아마도 비용은 커피숍에서 구입할 수 있는 latte 미만입니다.

## <a name="visual-studio-team-services-vsts"></a>VSTS(Visual Studio Team Services)

VSTS에서 배포 하려는 응용 프로그램 개발에 도움이 기능의 수를 제공 합니다.

- (분산) Git 및 TFVC (중앙 집중식) 소스 제어를 모두 지원 합니다.
- 즉, 동적으로 빌드 서버 필요할 때 만들고 완료 되 면 아래로 이동 탄력적인 빌드 서비스를 제공 합니다. 소스 코드 변경 내용을 체크 인할 때 할당 한 고 유휴 시간의 대부분을 특정 사용자 지정 빌드 서버에 대 한 지불 필요가 자동으로 빌드 시작할 수 있습니다. 빌드가 서비스는 특정 빌드 수를 초과 하지 않습니다. 많은 양의 빌드를 수행 하려는 경우 예약 된 빌드 서버를 약간 추가 결제할 수 있습니다.
- Azure로 지속적인 업데이트를 지원합니다.
- 자동화 된 부하 테스트를 지원합니다. 부하 테스트 클라우드 앱에 중요 한 있지만 너무 늦게 완료 될 때까지 들어오지 종종 됩니다. 수천 명의 사용자, 병목 지점 찾기 및 처리량을 향상 시킬 수 있도록 하 여 앱의 과도 한 사용 시뮬레이션 부하 테스트-프로덕션 환경에 앱을 출시 전에 합니다.
- 단체 방 공동 작업, 실시간 통신 및 소규모 agile 팀을 위한 공동 작업을 용이 하 게 지원 합니다.
- Agile 프로젝트 관리를 지원합니다.


연속 통합 및 VSTS의 배달 기능에 대 한 자세한 내용은 참조 하세요. [Visual Studio Team Services](https://www.visualstudio.com/team-services/)합니다.

원하는 턴키 프로젝트 관리, 팀 공동 작업 및 소스 제어 솔루션을 체크 아웃 VSTS 합니다. 서비스는 최대 5 명 사용자까지 무료이 고에서 등록할 수 있습니다 [Visual Studio Team Services](https://www.visualstudio.com/team-services/)합니다.

## <a name="summary"></a>요약

짧은 주기 시간을 사용 하 여 반복 가능 하 고 안정적 이며 예측 가능한 개발 프로세스를 구현 하는 방법에 대 한 첫 번째 세 가지 클라우드 개발 패턴 되었습니다. 에 [다음 장에서](web-development-best-practices.md) 아키텍처 및 코딩 패턴을 검토 하기 시작 했습니다.

## <a name="resources"></a>자료

자세한 내용은 [Azure App Service에서 웹 앱 배포](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)합니다.

다음 리소스를 참조 하세요.

- [Team Foundation Server 2012 사용 하 여 릴리스 파이프라인 빌드](http://aka.ms/ReleasePipeline)합니다. 전자책, 실습 및 샘플 코드에서 Microsoft Patterns and Practices, 지속적인 업데이트를 자세히 소개를 제공 합니다. Visual Studio Lab Management 및 Visual Studio Release Management의 내부적 사용 합니다.
- [ALM Ranger DevOps 도구 및 지침](https://aka.ms/vsarsolutions/)합니다. ALM Rangers DevOps Workbench 샘플 도우미 솔루션 및 공동 작업 패턴을 사용 하 여 실질적인 지침을 도입 &amp; 사례 책 *TFS 2012를 사용 하 여 릴리스 파이프라인을 만들*를 시작 하는 좋은 방법으로 DevOps의 개념과 &amp; Release Management를 TFS 2012에 대 한 및 평가 합니다. 지침에는 한 번 빌드하여 여러 환경에 배포 하는 방법을 보여 줍니다.
- [Visual Studio 2012를 사용한 연속 배달 테스트](https://msdn.microsoft.com/library/jj159345.aspx)합니다. 전자책을 참고 하 여 Microsoft Patterns and Practices에 지속적인 업데이트를 사용 하 여 자동화 된 테스트를 통합 하는 방법에 설명 합니다.
- [WindowsAzureDeploymentTracker](https://github.com/RyanTBerry/WindowsAzureDeploymentTracker). 소스 코드를 캡처하고 (레이블 기반)는 TFS에서 빌드, 빌드, 패키지의 특정 측면을 구성 하는 DevOps 역할에서 허용 하는 사용자가 Azure로 푸시 설계 된 도구입니다. 도구 "롤백" 이전에 배포 된 버전으로 작업을 사용 하도록 설정 하기 위해 배포 프로세스를 추적 합니다. 이 도구는 외부 종속성이 없습니다 하며 TFS Api 및 Azure SDK에는 독립 실행형를 사용 하 여 작동할 수 있습니다.
- [지속적인 제공: 신뢰할 수 있는 소프트웨어를 빌드, 테스트 및 배포 자동화를 통해 해제](https://www.amazon.com/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912/ref=sr_1_1?s=books&amp;ie=UTF8&amp;qid=1377126361)합니다. Jez Humble 책입니다.
- [해제! 디자인 및 프로덕션이 준비 된 소프트웨어 배포](https://www.amazon.com/Release-It-Production-Ready-Pragmatic-Programmers/dp/0978739213)합니다. Michael T. Nygard 책입니다.

> [!div class="step-by-step"]
> [이전](source-control.md)
> [다음](web-development-best-practices.md)
