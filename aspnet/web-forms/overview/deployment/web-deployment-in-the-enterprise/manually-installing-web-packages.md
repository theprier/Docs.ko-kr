---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
title: "웹 패키지를 수동으로 설치 | Microsoft Docs"
author: jrjlee
description: "이 항목에서는 인터넷 정보 서비스 (IIS)에 웹 배포 패키지를 수동으로 가져오는 방법에 설명 합니다. 항목 건물과 패키징 웹 Applicati 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 05/04/2012
ms.topic: article
ms.assetid: f11d22a7-5d32-4ad0-8a9b-276460a61c06
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
msc.type: authoredcontent
ms.openlocfilehash: 0ab0b4c24c1771a21c45bac011b5f156cb15d28a
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="manually-installing-web-packages"></a>웹 패키지를 수동으로 설치
====================
으로 [Jason lee 공저](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 인터넷 정보 서비스 (IIS)에 웹 배포 패키지를 수동으로 가져오는 방법에 설명 합니다.
> 
> 항목 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md) 설명 된 패키지는 IIS 웹 배포 도구 (웹 배포), Microsoft Build Engine (MSBuild) 및 웹 게시 파이프라인 (WPP)을 함께 사용 하면 있습니다 어떻게 프로그램 단일 zip 파일에 웹 응용 프로그램 프로젝트입니다. 일반적으로 웹 배포 패키지 (또는 단순히 배포 패키지) 라고 하는이 파일을 IIS 웹 서버에서 웹 응용 프로그램을 다시 만드는 데 필요 함을 모든 콘텐츠 및 구성 정보를 포함 합니다.
> 
> 웹 배포 패키지를 만든 후에 다양 한 방법으로 IIS 서버에 게시할 수 있습니다. 시나리오는 다양 MSBuild, WPP, 및 웹 배포를 만들고는 단일 단계 또는 자동화 된 빌드 및 배포 프로세스의 일부로 웹 패키지를 원격으로 설치 하려면 사이의 통합 지점 기능을 활용 합니다. 이 프로세스에 설명 되어 [웹 패키지 배포](deploying-web-packages.md)합니다. 그러나이 항상 할 수 없습니다. 인터넷 연결 프로덕션 환경에 웹 응용 프로그램을 배포 한다고 가정 합니다. 보안상의 이유로 경계 네트워크 (DMZ, 완충 지역 및 스크린 된 서브넷이 라고도 함)의 빌드 서버와에서 분리 되는 서브넷에서 방화벽 뒤에 가능성이 매우 가장 낮은 떨어진 프로덕션 환경이입니다. 많은 경우, 프로덕션 환경 또는 물리적으로 격리 된 네트워크 별도 도메인에 됩니다.
> 
> 이러한 시나리오에서 수정할 수 있는 유일한 방법은 IIS로 수동으로 가져옵니다 및 대상 서버에 웹 패키지 포트 수 있습니다. 이 방법은 자동된 배포를 불가능, 이지만 여전히 웹 응용 프로그램 & #x 2014 게시 하기 위한 매우 효과적인 기법은; 단순히 웹 서버에 단일 zip 파일을 복사 하 고 마법사를 사용 하 여 가져오기 프로세스를 안내 합니다.


이 항목의 Fabrikam, inc. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 바탕으로 하는 자습서 시리즈의 일부를 형성 합니다. 이 자습서 시리즈 샘플 솔루션 & #x 2014;을 사용 하는 [Contact Manager 솔루션](the-contact-manager-solution.md)& #x 2014; 현실적인 수준의 복잡성을 Windows ASP.NET MVC 3 응용 프로그램을 포함 하 여 웹 응용 프로그램을 나타내기 위해 Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 제공 합니다.

## <a name="task-overview"></a>작업 개요

IIS에 웹 배포 패키지를 가져오려면 이러한 높은 수준의 작업을 완료 해야 합니다.

- MSBuild 명령줄, 팀 빌드 또는 Visual Studio 2010을 사용 하 여 웹 배포 패키지를 만듭니다.
- 대상 웹 서버에 웹 패키지를 복사 합니다.
- 웹 패키지를 설치 하 고 연결 문자열 및 서비스 끝점 같은 변수에 대 한 값을 제공 하려면 IIS 관리자에서 응용 프로그램 패키지 가져오기 마법사를 사용 합니다.

이 항목에서는 이러한 절차를 수행 하는 방법을 보여줍니다. 작업 및이 항목의 연습 웹 패키지, 웹 배포 및 WPP 개념에 잘 알고 이미 하 가정 합니다. 자세한 내용은 참조 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.

> [!NOTE]
> 이 항목은 함께에 가장 적합 [웹 배포 게시 (오프 라인 배포)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md), 필수 구성 요소를 설치 하 고 패키지 가져오기를 위해 IIS 웹 사이트를 준비 하는 방법에 설명입니다.


## <a name="create-a-web-deployment-package"></a>웹 배포 패키지 만들기

첫 번째 작업을 배포할 웹 응용 프로그램 프로젝트에 대 한 웹 배포 패키지를 만드는 것입니다. 여러 가지 방법으로 웹 패키지를 만들 수 있습니다.

**접근 방식 1: Visual Studio와 함께 빌드 프로세스의 일환으로 패키지 만들기**

웹 배포 패키지를 통해 빌드할 때마다 빌드 후 만들려는 웹 응용 프로그램 프로젝트를 구성할 수는 **웹 패키지 및 게시** 프로젝트 속성 페이지에서 탭 합니다. 이 프로세스에 설명 되어 [빌드 및 패키징 웹 응용 프로그램 프로젝트](building-and-packaging-web-application-projects.md)합니다.

**방법 2: msbuild 빌드 프로세스의 일환으로 패키지 만들기**

MSBuild를 직접 사용자 지정 MSBuild 프로젝트 파일을 통해 또는 명령줄에서 사용 하 여 웹 응용 프로그램 프로젝트를 작성 하는 경우 만들 수 있습니다 웹 배포 패키지를 빌드 프로세스의 일부로 포함 하 여는 **DeployOnBuild = true** 및 **DeployTarget 패키지 =** 명령에는 속성입니다. 이 프로세스에 설명 되어 [빌드 프로세스를 이해](understanding-the-build-process.md)합니다.

**방법 3: Visual Studio에서 필요에 따라 패키지 만들기**

언제 든 지 Visual Studio 2010에서 웹 응용 프로그램 프로젝트에 대 한 웹 배포 패키지를 만들 수 있습니다. 이 수행 하는 **솔루션 탐색기** 창에서 웹 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **배포 패키지 빌드**합니다.

![](manually-installing-web-packages/_static/image1.png)

**방법 4: 명령줄에서 필요에 따라 패키지 만들기**

호출 하 여 명령줄에서 웹 배포 패키지를 만들 수 있습니다는 **패키지** MSBuild를 사용 하 여 웹 응용 프로그램 프로젝트에서 대상입니다. 이 명령은이 다음과 비슷합니다.


[!code-console[Main](manually-installing-web-packages/samples/sample1.cmd)]


방법에 더 사용 하 여, 최종 결과 동일 합니다. WPP 웹 응용 프로그램 프로젝트의 출력 폴더에 다양 한 지원 리소스와 함께 zip 파일로 웹 배포 패키지를 만듭니다.

![](manually-installing-web-packages/_static/image2.png)

웹 패키지를 수동으로 가져올 계획인 zip 파일에만 필요 합니다. 대상 웹 서버에이 파일을 복사 및 가져오기 프로세스를 시작할 수 있습니다.

## <a name="import-a-web-package-into-iis"></a>IIS에 웹 패키지 가져오기

IIS 웹 사이트에 웹 배포 패키지를 로컬 파일 시스템에서 가져오려면 다음 절차를 사용할 수 있습니다. 이 절차를 수행 하기 전에 있는지 확인 합니다.

- 웹 서버에 웹 배포 패키지를 복사 합니다.
- 응용 프로그램을 호스팅하는 IIS 웹 서버를 구성 합니다.

웹 배포 패키지를 지원 하기 위해 IIS 웹 서버를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [웹 배포 게시 (오프 라인 배포)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)합니다.

**IIS 관리자를 사용 하 여 웹 배포 패키지를 가져오려면**

1. IIS 관리자에서에서 **연결** 창 IIS 웹 사이트를 마우스 오른쪽 단추로 클릭, 가리킨 **배포**, 클릭 하 고 **응용 프로그램 가져오기**합니다.

    ![](manually-installing-web-packages/_static/image3.png)
2. 응용 프로그램 패키지 가져오기 마법사에는 **패키지 선택** 페이지, 웹 배포 패키지의 위치로 이동 하 고 클릭 **다음**합니다.
3. 에 **패키지의 내용을 선택** 페이지에서 요구 한 클릭 하지 않는 **다음**합니다.

    ![](manually-installing-web-packages/_static/image4.png)

    > [!NOTE]
    > 대부분의 경우에서 싶지 않은 웹 배포 패키지와 함께 제공 되는 모든 항목을 가져옵니다. 예를 들어 연결된 된 데이터베이스를 대체 하기 위해 Web Deploy를 허용 하지 않을 수 있습니다.  
    > **권한을 부여** 항목 응용 프로그램 풀 id 웹 사이트 콘텐츠를 저장 하는 실제 폴더에 액세스할 수 있는지 확인 하려면 대상 파일 시스템에 사용 권한을 설정 합니다. 또한, 익명 인증 사용자 읽기 MIME Multipurpose Internet Mail Extensions () 형식 파일을 제공 하는 응용 프로그램을 폴더에 권한은 부여 합니다. 원하는 경우 이러한 항목을 제거할 수 있으며 사용 권한을 수동으로 구성.
4. 에 **응용 프로그램 패키지 정보 입력** 페이지에서 필요한 정보를 제공 합니다.

    ![](manually-installing-web-packages/_static/image5.png)
5. 웹 패키지를 만들 때에 WPP 응용 프로그램에 대 한 구성 파일을 분석 하 고 연결 문자열 및 서비스 끝점 같은 변수를 검색 합니다. 이 경우:

    1. **응용 프로그램 경로** 응용 프로그램을 설치 하려면 IIS 경로입니다. 이 설정은 WPP 만들어지는 모든 배포 패키지에 공통적으로 적용 됩니다.
    2. **서비스 끝점 주소 ContactService** 응용 프로그램이 배포 된 WCF 서비스와 통신 하는 데 사용 해야 하는 주소입니다. 이 설정은 해당의 항목에는 *web.config* 파일입니다.
    3. 첫 번째 **연결 문자열** 설정은 웹 배포 배포 중인 응용 프로그램 (이 경우 ASP.NET 멤버 자격 데이터베이스)와 관련 된 데이터베이스를 사용 해야 하는 연결 문자열입니다. 이 설정은에 있는 설정에 해당는 **SQL 패키지 및 게시** Visual Studio에서 탭 합니다.
    4. 두 번째 **연결 문자열** 설정은 응용 프로그램에서 실제로 실행 되었을 때 데이터베이스와 통신에 사용할 연결 문자열입니다. 연결 문자열 항목에 해당는 *web.config* 파일입니다.

        > [!NOTE]
        > 이러한 매개 변수에서 발생 한 위치에 대 한 자세한 내용은 참조 하십시오. [웹 패키지 배포에 대 한 매개 변수 구성](configuring-parameters-for-web-package-deployment.md)합니다.
6. **다음**을 클릭합니다.
7. 이 웹 사이트에 응용 프로그램을 배포한 경우 처음으로 없는 경우 설치 하기 전에 모든 기존 콘텐츠가 삭제 것인지 여부를 지정 하 라는 메시지가 표시 합니다. 요구 사항에 적합 한 옵션을 선택한 다음 클릭 **다음**합니다.

    ![](manually-installing-web-packages/_static/image6.png)
8. IIS 설치 패키지를 완료 하는 경우 클릭 **마침**합니다.

    ![](manually-installing-web-packages/_static/image7.png)

이 시점에서 IIS에 웹 응용 프로그램을 성공적으로 게시 했습니다.

## <a name="conclusion"></a>결론

이 항목에는 IIS 관리자를 사용 하 여 IIS 웹 사이트에 웹 배포 패키지를 가져오는 방법에 설명 합니다. 이 웹 응용 프로그램 게시 방법은 적절 한 보안 또는 인프라 제약 조건은 불가능 하거나 바람직하지 않은 원격 배포를 만들 때입니다.

## <a name="further-reading"></a>추가 정보

웹 패키지를 수동으로 가져오는 지원 하기 위해 IIS 웹 서버를 구성 하는 방법에 대 한 지침을 참조 하십시오. [웹 배포 게시 (오프 라인 배포)에 대 한 웹 서버를 구성](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)합니다. 웹 패키지를 배포 하는 방법에 대 한 보다 일반적인 지침을 참조 하십시오. [연습: 웹 배포 패키지 (파트 1/4)를 사용 하 여 웹 응용 프로그램 프로젝트 배포](https://msdn.microsoft.com/en-us/library/dd483479.aspx)합니다.

>[!div class="step-by-step"]
[이전](creating-and-running-a-deployment-command-file.md)
