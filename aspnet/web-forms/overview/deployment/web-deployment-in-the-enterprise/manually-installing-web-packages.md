---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
title: 수동으로 웹 패키지 설치 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 인터넷 정보 서비스 (IIS)에 웹 배포 패키지를 수동으로 가져오는 방법을 설명 합니다. 항목 빌드 및 패키징 웹 응용 프로그램...
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: f11d22a7-5d32-4ad0-8a9b-276460a61c06
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
msc.type: authoredcontent
ms.openlocfilehash: d2b2e4852d01f62feef40f8b15252737327ec4ec
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37386629"
---
<a name="manually-installing-web-packages"></a>수동으로 웹 패키지 설치
====================
[Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 인터넷 정보 서비스 (IIS)에 웹 배포 패키지를 수동으로 가져오는 방법을 설명 합니다.
> 
> 항목 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md) 설명 패키지 있습니다 IIS 웹 배포 도구 (웹 배포)를 Microsoft Build Engine (MSBuild) 및 웹 게시 파이프라인 (WPP)을와 함께에서 하는 방법에 웹 응용 프로그램 프로젝트를 단일 zip 파일에 있습니다. 일반적으로 웹 배포 패키지 (또는 배포 패키지를 단순히) 라고도 하는이 파일에는 IIS 웹 서버에서 웹 응용 프로그램을 다시 만들려면 해야 함을 모든 콘텐츠 및 구성 정보가 들어 있습니다.
> 
> 웹 배포 패키지를 만든 후에 다양 한 방법으로 IIS 서버에 게시할 수 있습니다. 많은 시나리오의 경우, MSBuild, WPP, 및 웹 배포를 만들고 자동화 하거나 단일 단계 빌드 및 배포 프로세스의 일부로 웹 패키지를 원격으로 설치 간에 통합 지점의 활용 합니다. 이 프로세스에 설명 되어 [웹 배포 패키지](deploying-web-packages.md)합니다. 그러나이 항상 할 수 없습니다. 인터넷 프로덕션 환경에 웹 응용 프로그램을 배포 하려고 한다고 가정 합니다. 보안상의 이유로 프로덕션 환경에서 경계 네트워크 (DMZ, 완충 지역 및 스크린 된 서브넷이 라고도 함) 빌드 서버에서 별도 서브넷에서 방화벽 뒤에 매우 가장 자주 떨어진입니다. 다 수의 사례를 프로덕션 환경에 물리적으로 격리 된 네트워크 또는 별도 도메인에서 됩니다.
> 
> 이러한 시나리오에서 유일한 옵션 포트는 대상 서버로 웹 패키지 및 수동으로 IIS에 가져올 수 있습니다. 이 방법을 사용 하므로 자동화 된 배포, 이지만 여전히 웹 응용 프로그램을 게시 하기 위한 매우 효과적인 기법은&#x2014;단순히 웹 서버를 단일 zip 파일을 복사 하는 마법사를 사용 하 여 가져오기 프로세스를 안내 합니다.


이 항목의 Fabrikam, Inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항 기반 자습서 시리즈의 일부를 형성 합니다. 샘플 솔루션을 사용 하 여이 자습서 시리즈&#x2014;는 [Contact Manager 솔루션](the-contact-manager-solution.md)&#x2014;현실적인 수준의 복잡성을 Windows Communication ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내는 Foundation (WCF) 서비스 및 데이터베이스 프로젝트입니다.

## <a name="task-overview"></a>작업 개요

IIS에 웹 배포 패키지를 가져오려면 이러한 상위 수준의 작업을 완료 해야 합니다.

- MSBuild 명령줄, Team Build 또는 Visual Studio 2010을 사용 하 여 웹 배포 패키지를 만듭니다.
- 대상 웹 서버로 웹 패키지를 복사 합니다.
- 응용 프로그램 패키지 가져오기 마법사를 IIS 관리자에서 사용 하 여 웹 패키지를 설치 하 여 연결 문자열에서 서비스 끝점 등의 변수에 대 한 값을 제공 합니다.

이 항목에서는 이러한 절차를 수행 하는 방법을 보여줍니다. 작업은이 문서의 연습 웹 패키지, 웹 배포 및 WPP 개념에 익숙한 이미 있다고 가정 합니다. 자세한 내용은 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.

> [!NOTE]
> 이 항목은 함께에 가장 적합 [웹 배포 게시 (오프 라인 배포)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md), 필수 구성 요소를 설치 하 고 패키지를 가져오기 위해 IIS 웹 사이트를 준비 하는 방법을 설명 합니다.


## <a name="create-a-web-deployment-package"></a>웹 배포 패키지 만들기

첫 번째 작업을 배포할 웹 응용 프로그램 프로젝트에 대 한 웹 배포 패키지를 만드는 것입니다. 여러 가지 방법으로 웹 패키지를 만들 수 있습니다.

**접근 방식 1: Visual Studio를 사용 하 여 빌드 프로세스의 일부로 패키지 만들기**

웹 배포 패키지를 통해 각 빌드 후 만들려는 웹 응용 프로그램 프로젝트를 구성할 수는 **웹 패키지 및 게시** 프로젝트 속성 페이지의 탭 합니다. 이 프로세스에 설명 되어 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.

**방법 2: MSBuild를 사용 하 여 빌드 프로세스의 일부로 패키지 만들기**

MSBuild를 직접 사용자 지정 MSBuild 프로젝트 파일을 통해 또는 명령줄에서 사용 하 여 웹 응용 프로그램 프로젝트를 빌드하면 만들면 웹 배포 패키지 빌드 프로세스의 일부로 포함 하 여는 **DeployOnBuild = true** 하 고 **DeployTarget 패키지 =** 명령에는 속성입니다. 이 프로세스에 설명 되어 [빌드 프로세스를 이해](understanding-the-build-process.md)합니다.

**접근 방식 3: Visual Studio에서 요청 시 패키지 만들기**

언제 든 지 Visual Studio 2010에서 웹 응용 프로그램 프로젝트에 대 한 웹 배포 패키지를 만들 수 있습니다. 이 수행 하는 **솔루션 탐색기** 창에서 웹 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **배포 패키지 빌드**합니다.

![](manually-installing-web-packages/_static/image1.png)

**방법 4: 명령줄에서 필요에 따라 패키지 만들기**

호출 하 여 명령줄에서 웹 배포 패키지를 만들 수는 **패키지** MSBuild를 사용 하 여 웹 응용 프로그램 프로젝트의 대상입니다. 이 명령은 다음과 비슷합니다.


[!code-console[Main](manually-installing-web-packages/samples/sample1.cmd)]


방법 중 사용 하 여, 최종 결과 동일 합니다. WPP 웹 응용 프로그램 프로젝트의 출력 폴더에 다양 한 지원 리소스를 함께 zip 파일로 웹 배포 패키지를 만듭니다.

![](manually-installing-web-packages/_static/image2.png)

웹 패키지를 수동으로 가져올 계획인 경우 zip 파일만이 필요 합니다. 대상 웹 서버에이 파일을 복사 하 고 가져오기 프로세스를 시작할 수 있습니다.

## <a name="import-a-web-package-into-iis"></a>IIS에 웹 패키지 가져오기

IIS 웹 사이트에 로컬 파일 시스템에서 웹 배포 패키지를 가져오려면 다음 절차를 사용할 수 있습니다. 이 절차를 수행 하기 전에 있는지 확인 합니다.

- 웹 서버에 웹 배포 패키지를 복사 합니다.
- 응용 프로그램을 호스팅하는 IIS 웹 서버를 구성 합니다.

웹 배포 패키지를 지원 하기 위해 IIS 웹 서버를 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [웹 배포 게시 (오프 라인 배포)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)합니다.

**IIS 관리자를 사용 하 여 웹 배포 패키지를 가져오려면**

1. IIS 관리자에서에 **연결** 창, IIS 웹 사이트를 마우스 오른쪽 단추로 클릭을 가리킵니다 **배포**를 클릭 하 고 **응용 프로그램 가져오기**합니다.

    ![](manually-installing-web-packages/_static/image3.png)
2. 응용 프로그램 패키지 가져오기 마법사에서에 **패키지 선택** 페이지에서 웹 배포 패키지의 위치로 이동 하 고 클릭 **다음**합니다.
3. 에 **패키지의 콘텐츠를 선택** 페이지에서, 필요 하 고 클릭 하지는 내용을 지우기 **다음**합니다.

    ![](manually-installing-web-packages/_static/image4.png)

    > [!NOTE]
    > 대부분의 경우에 웹 배포 패키지를 함께 제공 되는 모든 항목을 가져옵니다 하지 좋습니다. 예를 들어, 연결된 된 데이터베이스의 이름을 바꾸려면 웹 배포를 허용 하지 않을 수 있습니다.  
    > 합니다 **권한을 부여** 항목 응용 프로그램 풀 id를 웹 사이트 콘텐츠를 저장 하는 실제 폴더에 액세스할 수 있도록 대상 파일 시스템에서 사용 권한을 설정 합니다. 또한 익명 인증 사용자 읽기 응용 프로그램 인터넷 메일 MIME (Multipurpose Extensions) 형식 파일을 사용할 수 있도록 폴더에 권한은 부여 합니다. 원하는 경우 이러한 항목을 제거 하 고 사용 권한을 수동으로 구성 수입니다.
4. 에 **응용 프로그램 패키지 정보 입력** 페이지에서 요청된 된 정보를 제공 합니다.

    ![](manually-installing-web-packages/_static/image5.png)
5. 웹 패키지를 만들면 WPP 응용 프로그램에 대 한 구성 파일을 분석 하 고 연결 문자열에서 서비스 끝점 등의 모든 변수를 감지 합니다. 이 경우:

    1. **응용 프로그램 경로** 응용 프로그램을 설치 하려는 IIS 경로입니다. 이 설정은 WPP 만들어지는 모든 배포 패키지에 공통적으로 적용 됩니다.
    2. **서비스 끝점 주소 ContactService** 응용 프로그램이 배포 된 WCF 서비스와 통신을 사용 해야 하는 주소입니다. 이 설정은 항목에 해당 합니다 *web.config* 파일입니다.
    3. 첫 번째 **연결 문자열** 설정은 웹 배포 응용 프로그램 (이 경우 ASP.NET 멤버 자격 데이터베이스)를 사용 하 여 관련 데이터베이스를 배포 하는 데 사용 해야 하는 연결 문자열입니다. 이 설정에서 설정에 해당 합니다 **SQL 패키지 및 게시** Visual Studio에서 탭 합니다.
    4. 두 번째 **연결 문자열** 설정은 응용 프로그램가 실제로 실행 되었을 때 데이터베이스와 통신 하는 데 사용할 연결 문자열입니다. 이 항목에 해당 하는 연결 문자열에는 *web.config* 파일입니다.

        > [!NOTE]
        > 이러한 매개 변수에서 제공 하는 위치에 대 한 자세한 내용은 참조 하세요. [웹 패키지 배포용 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)합니다.
6. **다음**을 클릭합니다.
7. 이것이이 웹 사이트에 응용 프로그램을 배포한 경우 처음으로 설치 하기 전에 모든 기존 콘텐츠를 삭제할 것인지 여부를 지정 하 라는 메시지가 됩니다. 요구 사항에 맞게 적절 한 옵션을 선택 하 고 클릭 **다음**합니다.

    ![](manually-installing-web-packages/_static/image6.png)
8. IIS 패키지 설치 완료 되 면 클릭 **완료**합니다.

    ![](manually-installing-web-packages/_static/image7.png)

이 시점에서 IIS에 웹 응용 프로그램을 성공적으로 게시 했습니다.

## <a name="conclusion"></a>결론

이 항목에서는 IIS 관리자를 사용 하 여 IIS 웹 사이트에 웹 배포 패키지를 가져오는 방법을 설명 합니다. 이 방법은 웹 응용 프로그램 게시 불가능 하거나 바람직하지 않은 보안 또는 인프라 제약 조건은 원격 배포를 만들 때 적합 합니다.

## <a name="further-reading"></a>추가 정보

수동으로 웹 패키지를 가져오는 지원 하기 위해 IIS 웹 서버를 구성 하는 방법에 대 한 지침을 참조 하세요 [웹 배포 게시 (오프 라인 배포)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)합니다. 웹 패키지 배포에 대 한 보다 일반적인 지침을 참조 하세요 [연습: 웹 배포 패키지 (파트 1 / 4)를 사용 하 여 웹 응용 프로그램 프로젝트 배포](https://msdn.microsoft.com/library/dd483479.aspx)합니다.

> [!div class="step-by-step"]
> [이전](creating-and-running-a-deployment-command-file.md)
