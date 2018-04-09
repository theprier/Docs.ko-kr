---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
title: '시나리오: 웹 배포를 위한 테스트 환경 구성 | Microsoft Docs'
author: jrjlee
description: 이 항목 개발자를 위한 일반 웹 배포 시나리오에 설명 하 고 테스트 환경 또는 si를 설정 하기 위해 완료 해야 할 작업에 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 44a22ac7-1fc7-4174-b946-c6129fb6a19b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 2976be642815e715ac19bd9db34485cf5474cb32
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="scenario-configuring-a-test-environment-for-web-deployment"></a>시나리오: 웹 배포를 위한 테스트 환경 구성
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목 개발자를 위한 일반 웹 배포 시나리오에 설명 하 고 또는 테스트 환경, 유사한 환경을 설정 하기 위해 완료 해야 할 작업에 설명 합니다.


개발자가 웹 응용 프로그램에 작업을 하는 경우 종종 지정 된 액세스 현실적인 설정에서 응용 프로그램에 대 한 변경 내용을 테스트 하는 데 사용할 수 있는 서버 환경에 있습니다. 이러한 종류의 개발 또는 테스트 환경에는 일반적으로 이러한 특징이 있습니다.

- 환경 단일 웹 서버 및 단일 데이터베이스 서버로 구성 됩니다.
- 일반적으로 개발자는 응용 프로그램의 요구 사항에 환경을 구성할 수 있도록 서버에서 관리자 권한이 유지 합니다.
- 응용 프로그램을 변경을 자주 배포 되므로 환경을 단일 단계를 지원 해야 하거나 자동 배포 합니다.

예를 들어, 우리의 [자습서 시나리오](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Matt Hink Fabrikam, Inc.의 개발자는 Matt 않아 솔루션에서 작동 하 고 정기적으로 변경 내용을 테스트 환경에 배포 해야 합니다. Matt은 테스트 웹 서버와 테스트 데이터베이스 서버에는 관리자. 처음에 Matt 테스트 환경에 솔루션을 직접 배포할 수 있어야 합니다.

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image1.png)

작업으로 진행 되 고 더 많은 개발자 들 CI (연속 통합) Team Foundation Server (TFS)에 대 한 솔루션은 구성 않아 팀에 참가 합니다. 개발자가 내용에서 체크 인하 때마다 팀 빌드 솔루션을 빌드합니다, 그리고 모든 단위 테스트를 실행할를 자동으로 테스트 환경에 솔루션을 배포 합니다.

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image2.png)

## <a name="solution-overview"></a>솔루션 개요

테스트 환경에는 두 가지 주요 방법 중 선택할 수 있으므로 원격 컴퓨터에서 배포를 자동 또는 단일 단계를 지원 해야 합니다. 다음과 같은 작업을 수행할 수 있습니다.

- 웹 배포 에이전트 서비스 ("원격 에이전트")를 사용 하 여 배포를 지원 하기 위해 테스트 웹 서버를 구성 합니다.
- 웹 배포 처리기를 사용 하 여 배포를 지원 하기 위해 테스트 웹 서버를 구성 합니다.

> [!NOTE]
> 사용 해도 [주문형 웹 배포](https://technet.microsoft.com/library/ee517345(WS.10).aspx) ("임시 에이전트"). 요구 사항 및 제약 조건을 기준으로 원격 에이전트 방식을 사용 하는 것과 비슷합니다.


이 경우 개발자를 대상 서버에서 관리자 권한이 있어야 하 고 테스트 환경 아니므로 엄격한 보안 제약 조건에 따라 원격 에이전트를 사용 하 여 배포를 지원 하기 위해 테스트 웹 서버를 구성 하는 것이 좋습니다. 이것은 덜 복잡 하며 웹 배포 처리기의 접근 방법 보다 덜 초기 구성을 수행 해야 합니다. 원격 액세스 및 배포를 지원 하기 위해 데이터베이스 서버를 구성 해야 합니다.

이러한 항목에서는 이러한 작업을 완료 하는 데 필요한 모든 정보를 제공 합니다.

- [웹 배포 게시 (원격 에이전트)에 대 한 웹 서버를 구성](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)합니다. 이 항목에서는 웹 배포 게시를 원격 에이전트 방식을 사용 하 여 Windows Server 2008 R2 클린 빌드를 시작 하는 웹 서버를 구축 하는 방법에 설명 합니다.
- [웹 배포 게시에 대 한 데이터베이스 서버를 구성](configuring-a-database-server-for-web-deploy-publishing.md)합니다. 이 항목에서는 원격 액세스 및 SQL Server 2008 r 2의 기본 설치에서 시작 하는 배포를 지원 하기 위해 데이터베이스 서버를 구성 하는 방법에 설명 합니다.

## <a name="further-reading"></a>추가 정보

일반적인 스테이징 환경 구성에 대 한 지침을 참조 하십시오. [시나리오: 웹 배포를 위해 스테이징 환경 구성](scenario-configuring-a-staging-environment-for-web-deployment.md)합니다. 일반적인 프로덕션 환경 구성에 대 한 지침을 참조 하십시오. [시나리오: 웹 배포를 위해 프로덕션 환경 구성](scenario-configuring-a-production-environment-for-web-deployment.md)합니다.

> [!div class="step-by-step"]
> [이전](choosing-the-right-approach-to-web-deployment.md)
> [다음](scenario-configuring-a-staging-environment-for-web-deployment.md)
