---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 명령줄 배포 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) 실행 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/15/2013
ms.topic: article
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: acc4a0e7f4744a3759b90e0f1b159da68b7c7362
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30890530"
---
<a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 명령줄 배포
====================
으로 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](http://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈를 배포 하는 방법을 보여 줍니다. ASP.NET (게시) Visual Studio 2012 또는 Visual Studio 2010을 사용 하 여 웹 응용 프로그램을 Azure 앱 서비스 웹 앱 또는 타사 호스팅 공급자입니다. 계열에 대 한 정보를 참조 하십시오. [시리즈의 첫 번째 자습서](introduction.md)합니다.


## <a name="overview"></a>개요

이 자습서는 Visual Studio 웹 호출 하는 방법을 보여 줍니다. 명령줄에서 파이프라인을 게시 합니다. 시나리오에 유용 합니다 [배포 프로세스를 자동화](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) 대신 수동으로 작업 하면 Visual Studio에서, 일반적으로 사용 하 여 한 [소스 코드 버전 제어 시스템이](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)합니다.

## <a name="make-a-change-to-deploy"></a>배포에 대 한 변경 확인

현재 정보 페이지 템플릿 코드를 표시 합니다.

![템플릿 코드 페이지 정보](command-line-deployment/_static/image1.png)

학생 등록 요약을 표시 하는 코드를 있는에서는 바꿉니다.

열기는 *About.aspx* 페이지에서 모든 내부의 태그를 삭제는 `MainContent` `Content` 요소와 해당 위치에 다음 태그를 삽입 합니다.

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

프로젝트를 실행 하 고 선택 된 **에 대 한** 페이지.

![정보 페이지](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a>명령줄을 사용 하 여 테스트를 배포

데이터베이스 변경 내용을 다른 aspnet ContosoUniversity 데이터베이스에 대 한 너무 dbDacFx 데이터베이스 배포 사용 안 함을 배포 하 고 없습니다. 열기는 **웹 게시** 그리고 세 개의 각 마법사는 게시 프로필을 선택 취소는 **데이터베이스 업데이트** 확인란은 **설정** 탭 합니다.

Windows 8 시작 페이지에서 검색할 **v s 2012 용 개발자 명령 프롬프트**합니다.

에 대 한 아이콘을 마우스 오른쪽 단추로 클릭 **v s 2012 용 개발자 명령 프롬프트** 클릭 **관리자 권한으로 실행**합니다.

솔루션 파일의 경로를으로 솔루션 파일의 경로를 대체 명령 프롬프트에서 다음 명령을 입력 합니다.

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

MSBuild 솔루션을 빌드하고 테스트 환경에 배포 합니다.

![명령줄 출력](command-line-deployment/_static/image3.png)

브라우저를 열고로 이동 `http://localhost/ContosoUniversity`, 클릭는 **에 대 한** 페이지 배포에 성공 했는지 확인 합니다.

테스트의 어떤 학생을 만들지 않은 경우에 아래에서 빈 페이지 표시 됩니다는 **학생 본문 통계** 제목입니다. 로 이동는 **학생** 페이지를 클릭 **학생 추가**, 일부 학생 추가 고으로 돌아 오세요는 **에 대 한** 페이지 학생 통계를 볼 수 있습니다.

![테스트 환경에서 페이지에 대 한](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a>키 명령줄 옵션

MSBuild에 솔루션 파일 경로 두 가지 속성을 전달 된 입력 된 명령:

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a>개별 프로젝트를 배포 및 솔루션 배포

솔루션을 빌드하려면 하면 모든 프로젝트에서 솔루션 파일을 지정 합니다. 여러 개의 웹 프로젝트가 솔루션에 있는 경우에 다음과 같은 MSBuild 동작이 적용 됩니다.

- 명령줄에서 지정 하는 속성은 모든 프로젝트에 전달 됩니다. 따라서 각 웹 프로젝트에 사용자가 지정한 이름의 게시 프로필이 있어야 합니다. 지정 하는 경우 `/p:PublishProfile=Test`, 각 웹 프로젝트에는 명명 된 게시 프로필이 있어야 *테스트*합니다.
- 다른도 빌드되지 않으면 때 하나의 프로젝트를 성공적으로 게시 될 수 있습니다. 자세한 내용은 stackoverflow 스레드를 참조 하십시오. [MSBuild 두 개의 패키지와 함께 실패](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages)합니다.

개별 프로젝트 대신 솔루션을 지정 하면 Visual Studio 버전을 지정 하는 매개 변수를 추가 해야 합니다. Visual Studio 2012를 사용 하는 경우 명령줄에 다음 예와 유사 합니다.

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

Visual Studio 2010에 대 한 버전 번호는 10.0입니다. 자세한 내용은 참조 [Visual Studio 프로젝트 호환성 및 VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) Sayed Hashimi 블로그.

### <a name="specifying-the-publish-profile"></a>게시 프로필을 지정

이름이 나 전체 경로를 게시 프로필을 지정할 수는 *.pubxml* 다음 예제와 같이 파일:

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a>명령줄 게시를 위해 지원 되는 방법으로 웹 게시

메서드를 게시 하는 3 개의 명령줄 게시에 대해 지원 됩니다.

- `MSDeploy` -웹 배포를 사용 하 여 게시 합니다.
- `Package` -웹 배포 패키지를 만들어 게시 합니다. 만든 MSBuild 명령에서 패키지를 별도로 설치 해야 합니다.
- `FileSystem` -지정 된 폴더에 파일을 복사 하 여 게시 합니다.

### <a name="specifying-the-build-configuration-and-platform"></a>빌드 구성 및 플랫폼 지정

Visual Studio 또는 명령줄에서 빌드 구성 및 플랫폼 설정 되어야 합니다. 명명 된 속성을 포함 하는 게시 프로필 `LastUsedBuildConfiguration` 및 `LastUsedPlatform`, 하지만 프로젝트를 빌드할 방법을 결정 하기 위해 이러한 속성을 설정할 수 없습니다. 자세한 내용은 참조 [MSBuild: 구성 속성을 설정 하는 방법](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) Sayed Hashimi 블로그.

## <a name="deploy-to-staging"></a>스테이징 배포

Azure에 배포 하려면 명령줄에 암호를 추가 해야 합니다. 에 암호화 된 형태로 저장 된 Visual Studio에서 게시 프로필에서 암호를 저장 하는 경우는 사용자 *. pubxml.user* 파일입니다. 해당 파일 이므로 명령줄 매개 변수에서 암호를 전달 해야 명령줄 배포 작업을 수행할 때 MSBuild에서 액세스할 수 없습니다.

1. 필요한 암호를 복사는 *.publishsettings* 스테이징 웹 사이트에 대 한 이전 다운로드 한 파일입니다. 암호는의 값은 `userPWD` 웹 배포에 대 한 특성 `publishProfile` 요소입니다.

    ![웹 배포 암호](command-line-deployment/_static/image5.png)
2. Windows 8 시작 페이지에서 검색할 **v s 2012 용 개발자 명령 프롬프트**, 명령 프롬프트를 열려면 아이콘을 클릭 합니다. (필요가 없습니다 것 관리자 권한으로이 시간 때문에 열 로컬 컴퓨터에서 IIS에 배포 되지 않습니다.)
3. 솔루션 파일 및 암호와 암호에 경로로 솔루션 파일의 경로를 대체 명령 프롬프트에서 다음 명령을 입력 합니다.

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    이 명령줄에 추가 매개 변수가 포함 되도록 공지: `/p:AllowUntrustedCertificate=true`합니다. 이 자습서를 쓰고 처럼는 `AllowUntrustedCertificate` 명령줄에서 Azure에 게시할 때 속성을 설정 해야 합니다. 이 버그에 대 한 수정 프로그램이 해제 될 때 해당 매개 변수가 필요 하지는 않습니다.
4. 브라우저를 열고 준비 사이트의 URL로 이동 하 고 한 다음 클릭는 **에 대 한** 페이지 배포에 성공 했는지 확인 합니다.

    테스트 환경에 대 한 앞서 살펴본 것 처럼 일부 학생의 통계를 만들어야 할 수도 **에 대 한** 페이지.

## <a name="deploy-to-production"></a>프로덕션 환경에 배포

프로덕션 환경에 배포 하기 위한 프로세스는 준비에 대 한 작업과 프로세스가 비슷합니다.

1. 필요한 암호를 복사는 *.publishsettings* 이전 프로덕션 웹 사이트에 대 한 다운로드 한 파일입니다.
2. 열기 **v s 2012 용 개발자 명령 프롬프트**합니다.
3. 솔루션 파일 및 암호와 암호에 경로로 솔루션 파일의 경로를 대체 명령 프롬프트에서 다음 명령을 입력 합니다.

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    실제 프로덕션 사이트에 대 한 데이터베이스 변경 서버가 이기도 한 경우 일반적으로 복사 된 *앱\_offline.htm* 배포 하기 전에 사이트에 파일 및 배포 된 후 삭제 합니다.
4. 브라우저를 열고 준비 사이트의 URL로 이동 하 고 한 다음 클릭는 **에 대 한** 페이지 배포에 성공 했는지 확인 합니다.

## <a name="summary"></a>요약

이제 명령줄을 사용 하 여 응용 프로그램 업데이트를 배포 했습니다.

![테스트 환경에서 페이지에 대 한](command-line-deployment/_static/image6.png)

다음 자습서에서는 웹을 확장 하는 방법의 예가 표시 됩니다 파이프라인을 게시 합니다. 이 예제에서는 프로젝트에 포함 되지 않은 파일을 배포 하는 방법을 설명 합니다.

> [!div class="step-by-step"]
> [이전](deploying-a-database-update.md)
> [다음](deploying-extra-files.md)
