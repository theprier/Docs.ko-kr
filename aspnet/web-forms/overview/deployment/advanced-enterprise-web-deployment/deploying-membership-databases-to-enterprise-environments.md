---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
title: 엔터프라이즈 환경에 멤버 자격 데이터베이스 배포 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 주요 고려 사항 및 ASP.NET 응용 프로그램 서비스 데이터베이스 (보다 일반적...를 프로 비전 할 때 해결 해야 하는 문제를 설명 합니다.
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 3cf765df-d311-4f68-a295-c9685ceea830
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
msc.type: authoredcontent
ms.openlocfilehash: 9df152866b54f55c2b00611331e868f98bd2f3e4
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37827190"
---
<a name="deploying-membership-databases-to-enterprise-environments"></a>엔터프라이즈 환경에 멤버 자격 데이터베이스 배포
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 주요 고려 사항 및 ASP.NET 응용 프로그램 구축, 테스트, 준비 또는 프로덕션 환경에서 데이터베이스 (일반적으로 멤버 자격 데이터베이스 라고도 함) 서비스를 해결 해야 하는 문제를 설명 합니다. 이러한 과제를 충족 하는 데 사용할 수 하는 방법을 설명 합니다.


이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.

이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="what-are-the-issues-when-you-deploy-a-membership-database"></a>멤버 자격 데이터베이스를 배포할 때의 문제점은 무엇입니까?

대부분의 경우에서 데이터베이스에 대 한 배포 전략을 고안 하는 경우 가장 먼저 고려해 야 할 경우 배포 하려는 데이터 개발 또는 테스트 환경에서 쉽고 빠른 테스트를 용이 하 게 사용자 계정 데이터를 배포 하는 것이 좋습니다. 스테이징 또는 프로덕션 환경에서 매우 그럴 가능성은 사용자 계정 데이터를 배포 하려는 것입니다.

아쉽게도 ASP.NET 멤버 자격 데이터베이스에는 훨씬 더 복잡 한이 의사 결정을 하는 몇 가지 특정 과제 소개:

- 스키마 전용 배포가 작동 하지 않는 상태에 멤버 자격 데이터베이스가 종료 됩니다. 멤버 자격 데이터베이스에 일부 구성 데이터가 포함 되어 있으므로이 (에 **aspnet\_SchemaVersions** 테이블)에 작동 하는 데 필요한 데이터베이스. 따라서 사용자 계정 데이터를 제외 하기 위해 멤버 자격 데이터베이스의 스키마만 배포를 수행 하는 경우에 필수 구성 데이터를 추가 하려면 배포 후 스크립트를 실행 해야 합니다.
- 멤버 자격 데이터베이스를 구성 하는 방법에 따라 멤버 자격 공급자를 암호를 암호화 하 여 데이터베이스에 저장할 컴퓨터 키를 사용할 수 있습니다. 이 경우 데이터베이스를 사용 하 여 배포할 모든 사용자 계정 데이터는 대상 서버의 없게 됩니다. 따라서 사용자 계정 데이터 배포는 지원 되는 시나리오가 아닙니다.

## <a name="choosing-a-membership-database-strategy"></a>멤버 자격 데이터베이스 전략 선택

엔터프라이즈 서버 환경에서 멤버 자격 데이터베이스를 프로 비전 하는 방법을 선택할 때 이러한 지침을 따르세요.

- 가능한 경우 멤버 자격 데이터베이스를 배포 하지 않습니다. 대상 데이터베이스 서버에서 멤버 자격 데이터베이스를 수동으로 만들 대신 합니다. 멤버 자격 데이터베이스 스키마를 사용자 지정 하지 않은 경우 단순히 만들면 새로 situ에서 사용 하 여 대상 합니다 [ASP.NET SQL Server 등록 도구 (aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)합니다.
- 에 멤버 자격 데이터베이스를 배포 하지만 옵션이 없는 경우&#x2014;예를 들어, 데이터베이스 스키마를 광범위 하 게 수정할 수 있습니다&#x2014;사용자 계정 데이터를 제외 하려면 멤버 자격 데이터베이스의 스키마만 배포를 수행 해야 하 고 필요한 구성 데이터를 추가 하는 배포 후 스크립트를 실행 합니다. 이러한 접근 방식에서 광범위 한 지침을 찾을 수 있습니다 [방법: ASP.NET 멤버 자격 데이터베이스 없이 포함 하 여 사용자 계정을 배포](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx)합니다.

반드시 *멤버 자격 데이터베이스의 스키마가 상당히 정적일 가능성이*합니다. 정기적으로 스키마를 업데이트 해야 그럴 가능성은 멤버 자격 데이터베이스를 지정한 경우에&#x2014;웹 응용 프로그램 또는 데이터베이스 프로젝트의 코드와 동일한 빈도로 변경 하지 않습니다. 이와 같이 모든 배포를 자동화 하거나 단일 단계 프로세스에 멤버 자격 데이터베이스를 포함할 필요가 없습니다.

## <a name="using-vsdbcmd-to-update-a-membership-database-schema"></a>VSDBCMD를 사용 하 여 멤버 자격 데이터베이스 스키마를 업데이트 하려면

첫 번째 배포 후 멤버 자격 데이터베이스의 구조를 수정 하면 데이터베이스를 다시 배포 하려면 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하려는 없습니다. 웹 배포에서 데이터베이스 배포 기능을 대상 데이터베이스에 차등 업데이트를 확인 하는 기능을 포함 하지 않습니다&#x2014;대신, 웹 배포 삭제 하 고 다시 만들어야 데이터베이스입니다. 이 스테이징 또는 프로덕션 환경에서 일반적으로 필요 없는 모든 기존 사용자 계정 데이터를 손실 하는 것을 의미 합니다.

대안은은 VSDBCMD 유틸리티를 사용 하 여 대상 데이터베이스의 스키마를 업데이트 하는 것입니다. VSDBCMD 두 가지 중요 한 기능이 포함 되어 있습니다. 먼저.dbschema 파일로 기존 데이터베이스의 스키마를 가져올 수 것입니다. 둘째, 배포할 수 있습니다.dbschema 파일을 기존 데이터베이스에는 대상 데이터베이스를 최신 상태로 만드는 데 필요한 변경만 수행할 수 있고 모든 데이터가 손실 되지 않도록 하는 차등 업데이트와 합니다.

멤버 자격 데이터베이스 스키마를 업데이트 하려면 다음 대략적인 단계를 사용할 수 있습니다.

1. VSDBCMD 사용 하 여 **가져오기** 원본 멤버 자격 데이터베이스에 대 한.dbschema 파일을 생성 하는 작업입니다. 이 절차에 설명 되어 [방법: 명령 프롬프트에서 스키마를 가져오는](https://msdn.microsoft.com/library/dd172135.aspx)합니다.
2. VSDBCMD 사용 하 여 **배포** .dbschema 파일 대상 멤버 자격 데이터베이스를 배포 하는 작업입니다. 이 절차에 설명 되어 [VSDBCMD에 대 한 명령줄 참조 합니다. EXE (배포 및 스키마 가져오기)](https://msdn.microsoft.com/library/dd193283.aspx)합니다.

## <a name="conclusion"></a>결론

이 항목에서는 다양 한 대상 환경에서 ASP.NET 멤버 자격 데이터베이스를 프로 비전 해야 할 때 직면 하 고 문제 중 일부를 설명 합니다. 특히 이유 스키마 전용 배포는 멤버 자격 데이터베이스를 비작동 상태로 남겨 이유 배포 사용자 계정 데이터는 지원 되지 않습니다 및 설명 되어 있습니다. 또한 항목 프로 비전, 배포 및 다양 한 시나리오에서 멤버 자격 데이터베이스를 업데이트 하는 방법에 지침을 제공 합니다.

## <a name="further-reading"></a>추가 정보

자세한 지침 및 VSDBCMD를 사용 하는 방법의 예제를 참조 하세요. [VSDBCMD에 대 한 명령줄 참조 합니다. (배포 및 스키마 가져오기) EXE](https://msdn.microsoft.com/library/dd193283.aspx) 하 고 [방법: 명령 프롬프트에서 스키마를 가져오는](https://msdn.microsoft.com/library/dd172135.aspx). Aspnet를 사용 하 여 대 한 자세한 내용은\_멤버 자격 데이터베이스를 만드는 regsql.exe 참조 [ASP.NET SQL Server 등록 도구 (aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)합니다. 멤버 자격 데이터베이스 배포에 대 한 보다 일반적인 지침을 참조 하세요 [방법: ASP.NET 멤버 자격 데이터베이스 없이 포함 하 여 사용자 계정을 배포](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx)합니다.

> [!div class="step-by-step"]
> [이전](deploying-database-role-memberships-to-test-environments.md)
> [다음](excluding-files-and-folders-from-deployment.md)
