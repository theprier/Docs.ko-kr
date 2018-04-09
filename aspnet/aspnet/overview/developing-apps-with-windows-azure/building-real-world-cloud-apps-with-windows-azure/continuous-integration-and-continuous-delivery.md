---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
title: 연속 통합 및 지속적인 업데이트 (Azure로 응용 프로그램 빌딩 실제 클라우드) | Microsoft Docs
author: MikeWasson
description: 실제 세계 클라우드로 응용 프로그램 빌딩 Azure 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴 및 그을 수 있는 방법에 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/12/2014
ms.topic: article
ms.assetid: eaece9f5-f80c-428b-b771-5db66d275b7d
ms.technology: ''
ms.prod: .net-framework
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
msc.type: authoredcontent
ms.openlocfilehash: 4d482aaa0d25d6e6baaf196df4b4bb9335408e46
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="continuous-integration-and-continuous-delivery-building-real-world-cloud-apps-with-azure"></a>연속 통합 및 지속적인 업데이트 (Azure로 응용 프로그램 빌딩 실제 클라우드)
====================
여 [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson](https://github.com/Rick-Anderson), [Tom Dykstra](https://github.com/tdykstra)

[다운로드 해결 프로젝트](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자책 다운로드](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **실제 세계 클라우드로 응용 프로그램 빌딩 Azure** 전자책 Scott Guthrie에서 개발 된 프레젠테이션을 기반으로 합니다. 13 패턴에 설명 하 고 사례 수 있는 클라우드에 대 한 웹 앱을 개발 성공적으로 수행 되어야 합니다. 전자책에 대 한 정보를 참조 하십시오. [첫 번째 장](introduction.md)합니다.


개발 프로세스 패턴 된 처음 두 권장 [모든 자동화](automate-everything.md) 및 [소스 제어](source-control.md)를 합쳐 세 번째 프로세스 패턴 및 합니다. CI (연속 통합) 개발자가 소스 리포지토리를 코드에서 체크 인하 때마다 빌드를 자동으로 트리거되는 것을 의미 합니다. 지속적인 업데이트 (CD)이를 한 단계를 추가로 사용: 빌드 및 자동화 된 단위 테스트 성공 후 자동으로 응용 프로그램을 배포한 환경 더 철저 한 테스트를 수행할 수 있습니다.

클라우드를 사용 하면 지불 하기 때문에 환경 리소스에 대 한 사용 하는 상태로 테스트 환경 유지 관리 비용을 최소화할 수 있습니다. 필요할 때 완료 되 면 환경은 수행할 수 CD 프로세스 테스트 환경을 설정 수 테스트 합니다.

## <a name="continuous-integration-and-continuous-delivery-workflow"></a>연속 통합 및 지속적인 업데이트 워크플로

일반적으로 사용자가 개발 또는 스테이징 환경을로 지속적인 배달을 수행 하는 것이 좋습니다. 대부분의 팀도 Microsoft에서 프로덕션 배포에 대 한 수동 검토 및 승인 프로세스를 필요합니다. 프로덕션에 대 한 개발 팀에서 키의 사람들이 가장 잘 지원 또는 트래픽이 낮은 기간 동안 사용할 수 있는지 확인 하려는 배포 발생 합니다. 하지만 수용 테스트 용으로 설정 되도록 작업을 수행 하는 개발자가 변경, 환경 체크인 개발 및 테스트 환경을 완전히 자동화 하지 않도록 하려면 아무 것도 있습니다.

다음 다이어그램에서 [는 Microsoft Patterns and Practices 전자책 지속적인 업데이트에 대 한](http://aka.ms/ReleasePipeline) 일반적인 워크플로 보여 줍니다. 원래 컨텍스트에서 전체 크기를 볼 이미지를 클릭 합니다.

[![지속적인 업데이트 워크플로](continuous-integration-and-continuous-delivery/_static/image1.png)](https://msdn.microsoft.com/library/dn449955.aspx)

## <a name="how-the-cloud-enables-cost-effective-ci-and-cd"></a>클라우드 비용 효율적인 CI 및 CD를 사용 하는 방법을

Azure에서 이러한 프로세스를 자동화 하는 것은 간단 합니다. 를 실행 중인 모든 클라우드에서를 구입 하거나 빌드 또는 테스트 환경에 대 한 서버를 관리할 필요는 없습니다. 및에서 테스트를 사용할 수 있도록 서버에 대 한 대기 필요가 없습니다. 수행 하는 모든 빌드, 자동화 스크립트, 실행된 승인 테스트 또는,에 대 한 깊이 있는 자세한 테스트를 사용 하 여 Azure의 테스트 환경을를 시작 하 고 방금 완료 되 면 중지할 것 수 있습니다. 하며만 8 시간 또는 하루에 2 시간에 대 한 해당 서버를 실행 하면 금액에 대 한 비용을 지불 해야 하는 최소 수준 때문에 컴퓨터를 실제로 실행 되는 시간에만 지불할 수입니다. 예를 들어 환경에 필요한 수정 프로그램 응용 프로그램 기본적으로 비용이 소요 시간 당 1 cent 약 무료 수준에서 1 단계 이동 합니다. 한 달에 걸쳐 한 번에 한 시간 환경 에서만 실행 되는 경우 테스트 환경의 아마도 비용 커피숍에서 구입할 수 있는 latte 보다 작습니다.

## <a name="visual-studio-team-services-vsts"></a>VSTS(Visual Studio Team Services)

VSTS는 다양 한 배포를 계획에서 응용 프로그램 개발에 도움이 되는 기능을 제공 합니다.

- (배포) 하는 Git 및 TFVC (중앙 집중식) 소스 제어를 지원 합니다.
- 동적으로 필요한 경우 빌드 서버를 만듭니다 고 작업이 완료 되 면 아래로 누르게 한 탄력적인 빌드 서비스를 제공 합니다. 가 할당 하 고 대부분의 유휴 상태에 있는 빌드 서버에 대 한 비용을 지불 하지 않아도 소스 코드 변경 내용에서 체크 누군가가 때에 자동으로 빌드를 시작 수 있습니다. 빌드 서비스는 특정 빌드 수를 초과 하지 않습니다. 많은 양의 빌드를 수행 하려는 경우 예약 된 빌드 서버에 대 한 거의 추가 비용을 지불 수 있습니다.
- Azure로 지속적인 배달을 지원합니다.
- 자동화 된 부하 테스트를 지원합니다. 부하 테스트 클라우드 앱에 중요 한 있지만 너무 늦었습니다 될 때까지 반납 종종 됩니다. 수천 명의 사용자가 병목 현상을 찾는 및 처리량을 향상 시킬 수 있도록 하 여 응용 프로그램의 사용을 시뮬레이트합니다 부하 테스트-프로덕션 환경에 응용 프로그램을 해제 하기 전에.
- 단체 방 공동 작업을 실시간으로 통신 및 소규모 agile 팀 공동 작업을 용이 하 게를 지원 합니다.
- Agile 프로젝트 관리를 지원합니다.


연속 통합 및 VSTS의 배달 기능에 대 한 자세한 내용은 참조 하십시오. [Visual Studio Team Services](https://www.visualstudio.com/team-services/)합니다.

턴키 프로젝트 관리에 대 한 원하는 팀 공동 작업 및 원본 제어 솔루션을 체크 아웃 VSTS 합니다. 최대 5 명의 사용자에 대 한이 서비스는 및에서에 등록할 수 [Visual Studio Team Services](https://www.visualstudio.com/team-services/)합니다.

## <a name="summary"></a>요약

낮은 주기 시간을 사용 하는 반복 가능 하 고 예측 가능한 신뢰할 수 있는 개발 프로세스를 구현 하는 방법에 대 한 첫 번째 세 가지 클라우드 개발 패턴 되었습니다. 에 [다음 장에서](web-development-best-practices.md) 아키텍처 및 코딩 패턴을 검토 하기 시작 했습니다.

## <a name="resources"></a>자료

자세한 내용은 참조 [Azure 앱 서비스의 웹 앱을 배포](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)합니다.

다음 리소스를 참조 하십시오.

- [Team Foundation server 2012 릴리스 파이프라인을 구축](http://aka.ms/ReleasePipeline)합니다. 전자책, 실습 및 예제 코드에서 Microsoft Patterns and Practices, 지속적인 업데이트에 대 한 자세한 소개를 제공 합니다. Visual Studio Lab Management 및 Visual Studio Release Management의 내부적 사용 합니다.
- [ALM Rangers DevOps 도구 및 지침](https://aka.ms/vsarsolutions/)합니다. DevOps 워크 벤치 샘플 도우미 솔루션 및 패턴으로 공동 작업에 대 한 지침에서는 ALM Rangers 도입 &amp; 사례 책 *TFS 2012와 릴리스 파이프라인을 구축*를 시작 하는 좋은 방법으로 DevOps 개념과 &amp; TFS 2012에 대 한 및 넣지 릴리스 관리 합니다. 지침에는 한 번 빌드하여 여러 환경에 배포 하는 방법을 보여 줍니다.
- [Visual Studio 2012를 사용한 지속적인 업데이트 테스트](https://msdn.microsoft.com/library/jj159345.aspx)합니다. 전자책 (영문)에서 Microsoft Patterns and Practices, 지속적인 업데이트를 사용 하 여 자동화 된 테스트를 통합 하는 방법에 설명 합니다.
- [WindowsAzureDeploymentTracker](https://github.com/RyanTBerry/WindowsAzureDeploymentTracker). TFS (레이블을에 기반)에서 빌드를 캡처, 빌드, 패키지,의 특정 측면을 구성 하는 DevOps 역할에서 허용 하는 사용자 및 Azure에 밀어 넣습니다 설계 도구에 대 한 소스 코드입니다. 도구 작업 "롤백"를 이전에 배포 된 버전을 사용할 수 있도록 배포 프로세스를 추적 합니다. 이 도구는 외부 종속성이 없습니다 하며 TFS Api 및 Azure SDK에는 독립 실행형를 사용 하 여 작동할 수 있습니다.
- [지속적인 업데이트: 신뢰할 수 있는 소프트웨어를 빌드, 테스트 및 배포 자동화를 통해 해제](https://www.amazon.com/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912/ref=sr_1_1?s=books&amp;ie=UTF8&amp;qid=1377126361)합니다. 미 천 한 Jez의 책입니다.
- [해제! 디자인 및 프로덕션에 사용 가능한 소프트웨어 배포](https://www.amazon.com/Release-It-Production-Ready-Pragmatic-Programmers/dp/0978739213)합니다. Michael 화 Nygard의 책입니다.

> [!div class="step-by-step"]
> [이전](source-control.md)
> [다음](web-development-best-practices.md)
