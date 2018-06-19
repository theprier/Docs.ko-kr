---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
title: 멤버 자격 데이터베이스 엔터프라이즈 환경에 배포 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 주요 고려 사항 및 (더 일반적... ASP.NET 응용 프로그램 서비스 데이터베이스를 프로 비전 할 때 해결 해야 하는 문제 설명
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 3cf765df-d311-4f68-a295-c9685ceea830
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
msc.type: authoredcontent
ms.openlocfilehash: b783fcf57759f2a431480eec6902105f6d683408
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30892480"
---
<a name="deploying-membership-databases-to-enterprise-environments"></a>멤버 자격 데이터베이스 엔터프라이즈 환경에 배포
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 주요 고려 사항 및 테스트, 준비 또는 프로덕션 환경에서 (일반적으로 멤버 자격 데이터베이스 라고도 함)는 데이터베이스를 서비스 하는 ASP.NET 응용 프로그램 구축 때 알아야 할 문제를 설명 합니다. 이러한 과제를 충족 하는 데 사용할 수는 방법에 대해서도 설명 합니다.


이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하는 자습서 시리즈가&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성, Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 WCF (foundation) 서비스 및 데이터베이스 프로젝트.

이 자습서의 핵심에는 배포 방법에 설명 된 분할 프로젝트 파일 접근 방식에 따라 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에 빌드 프로세스에 의해 제어 되는&#x2014;포함 환경 관련 빌드 및 배포 설정을 포함 하는 하나 및 모든 대상 환경에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 구성 하기 위해 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="what-are-the-issues-when-you-deploy-a-membership-database"></a>멤버 자격 데이터베이스를 배포할 때 문제점은 무엇입니까?

대부분의 경우에는 데이터베이스에 대 한 배포 전략을 고안 가장 먼저 고려해 야 할 배포 하려는 데이터입니다. 개발 또는 테스트 환경에서 사용자 계정 데이터를 쉽게 빠르고 쉬운 테스트를 배포 하는 것이 좋습니다. 스테이징 또는 프로덕션 환경에서 사용자 계정 데이터를 배포 하려는 것 가능성이 매우 아닙니다.

안타깝게도, ASP.NET 멤버 자격 데이터베이스 사항이이 결정을 훨씬 더 복잡 한 구성 하는 몇 가지 특정 문제.

- 스키마 전용 배포에는 작동 하지 않는 상태에 멤버 자격 데이터베이스를 종료 됩니다. 멤버 자격 데이터베이스 일부 구성 데이터를 포함 하기 때문에 이것이 (에 **aspnet\_SchemaVersions** 테이블) 데이터베이스에 필요한 실행 되기 위해서는 합니다. 이와 같이 사용자 계정 데이터를 제외 멤버 자격 데이터베이스의 스키마 전용 배포를 수행 하는 경우에 essential 구성 데이터를 추가 하는 배포 후 스크립트를 실행 해야 합니다.
- 멤버 자격 데이터베이스 구성 방법에 따라 멤버 자격 공급자 컴퓨터 키를 사용 하 여 암호를 암호화 하 여 데이터베이스에 저장할 수 있습니다. 이 경우 데이터베이스와 배포 사용자 계정 데이터는 대상 서버에서 사용할 수 없게 됩니다. 이러한 이유로 사용자 계정 데이터 배포는 시나리오 지원된 되지 않습니다.

## <a name="choosing-a-membership-database-strategy"></a>멤버 자격 데이터베이스 전략 선택

엔터프라이즈 서버 환경에서 멤버 자격 데이터베이스를 프로 비전 하는 방법을 선택할 때 이러한 지침을 따르세요.

- 가능 하면 멤버 자격 데이터베이스를 배포 하지 마십시오. 대상 데이터베이스 서버에서 멤버 자격 데이터베이스를 수동으로 만들 대신 합니다. 멤버 자격 데이터베이스 스키마를 사용자 지정 하지 않은 경우 만들 수 있습니다 간단히 새 situ에 사용 하 여 대상에는 [ASP.NET SQL Server 등록 도구 (aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)합니다.
- 경우에 멤버 자격 데이터베이스를 배포 하지만 옵션이 없습니다&#x2014;예를 들어, 데이터베이스 스키마를 광범위 하 게 수정할을 만든 경우&#x2014;사용자 계정 데이터를 제외 멤버 자격 데이터베이스의 스키마 전용 배포를 수행 해야 하면 다음 모든 필수 구성 데이터를 추가 하는 배포 후 스크립트를 실행 합니다. 이러한 방법에 대 한 광범위 한 지침을 찾을 수 있습니다 [하는 방법: ASP.NET 멤버 자격 데이터베이스 없이 포함 하 여 사용자 계정을 배포](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx)합니다.

사항에 유의 해야 *멤버 자격 데이터베이스의 스키마가 상당히 정적일 가능성이*합니다. 정기적으로 스키마를 업데이트 해야 그럴 가능성은 멤버 자격 데이터베이스를 사용자 지정한 경우에&#x2014;것은 잘못 된 웹 응용 프로그램 또는 데이터베이스 프로젝트의 코드와 동일한 빈도로 변경 합니다. 따라서 멤버 자격 데이터베이스는 단일 단계 또는 자동화 된 배포 프로세스에 포함할 필요는 없습니다.

## <a name="using-vsdbcmd-to-update-a-membership-database-schema"></a>VSDBCMD를 사용 하 여 멤버 자격 데이터베이스 스키마를 업데이트 하려면

첫 번째 배포 후 멤버 자격 데이터베이스의 구조를 수정 하는 경우 데이터베이스를 다시 배포 하려면 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하려는 하지 않습니다. 웹 배포에서 데이터베이스 배포 기능에는 대상 데이터베이스에 차등 업데이트를 확인 하는 기능이 포함 되어 있지 않습니다&#x2014;대신, 웹 배포 삭제 하 고 다시 만들어야 데이터베이스입니다. 즉, 스테이징 또는 프로덕션 환경에서 일반적으로 것이 바람직하지 않은 모든 기존 사용자 계정 데이터를 잃게 됩니다.

대신 사용 하는 대상 데이터베이스의 스키마를 업데이트 하는 VSDBCMD 유틸리티를 사용 하는 것입니다. VSDBCMD 두 가지 중요 한 기능이 포함 되어 있습니다. 첫째,.dbschema 파일로 기존 데이터베이스의 스키마를 가져올 수 것입니다. 둘째, 대상 데이터베이스를 최신 상태로 만드는 데 필요한 변경 내용을 더욱 모든 데이터가 손실 되지 않으며 차등 업데이트를으로 기존 데이터베이스에.dbschema 파일을 배포할 수 것입니다.

멤버 자격 데이터베이스 스키마를 업데이트 하려면 같은 대략적인 단계를 사용할 수 있습니다.

1. VSDBCMD 사용 하 여 **가져오기** 소스 멤버 자격 데이터베이스에 대 한.dbschema 파일을 생성 하는 작업입니다. 이 절차에 설명 되어 [하는 방법: 명령 프롬프트에서 스키마 가져오기](https://msdn.microsoft.com/library/dd172135.aspx)합니다.
2. VSDBCMD 사용 하 여 **배포** .dbschema 파일 대상 멤버 자격 데이터베이스에 배포 하는 작업입니다. 이 절차에 설명 되어 [VSDBCMD에 대 한 명령줄 참조 합니다. EXE (배포 및 스키마 가져오기)](https://msdn.microsoft.com/library/dd193283.aspx)합니다.

## <a name="conclusion"></a>결론

이 항목에는 다양 한 대상 환경에서 ASP.NET 멤버 자격 데이터베이스를 프로 비전 해야 할 때 직면할 수 있는 문제 중 일부를 설명 합니다. 특히, 이유 스키마 전용 배포는 멤버 자격 데이터베이스는 작동 하지 않는 상태로 남겨 및 사용자 계정 데이터 배포는 지원 되지 않는 이유 설명 되어 있습니다. 또한 항목, 프로 비전 하 고, 배포 하 고, 다양 한 시나리오에서 멤버 자격 데이터베이스를 업데이트 하는 방법에 지침을 표현 합니다.

## <a name="further-reading"></a>추가 정보

자세한 내용과 예 VSDBCMD를 사용 하는 방법에 대 한 참조 [VSDBCMD에 대 한 명령줄 참조 합니다. EXE (배포 및 스키마 가져오기)](https://msdn.microsoft.com/library/dd193283.aspx) 및 [하는 방법: 명령 프롬프트에서 스키마 가져오기](https://msdn.microsoft.com/library/dd172135.aspx)합니다. Aspnet를 사용 하 여 대 한 자세한 내용은\_멤버 자격 데이터베이스를 만들 regsql.exe 참조 [ASP.NET SQL Server 등록 도구 (aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)합니다. 멤버 자격 데이터베이스 배포에 대 한 보다 일반적인 지침을 참조 하십시오. [하는 방법: ASP.NET 멤버 자격 데이터베이스 없이 포함 하 여 사용자 계정을 배포](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx)합니다.

> [!div class="step-by-step"]
> [이전](deploying-database-role-memberships-to-test-environments.md)
> [다음](excluding-files-and-folders-from-deployment.md)
