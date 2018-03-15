---
title: "Visual Studio를 사용 하 여 Azure 및 ASP.NET Core를 사용 하 여 Git 연속 배포"
author: rick-anderson
description: "Visual Studio를 사용하여 ASP.NET Core 웹앱을 만들고 연속 배포를 위한 Git을 사용하여 Azure App Service에 배포하는 방법을 알아봅니다."
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 10/14/2016
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/azure-apps/azure-continuous-deployment
ms.openlocfilehash: 7302de1ace62dba53b317039aac7f4763314aa19
ms.sourcegitcommit: 493a215355576cfa481773365de021bcf04bb9c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="continuous-deployment-to-azure-with-visual-studio-and-git-with-aspnet-core"></a>Visual Studio를 사용 하 여 Azure 및 ASP.NET Core를 사용 하 여 Git 연속 배포

작성자: [Erik Reitan](https://github.com/Erikre)

[!INCLUDE[Azure App Service Preview Notice](../../includes/azure-apps-preview-notice.md)]

이 자습서 연속 배포를 사용 하 여 Visual Studio를 사용 하 여 ASP.NET Core 웹 앱을 만들고 Visual Studio에서 Azure 앱 서비스에 배포 하는 방법을 보여 줍니다.

또한 [연속 배포를 사용하여 Azure Web App을 빌드하고 게시하기 위해 VSTS 사용](/vsts/build-release/archive/apps/aspnet/aspnet-4-ci-cd-azure-automatic)을 참조하세요. 여기서는 Visual Studio Team Services를 사용하여 [Azure App Service](/azure/app-service/app-service-web-overview)에 대한 CD(지속적인 업데이트) 워크플로를 구성하는 방법을 보여줍니다. Team Services에서 azure 지속적인 업데이트 Azure 앱 서비스에서 호스트 되는 앱에 대 한 업데이트를 게시 하는 강력한 배포 파이프라인 설정을 간단 하 게 합니다. 파이프라인을 빌드, 테스트 실행, 스테이징 슬롯에 배포 및 다음 프로덕션에 배포 하기 위해 Azure 포털에서 구성할 수 있습니다.

> [!NOTE]
> 이 자습서를 완료 하려면 Microsoft Azure 계정은 필수입니다. 계정을 가져오려면 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/?WT.mc_id=A261C142F) 또는 [무료 평가판에 등록](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)합니다.

## <a name="prerequisites"></a>전제 조건

이 자습서에서는 다음 소프트웨어가 설치 되어 가정 합니다.

* [Visual Studio](https://www.visualstudio.com)
* [.NET core SDK](https://www.microsoft.com/net/download/core) (런타임 및 도구가)
* Windows용 [Git](https://git-scm.com/downloads)

## <a name="create-an-aspnet-core-web-app"></a>ASP.NET Core 웹앱 만들기

1. Visual Studio를 시작합니다.

1. **파일** 메뉴에서 **새로 만들기** > **프로젝트**를 선택합니다.

1. **ASP.NET Core 웹 응용 프로그램** 프로젝트 템플릿을 선택합니다. **설치됨** > **템플릿** > **Visual C#** > **.NET Core** 아래에 표시됩니다. 프로젝트 이름을 `SampleWebAppDemo`로 지정합니다. 선택 된 **새 Git 리포지토리 만들기** 옵션 **확인**합니다.

   ![새 프로젝트 대화 상자](azure-continuous-deployment/_static/01-new-project.png)

1. **새 ASP.NET Core 프로젝트** 대화 상자에서 ASP.NET Core **빈** 템플릿을 선택한 후 **확인**을 클릭합니다.

   ![새 ASP.NET 프로젝트 대화 상자](azure-continuous-deployment/_static/02-web-site-template.png)

> [!NOTE]
> .NET Core의 최신 버전은 2.0입니다.

### <a name="running-the-web-app-locally"></a>로컬로 웹앱 실행

1. Visual Studio에서 앱 만들기를 완료하면 **디버그** > **디버깅 시작**을 선택하여 앱을 실행합니다. 눌러 **F5**합니다.

   Visual Studio 및 새 앱을 초기화하는 데 시간이 걸릴 수 있습니다. 완료 되 면 브라우저에서 실행 중인 응용 프로그램으로 표시 됩니다.

   ![브라우저 창에서는 'Hello World!'을 표시하는 응용 프로그램이 실행 중이라고 표시합니다.](azure-continuous-deployment/_static/04-browser-runapp.png)

1. 실행 중인 웹 응용 프로그램을 검토 한 후 브라우저를 닫고 응용 프로그램을 중지 하려면 Visual Studio의 도구 모음에서 "디버깅을 중지" 아이콘을 선택 합니다.

## <a name="create-a-web-app-in-the-azure-portal"></a>Azure Portal에서 웹앱 만들기

다음 단계에서는 Azure 포털에서 웹 앱을 만듭니다.

1. 에 로그인 하 고 [Azure 포털](https://portal.azure.com)합니다.

1. 선택 **새로** 에서 맨 왼쪽 포털 인터페이스입니다.

1. 선택 **웹 + 모바일** > **웹 앱**합니다.

   ![Microsoft Azure Portal: 새 단추: Marketplace 아래에서 웹 + 모바일: 주요 앱 아래에서 Web App 단추](azure-continuous-deployment/_static/05-azure-newwebapp.png)

1. **Web App** 블레이드에서 **App Service 이름**에 고유한 값을 입력합니다.

   ![Web App 블레이드](azure-continuous-deployment/_static/06-azure-newappblade.png)

   > [!NOTE]
   > **응용 프로그램 서비스 이름** 이름은 고유 해야 합니다. 포털에서 이름이 제공 된 경우이 규칙을 적용 합니다. 다른 값을 제공 하는 경우 각 해당 값을 대체 **SampleWebAppDemo** 이 자습서에서는 합니다.

   또한 **Web App** 블레이드에서 기존 **App Service 계획/위치**를 선택하거나 새로 만듭니다. 새 계획을 만드는 경우 가격 책정 계층, 위치 및 기타 옵션을 선택 합니다. 앱 서비스 계획에 대 한 자세한 내용은 참조 하십시오. [Azure 앱 서비스 계획 심도 깊은 개요](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)합니다.

1. **만들기**를 선택합니다. Azure 프로 비전 하 고 웹 응용 프로그램을 실행 합니다.

   ![Azure Portal: 샘플 Web App 데모 01 Essentials 블레이드](azure-continuous-deployment/_static/07-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a>새 웹앱에 대한 Git 게시 사용

Git는 Azure 앱 서비스 웹 앱을 배포 하는 데 사용할 수 있는 분산된 버전 제어 시스템입니다. 웹 앱 코드는 로컬 Git 리포지토리에 저장 됩니다 및 코드를 원격 리포지토리에 푸시 하 여 Azure에 배포 합니다.

1. 에 로그인 된 [Azure 포털](https://portal.azure.com)합니다.

1. 선택 **응용 프로그램 서비스** Azure 구독과 연결 된 응용 프로그램 서비스의 목록을 볼 수 있습니다.

1. 이 자습서의 이전 섹션에서 만든 웹 응용 프로그램을 선택 합니다.

1. **배포** 블레이드에서 **배포 옵션** > **원본 선택** > **로컬 Git 리포지토리**를 선택합니다.

   ![설정 블레이드: 배포 원본 블레이드: 원본 블레이드 선택](azure-continuous-deployment/_static/deployment-options.png)

1. **확인**을 선택합니다.

1. 웹 앱 또는 다른 앱 서비스 앱 게시에 대 한 배포 자격 증명 설정 이전에 하지 않은, 경우에 지금 설정:

   * 선택 **설정** > **배포 자격 증명**합니다. **배포 자격 증명 설정** 블레이드가 표시 됩니다.
   * 사용자 이름 및 암호를 만듭니다. Git를 설정 하는 경우 나중에 사용할 암호를 저장 합니다.
   * **저장**을 선택합니다.

1. 에 **웹 앱** 블레이드를 **설정** > **속성**합니다. 배포 하려면 원격 Git 리포지토리의 URL은 아래에 표시 된 **GIT URL**합니다.

1. 나중에 자습서에서 사용할 **GIT URL** 값을 복사합니다.

   ![Azure Portal: 응용 프로그램 속성 블레이드](azure-continuous-deployment/_static/09-azure-giturl.png)

## <a name="publish-the-web-app-to-azure-app-service"></a>Azure 앱 서비스에 웹 앱을 게시

이 섹션에서는 사용 하 여 Visual Studio 및 푸시 해당 리포지토리 로부터 Azure에 웹 앱을 배포 하는 로컬 Git 리포지토리를 만듭니다. 관련 단계에는 다음이 포함됩니다.

* 로컬 저장소를 Azure에 배포할 수 있도록 GIT URL 값을 사용 하 여 원격 리포지토리 설정을 추가 합니다.
* 프로젝트 변경 내용을 커밋하십시오.
* Azure에서 원격 저장소에 로컬 저장소에서 프로젝트 변경 내용 적용 합니다.

1. **솔루션 탐색기**에서 **솔루션 'SampleWebAppDemo'**를 마우스 오른쪽 단추로 클릭하고 **커밋**을 선택합니다. **팀 탐색기** 표시 됩니다.

   ![팀 탐색기 연결 탭](azure-continuous-deployment/_static/10-team-explorer.png)

1. **팀 탐색기**에서 **홈**(홈 아이콘) > **설정** > **리포지토리 설정**을 선택합니다.

1. 에 **원격** 섹션은 **리포지토리 설정**선택, **추가**합니다. **원격 추가** 대화 상자가 표시 됩니다.

1. 원격 리포지토리의 **이름**을 **Azure SampleApp**으로 설정합니다.

1. 에 대 한 값 설정 **인출** 에 **Git URL** 이 자습서의 앞부분에 나오는 Azure에서 복사 하는 합니다. 이 URL은 **.git**로 끝납니다.

   ![원격 대화 상자 편집](azure-continuous-deployment/_static/11-add-remote.png)

   > [!NOTE]
   > 대신 원격 저장소에서 지정는 **명령 창** 열어는 **명령 창**프로젝트 디렉터리를 변경 하 고 명령을 입력 합니다. 예제:
   >
   > `git remote add Azure-SampleApp https://me@sampleapp.scm.azurewebsites.net:443/SampleApp.git`

1. **홈**(홈 아이콘) > **설정** > **전역 설정**을 선택합니다. 이름 및 전자 메일 주소가 설정 되어 있는지 확인 합니다. 선택 **업데이트** 필요한 경우.

1. **홈** > **변경 내용**을 선택하여 **변경 내용** 보기로 돌아갑니다.

1. 커밋 메시지를 같은 입력 **초기 푸시 #1** 선택 **커밋**합니다. 이 작업을 만듭니다는 *커밋* 로컬로 합니다.

   ![팀 탐색기 연결 탭](azure-continuous-deployment/_static/12-initial-commit.png)

   > [!NOTE]
   > 변경 커밋 엔터티나는 **명령 창** 열어는 **명령 창**프로젝트 디렉터리를 변경 하 고에서 git 명령을 입력 합니다. 예제:
   >
   > `git add .`
   >
   > `git commit -am "Initial Push #1"`

1. **홈** > **동기화** > **동작** > **명령 프롬프트 열기**를 선택합니다. 프로젝트 디렉터리에 명령 프롬프트가 열립니다.

1. 명령 창에서 다음 명령을 입력합니다.

   `git push -u Azure-SampleApp master`

1. Azure 입력 **배포 자격 증명** Azure 앞부분에서 만든 암호입니다.

   이 명령은 로컬 프로젝트 파일을 Azure로 푸시할 프로세스를 시작 합니다. 위 명령의 출력을에서 배포가 성공 했다는 메시지가로 끝납니다.

   ```
   remote: Finished successfully.
   remote: Running post deployment command(s)...
   remote: Deployment successful.
   To https://username@samplewebappdemo01.scm.azurewebsites.net:443/SampleWebAppDemo01.git
   * [new branch]      master -> master
   Branch master set up to track remote branch master from Azure-SampleApp.
   ```

   > [!NOTE]
   > 공동 작업 프로젝트에 필요한 경우에 강제 설치 하 여 [GitHub](https://github.com) azure 푸시하기 전에 합니다.
 
### <a name="verify-the-active-deployment"></a>활성 배포 확인

로컬 환경에서 웹 앱 전송 하기 위해서는 Azure 성공 했는지 확인 합니다.

에 [Azure 포털](https://portal.azure.com), 웹 사이트를 선택 합니다. 선택 **배포** > **배포 옵션**합니다.

![Azure Portal: 설정 블레이드: 성공적인 배포를 보여주는 배포 블레이드](azure-continuous-deployment/_static/13-verify-deployment.png)

## <a name="run-the-app-in-azure"></a>Azure에서 앱 실행

웹 앱을 Azure에 배포 했으므로 응용 프로그램을 실행 합니다.

이 두 가지 방법으로 수행할 수 있습니다.

* Azure 포털에서 웹 앱에 대 한 웹 앱 블레이드를 찾습니다. 선택 **찾아보기** 기본 브라우저에서 앱을 볼 수 있습니다.
* 브라우저를 열고 웹 앱에 대 한 URL을 입력 합니다. 예: `http://SampleWebAppDemo.azurewebsites.net`

## <a name="update-the-web-app-and-republish"></a>웹 앱을 업데이트 하 고 다시 게시

로컬 코드를 변경한 후 다시 게시 합니다.

1. Visual Studio의 **솔루션 탐색기**에서 *Startup.cs* 파일을 엽니다.

1. `Configure` 메서드에서 `Response.WriteAsync` 메서드를 수정하여 다음과 같이 표시되도록 합니다.

   ```csharp
   await context.Response.WriteAsync("Hello World! Deploy to Azure.");
   ```

1. 에 변경 내용을 저장 *Startup.cs*합니다.

1. **솔루션 탐색기**에서 **솔루션 'SampleWebAppDemo'**를 마우스 오른쪽 단추로 클릭하고 **커밋**을 선택합니다. **팀 탐색기** 표시 됩니다.

1. 커밋 메시지를 같은 입력 `Update #2`합니다.

1. **커밋** 단추를 눌러 프로젝트 변경 내용을 커밋합니다.

1. **홈** > **동기화** > **작업** > **푸시**를 선택합니다.

> [!NOTE]
> 변경 내용 적용을 사용 하는 대신는 **명령 창** 열어는 **명령 창**프로젝트 디렉터리를 변경 하 고 git 명령을 입력 합니다. 예제:
> 
> `git push -u Azure-SampleApp master`

## <a name="view-the-updated-web-app-in-azure"></a>Azure에서 업데이트된 웹앱 보기

업데이트 된 웹 응용 프로그램을 선택 하 여 볼 **찾아보기** Azure 포털에서 또는 브라우저를 열고 웹 앱에 대 한 URL을 입력 하 여 웹 앱 블레이드에서 합니다. 예: `http://SampleWebAppDemo.azurewebsites.net`

## <a name="additional-resources"></a>추가 자료

* [VSTS 연속 배포를 사용 하 여 Azure 웹 앱을 빌드하고 게시를 사용 하 여](/vsts/build-release/archive/apps/aspnet/aspnet-4-ci-cd-azure-automatic)
* [프로젝트 Kudu](https://github.com/projectkudu/kudu/wiki)
