---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
title: 데이터베이스 역할 멤버 자격 테스트 환경에 배포 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 테스트 환경에 솔루션 배포의 일부로 데이터베이스 역할에 사용자 계정을 추가 하는 방법을 설명 합니다. 포함 된 솔루션을 배포할 때 사용 하는 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: 9b2af539-7ad9-47aa-b66e-873bd9906e79
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
msc.type: authoredcontent
ms.openlocfilehash: 42ceaa654c7f690f8455c0569e347cd5e9fccf7a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37401862"
---
<a name="deploying-database-role-memberships-to-test-environments"></a>테스트 환경에 배포 데이터베이스 역할 멤버 자격
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 테스트 환경에 솔루션 배포의 일부로 데이터베이스 역할에 사용자 계정을 추가 하는 방법을 설명 합니다.
> 
> 스테이징 또는 프로덕션 환경에 데이터베이스 프로젝트를 포함 하는 솔루션을 배포할 때는 일반적으로 원하지 개발자가 데이터베이스 역할에 사용자 계정을 추가 자동화할 수입니다. 대부분의 경우에서 개발자는 데이터베이스 역할에 추가 해야 하는 사용자 계정을 알 수 없습니다 하 고 언제 든 지 이러한 요구 사항을 변경할 수 없습니다. 그러나을 개발 하는 데이터베이스 프로젝트를 포함 하는 솔루션을 배포 하거나 테스트 환경을 상황은 일반적으로 다른:
> 
> - 개발자는 일반적으로 다시 솔루션도 배포 합니다는 정기적으로 하루에 여러 번 경우가 많습니다.
> - 일반적으로 데이터베이스는 데이터베이스 사용자를 생성 및 모든 배포 후 역할에 추가 해야 하는 모든 배포에서 다시 생성 됩니다.
> - 일반적으로 개발자가 대상 개발 또는 테스트 환경 전체 제어 합니다.
> 
> 이 시나리오에서는 자동으로 데이터베이스 사용자를 만들고 배포 프로세스의 일부로 데이터베이스 역할 멤버 자격을 할당 하는 데 유용한 경우가 있습니다.
> 
> 주요 요인은이 작업 해야 함을 조건부 대상 환경에 따라입니다. 스테이징 또는 프로덕션 환경에 배포 하는 경우 작업을 건너 뛰 려 합니다. 개발자에 게 배포 하는 환경 테스트 하거나, 추가 개입 없이 역할 멤버 자격을 배포 하려고 합니다. 이 항목에서는 한 가지 방법은이 문제를 해결 하기 위해 사용할 수 있습니다.


이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.

이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="task-overview"></a>작업 개요

이 항목을 가정합니다.

- 분할 프로젝트 파일 방법은 솔루션 배포를 사용 하 여에 설명 된 대로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다.
- 에 설명 된 대로 VSDBCMD 데이터베이스 프로젝트를 배포 하려면 프로젝트 파일에서 호출할 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)합니다.

데이터베이스 사용자를 만들고 테스트 환경에 데이터베이스 프로젝트를 배포할 때 역할 멤버 자격을 할당 하려면를 해야 합니다.

- 필요한 데이터베이스 변경을 수행 하는 Transact 구조적 쿼리 언어 (TRANSACT-SQL) 스크립트를 만듭니다.
- Sqlcmd.exe 유틸리티를 사용 하 여 SQL 스크립트를 실행 하는 Microsoft Build Engine (MSBuild) 대상을 만듭니다.
- 테스트 환경에 솔루션을 배포 하는 경우 대상을 호출 하 여 프로젝트 파일을 구성 합니다.

이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여줍니다.

## <a name="scripting-the-database-role-memberships"></a>데이터베이스 역할 멤버 자격을 스크립팅

다른 방법으로 많은 Transact SQL 스크립트를 만들고 원하는 위치에. 가장 쉬운 방법은 Visual Studio 2010의 솔루션 내에서 스크립트를 만드는 것입니다.

**SQL 스크립트를 만들려면**

1. 에 **솔루션 탐색기** 창에서 데이터베이스 프로젝트 노드를 확장 합니다.
2. 마우스 오른쪽 단추로 클릭 합니다 **스크립트** 폴더를 가리킵니다 **추가**를 클릭 하 고 **새 폴더**합니다.
3. 형식 **테스트** 폴더 이름과 한 다음 Enter 키를 누릅니다.
4. 마우스 오른쪽 단추로 클릭 합니다 **테스트** 폴더를 가리킵니다 **추가**를 클릭 하 고 **스크립트**합니다.
5. 에 **새 항목 추가** 대화 상자에서 스크립트에 의미 있는 이름을 (예를 들어 **AddRoleMemberships.sql**)를 클릭 하 고 **추가**합니다.

    ![](deploying-database-role-memberships-to-test-environments/_static/image1.png)
6. 에 *AddRoleMemberships.sql* 파일, TRANSACT-SQL 문을 추가 하는:

    1. 데이터베이스를 액세스 하는 SQL Server 로그인에 대 한 데이터베이스 사용자를 만듭니다.
    2. 필요한 데이터베이스 역할에 데이터베이스 사용자를 추가 합니다.
7. 파일은 다음과 같습니다.

    [!code-sql[Main](deploying-database-role-memberships-to-test-environments/samples/sample1.sql)]
8. 파일을 저장합니다.

## <a name="executing-the-script-on-the-target-database"></a>대상 데이터베이스에서 스크립트를 실행합니다.

이상적으로 데이터베이스 프로젝트를 배포할 때 배포 후 스크립트의 일부로 모든 필요한 TRANSACT-SQL 스크립트를 실행할 것 있습니다. 그러나 배포 후 스크립트 솔루션 구성 또는 빌드 속성에 따라 조건부 논리를 실행할 수 없습니다. 대안은 만들어 MSBuild 프로젝트 파일에서 직접 SQL 스크립트를 실행 하는 **대상** sqlcmd.exe 명령을 실행 하는 요소입니다. 대상 데이터베이스에서 스크립트를 실행 하려면이 명령을 사용할 수 있습니다.


[!code-console[Main](deploying-database-role-memberships-to-test-environments/samples/sample2.cmd)]


> [!NOTE]
> Sqlcmd 명령줄 옵션에 대 한 자세한 내용은 참조 하세요. [sqlcmd 유틸리티](https://msdn.microsoft.com/library/ms162773.aspx)합니다.


이 명령은 MSBuild 대상에 포함 하면 전에 고려해 야 어떤 조건에서 스크립트를 실행 해야 합니다.

- 대상 데이터베이스의 역할 멤버 자격을 변경 하기 전에 존재 해야 합니다. 이 스크립트를 실행 해야 하는 이와 같이 *후* 데이터베이스 배포 합니다.
- 스크립트를 테스트 환경에만 실행 되도록 조건을 포함 해야 합니다.
- "What if" 배포를 실행 하는 경우&#x2014;즉, 배포 스크립트를 생성 하지만 실제로 실행 하는 경우&#x2014;SQL 스크립트를 실행 해서는 안 됩니다.

에 설명 된 분할 프로젝트 파일 방법을 사용 하는 경우 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), Contact Manager 샘플 솔루션에서 볼 수 있듯이, 다음과 같은 SQL 스크립트에 대 한 빌드 지침을 분할할 수 있습니다.

- 환경 관련 프로젝트 파일의 권한을 배포할지 여부를 결정 하는 속성과 함께 환경 관련 속성을 이동 해야 필요한 (예를 들어 *Env Dev.proj*).
- 대상 환경 간에 변경 되지 않는 모든 속성과 함께 MSBuild 대상 자체 유니버설 프로젝트 파일에서 이동 해야 합니다 (예를 들어 *Publish.proj*).

환경 관련 프로젝트 파일에서 데이터베이스 서버 이름, 대상 데이터베이스 이름 및 역할 멤버 자격을 배포할지 여부를 지정할 수 있도록 하는 부울 속성을 정의 해야 합니다.


[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample3.xml)]


유니버설 프로젝트 파일에서 sqlcmd 실행 파일의 위치 및를 실행 하려는 SQL 스크립트의 위치를 제공 해야 합니다. 이러한 속성 대상 환경에 관계 없이 동일 하 게 유지 됩니다. Sqlcmd 명령을 실행 하는 MSBuild 대상을 만드는 해야 합니다.


[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample4.xml)]


다른 대상에 유용할 수 있습니다이으로 정적 속성으로 sqlcmd 실행 파일의 위치를 추가 하는 확인 합니다. 반면, SQL 스크립트의 위치 및 sqlcmd 명령의 구문을 대상 속성을 동적으로으로 정의한 되지 않으므로 필요한 대상이 실행 되기 전에 합니다. 이 경우에 **DeployTestDBPermissions** 대상 이러한 조건이 충족 될 경우에 실행 됩니다.

- 합니다 **DeployTestDBRoleMemberships** 속성이 **true**합니다.
- 사용자 지정 되지 않은 한 **WhatIf = true** 플래그입니다.

마지막으로 반드시 대상을 호출 합니다. 에 *Publish.proj* 파일을 할 수 있는이 대상 기본값에 대 한 종속성 목록에 추가 하 여 **FullPublish** 대상입니다. 되도록 해야 합니다 **DeployTestDBPermissions** 대상 될 때까지 실행 되지 않습니다는 **PublishDbPackages** 대상이 실행 되었는지 합니다.


[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample5.xml)]


## <a name="conclusion"></a>결론

이 항목에서는 단방향은 추가할 수 있습니다 데이터베이스 사용자 및 역할 멤버 자격 배포 후 작업으로 데이터베이스 프로젝트를 배포 하는 경우를 설명 합니다. 정기적으로 테스트 환경에서 데이터베이스를 다시 만들 경우 일반적으로를 피해 야 스테이징 또는 프로덕션 환경에 데이터베이스를 배포할 때 일반적으로 유용 합니다. 따라서 이렇게 하려면 적절 한 경우 데이터베이스 사용자 및 역할 멤버 자격만 생성 됩니다 있도록 필요한 조건부 논리를 사용 하는 확인 해야 합니다.

## <a name="further-reading"></a>추가 정보

VSDBCMD를 사용 하 여 데이터베이스 프로젝트를 배포 하는 방법은 참조 하세요 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)합니다. 사용자 지정 된 다른 대상 환경에 대 한 데이터베이스 배포에 대 한 지침을 참조 하세요 [여러 환경에 대 한 데이터베이스 배포 사용자 지정](customizing-database-deployments-for-multiple-environments.md)합니다. 사용자 지정 MSBuild 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하에 대 한 자세한 내용은 참조 하세요. [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 하 고 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)합니다. Sqlcmd 명령줄 옵션에 대 한 자세한 내용은 참조 하세요. [sqlcmd 유틸리티](https://msdn.microsoft.com/library/ms162773.aspx)합니다.

> [!div class="step-by-step"]
> [이전](customizing-database-deployments-for-multiple-environments.md)
> [다음](deploying-membership-databases-to-enterprise-environments.md)
