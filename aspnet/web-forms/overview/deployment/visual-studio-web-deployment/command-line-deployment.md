---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 명령줄 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시)에서 실행 중인 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
ms.technology: dotnet-webforms
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: 5673a4733257fae88fb66a3da43dfceb98c3b37a
ms.sourcegitcommit: 953ff9ea4369f154d6fd0239599279ddd3280009
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37390876"
---
<a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 명령줄 배포
====================
[Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다. 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](introduction.md)합니다.


## <a name="overview"></a>개요

이 자습서는 Visual Studio 웹을 호출 하는 방법을 보여 줍니다. 명령줄에서 파이프라인을 게시 합니다. 하려는 시나리오에 유용 [배포 프로세스를 자동화](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) 것 수동으로 Visual Studio에서 작업을 수행 하는 대신 일반적으로 사용 하 여를 [소스 코드 버전 제어 시스템이](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)합니다.

## <a name="make-a-change-to-deploy"></a>배포 변경

현재 정보 페이지 템플릿 코드를 표시합니다.

![템플릿 코드를 사용 하 여 페이지에 대 한](command-line-deployment/_static/image1.png)

학생 등록의 요약을 표시 하는 코드를 사용 하 여는 대체 됩니다.

열기는 *About.aspx* 페이지에서 모든 내부 태그를 삭제 합니다 `MainContent` `Content` 요소와 해당 위치에 다음 태그를 삽입:

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

프로젝트를 실행 하 고 선택 합니다 **에 대 한** 페이지입니다.

![정보 페이지](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a>명령줄을 사용 하 여 테스트 배포

다른 데이터베이스 변경, 따라서 사용 하지 않도록 설정 dbDacFx 데이터베이스 aspnet ContosoUniversity 데이터베이스 배포를 배포 하 고 하지 않습니다. 열기는 **웹 게시** 마법사에 세 개의 각 게시 프로필을 선택 취소 합니다 **데이터베이스 업데이트** 확인란을 **설정** 탭.

Windows 8 시작 페이지에서 검색할 **VS2012 용 개발자 명령 프롬프트**합니다.

에 대 한 아이콘을 마우스 오른쪽 단추로 클릭 **VS2012 용 개발자 명령 프롬프트** 누릅니다 **관리자 권한으로 실행**합니다.

솔루션 파일의 경로 사용 하 여 솔루션 파일의 경로를 대체 명령 프롬프트에서 다음 명령을 입력 합니다.

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

MSBuild는 솔루션을 빌드 및 테스트 환경에 배포 합니다.

![명령줄 출력](command-line-deployment/_static/image3.png)

브라우저를 열고 다음으로 이동 `http://localhost/ContosoUniversity`를 클릭 합니다 **에 대 한** 페이지 배포 되었는지 확인 합니다.

테스트에 학생이 있는지를 만들지를 보면 아래에서 빈 페이지는 **학생 본문 통계** 제목입니다. 로 이동 합니다 **학생** 페이지에서 **학생 추가**, 학생이 몇 명 추가 및 돌아옵니다를 **에 대 한** 학생 통계를 보려면 페이지를 합니다.

![테스트 환경에서 페이지에 대 한](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a>키 명령줄 옵션

MSBuild에서 솔루션 파일 경로 및 두 개의 속성 전달할 입력 한 명령입니다.

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a>개별 프로젝트를 배포 및 솔루션 배포

만들려는 솔루션에 하면 모든 프로젝트를 솔루션 파일을 지정 합니다. 여러 개의 웹 프로젝트가 솔루션에 있는 경우에 다음과 같은 MSBuild 동작이 적용 됩니다.

- 명령줄에서 지정 하는 속성은 모든 프로젝트에 전달 됩니다. 따라서 각 웹 프로젝트 게시 프로필을 지정 하는 이름이 있어야 합니다. 지정 하는 경우 `/p:PublishProfile=Test`, 각 웹 프로젝트 라는 게시 프로필이 있어야 *테스트*합니다.
- 다른 빌드되지도 하는 경우에 성공적으로 한 프로젝트를 게시할 수 있습니다. 자세한 내용은 참조는 stackoverflow 스레드 [두 개의 패키지를 사용 하 여 MSBuild 실패](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages)합니다.

솔루션을 대신 개별 프로젝트를 지정 하는 경우 Visual Studio 버전을 지정 하는 매개 변수를 추가 해야 합니다. Visual Studio 2012를 사용 하는 경우에 명령줄 다음 예제와 비슷한 것:

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

Visual Studio 2010에 대 한 버전 번호를은 10.0입니다. 자세한 내용은 [Visual Studio 프로젝트 호환성 및 VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) Sayed Hashimi의 블로그입니다.

### <a name="specifying-the-publish-profile"></a>게시 프로필을 지정

이름 또는 전체 경로를 게시 프로필을 지정할 수 있습니다 합니다 *.pubxml* 다음 예제에서와 같이 파일:

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a>웹 게시 명령줄 게시를 위해 지원 되는 메서드

메서드를 게시 하는 세 개의 명령줄 게시를 위해 지원 됩니다.

- `MSDeploy` 웹 배포를 사용 하 여 게시 합니다.
- `Package` 웹 배포 패키지를 만들어 게시 합니다. 만든 MSBuild 명령에서 패키지를 별도로 설치 해야 합니다.
- `FileSystem` 지정된 된 폴더에 파일을 복사 하 여 게시 합니다.

### <a name="specifying-the-build-configuration-and-platform"></a>빌드 구성 및 플랫폼 지정

Visual Studio 또는 명령줄에서 빌드 구성 및 플랫폼 설정 되어야 합니다. 명명 된 속성을 포함 하는 게시 프로필 `LastUsedBuildConfiguration` 고 `LastUsedPlatform`, 있지만 프로젝트가 빌드되는 방식을 확인 하기 위해 이러한 속성을 설정할 수 없습니다. 자세한 내용은 [MSBuild: 구성 속성을 설정 하는 방법을](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) Sayed Hashimi의 블로그입니다.

## <a name="deploy-to-staging"></a>스테이징에 배포

Azure에 배포 하려면 명령줄에 암호를 추가 해야 합니다. 에 암호화 된 형태로 저장 된 Visual Studio에서 게시 프로필의 암호를 저장 하는 경우는 사용자 *. pubxml.user* 파일입니다. 해당 파일에서 명령줄 매개 변수에서 암호를 전달 해야 하므로 명령줄 배포를 수행할 때 MSBuild를 통해 액세스할 수 없습니다.

1. 필요한 암호를 복사 합니다 *.publishsettings* 스테이징 웹 사이트의 앞서 다운로드 한 파일입니다. 암호는 값을 `userPWD` 웹 배포에 대 한 특성 `publishProfile` 요소입니다.

    ![웹 배포 암호](command-line-deployment/_static/image5.png)
2. Windows 8 시작 페이지에서 검색할 **VS2012 용 개발자 명령 프롬프트**, 명령 프롬프트를 열려면 아이콘을 클릭 합니다. (필요가 엽니다 관리자로이 이번 되므로 로컬 컴퓨터의 IIS에 배포 되지 않습니다.)
3. 솔루션 파일 및 암호를 사용 하 여 암호에 대 한 경로 사용 하 여 솔루션 파일의 경로를 대체 명령 프롬프트에서 다음 명령을 입력 합니다.

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    이 명령줄에 추가 매개 변수를 포함 하는 알림: `/p:AllowUntrustedCertificate=true`합니다. 이 자습서가 작성 하는 대로 `AllowUntrustedCertificate` 명령줄에서 Azure에 게시할 때 속성을 설정 해야 합니다. 이 버그에 대 한 수정이 릴리스되면 해당 매개 변수를 필요 하지 않습니다.
4. 브라우저를 열고 스테이징 사이트의 URL로 이동 하 고 클릭 합니다 **에 대 한** 페이지 배포 되었는지 확인 합니다.

    테스트 환경에 대해 앞서 살펴본에서 통계를 보려면 학생이 몇 명 만들어야 할 수도 합니다 **에 대 한** 페이지입니다.

## <a name="deploy-to-production"></a>프로덕션 환경에 배포

프로덕션에 배포 하기 위한 프로세스는 스테이징에 대 한 프로세스와 비슷합니다.

1. 필요한 암호를 복사 합니다 *.publishsettings* 프로덕션 웹 사이트의 앞서 다운로드 한 파일입니다.
2. 오픈 **VS2012 용 개발자 명령 프롬프트**합니다.
3. 솔루션 파일 및 암호를 사용 하 여 암호에 대 한 경로 사용 하 여 솔루션 파일의 경로를 대체 명령 프롬프트에서 다음 명령을 입력 합니다.

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    실제 프로덕션 사이트에 대 한 데이터베이스 변경에도 발생 한 경우 일반적으로 복사 합니다 *앱\_offline.htm* 배포 하기 전에 사이트에 파일 및 성공적인 배포 후에 삭제 합니다.
4. 브라우저를 열고 스테이징 사이트의 URL로 이동 하 고 클릭 합니다 **에 대 한** 페이지 배포 되었는지 확인 합니다.

## <a name="summary"></a>요약

이제 명령줄을 사용 하 여 응용 프로그램 업데이트를 배포 했습니다.

![테스트 환경에서 페이지에 대 한](command-line-deployment/_static/image6.png)

다음 자습서에서는 웹을 확장 하는 방법의 예가 표시 됩니다 파이프라인을 게시 합니다. 예제는 프로젝트에 포함 되지 않은 파일을 배포 하는 방법을 보여 줍니다.

> [!div class="step-by-step"]
> [이전](deploying-a-database-update.md)
> [다음](deploying-extra-files.md)
