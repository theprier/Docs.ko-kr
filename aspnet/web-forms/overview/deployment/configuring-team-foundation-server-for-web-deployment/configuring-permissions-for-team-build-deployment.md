---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
title: 빌드 배포 팀의 사용 권한과 구성 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 자동화 된 b의 일부로 콘텐츠 웹 서버와 데이터베이스 서버를 배포 하려면 빌드 서버에 사용할 수 있도록 권한을 구성 하는 방법을 설명...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 2488a91e-b0a8-465a-b874-3233f724b56b
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
msc.type: authoredcontent
ms.openlocfilehash: 4698349d664816ec49475bbfe71fb32af79ea96d
ms.sourcegitcommit: 6784510cfb589308c3875ccb5113eb31031766b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2018
ms.locfileid: "30890283"
---
<a name="configuring-permissions-for-team-build-deployment"></a>팀에 대 한 구성 권한 빌드 배포
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에는 자동화 된 빌드 프로세스의 일부로 콘텐츠 웹 서버와 데이터베이스 서버를 배포 하려면 빌드 서버에 사용할 수 있도록 권한을 구성 하는 방법을 설명 합니다.


이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하는 자습서 시리즈가&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성, Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 WCF (foundation) 서비스 및 데이터베이스 프로젝트.

이 자습서의 핵심에는 배포 방법에 설명 된 분할 프로젝트 파일 접근 방식에 따라 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에 빌드 프로세스에 의해 제어 되는&#x2014;포함 환경 관련 빌드 및 배포 설정을 포함 하는 하나 및 모든 대상 환경에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 구성 하기 위해 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="task-overview"></a>작업 개요

Team Foundation Server (TFS) 2010 빌드 서비스를 설치할 때 서비스를 실행 하려는 id를 지정 합니다. 기본적으로 네트워크 서비스 계정입니다. 또는 도메인 계정을 사용 하 여 실행 되도록 빌드 서비스를 구성할 수 있습니다.

팀 빌드를 사용 하 여 자동화 하려는 및 Windows 인증을 요구 하는 모든 배포 작업은 빌드 서비스 id를 사용 하 여 실행 됩니다. 따라서 빌드 서비스 id를 웹 서버와 데이터베이스 서버에 필요한 사용 권한을 부여 해야 합니다.

> [!NOTE]
> 네트워크 서비스 계정으로 시스템 계정을 사용 하 여 다른 컴퓨터를 인증. 컴퓨터 계정에는 다음 양식을 사용 * [도메인 이름]\[컴퓨터 이름] ***$**&#x2014;예를 들어 **FABRIKAM\TFSBUILD$** 합니다. 이와 같이 빌드 서비스가 네트워크 서비스 id를 사용 하 여 실행을 빌드 서버에 대 한 컴퓨터 계정 id에 필요한 모든 권한을 부여 해야.


## <a name="configuring-web-server-permissions"></a>웹 서버 사용 권한 구성

에 설명 된 대로 [웹 배포에 대 한 오른쪽 접근 방식을 선택](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md), 두 가지가 주요 원격 웹 서버에 웹 패키지를 배포 하려는 경우 사용할 수 있습니다.

- 대상으로 하 여 원격 위치에서 응용 프로그램 배포는 *웹 배포 에이전트 서비스가* (원격 에이전트 라고도 함) 대상 서버에 있습니다.
- 대상으로 하 여 원격 위치에서 응용 프로그램 배포는 *인터넷 정보 서비스* (*IIS) 웹 배포 처리기* 대상 서버에 있습니다.

원격 에이전트에는 경우 두 가지 주요 제한이 있습니다.

- 원격 에이전트에는 NTLM 인증만을 지원합니다. 즉, 배포 빌드 서비스 id를 사용 해야&#x2014;계정이 다른 계정을 가장할 수 없습니다.
- 원격 에이전트를 사용 하려면 배포를 수행 하는 계정에 대상 서버에서 관리자 여야 합니다.

함께, 이러한 두 가지 제한 구성 원격 에이전트 접근 방식이 자동된 팀 빌드 배포에 대 한 바람직하지 않은 합니다. 이 방법을 사용 하려면 모든 대상 웹 서버에서 관리자 계정 빌드 서비스를 확인 해야 합니다.

반면, 웹 배포 처리기 접근 방식에서는 다양 한 장점을 제공합니다.

- 웹 배포 처리기는 IIS 웹 배포 도구 (웹 배포)를 대체 계정의 자격 증명을 전달할 수 있도록 하는 HTTPS를 통해 기본 인증을 지원 합니다.
- 관리자가 아닌 사용자가 웹 배포 처리기를 사용 하 여 특정 IIS 웹 사이트에 콘텐츠를 배포할 수 있도록 대상 웹 서버를 구성할 수 있습니다.

결과적으로, 팀 빌드 웹 패키지 배포를 자동화 하는 경우 웹 배포 처리기를 대상으로 명확 하 게 보다 선호 됩니다. 다음은 권장 되는 프로세스입니다.

1. 배포에 사용할 권한이 낮은 도메인 계정을 만듭니다.
2. 웹 배포 처리기를 구성 하 고에 설명 된 대로 계정에는 특정 IIS 웹 사이트에 콘텐츠를 배포 하는 데 필요한 권한을 부여 [웹 배포 게시 (웹 배포 처리기)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)합니다.
3. 웹 배포를 호출 및 웹 배포 처리기 대상, 기본 인증을 사용 하 고 도메인 계정의 자격 증명을 제공을 만든 배포를 수행 합니다.

에 [않아](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) 샘플 솔루션을 인증 유형을 지정 (기본 또는 NTLM), 웹 배포 자격 증명 및 환경별 프로젝트 파일에서 끝점 주소 (원격 에이전트 또는 웹 배포 처리기). 이러한 값은 작성 하 고 프로젝트 파일에서 실행 될 때 웹 배포 명령 실행에 사용 됩니다. 자세한 내용은 참조 [웹 패키지 배포](../web-deployment-in-the-enterprise/deploying-web-packages.md)합니다.

웹 배포 처리기를 권한을 구성 하는 방법을 비롯 하 여를 구성 하는 방법에 대 한 자세한 내용은 참조 [웹 배포 게시 (웹 배포 처리기)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)합니다. 원격 에이전트를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [웹 배포 게시 (원격 에이전트)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)합니다.

## <a name="configuring-database-server-permissions"></a>데이터베이스 서버 사용 권한 구성

SQL Server로 데이터베이스를 배포 하려면 다음을 수행 해야 합니다.

- SQL Server 인스턴스에 배포 하는 계정에 대 한 로그인을 만듭니다.
- 로그인 권한을 부여 **DBCreator** SQL Server 인스턴스에 대 한 합니다.
- 초기 배포 후에 로그인 추가 **db\_소유자** 대상 데이터베이스 역할을 합니다. 후속 배포에는 기존 데이터베이스를 수정 하지 않고 있습니다 새 데이터베이스 만들기 때문에 이것이 필요 합니다.

NTLM 인증 또는 SQL Server 인증을 사용 하 여 SQL Server 인스턴스에 인증할 수 있습니다.

- NTLM 인증을 사용 하는 경우 빌드 서비스 계정에 위에 설명 된 사용 권한을 부여 해야 합니다.
- SQL Server 인증을 사용 하는 경우 SQL Server 계정에 위에 설명 된 사용 권한을 부여 해야 합니다. 데이터베이스를 배포 하는 사용 하 여 연결 문자열에 SQL Server 사용자 이름 및 암호를 포함 해야 합니다.

데이터베이스 배포에 대 한 사용 권한을 구성 하는 방법에 대 한 단계별 정보를 참조 하십시오. [웹 배포 게시에 대 한 데이터베이스 서버 구성](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)합니다.

## <a name="conclusion"></a>결론

이 시점에서 필요한 권한, 사용자에 게 열기 인증 옵션과 함께 팀 빌드 웹 응용 프로그램 및 데이터베이스 배포를 자동화 하는 경우를 이해 해야 합니다. 또한 IIS 웹 서버와 SQL Server 데이터베이스 서버에 필요한 권한을 구현할 수 있습니다.

## <a name="further-reading"></a>추가 정보

원격 배포를 지원할 Windows 서버 환경 구성에 대 한 자세한 내용은 참조 하십시오. [웹 배포에 대 한 서버 환경을 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)합니다.

> [!div class="step-by-step"]
> [이전](deploying-a-specific-build.md)
