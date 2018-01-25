---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
title: "시나리오: 웹 배포에 대 한 스테이징 환경 구성 | Microsoft Docs"
author: jrjlee
description: "스테이징 환경에 대 한 일반 웹 배포 시나리오를 설명 하 고 비슷한 env를 설정 하기 위해 완료 해야 할 작업에 설명 하는이 항목..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 5a8e49b7-5317-4125-b107-7e2466b47bb3
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 683a0cf88225fee762e82925afe3785a2defd5bf
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="scenario-configuring-a-staging-environment-for-web-deployment"></a>시나리오: 웹 배포에 대 한 스테이징 환경 구성
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목 스테이징 환경에 대 한 일반 웹 배포 시나리오에 설명 하 고 유사한 환경을 설정 하기 위해 완료 해야 할 작업에 설명 합니다.


조직에서는 많은 스테이징 환경을 사용 하 여 웹 응용 프로그램 또는 웹 사이트에 대 한 업데이트를 미리 봅니다. 이렇게 하면 조직 내 사용자를 탐색 하 고 사이트 ", 가동 되기" 또는 즉 프로덕션 환경에 배포 된 전에 새로운 기능 또는 콘텐츠를 검토 하 합니다. 스테이징 환경 현실적인 미리 보기를 제공 하기 위해 프로덕션 환경 최대한 근접 하 게 복제 하도록 설계 되었습니다. 이러한 종류의 스테이징 환경에는 일반적으로 이러한 특징이 있습니다.

- 환경의 여러 부하 분산 된 웹 서버와 장애 조치 클러스터링 및 데이터베이스 미러링과 함께 하나 이상의 데이터베이스 서버 구성 됩니다.
- 개발 팀 또는 팀 빌드 서버에 의해 자동으로 응용 프로그램을 수동으로 배포할 수 있습니다.
- 사용자 또는 응용 프로그램을 배포 하는 프로세스 계정을 가능성이 준비 서버에서 관리자 권한이 있어야 합니다.
- 응용 프로그램을 변경을 자주 배포 되므로 환경을 단일 단계를 지원 해야 하거나 자동 배포 합니다.

> [!NOTE]
> 이 자습서의 범위를 벗어납니다 여러 서버에서 데이터베이스 배포를 확장 합니다. 이 영역에 대 한 자세한 내용은 참조 하십시오 [SQL Server 온라인 설명서](https://technet.microsoft.com/library/ms130214.aspx)합니다.


예를 들어, 우리의 [자습서 시나리오](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Team Foundation Server (TFS) Contact Manager 솔루션을 관리 합니다. Rob 받는 TFS 관리자, 개발자가 필요에 따라 스테이징 환경에 배포를 트리거할 수 있는 빌드 정을 만들었습니다.

![](scenario-configuring-a-staging-environment-for-web-deployment/_static/image1.png)

대부분의 경우에서 않습니다 반드시 되도록 스테이징 환경에 최신 빌드가 배포 참고 합니다. 대신, 가능성이 훨씬 더 이미 조치가 유효성 검사 및 테스트 환경에서 확인을 실행 하는 특정 빌드를 배포 하려고 합니다.

## <a name="solution-overview"></a>솔루션 개요

이 시나리오에서 배포 요구 사항 분석에서 이러한 팩트를 추론할 수 있습니다.

- 배포를 수행 하는 사용자 또는 프로세스 계정은 스테이징 웹 서버 관리자가 아닌 배포를 지원 해야 하므로 준비 서버에서 관리자 권한이 있어야 없습니다. 따라서 원격 에이전트를 사용 하지 않고 웹 배포 처리기를 사용 하도록 스테이징 웹 서버를 구성 해야 합니다.
- 스테이징 환경에 여러 웹 서버에 포함 되어 있지만 까다롭기 때문에 서버 팜을 만들어야 하는 웹 팜 프레임 워크 WFF ()를 사용 하 여 한 번의 클릭 또는 자동화 된 배포의 경우 지원이 필요 합니다. 이 방법을 사용 하면 하나의 웹 서버 (주 서버) 응용 프로그램을 배포할 수 있습니다 및 WFF 스테이징 환경에서 모든 기타 웹 서버에서 배포를 복제 합니다.
- 사용자 또는 프로세스 계정 배포를 수행 하는 데이터베이스를 만들 수 있는 권한이 있어야 합니다. 에 계정을 추가 해야 하는 이와 같이 **dbcreator** 원격 액세스 및 배포를 지원 하기 위해 데이터베이스 서버를 구성 하는 것 외에도 데이터베이스 서버의 서버 역할입니다.

이러한 항목에서는 이러한 작업을 완료 하는 데 필요한 모든 정보를 제공 합니다.

- [웹 팜 프레임 워크와 서버 팜 만들기](creating-a-server-farm-with-the-web-farm-framework.md)합니다. 이 항목에는 만들고 웹 플랫폼 제품 및 구성 요소, 구성 설정 및 웹 사이트 및 응용 프로그램은 여러 부하 분산 된 웹 서버에서 복제 된 WFF를 사용 하 여 서버 팜을 구성 하는 방법을 설명 합니다.
- [웹 배포 게시에 대 한 웹 서버 구성 (웹 처리기를 배포 하는 데 사용)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)합니다. 이 항목에서는 웹 배포 게시를 원격 에이전트 방식을 사용 하 여 Windows Server 2008 R2 클린 빌드를 시작 하는 웹 서버를 구축 하는 방법에 설명 합니다.
- [웹 배포 게시에 대 한 데이터베이스 서버를 구성](configuring-a-database-server-for-web-deploy-publishing.md)합니다. 이 항목에서는 원격 액세스 및 SQL Server 2008 r 2의 기본 설치에서 시작 하는 배포를 지원 하기 위해 데이터베이스 서버를 구성 하는 방법에 설명 합니다.

## <a name="further-reading"></a>추가 정보

일반적인 개발자 테스트 환경 구성에 대 한 지침을 참조 하십시오. [시나리오: 웹 배포를 위해 테스트 환경 구성](scenario-configuring-a-test-environment-for-web-deployment.md)합니다. 일반적인 프로덕션 환경 구성에 대 한 지침을 참조 하십시오. [시나리오: 웹 배포를 위해 프로덕션 환경 구성](scenario-configuring-a-production-environment-for-web-deployment.md)합니다.

>[!div class="step-by-step"]
[이전](scenario-configuring-a-test-environment-for-web-deployment.md)
[다음](scenario-configuring-a-production-environment-for-web-deployment.md)
