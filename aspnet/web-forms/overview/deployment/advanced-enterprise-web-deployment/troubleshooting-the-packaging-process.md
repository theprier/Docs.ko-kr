---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: 패키징 프로세스 문제 해결 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 M EnablePackageProcessLoggingAndAssert 속성을 사용 하 여 패키징 프로세스에 대 한 자세한 정보를 수집 하는 방법 설명 하는 중...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 22be1ccc5a1ec52d143bedffd79264918c1a45e1
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41829905"
---
<a name="troubleshooting-the-packaging-process"></a>패키징 프로세스 문제 해결
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 사용 하 여 패키징 프로세스에 대 한 자세한 정보를 수집 하는 방법에 대해 설명 합니다 **EnablePackageProcessLoggingAndAssert** Microsoft Build Engine (MSBuild)의 속성입니다.
> 
> 설정한 경우 합니다 **EnablePackageProcessLoggingAndAssert** 속성을 **true**, MSBuild는:
> 
> - 빌드 로그에는 패키징 프로세스에 대 한 추가 정보를 추가 합니다.
> - 중복 파일 패키징 목록에 없으면 예를 들어, 특정 조건에서 오류를 기록 합니다.
> - 로그 디렉터리를 만듭니다는 *ProjectName*\_패키지 폴더를 압축 하 고 있는 파일에 대 한 정보를 기록 하는 데 사용 합니다.
> 
> 패키징 프로세스가 실패 하는 경우 웹 배포 패키지는 예상 되는 파일을 포함 하지 가지 잘못 된 것은이 정보 프로세스 및 pinpoint 문제를 해결 하려면 사용할 수 있습니다.
> 
> > [!NOTE]
> > 합니다 **EnablePackageProcessLoggingAndAssert** 속성이 사용 하 여 프로젝트를 빌드하는 경우에 작동 합니다 **디버그** 구성 합니다. 속성은 다른 구성에서 무시 됩니다.


이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.

이 자습서의 핵심 배포 방법에 설명 된 분할 프로젝트 파일 방법을 기반으로 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md), 두 개의 프로젝트 파일에서 빌드 프로세스에 의해 제어 되는&#x2014;포함 된 모든 대상 환경 및 환경 관련 빌드 및 배포 설정을 포함 하는 하나에 적용 되는 지침을 빌드하십시오. 빌드 시 환경 관련 프로젝트 파일은 빌드 지침의 전체 집합을 이루는 환경을 알 수 없는 프로젝트 파일에 병합 됩니다.

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a>EnablePackageProcessLoggingAndAssert 속성 이해

[빌드 및 패키징 웹 응용 프로그램 프로젝트](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md) 웹 게시 파이프라인 (WPP) MSBuild의 기능을 확장 하 고 인터넷 정보 서비스 (IIS) 웹을 통합할 수 있도록 하는 MSBuild 대상 집합을 제공 하는 방법을 설명 합니다. 배포 도구 (웹 배포). 웹 응용 프로그램 프로젝트를 패키지할 때는 WPP 대상을 호출 하 합니다.

이러한 WPP 대상 많은 추가 정보를 기록 하는 조건부 논리를 포함할 때 합니다 **EnablePackageProcessLoggingAndAssert** 속성이 **true**합니다. 예를 들어, 검토 하는 경우는 **패키지** 대상에 추가 로그 디렉터리를 만드는 경우 파일의 목록을 텍스트 파일에 쓰는 볼 수 있습니다 **EnablePackageProcessLoggingAndAssert** 같으면**true**합니다.


[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]


> [!NOTE]
> WPP 대상에 정의 된 합니다 *Microsoft.Web.Publishing.targets* %PROGRAMFILES (x86) %\MSBuild\Microsoft\VisualStudio\v10.0\Web 폴더의 파일입니다. 이 파일을 열고 Visual Studio 2010 또는 XML 편집기에서 대상 검토 합니다. 파일의 내용을 수정할 수 없도록 주의 해야 합니다.


## <a name="enabling-the-additional-logging"></a>추가 로깅을 사용 하도록 설정

에 대 한 값을 제공할 수 있습니다 합니다 **EnablePackageProcessLoggingAndAssert** 프로젝트를 작성 하는 방법에 따라 다양 한 방법으로 속성입니다.

명령줄에서 프로젝트를 빌드하는 경우에 대 한 값을 제공할 수 있습니다 합니다 **EnablePackageProcessLoggingAndAssert** 명령줄 인수로 속성:


[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]


사용자 지정 프로젝트 파일에 프로젝트 빌드를 사용 하는 경우 포함할 수 있습니다는 **EnablePackageProcessLoggingAndAssert** 값을 **속성** 특성을 **MSBuild**작업:


[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]


를 사용 하 여 프로젝트를 빌드할 Team Foundation Server (TFS) 빌드 정의 사용 하는 경우에 대 한 값을 제공할 수 있습니다 합니다 **EnablePackageProcessLoggingAndAssert** 속성에는 **MSBuild 인수** 행:![](troubleshooting-the-packaging-process/_static/image1.png)

> [!NOTE]
> 작성 및 빌드 정의 구성에 대 한 자세한 내용은 참조 하세요. [배포를 만드는 빌드 정의 지 원하는](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)합니다.


또는 모든 빌드에서 패키지를 포함 하려는 경우 수정할 수 있습니다 설정 하 여 웹 응용 프로그램 프로젝트용 프로젝트 파일을 **EnablePackageProcessLoggingAndAssert** 속성을 **true**합니다. 첫 번째 속성을 추가 해야 하면 **PropertyGroup** .csproj 또는.vbproj 파일 내의 요소입니다.


[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]


## <a name="reviewing-the-log-files"></a>로그 파일 검토

빌드 및 사용 하 여 웹 응용 프로그램 프로젝트를 패키지 있습니다 **EnablePackageProcessLoggingAndAssert** 로 설정 **true**, MSBuild 로그인 이라는 추가 폴더를 만듭니다는 *ProjectName* \_패키지 폴더입니다. 로그 폴더에는 다양 한 파일이 들어 있습니다.

![](troubleshooting-the-packaging-process/_static/image2.png)

표시 되는 파일 목록을 프로젝트 및 빌드 프로세스 작업에 따라 달라 집니다. 그러나 이러한 파일은 프로세스의 여러 단계에서 패키징의 경우 WPP가 수집 하는 파일 목록을 기록 하려면 일반적으로 사용 됩니다.

- 합니다 *PreExcludePipelineCollectFilesPhaseFileList.txt* 파일 제외에 대 한 지정 된 모든 파일이 제거 되기 전에 패키지에 MSBuild를 수집 하는 파일을 나열 합니다.
- 합니다 *AfterExcludeFilesFilesList.txt* 파일 제외에 대 한 지정 된 모든 파일을 제거한 후 수정 된 파일 목록을 포함 합니다.

    > [!NOTE]
    > 패키징 프로세스에서 파일 및 폴더를 제외 하는 방법은 참조 하세요 [배포에서 제외 하 고 파일 및 폴더](excluding-files-and-folders-from-deployment.md)합니다.
- *AfterTransformWebConfig.txt* 파일에 대 한 패키징 후 수집 된 파일에 나열 *Web.config* 변환을 수행 합니다. 이 목록의 모든 구성별 *Web.config* 같은 파일을 변환 *Web.Debug.config* 하 고 *Web.Release.config*, 파일 목록에서 제외 됩니다 패키지입니다. 변환 하는 단일 *Web.config* 그 자리에 포함 됩니다.
- *PostAutoParameterizationWebConfigConnectionStrings.txt* 파일의 연결 문자열을 한 후 파일의 목록을 포함 합니다 *Web.config* 파일 매개 변수가 있습니다. 이것이 패키지를 배포할 때 대상 환경에 대 한 올바른 설정을 사용 하 여 연결 문자열을 대체할 수 있도록 허용 하는 프로세스입니다.
- 합니다 *Prepackage.txt* 파일 패키지에 포함 될 파일의 완료 된 빌드 전 목록을 포함 합니다.

> [!NOTE]
> WPP 대상에 추가 로그 파일의 이름은 일반적으로 해당 합니다. 검사 하 여 이러한 목표를 검토할 수 있습니다 합니다 *Microsoft.Web.Publishing.targets* %PROGRAMFILES (x86) %\MSBuild\Microsoft\VisualStudio\v10.0\Web 폴더의 파일입니다.


웹 패키지의 내용을 예상한 바가 없는 경우 이러한 파일을 검토 프로세스 작업에서 어떤 지점 잘못 식별 하는 유용한 방법 수 있습니다.

## <a name="conclusion"></a>결론

이 항목에서는 사용 하는 방법을 설명 합니다 **EnablePackageProcessLoggingAndAssert** 패키징 프로세스 문제를 해결 하는 MSBuild의 속성입니다. 속성을 설정 하는 경우 기록 되는 추가 정보를 설명 하 고 빌드 프로세스에 속성 값을 제공할 수 있는 다양 한 방법을 설명 했습니다 **true**합니다.

## <a name="further-reading"></a>추가 정보

사용자 지정 MSBuild 프로젝트 파일을 사용 하 여 배포 프로세스를 제어 하에 대 한 자세한 내용은 참조 하세요. [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md) 하 고 [빌드 프로세스를 이해](../web-deployment-in-the-enterprise/understanding-the-build-process.md)합니다. WPP 및 패키징 프로세스를 관리 하는 방법에 대 한 자세한 내용은 참조 하세요. [빌드 및 패키징 웹 응용 프로그램 프로젝트](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)합니다. 웹 배포 패키지에서 특정 파일 및 폴더를 제외 하는 방법에 대 한 지침을 참조 하세요 [배포에서 제외 하 고 파일 및 폴더](excluding-files-and-folders-from-deployment.md)합니다.

> [!div class="step-by-step"]
> [이전](running-windows-powershell-scripts-from-msbuild-project-files.md)
