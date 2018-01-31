---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
title: "사용자 지정 된 여러 환경에 대 한 데이터베이스 배포 | Microsoft Docs"
author: jrjlee
description: "이 항목에서는 배포 프로세스의 일환으로 특정 대상 환경에 데이터베이스의 속성을 구성 하는 방법을 설명 합니다. 참고: 항목 가정 번째 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: a172979a-1318-4318-a9c6-4f9560d26267
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
msc.type: authoredcontent
ms.openlocfilehash: f3ca344c2466d9d538f55cd8ff0a5bf5b7bac808
ms.sourcegitcommit: 060879fcf3f73d2366b5c811986f8695fff65db8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2018
---
<a name="customizing-database-deployments-for-multiple-environments"></a>사용자 지정 된 여러 환경에 대 한 데이터베이스 배포
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 배포 프로세스의 일환으로 특정 대상 환경에 데이터베이스의 속성을 구성 하는 방법을 설명 합니다.
> 
> > [!NOTE]
> > 항목은 VSDBCMD.exe 및 MSBuild.exe를 사용 하 여 Visual Studio 2010 데이터베이스 프로젝트를 배포 한다고 가정 합니다. 이 방법은 수도 있습니다에 대 한 자세한 내용은 참조 하십시오. [기업에서 웹 배포](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md) 및 [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)합니다.
> 
> 
> 여러 대상에 데이터베이스 프로젝트를 배포할 때 각 대상 환경에 데이터베이스 배포 속성을 사용자 지정 하고자 합니다. 예를 들어 테스트 환경에서 일반적으로 다시 만드는 것 모든 배포에 있는 데이터베이스 반면 스테이징 또는 프로덕션 환경에서 수 더 많은 데이터를 보존 하도록 증분 업데이트를 수행 합니다.
> 
> Visual Studio 2010 데이터베이스 프로젝트의 배포 설정은 배포 구성 (.sqldeployment) 파일 포함 되어 있습니다. 이 항목에서는 환경 관련 배포 구성 파일을 만들고 VSDBCMD 매개 변수로 사용 하려면를 지정 하는 방법을 보여줍니다.


이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 이 자습서 시리즈 샘플 솔루션 & #x 2014;을 사용 하는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)& #x 2014; 현실적인 수준의 복잡성을 Windows ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 제공 합니다.

이 자습서의 핵심에는 배포 방법에 설명 된 분할 프로젝트 파일 접근 방식에 따라 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 빌드 프로세스에 의해 제어 되는 두 프로젝트에 파일 & #x 2014; 포함 환경 관련 빌드 및 배포 설정을 포함 하는 하나 및 모든 대상 환경에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 구성 하기 위해 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="task-overview"></a>작업 개요

이 항목에 있다고 가정 합니다.

- 솔루션 배포에 대 한 분할 프로젝트 파일 접근을 사용 하 여에 설명 된 대로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)합니다.
- 에 설명 된 대로 VSDBCMD 데이터베이스 프로젝트를 배포할 프로젝트 파일에서 호출 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)합니다.

대상 환경 간에 데이터베이스 배포 속성을 다양 한 배포 프로그램을 만들려면 해야 합니다.

- 각 대상 환경에 배포 (.sqldeployment) 구성 파일을 만듭니다.
- 명령줄 스위치와 배포 구성 파일을 지정 하는 VSDBCMD 명령을 만듭니다.
- VSDBCMD 옵션은 대상 환경에 적절 한 수 있도록 Microsoft Build Engine (MSBuild) 프로젝트 파일에서 VSDBCMD 명령을 매개 변수화 합니다.

이 항목에서는 이러한 각 절차를 수행 하는 방법을 보여줍니다.

## <a name="creating-environment-specific-deployment-configuration-files"></a>환경 관련 배포 구성 파일 만들기

기본적으로 데이터베이스 프로젝트 라는 단일 배포 구성 파일을 포함 *Database.sqldeployment*합니다. Visual Studio 2010에서이 파일을 열 경우 사용할 수 있는 다양 한 배포 옵션을 확인할 수 있습니다.

- **배포 비교 데이터 정렬**합니다. 이렇게 하면 프로젝트의 데이터베이스 데이터 정렬을 사용할지 여부를 선택할 수 있습니다 (의 *소스* 데이터 정렬) 또는 대상 서버의 데이터베이스 데이터 정렬 (의 *대상* 데이터 정렬). 대부분의 경우, 환경을 테스트 나 개발에 배포할 때 원본 데이터 정렬을 사용 합니다. 스테이징 또는 프로덕션 환경에 배포할 때 대상 데이터 정렬의 상호 운용성 문제를 방지 하기 위해 변경 되지 않은 상태로 그대로 둡니다. 일반적으로 해야 합니다.
- **데이터베이스 속성 배포**합니다. 에 정의 된 대로 데이터베이스 속성을 적용할지 여부를 선택할 수 있습니다는 *Database.sqlsettings* 파일입니다. 처음으로 데이터베이스를 배포 하는 경우에 데이터베이스 속성 배포 해야 합니다. 기존 데이터베이스를 업데이트 하는 경우 속성을 제자리에 이미 있어야 하 고 다시 배포할 필요는 없습니다.
- **항상 데이터베이스 다시 만들기**합니다. 배포 하거나 스키마와 대상 데이터베이스의 증분 변경 내용을 최신 상태로 확인 될 때마다 데이터베이스에서 대상 데이터베이스로 다시 만들지 여부를 선택할 수이 있습니다. 데이터베이스를 다시 만드는 경우에 기존 데이터베이스의 모든 데이터를 손실 됩니다. 따라서 일반적으로으로 설정 해야이 **false** 스테이징 또는 프로덕션 환경에 배포 합니다.
- **데이터가 손실 되 면 증분 배포 차단**합니다. 데이터베이스 스키마에 대 한 변경으로 인해 데이터가 손실 될 경우 배포를 중지할지 여부를 선택할 수 있습니다. 일반적으로 설정 하면 **true** 개입 하 고 중요 한 데이터를 보호 하는 기회를 제공 하려면 프로덕션 환경에 배포 합니다. 설정한 경우 **항상 데이터베이스 다시 만들기** 를 **false**,이 설정은 아무런 효과가 없습니다.
- **단일 사용자 모드에서 배포를 실행**합니다. 이것이 일반적으로 개발 또는 테스트 환경에서 문제입니다. 그러나 일반적으로를 설정 해야이 **true** 스테이징 또는 프로덕션 환경에 배포 합니다. 이 사용자를가 배포 진행 중일 때 데이터베이스를 변경 하 수 없습니다.
- **배포 하기 전에 데이터베이스를 백업**합니다. 일반적으로 설정 하면 **true** 데이터 손실 방지 하기 위해 프로덕션 환경에 배포할 때. 이 속성을 설정 하려면 **true** 스테이징 환경에 배포할 때 많은 양의 데이터를 포함 하는 준비 데이터베이스입니다.
- **대상 데이터베이스에 있지만 데이터베이스 프로젝트에 없는 개체에 대 한 DROP 문 생성**합니다. 대부분의 경우에서 데이터베이스에 대 한 증분 변경의 정수이 고 필수적인 부분입니다. 설정한 경우 **항상 데이터베이스 다시 만들기** 를 **false**,이 설정은 아무런 효과가 없습니다.
- **CLR 유형 업데이트 하려면 ALTER ASSEMBLY 문을 사용 하지 마십시오**합니다. 이 설정은 SQL Server 최신 어셈블리 버전에는 공용 언어 런타임 (CLR) 형식 업데이트 해야 방법을 결정 합니다. 이 값 설정 해야 **false** 대부분의 시나리오에서 합니다.

이 테이블에는 다른 대상 환경에 대 한 일반적인 배포 설정을 보여 줍니다. 그러나 설정을 정확한 요구 사항에 따라 다를 수 있습니다.

|  | 개발자/테스트 | 준비/통합 | 프로덕션 |
| --- | --- | --- | --- |
| **배포 비교 데이터 정렬** | 소스 | 대상 | 대상 |
| **데이터베이스 속성 배포** | True | 최초 구매 시에만 입력 | 최초 구매 시에만 입력 |
| **항상 데이터베이스 다시 만들기** | True | False | False |
| **데이터가 손실 되 면 증분 배포 차단** | False | 미정 | True |
| **단일 사용자 모드에서 배포 스크립트 실행** | False | True | True |
| **배포 하기 전에 데이터베이스 백업** | False | 미정 | True |
| **대상 데이터베이스에 있지만 데이터베이스 프로젝트에 없는 개체에 대 한 DROP 문 생성** | False | True | True |
| **CLR 유형 업데이트 하려면 ALTER ASSEMBLY 문을 사용 하지 마십시오** | False | False | False |
  

> [!NOTE]
> 데이터베이스 배포 속성 및 환경 고려 사항에 대 한 자세한 내용은 참조 하십시오. [는 개요의 데이터베이스 프로젝트 설정이](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx), [하는 방법: 배포 세부 정보에 대 한 구성 속성](https://msdn.microsoft.com/library/dd172125.aspx), [ 빌드 및 격리 된 개발 환경에 데이터베이스 배포](https://msdn.microsoft.com/library/dd193409.aspx), 및 [스테이징 또는 프로덕션 환경에 데이터베이스를 빌드하여](https://msdn.microsoft.com/library/dd193413.aspx)합니다.


여러 대상에 데이터베이스 프로젝트의 배포를 지원 하려면 각 대상 환경에 배포 구성 파일을 만들어야 합니다.

**환경 관련 구성 파일을 만들려면**

1. Visual Studio 2010에서에 **솔루션 탐색기** 창 데이터베이스 프로젝트를 마우스 오른쪽 단추로 클릭 **속성**합니다.
2. 데이터베이스 프로젝트 속성 페이지에서에 **배포** 탭에 **배포 구성 파일** 행에서 클릭 **새로**합니다.

    ![](customizing-database-deployments-for-multiple-environments/_static/image1.png)
3. 에 **새 배포 구성 파일** 대화 상자에서 파일에 의미 있는 이름을 지정 (예를 들어 **TestEnvironment.sqldeployment**)를 클릭 하 고 **저장**합니다.
4. 에 *[Filename] * * *.sqldeployment** 페이지, 대상 환경의 요구 사항에 맞게 배포 속성을 설정 하 고 다음 파일을 저장 합니다.

    ![](customizing-database-deployments-for-multiple-environments/_static/image2.png)
5. 공지 새 파일이 데이터베이스 프로젝트의 Properties 폴더에 추가 됩니다.

    ![](customizing-database-deployments-for-multiple-environments/_static/image3.png)

## <a name="specifying-the-deployment-configuration-file-in-vsdbcmd"></a>VSDBCMD에서 배포 구성 파일을 지정합니다.

Visual Studio 2010 내에서 (예: 디버그 및 릴리스) 솔루션을 구성을 사용 하는 경우 각 구성 된 배포 구성 파일을 연결할 수 있습니다. 특정 구성을 빌드할 때 빌드 프로세스 구성 관련 배포 구성 파일을 가리키는 구성 관련 배포 매니페스트 파일을 생성 합니다. 그러나 Visual Studio 2010 및 솔루션 구성을 사용 하지 않고 배포 프로세스를 제어 하는 기능 사용자에 게이 자습서에 설명 된 배포에 대 한 접근의 주요 목표 중 하나입니다. 이 방법에서 솔루션 구성을 대상 배포 환경에 관계 없이 같습니다. 데이터베이스 배포를 특정 대상 환경에 맞게 배포 구성 파일을 지정 하려면 VSDBCMD 명령줄 옵션을 사용할 수 있습니다.

사용 하 여 프로그램 VSDBCMD 배포 구성 파일을 지정 하려면는 **p: / DeploymentConfigurationFile** 전환 하 고 파일에 전체 경로 제공 합니다. 그러면 배포 매니페스트를 식별 하는 배포 구성 파일을 재정의 됩니다. 예를 들어이 VSDBCMD 명령을 배포에 사용할 수 있습니다는 **ContactManager** 테스트 환경에 데이터베이스:


[!code-console[Main](customizing-database-deployments-for-multiple-environments/samples/sample1.cmd)]


> [!NOTE]
> 참고 출력 디렉터리에 파일을 복사 하는 경우 빌드 프로세스.sqldeployment 파일 이름을 바꿀 수 있습니다.


배포 전 또는 배포 후 SQL 스크립트에서 SQL 명령 변수를 사용 하는 경우에 배포와 환경별.sqlcmdvars 파일을 연결 하려면 유사한 방법을 사용할 수 있습니다. 사용 하는 경우에 **p: / SqlCommandVariablesFile** 스위치.sqlcmdvars 파일을 식별 합니다.

## <a name="running-the-vsdbcmd-command-from-an-msbuild-project-file"></a>MSBuild 프로젝트 파일에서 VSDBCMD 명령을 실행

사용 하 여 MSBuild 프로젝트 파일에서 VSDBCMD 명령을 호출할 수 있습니다는 **Exec** MSBuild 대상 내에서 작업 합니다. 가장 간단한 형태의 것은 다음과 같습니다.


[!code-xml[Main](customizing-database-deployments-for-multiple-environments/samples/sample2.xml)]


- 실제로 프로젝트 파일을 쉽게 읽고를 다시 사용할 수 있도록 하려면 합니다를 만드는 다양 한 명령줄 매개 변수를 저장 하는 속성. 따라서 환경별 프로젝트 파일에서 속성 값을 제공 하거나 MSBuild 명령줄에서 기본값을 재정의 하려면 사용자가 쉽게 있습니다. 에 설명 된 분할 프로젝트 파일 접근 방식을 사용 하는 경우 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 빌드 지침과 두 파일 간에 속성을 적절 하 게 구분 해야 합니다.
- 배포 구성 파일 이름, 데이터베이스 연결 문자열 및 대상 데이터베이스 이름이 같은 환경 관련 설정 환경별 프로젝트 파일에 복사 해야 합니다.
- 해당 VSDBCMD 실행 파일의 위치와 같은 모든 유니버설 속성 VSDBCMD 명령을 실행 하는 MSBuild 대상을 유니버설 프로젝트 파일에 복사 해야 합니다.

또한.deploymanifest 파일이 생성 되 고 사용할 준비가 되도록 VSDBCMD를 호출 하기 전에 데이터베이스 프로젝트를 빌드할 확인 해야 합니다. 항목에이 접근 방법의 전체 예제를 확인할 수 있습니다 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md), 프로젝트 파일에서 안내 하는 [않아 샘플 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)합니다.

## <a name="conclusion"></a>결론

이 항목 VSDBCMD 및 MSBuild를 사용 하 여 데이터베이스 프로젝트를 배포할 때 다른 대상 환경에 대 한 데이터베이스 속성을 조정할 수는 방법을 설명 합니다. 이 방법은 더 큰, 엔터프라이즈 규모 솔루션의 일부분으로 데이터베이스 프로젝트를 배포 해야 할 때 유용 합니다. 이러한 솔루션은 대개 샌드박스 개발 또는 테스트 환경, 준비 또는 통합 플랫폼 및 프로덕션 라이브 환경 등의 여러 대상에 배포 됩니다. 일반적으로 각 대상 환경에 고유한 데이터베이스 배포 속성 집합이 필요합니다.

## <a name="further-reading"></a>추가 정보

VSDBCMD.exe를 사용 하 여 데이터베이스 프로젝트를 배포 하는 방법에 대 한 자세한 내용은 참조 하십시오. [데이터베이스 프로젝트 배포](../web-deployment-in-the-enterprise/deploying-database-projects.md)합니다. 배포 프로세스 제어 기능을 사용자 지정 MSBuild 프로젝트 파일 사용에 대 한 자세한 내용은 참조 하십시오. [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 및 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)합니다.

MSDN에서 이러한 문서에 데이터베이스 배포 보다 일반적인 지침을 제공합니다.

- [데이터베이스 프로젝트 설정의 개요](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx)
- [방법: 배포 세부 정보에 대 한 속성을 구성 합니다.](https://msdn.microsoft.com/library/dd172125.aspx)
- [빌드 및 격리 된 개발 환경에 데이터베이스 배포](https://msdn.microsoft.com/library/dd193409.aspx)
- [빌드 및 스테이징 또는 프로덕션 환경에 데이터베이스 배포](https://msdn.microsoft.com/library/dd193413.aspx)

>[!div class="step-by-step"]
[이전](performing-a-what-if-deployment.md)
[다음](deploying-database-role-memberships-to-test-environments.md)
