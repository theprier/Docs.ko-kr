---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
title: 데이터베이스 프로젝트 배포 | Microsoft Docs
author: jrjlee
description: '참고: 다 수의 엔터프라이즈 배포 시나리오에 필요한 배포 된 데이터베이스를 증분 업데이트를 게시 하는 기능입니다. 대안은를 다시 만드는 중...'
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: 832f226a-1aa3-4093-8c29-ce4196793259
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
msc.type: authoredcontent
ms.openlocfilehash: 1e5af29a91f5f432f9241dc3ba0c8fc0bfcf773f
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37804985"
---
<a name="deploying-database-projects"></a>데이터베이스 프로젝트 배포
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> [!NOTE]
> 다 수의 엔터프라이즈 배포 시나리오, 배포 된 데이터베이스를 증분 업데이트를 게시 하는 기능을 해야 합니다. 대안은 기존 데이터베이스에서 데이터를 잃게 즉 모든 배포에서 데이터베이스를 다시 만듭니다. Visual Studio 2010을 사용 하 여 작업할 때 VSDBCMD 사용할 증분 데이터베이스 게시에 대 한 권장된 접근 방법입니다. 그러나 다음 버전의 Visual Studio 및 웹 게시 파이프라인 (WPP) 증분 게시 직접 지원 되는 도구가 포함 됩니다.


Visual Studio 2010에서 Contact Manager 샘플 솔루션을 열면 데이터베이스 프로젝트 파일 4 개를 포함 하는 속성 폴더에 표시 됩니다.

![](deploying-database-projects/_static/image1.png)

프로젝트 파일과 함께 (*ContactManager.Database.dbproj* 이 경우), 빌드 및 배포 프로세스의 다양 한 측면을 제어 하는 이러한 파일:

- 합니다 *Database.sqlcmdvars* 파일 프로젝트를 배포할 때 사용할 SQLCMD 변수에 대 한 값을 제공 합니다. 각 솔루션 구성 (예: 디버그 및 릴리스) 다른.sqlcmdvars 파일을 지정할 수 있습니다.
- 합니다 *Database.sqldeployment* 파일은 프로젝트 또는 대상 서버의 데이터 정렬에 정의 된 데이터 정렬을 사용할지 여부와 같은 배포 별 설정 제공 대상 데이터베이스를 다시 여부를 모든 시간 또는 단순히 기존 데이터베이스를 최신으로 가져오고 등을 수정 합니다. 각 솔루션 구성 다른.sqldeployment 파일을 지정할 수 있습니다.
- 합니다 *Database.sqlpermissions* 파일은 대상 데이터베이스에 추가 하려는 모든 사용 권한을 정의 하는 데 사용할 수 있는 XML 문서입니다. 솔루션 구성을 모두 동일한.sqlpermissions 파일을 공유 합니다.
- 합니다 *Database.sqlsettings* 파일 데이터 정렬 비교 연산자의 동작을 사용할 등과 같은 데이터베이스를 만들 때 사용할 데이터베이스 수준 속성을 지정 합니다. 모든 솔루션 구성과 동일한.sqlsettings 파일을 공유 합니다.

Visual Studio에서 이러한 파일을 열고 내용을 숙지 살펴보도록 것입니다.

데이터베이스 프로젝트를 빌드할 때 빌드 프로세스는 두 개의 파일을 만듭니다.

- A *데이터베이스 스키마* (.dbschema 파일). XML 형식으로 만들려는 데이터베이스의 스키마를 설명 합니다.
- A *배포 매니페스트* (.deploymanifest 파일). 이 만들고 데이터베이스를 배포 하는 데 필요한 모든 정보를 포함 합니다. 배포 지침 (.sqldeployment 파일) 및 모든 배포 전 또는 배포 후 SQL 스크립트와 같은 다른 리소스와 함께.dbschema 파일을 참조합니다.

이러한 리소스 간의 관계를 보여 줍니다.

![](deploying-database-projects/_static/image2.png)

알 수 있듯이.sqlsettings 파일과.sqlpermissions 파일은 빌드 프로세스에 입력 합니다. 데이터베이스 프로젝트 파일과 함께 이러한 파일은 데이터베이스 스키마 파일을 만들려면 사용 됩니다. .Sqlcmdvars 파일과.sqldeployment 파일 변경 하지 않고 빌드 프로세스를 통해 전달 합니다. 배포 매니페스트는 데이터베이스 스키마,.sqldeployment 파일,.sqlcmdvars 파일 및 모든 배포 전 또는 배포 후 SQL 스크립트의 위치를 나타냅니다.

## <a name="why-use-vsdbcmd-to-deploy-a-database-project"></a>VSDBCMD를 사용 하 여 데이터베이스 프로젝트를 배포 하는 이유?

데이터베이스 프로젝트를 배포 하는 데 다양 한 다른 방법이 있습니다. 그러나 엔터프라이즈 환경에서 원격 서버에 데이터베이스 프로젝트 배포에 그 중 일부만 적합 합니다. 데이터베이스 프로젝트 배포에서 원하는 것이 좋습니다. 엔터프라이즈 배포 시나리오에서 원하는 가능성이:

- 원격 위치에서 데이터베이스 프로젝트를 배포할 수 있습니다.
- 기존 데이터베이스를 증분 업데이트를 수행할 수 있습니다.
- 배포 전 스크립트 또는 배포 후 스크립트를 포함할 수 있습니다.
- 여러 대상 환경에 배포를 조정 하는 기능.
- 보다 크고의 일부로 데이터베이스 프로젝트를 배포 하는 기능 일반적으로 스크립팅된 단일 단계 솔루션을 배포 합니다.

가지 데이터베이스 프로젝트를 배포 하 여 세 가지 주요 방법이 있습니다.

- Visual Studio 2010에서 데이터베이스 프로젝트 형식을 사용 하 여 배포 기능을 사용할 수 있습니다. 빌드하고 Visual Studio 2010에서 데이터베이스 프로젝트를 배포할 때 배포 프로세스 배포 매니페스트를 사용 하 여 빌드 구성에 적용 하 여 SQL 기반 배포 파일을 생성 합니다. 이 이미 존재 및 이미 있을 경우 데이터베이스에 필요한 변경을 수행 하지 않는 경우 데이터베이스를 만듭니다. SQLCMD.exe를 사용 하 여 대상 서버에서이 파일을 실행 하거나 만들고 파일을 실행 하려면 Visual Studio를 설정할 수 있습니다. 이 방법의 단점은 배포 설정 제어할만 제한 됩니다. 또한 종종 환경별 변수 값을 제공 하도록 SQL 배포 파일을 수정 해야 합니다. Visual Studio 2010이 설치를 사용 하 여 컴퓨터에서이 방법을 사용할 수 있습니다 및 개발자 인지 알고 있어야 하 고 모든 대상 환경에 대 한 연결 문자열 및 자격 증명을 제공 해야 합니다.
- 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 하 [웹 응용 프로그램 프로젝트의 일부로 데이터베이스를 배포](https://msdn.microsoft.com/library/dd465343.aspx)합니다. 그러나이 방법은 단순히 대상 서버에 기존 로컬 데이터베이스를 복제 하는 것이 아니라 데이터베이스 프로젝트를 배포 하려는 경우에 훨씬 더 복잡 합니다. 데이터베이스 프로젝트를 생성 하는 SQL 배포 스크립트를 실행 하지만 이렇게 하려면 웹 배포를 구성할 수 있습니다, 웹 응용 프로그램 프로젝트에 대 한 사용자 지정 WPP 대상 파일을 만들어야 합니다. 배포 프로세스에 상당한 복잡성이 추가 됩니다. 또한 웹 배포에서는 직접 없습니다 기존 데이터베이스에 대 한 증분 업데이트를. 이 방식에 대 한 자세한 내용은 참조 하세요. [SQL 파일을 배포 패키지 데이터베이스 프로젝트에 웹 게시 파이프라인 확장](https://go.microsoft.com/?linkid=9805121)합니다.
- VSDBCMD 유틸리티를 사용 하 여 데이터베이스 스키마 또는 배포 매니페스트를 사용 하 여 데이터베이스를 배포할 수 있습니다. 큰 스크립트를 사용한 배포 프로세스의 일부로 데이터베이스를 게시할 수 있는 MSBuild 대상에서 VSDBCMD.exe를 호출할 수 있습니다. 여러 빌드 구성 만들기 않고 다양 한 환경에 대 한 배포를 사용자 지정할 수 있는 VSDBCMD 명령에서 다른 데이터베이스 속성도 많은 고.sqlcmdvars 파일에서 변수를 재정의할 수 있습니다. VSDBCMD는 데이터베이스 스키마와 대상 데이터베이스에 맞게 필요한 변경 내용만 것을 의미 하는 차별화 기능을 제공 합니다. 또한 VSDBCMD 다양 한 배포 프로세스를 보다 세분화 된 제어 기능을 제공 하는 명령줄 옵션을 제공 합니다.

이 개요에서 VSDBCMD를 사용 하 여 MSBuild를 사용 하 여 일반적인 엔터프라이즈 배포 시나리오에 가장 적합 한 방법 인지를 확인할 수 있습니다.

|  | Visual Studio 2010 | 웹 배포 2.0 | VSDBCMD.exe |
| --- | --- | --- | --- |
| 원격 배포를 지원 합니다. | 예 | 예 | 예 |
| 증분 업데이트를 지원 합니다. | 예 | 아니요 | 예 |
| 배포 전/후 배포 스크립트를 지원 합니다. | 예 | 예 | 예 |
| 다중 환경 배포를 지원 합니다. | 제한됨 | 제한됨 | 예 |
| 배포 스크립트 작성된 지원? | 제한됨 | 예 | 예 |

이 항목의 나머지 부분에서는 데이터베이스 프로젝트를 배포 하는 MSBuild 사용 하 여 VSDBCMD 사용을 설명 합니다.

## <a name="understanding-the-deployment-process"></a>배포 프로세스를 이해합니다.

VSDBCMD 유틸리티를 사용 하면 데이터베이스 스키마 (.dbschema 파일) 또는 배포 매니페스트 (.deploymanifest 파일)를 사용 하 여 데이터베이스를 배포할 수 있습니다. 실제로 배포 매니페스트를 사용 하면 다양 한 배포 속성에 대 한 기본값을 제공 하 고 실행 하려면 모든 배포 전 또는 배포 후 SQL 스크립트를 식별 하는 대로 배포 매니페스트를 거의 항상 사용할 수 있습니다. 예를 들어 배포 하려면이 VSDBCMD 명령을 사용 합니다 **ContactManager** 테스트 환경에서 데이터베이스 서버에 데이터베이스:


[!code-console[Main](deploying-database-projects/samples/sample1.cmd)]


이 경우:

- 합니다 **/a** (또는 **/Action**) 원하는 작업을 수행 하는 VSDBCMD 스위치를 지정 합니다. 이 설정할 수 있습니다 **가져오기** 하거나 **배포**합니다. 합니다 **가져오기** 옵션은 기존 데이터베이스에서.dbschema 파일을 생성 하는 데 하며 **배포** 옵션이.dbschema 파일을 대상 데이터베이스를 배포 하는 데 사용 됩니다.
- 합니다 **/매니페스트** (또는 **/ManifestFile**) 스위치를 배포 하려는.deploymanifest 파일을 식별 합니다. .Dbschema 파일을 대신 사용 하려는 경우 사용 합니다 **/모델** (또는 **/ModelFile**) 전환 합니다.
- 합니다 **/cs** (또는 **/ConnectionString**) 스위치는 대상 데이터베이스 서버에 대 한 연결 문자열을 제공 합니다. 데이터베이스의 이름을 포함 하지 않습니다이&#x2014;VSDBCMD 데이터베이스를 만들려면 서버에 연결 해야 합니다. 개별 데이터베이스에 연결할 필요가 없습니다. .Deploymanifest 파일에 연결 문자열에 포함 된 경우이 스위치를 생략할 수 있습니다. 그래도 스위치를 사용 하면 스위치 값.deploymanifest 값 보다 우선 합니다.
- 합니다 <strong>/p:TargetDatabase</strong> 속성은 생성 시 대상 데이터베이스에 할당 하려는 이름을 제공 합니다. 이 값을 재정의 합니다 <strong>TargetDatabase</strong> .deploymanifest 파일의 속성입니다. 사용할 수는 <strong>/p:</strong> <em>[속성 이름]</em>.sqlcmdvars 파일에 선언 된 구문을 다양 한 배포 속성을 설정 하 고 모든 SQLCMD 변수를 재정의 합니다.
- 합니다 **/dd+** (또는 **/DeployToDatabase+**) 스위치를 배포를 만들고 대상 환경에 배포할 것임을 나타냅니다. 지정 하는 경우 **/dd-**, 또는 스위치를 생략 VSDBCMD 배포 스크립트를 생성 합니다 있지만 대상 환경에 배포 되지 것입니다. 이 스위치 혼동의 원인이 있고 섹션에서 자세히 설명 됩니다.
- 합니다 **/script** (또는 **/DeploymentScriptFile**) 스위치 배포 스크립트를 생성 하려는 위치를 지정 합니다. 이 값 배포 프로세스에 영향을 주지 않습니다.

VSDBCMD에 대 한 자세한 내용은 참조 하세요. [VSDBCMD에 대 한 명령줄 참조 합니다. (배포 및 스키마 가져오기) EXE](https://msdn.microsoft.com/library/dd193283.aspx) 및 [방법: VSDBCMD를 사용 하 여 명령 프롬프트에서 배포에 대 한 데이터베이스를 준비 합니다. EXE](https://msdn.microsoft.com/library/dd193258.aspx)합니다.

MSBuild 프로젝트 파일에서 VSDBCMD를 사용 하는 방법의 예제를 참조 하세요 [빌드 프로세스를 이해](understanding-the-build-process.md)합니다. 여러 환경에 대 한 데이터베이스 배포 설정을 구성 하는 방법의 예제를 참조 하세요 [여러 환경에 대 한 데이터베이스 배포 사용자 지정](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)합니다.

## <a name="understanding-the-deploytodatabase-switch"></a>DeployToDatabase 전환 이해

동작을 **/dd** 또는 **/DeployToDatabase** 스위치 VSDBCMD.dbschema 파일 또는.deploymanifest 파일을 사용 하 여 사용 여부에 따라 달라 집니다. .Dbschema 파일을 사용 하는 동작을 매우 간단 합니다.

- 지정 하는 경우 **/dd+** 하거나 **/dd**, VSDBCMD 배포 스크립트를 생성 되며 데이터베이스를 배포 합니다.
- 지정 하는 경우 **/dd-** 스위치를 생략 하거나, VSDBCMD만 배포 스크립트를 생성 합니다.

.Deploymanifest 파일을 사용 하는 경우 동작은 훨씬 더 복잡 합니다. .Deploymanifest 파일에 속성 이름이 때문에 이것이 **DeployToDatabase** 또한 결정 하는 데이터베이스 배포 되는지 여부를 합니다.


[!code-xml[Main](deploying-database-projects/samples/sample2.xml)]


이 속성의 값은 데이터베이스 프로젝트의 속성에 따라 설정 됩니다. 설정 하는 경우는 **배포 작업** 하 **배포 스크립트 (.sql)를 만들**, 값은 **False**합니다. 설정 하는 경우는 **배포 작업** 하 **배포 스크립트 (.sql)을 만들고 데이터베이스에 배포**, 값은 **True**.

> [!NOTE]
> 이러한 설정은 특정 빌드 구성 및 플랫폼을 사용 하 여 연결 합니다. 예를 들어에 대 한 설정을 구성 하는 경우는 **디버그** 구성을 사용 하 여 게시 합니다 **릴리스** 구성 설정을 사용 하지 것입니다.


![](deploying-database-projects/_static/image3.png)

> [!NOTE]
> 이 시나리오에서는 합니다 **배포 작업** 항상로 설정 해야 **배포 스크립트 (.sql)를 만들**데이터베이스를 배포 하려면 Visual Studio 2010 않으려고 하기 때문에, 합니다. 즉, 합니다 **DeployToDatabase** 속성은 항상 **False**합니다.


경우는 **DeployToDatabase** 속성을 지정 합니다 **/dd** 속성 값이 스위치는 속성을 재정의 **false**:

- 경우는 **DeployToDatabase** 속성은 **False**를 지정 **/dd+** 또는 **/dd**, VSDBCMD 재정의  **DeployToDatabase** 속성 및 데이터베이스를 배포 합니다.
- 경우는 **DeployToDatabase** 속성은 **False**를 지정 하면 **/dd-** 스위치를 생략 하거나, VSDBCMD 데이터베이스를 배포 하지 것입니다.
- 경우는 **DeployToDatabase** 속성은 **True**, VSDBCMD는 스위치를 무시 하 고 데이터베이스를 배포 합니다.
- 배포 스크립트는 물론 데이터베이스를 배포 하 든 관계 없이 각각의 경우에 생성 됩니다.

## <a name="conclusion"></a>결론

이 항목에서는 Visual Studio 2010에서 데이터베이스 프로젝트 빌드 및 배포 프로세스의 개요를 제공 합니다. 또한 엔터프라이즈 규모 데이터베이스 배포를 지원 하기 위해 MSBuild를 사용 하 여 VSDBCMD.exe를 사용 하는 방법을 설명 합니다.

실제로 작동 하는 방법에 대 한 자세한 내용은 참조 하세요. [여러 환경에 대 한 데이터베이스 배포 사용자 지정](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)합니다.

## <a name="further-reading"></a>추가 정보

각 환경에 대 한 별도 배포 구성 파일을 만들어 데이터베이스 배포를 사용자 지정 하는 방법에 대 한 자세한 내용은 [여러 환경에 대 한 데이터베이스 배포 사용자 지정](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)합니다. 배포 후 스크립트를 실행 하 여 데이터베이스 역할 멤버 자격을 구성 하는 방법에 대 한 지침을 참조 하세요 [배포 데이터베이스 역할 멤버 자격 테스트 환경에](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)입니다. 고유한 과제 중 일부는 멤버 자격을 관리 하는 지침은 데이터베이스 적용, 참조 [엔터프라이즈 환경에 멤버 자격 데이터베이스 배포](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)합니다.

MSDN의 이러한 항목에는 광범위 한 지침 및 배경 정보는 Visual Studio 데이터베이스 프로젝트 및 데이터베이스 배포 프로세스를 제공합니다.

- [Visual Studio 2010 SQL Server 데이터베이스 프로젝트](https://msdn.microsoft.com/library/ff678491.aspx)
- [데이터베이스 변경 내용 관리](https://msdn.microsoft.com/library/aa833404.aspx)
- [방법: VSDBCMD를 사용 하 여 명령 프롬프트에서 배포에 대 한 데이터베이스를 준비 합니다. EXE](https://msdn.microsoft.com/library/dd193258.aspx)
- [데이터베이스 빌드 및 배포 개요](https://msdn.microsoft.com/library/aa833165.aspx)

> [!div class="step-by-step"]
> [이전](deploying-web-packages.md)
> [다음](creating-and-running-a-deployment-command-file.md)
