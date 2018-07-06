---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
title: '시나리오: 웹 배포용 테스트 환경 구성 | Microsoft Docs'
author: jrjlee
description: 이 항목에서는 개발자를 위한 일반적인 웹 배포 시나리오를 설명 하 고 또는 테스트 환경,는 si를 설정 하기 위해 완료 해야 하는 작업에 설명 하는 중...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 44a22ac7-1fc7-4174-b946-c6129fb6a19b
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: ba77c944378245ed82d1cee92b668e31acc51a81
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37822372"
---
<a name="scenario-configuring-a-test-environment-for-web-deployment"></a>시나리오: 웹 배포용 테스트 환경 구성
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 개발자를 위한 일반적인 웹 배포 시나리오를 설명 하 고 또는 테스트 환경, 유사한 환경을 설정 하기 위해 완료 해야 하는 작업을 설명 합니다.


개발자가 웹 응용 프로그램에서 작동 하는 경우 종종 주어질 액세스 현실적인 설정에서 응용 프로그램에 대 한 변경 내용을 테스트 하는 데 사용할 수 있는 서버 환경입니다. 일반적으로 이러한 종류의 개발 또는 테스트 환경에 이러한 특징이 있습니다.

- 단일 웹 서버 및 단일 데이터베이스 서버 환경 구성 됩니다.
- 일반적으로 개발자는 응용 프로그램의 요구 사항을 환경을 구성할 수 있도록 하려면 서버에서 관리자 권한이 유지 합니다.
- 응용 프로그램을 변경을 자주 배포 되므로 단일 단계를 지원 해야 하는 환경 또는 배포를 자동화 합니다.

예를 들어, 우리의 [자습서 시나리오](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Matt Hink Fabrikam, Inc.의 개발자는 Matt은 Contact Manager 솔루션에서 작동 하 고 정기적으로 테스트 환경에 변경 내용을 배포 해야 합니다. Matt는 테스트 웹 서버와 테스트 데이터베이스 서버에서 관리자입니다. 처음에 Matt 테스트 환경에 솔루션을 직접 배포할 수 해야 합니다.

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image1.png)

작업으로 진행 되 고 더 많은 개발자가 솔루션은 CI (지속적인 통합)에서 Team Foundation Server (TFS)에 대 한 구성 되어 Contact Manager 팀을 조인 합니다. 개발자 콘텐츠 체크 인할 때마다 Team Build 해야 솔루션을 빌드합니다, 그리고 모든 단위 테스트를 실행 및 테스트 환경에 솔루션을 자동으로 배포 합니다.

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image2.png)

## <a name="solution-overview"></a>솔루션 개요

테스트 환경 단일 단계를 지원 해야 하는 경우 또는 두 가지 주요 방법 중 선택할 수 있습니다 있도록 원격 컴퓨터에서 배포를 자동화 합니다. 다음과 같은 작업을 수행할 수 있습니다.

- 웹 배포 에이전트 서비스 ("원격 에이전트")를 사용 하 여 배포를 지원 하기 위해 테스트 웹 서버를 구성 합니다.
- 웹 배포 처리기를 사용 하 여 배포를 지원 하기 위해 테스트 웹 서버를 구성 합니다.

> [!NOTE]
> 사용할 수도 있습니다 [주문형 웹 배포](https://technet.microsoft.com/library/ee517345(WS.10).aspx) ("임시 에이전트"). 요구 사항 및 제약 조건을 기준으로 원격 에이전트 접근 방식에는 것과 비슷합니다.


이 경우 개발자를 대상 서버에서 관리자 권한이 있어야 하 고 테스트 환경을 아니므로 엄격한 보안 제한에 따라 원격 에이전트를 사용 하 여 배포를 지원 하기 위해 테스트 웹 서버를 구성 하는 것이 좋습니다. 이 작업은 덜 복잡 하며 웹 배포 처리기의 접근 방법 보다 덜 초기 구성이 필요 합니다. 원격 액세스 및 배포를 지원 하기 위해 데이터베이스 서버를 구성 해야 합니다.

이러한 항목에는 이러한 작업을 완료 하기 위해 필요한 모든 정보를 제공 합니다.

- [웹 배포 게시용 (원격 에이전트)에 대 한 웹 서버를 구성할](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)합니다. 이 항목에서는 웹 배포 게시를 원격 에이전트 방식을 사용 하 여 Windows Server 2008 R2 빌드 정리에서 시작을 지 원하는 웹 서버를 구축 하는 방법을 설명 합니다.
- [웹 배포 게시용 데이터베이스 서버를 구성](configuring-a-database-server-for-web-deploy-publishing.md)합니다. 이 항목에서는 원격 액세스 및 SQL Server 2008 R2의 기본 설치에서 시작 하는 배포를 지원 하기 위해 데이터베이스 서버를 구성 하는 방법을 설명 합니다.

## <a name="further-reading"></a>추가 정보

일반적인 스테이징 환경 구성에 대 한 지침을 참조 하세요 [시나리오: 웹 배포용 스테이징 환경 구성](scenario-configuring-a-staging-environment-for-web-deployment.md)합니다. 일반적인 프로덕션 환경 구성에 대 한 지침을 참조 하세요 [시나리오: 웹 배포용 프로덕션 환경 구성](scenario-configuring-a-production-environment-for-web-deployment.md)합니다.

> [!div class="step-by-step"]
> [이전](choosing-the-right-approach-to-web-deployment.md)
> [다음](scenario-configuring-a-staging-environment-for-web-deployment.md)
