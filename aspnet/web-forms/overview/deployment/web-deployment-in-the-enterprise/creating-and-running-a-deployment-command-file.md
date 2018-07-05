---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: 명령 파일 만들기 및 배포를 실행 합니다. | Microsoft Docs
author: jrjlee
description: 이 항목에서는 단일 단계로, Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 하 여 다시 배포를 실행할 수 있도록 명령 파일을 작성 하는 방법을 설명 하는 중...
ms.author: aspnetcontent
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: 6b2a75e0740f648a3a6e4f39c00bd30609325728
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37830304"
---
<a name="creating-and-running-a-deployment-command-file"></a>만들기 및 배포 명령 파일을 실행 합니다.
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 Microsoft Build Engine (MSBuild) 프로젝트 파일을 사용 하 여 단일 단계 및 반복 가능한 프로세스로 배포를 실행할 수 있도록 명령 파일을 작성 하는 방법을 설명 합니다.


이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager](the-contact-manager-solution.md) 솔루션&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.

이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [빌드 프로세스를 이해](understanding-the-build-process.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="process-overview"></a>프로세스 개요

이 항목을 만들고이 프로젝트 파일을 사용 하 여 대상 환경에 반복 가능한 배포를 수행 하는 명령 파일을 실행 하는 방법에 알아봅니다. 기본적으로, 명령 파일 단순히 포함 해야 하는 MSBuild 명령입니다.

- 환경-알 수 없는 실행 하는 MSBuild 지시 *Publish.proj* 파일입니다.
- 지시 합니다 *Publish.proj* 파일 환경별 프로젝트 설정 및 그 위치를 포함 하는 파일입니다.

## <a name="create-an-msbuild-command"></a>MSBuild 명령 만들기

에 설명 된 대로 [빌드 프로세스를 이해](understanding-the-build-process.md), 환경별 프로젝트 파일을&#x2014;예를 들어 *Env Dev.proj*&#x2014;는 독립적인 환경으로 가져올 수 있도록 설계 되었습니다 *Publish.proj* 빌드 시에는 파일입니다. 함께,이 두 파일 MSBuild 빌드하고 솔루션을 배포 하는 방법을 알려주는 지침의 전체 집합을 제공 합니다.

합니다 *Publish.proj* 사용 하 여 파일을 **가져오기** 환경별 프로젝트 파일을 가져올 요소입니다.


[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]


따라서 MSBuild.exe를 사용 하 여 Contact Manager 솔루션을 빌드 및 배포 하는 경우에 필요 합니다.

- MSBuild.exe를 실행 합니다 *Publish.proj* 파일입니다.
- 라는 명령줄 매개 변수를 제공 하 여 환경 관련 프로젝트 파일의 위치를 지정할 **TargetEnvPropsFile**합니다.

이렇게 하려면 MSBuild 명령은 다음과 같습니다.


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]


여기에서 단일 단계를 반복 가능 하 고 배포를 이동 하는 간단한 단계가 것입니다. 하기만 하면 MSBuild 명령.cmd 파일에 추가 하는 것입니다. Contact Manager 솔루션을 게시 폴더 포함 이라는 파일로 *게시 Dev.cmd* 이 정확 하 게 수행 하는 합니다.


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]


> [!NOTE]
> 합니다 **/fl** 스위치를 지정 하면 명명 된 로그 파일을 만드는 MSBuild *msbuild.log* MSBuild.exe 호출 된 작업 디렉터리에 있습니다.


를 배포 하거나 Contact Manager 솔루션을 다시 배포 하기만 하면 실행 되는 *게시 Dev.cmd* 파일입니다. 파일을 실행 하는 경우 MSBuild는:

- 솔루션의 모든 프로젝트를 빌드하십시오.
- 웹 응용 프로그램 프로젝트에 대 한 배포 가능한 웹 패키지를 생성 합니다.
- 데이터베이스 프로젝트에 대 한.dbschema 및.deploymanifest 파일을 생성 합니다.
- 웹 서버에 웹 패키지를 배포 합니다.
- 데이터베이스 서버에 데이터베이스를 배포 합니다.

## <a name="run-the-deployment"></a>배포를 실행 합니다.

대상 환경에 대 한 명령 파일을 만든 경우에 단순히 파일을 실행 하 여 전체 배포를 완료할 수 해야 합니다.

**테스트 환경에 맞게 Contact Manager 솔루션을 배포 하려면**

1. 개발자 워크스테이션에서 Windows 탐색기를 열고 다음의 위치로 이동 합니다 *게시 Dev.cmd* 파일입니다.
2. 실행 파일을 두 번 클릭 합니다.
3. 경우는 **파일 열기-보안 경고** 대화 상자가 나타나면 **실행**합니다.
4. 구성 설정 및 테스트 서버를 설정 된 경우 올바르게는 명령 프롬프트 창에 표시 됩니다는 **빌드 성공** MSBuild 프로젝트 파일 처리를 완료 하는 경우 메시지입니다.

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. 테스트 웹 서버 컴퓨터 계정에 추가 해야 처음이이 환경에 솔루션을 배포한 경우 합니다 **db\_datawriter** 하 고 **db\_datareader**역할을 합니다 **ContactManager** 데이터베이스입니다. 이 절차에 설명 되어 [웹 배포 게시에 대 한 데이터베이스 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)합니다.

    > [!NOTE]
    > 데이터베이스를 만들 때 이러한 사용 권한을 할당 해야 합니다. 기본적으로 빌드 프로세스를 다시 만들지 모든 배포에서 데이터베이스&#x2014;대신 기존 데이터베이스를 최신 스키마를 비교 하 고 필요한 변경 내용만 확인 합니다. 결과적으로 이러한 데이터베이스 역할에 처음으로 솔루션을 배포한 매핑할 해야만 합니다.
6. Internet Explorer를 열고 연락처 관리자 응용 프로그램의 URL로 이동 (예를 들어 `http://testweb1:85/ContactManager/`).
7. 응용 프로그램이 예상 대로 작동 하는지 확인 하 고 연락처를 추가할 수 있습니다.

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a>결론

MSBuild 지침이 포함 된 명령 파일을 만들어 구축 하 고 다중 프로젝트 솔루션을 특정 대상 환경에 배포 하는 빠르고 쉬운 방법을 제공 합니다. 반복적으로 여러 대상 환경에 솔루션을 배포 하는 경우에 여러 명령 파일을 만들 수 있습니다. 각 명령 파일의 MSBuild 명령이 빌드할 동일한 유니버설 프로젝트 파일을 하지만 다양 한 환경 관련 프로젝트 파일을 지정 합니다. 예를 들어 테스트 환경 또는 개발자에 게 게시 하는 명령 파일에는이 MSBuild 명령을 포함할 수 있습니다.


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]


스테이징 환경에 게시 하는 명령 파일을이 MSBuild 명령을 포함할 수 있습니다.


[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]


> [!NOTE]
> 사용자 고유의 서버 환경에 대 한 환경 관련 프로젝트 파일 사용자 지정 하는 방법에 대 한 지침을 참조 하세요 [대상 환경에 대 한 배포 속성 구성](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)합니다.


또한 속성을 재정의 하거나 MSBuild 명령에 다른 다양 한 스위치를 설정 하 여 각 환경에 대 한 빌드 프로세스를 지정할 수 있습니다. 자세한 내용은 [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311.aspx)합니다.

> [!div class="step-by-step"]
> [이전](deploying-database-projects.md)
> [다음](manually-installing-web-packages.md)
