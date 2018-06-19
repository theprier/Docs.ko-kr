---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
title: Visual Studio 2010을 사용 하 여 엔터프라이즈 시나리오에서 웹 응용 프로그램 배포 | Microsoft Docs
author: jrjlee
description: 도구와 기술을 다양 한 엔터프라이즈 시나리오에서 웹 응용 프로그램을 배포 하는 데 자습서의이 집합에 설명 합니다. 최대한 활용 하는 방법에 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/03/2012
ms.topic: article
ms.assetid: 48cfe378-d62a-48c6-a4db-6be3cead6898
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 921b1ccd8a1f2109a51f3f75149588422fefb91d
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30890231"
---
<a name="deploying-web-applications-in-enterprise-scenarios-using-visual-studio-2010"></a>Visual Studio 2010을 사용 하 여 엔터프라이즈 시나리오에서 웹 응용 프로그램 배포
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 도구와 기술을 다양 한 엔터프라이즈 시나리오에서 웹 응용 프로그램을 배포 하는 데 자습서의이 집합에 설명 합니다. Visual Studio 2010, Microsoft Build Engine (MSBuild), 인터넷 정보 서비스 (IIS) 7.5, IIS 웹 배포 도구 (웹 배포), 웹 팜 프레임 워크 WFF (), 및를 VSDBCMD.exe와 같은 유틸리티와 같은 기술을 최대한 활용 하는 방법을 설명합니다 단순화 하 고 배포 프로세스를 관리 합니다. 개념 개요와 하는 데 도움이 되는 작업 지향적 지침 포함 됩니다.
> 
> - 검토 하 고 엔터프라이즈급 웹 응용 프로그램에 대 한 배포 요구 사항을 설정 합니다.
> - 웹 배포를 지원 하기 위해 테스트, 스테이징 및 프로덕션 웹 서버 환경 구성 합니다.
> - 자동화 된 웹 배포를 지원 하기 위해 Team Foundation Server (TFS) CI (연속 통합) 프로세스를 구성 합니다.
> - 다양 한 요구 사항 및 제한 사항으로 서로 다른 서버 환경에 엔터프라이즈급 웹 응용 프로그램을 배포 합니다.
> - 서로 다른 서버 환경에서 실행 되는 웹 응용 프로그램에 변경 내용을 배포 합니다.
> 
> > [!NOTE]
> > 이러한 자습서 CI 서버로 사용할의 TFS 설명 하지만 지침 CI는 모든 서버에 맞게 쉽게 됩니다. Tfs를 이해 하 고이 자습서를 활용 한 세부 정보를 제공 하지 않아도 됩니다.
> 
> 
> 다음 자습서는 이탈리아어로 번역에 대 한 방문 [ http://www.lucamorelli.it ](http://www.lucamorelli.it)합니다.


## <a name="about-the-authors"></a>저자 정보

Jason Lee와 주 기술자는 [콘텐츠 마스터](http://www.contentmaster.com/) 여기서 그의 근무 기간이 Microsoft 제품 및 기술, 특히: SharePoint 및 ASP.NET에서 여러 해 동안 합니다. Jason 계산에 포함 되며 현재 MCPD 및 인증 MCTS 있습니다. Jason의 기술 블로그에서 읽을 수 [www.jrjlee.com](http://www.jrjlee.com/)합니다.

Benjamin Curry와 주 기술자는 [콘텐츠 마스터](http://www.contentmaster.com/) 백서, SDK 설명서, PowerPoint 프레젠테이션 및 강사 및 온라인 교육 과정 셨 하는 동안 쓴에 게 있습니다. ASP.NET 설명서 팀의 원래 멤버, 작업 했습니다에 대 한 Microsoft의 웹 기술을 사용 10 년 이상.

## <a name="target-audience"></a>대상 사용자

자습서의이 집합은 ASP.NET 웹 응용 프로그램 개발자 및 엔터프라이즈급 웹 응용 프로그램을 만들려면 Visual Studio 2010을 사용 하는 설계자는 솔루션입니다. 내용에서 가장 많은 가치를 가져오려면 Visual Studio 2010을 사용 하 여 익숙해야를 ASP.NET MVC 3, Windows Communication Foundation (WCF), IIS, SQL와 같은 Microsoft 웹 플랫폼 기술 인식 하 여 함께 TFS의 기본 익숙한 서버 및 Visual Studio 데이터베이스 프로젝트를 제공 합니다. 그러나 배포 도구와 기술에 잘 알고 또는 CI 시스템을 설정 하는 방법을 알아야 할 필요가 없습니다.

## <a name="requirements"></a>요구 사항

연습을 수행 하 고이 자습서에서 설명 하는 작업을 수행 하려면 개발 컴퓨터에이 소프트웨어를 설치 해야 합니다.

- Visual Studio 2010 Premium 또는 Ultimate Edition 서비스 팩 1
- .NET Framework 4.0
- .NET framework 3.5 서비스 팩 1
- ASP.NET MVC 3.0
- IIS 7.5 Express
- SQL Server Express 2008 R2

이 연습에 설명 된 배포 단계를 수행 하려면 샘플 웹 응용 프로그램 배포 환경에 액세스 해야 합니다. 최상의 결과 이러한 환경에는 조직의 엔터프라이즈 배포 패턴을 반영 해야 합니다. 그런 다음 배포 환경 및 조직의 요구 사항을 반영 하기 위해이 설명서에서 제공 된 연습을 수정할 수 있습니다.

## <a name="series-contents"></a>계열 내용

이 소개 섹션 두 개의 추가 항목으로 구성 됩니다. 이 다음에 나오는 자습서에 대 한 몇 가지 광범위 한 컨텍스트를 제공 하도록 설계 되었습니다.

- [엔터프라이즈 웹 배포: 시나리오 개요](enterprise-web-deployment-scenario-overview.md)합니다. 이 항목에서는 각이 시리즈의 자습서도 다룹니다.이 시나리오를 설명 합니다. 시나리오의 엔터프라이즈급 웹 응용 프로그램을 개발 하는 대로 Fabrikam, Inc. 라는 가상 회사의 관리 ALM (Application Lifecycle) 요구 사항에 중점을 둡니다.
- [응용 프로그램 수명 주기 관리: 프로덕션 개발에서](application-lifecycle-management-from-development-to-production.md)합니다. 이 항목에서는 배포 프로세스의 상위 수준, 종단 간 개요를 제공 합니다. Fabrikam, Inc. 엔터프라이즈 규모 ASP.NET 웹 응용 프로그램 테스트, 스테이징 및 프로덕션 환경을 통해 연속 개발 프로세스의 일부분으로 이동 하는 방법을 보여 줍니다.

계열 4 자습서 집합을 포함합니다. 각 웹 배포의 다양 한 측면 중점적:

- [웹 배포는 기업에서](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)합니다. 이 자습서에는 MSBuild 프로젝트 파일에 대 한 개념 소개, 웹 게시 파이프라인, 웹 배포 및 기타 관련된 기술을 제공합니다. 방법을 함께 사용할 수 있습니다 이러한 도구 복잡 한 배포 프로세스를 관리 하에 대해 설명 합니다.
- [웹 배포를 위한 서버 환경을 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)합니다. 이 자습서에서는 웹 배포 에이전트 서비스 ("원격 에이전트") 또는 웹 배포 처리기 및 원격 데이터베이스 배포를 사용 하 여 원격 웹 패키지 배포를 비롯 한 다양 한 배포 시나리오를 지원 하기 위해 Windows 서버를 구성 하는 방법을 설명 합니다. 사용자 환경에 대 한 적절 한 배포 방법 선택에 지침을 제공 하 고는 WFF를 사용 하 여 서버 팜의 모든 웹 서버를 통해 배포 된 웹 응용 프로그램을 복제 하는 방법을 설명 합니다.
- [웹 배포에 대 한 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)합니다. 이 자습서에서는 수동으로 배포의 특정 빌드를 트리거 및 CI 프로세스의 일부로 자동화 된 배포를 비롯 한 다양 한 배포 시나리오를 지원 하도록 TFS를 구성 하는 방법을 설명 합니다.
- [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)합니다. 이 자습서에서는 사용자 지정 된 여러 환경에 대 한 데이터베이스 배포, 배포에서 파일 및 폴더를 제외 하 고 배포 프로세스 중 웹 응용 프로그램을 오프 라인 등의 다양 한 고급 배포 작업을 수행 하는 방법을 설명합니다 .

## <a name="where-to-start"></a>시작 위치를

자습서의이 집합 참조 구현을 제공 하 고 작업 및 연습 일반적인 컨텍스트를 제공 하는 가상의 엔터프라이즈 배포 시나리오와 함께 복잡성 현실적인 수준으로 샘플 솔루션을 사용 합니다. 다음 항목인 [엔터프라이즈 웹 배포: 시나리오 개요](enterprise-web-deployment-scenario-overview.md), 시나리오와 샘플 솔루션을 소개 합니다. 여기에서 자습서 및 요구 사항에 가장 근접 하는 항목을 통해 사용할 수 있습니다.

> [!div class="step-by-step"]
> [다음](enterprise-web-deployment-scenario-overview.md)
