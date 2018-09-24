---
title: 명령줄 도구를 사용하여 Azure에 ASP.NET Core 앱 게시
author: camsoper
description: Git 명령줄 클라이언트를 사용하여 Azure App Service에 ASP.NET Core 앱을 게시하는 방법을 알아봅니다.
ms.author: casoper
ms.custom: mvc
ms.date: 11/03/2017
services: multiple
uid: tutorials/publish-to-azure-webapp-using-cli
ms.openlocfilehash: 63a313de786b1f89e84c594cbd665d1b230e4ba3
ms.sourcegitcommit: c12ebdab65853f27fbb418204646baf6ce69515e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46523248"
---
# <a name="publish-an-aspnet-core-app-to-azure-with-command-line-tools"></a>명령줄 도구를 사용하여 Azure에 ASP.NET Core 앱 게시

작성자: [Cam Soper](https://twitter.com/camsoper)

[!INCLUDE [Azure App Service Preview Notice](../includes/azure-apps-preview-notice.md)]

이 자습서에서는 명령줄 도구를 사용하여 Microsoft Azure App Service에 ASP.NET Core 앱을 빌드하고 배포하는 방법을 보여줍니다. 작업이 완료되면 Azure App Service 웹앱으로 호스트된 ASP.NET MVC Core에 Razor Pages 웹앱을 빌드했습니다. 이 자습서는 Windows 명령줄 도구를 사용하여 작성되지만 macOS 및 Linux 환경에도 적용할 수 있습니다.

이 자습서에서는 다음 방법을 학습합니다.

> [!div class="checklist"]
> * Azure CLI를 사용하여 Azure App Service 웹 사이트 만들기
> * Git 명령줄 도구를 사용하여 ASP.NET Core 앱을 Azure App Service에 배포

## <a name="prerequisites"></a>전제 조건

이 자습서를 완료하려면 다음이 필요합니다.

* [Microsoft Azure 구독](https://azure.microsoft.com/free/)
* [!INCLUDE [](~/includes/net-core-sdk-download-link.md)]
* [Git](https://www.git-scm.com/) 명령줄 클라이언트

## <a name="create-a-web-app"></a>웹앱 만들기

웹앱의 새 디렉터리를 만들고, 새 ASP.NET Core Razor Pages 앱을 만든 다음, 웹 사이트를 로컬로 실행합니다.

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

::: moniker range=">= aspnetcore-2.1"

```console
REM Create a new ASP.NET Core Razor Pages app
dotnet new webapp -o MyApplication

REM Change to the new directory that was just created
cd MyApplication

REM Run the app
dotnet run
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```console
REM Create a new ASP.NET Core Razor Pages app
dotnet new razor -o MyApplication

REM Change to the new directory that was just created
cd MyApplication

REM Run the app
dotnet run
```

::: moniker-end

# <a name="othertabother"></a>[기타](#tab/other)

::: moniker range=">= aspnetcore-2.1"

```bash
# Create a new ASP.NET Core Razor Pages app
dotnet new webapp -o MyApplication

# Change to the new directory that was just created
cd MyApplication

# Run the app
dotnet run
```

::: moniker-end

::: moniker range="= aspnetcore-2.0"

```bash
# Create a new ASP.NET Core Razor Pages app
dotnet new razor -o MyApplication

# Change to the new directory that was just created
cd MyApplication

# Run the app
dotnet run
```

::: moniker-end

---

![명령줄 출력](publish-to-azure-webapp-using-cli/_static/new_prj.png)

`http://localhost:5000`으로 이동하여 앱을 테스트합니다.

![로컬로 실행되는 웹 사이트](publish-to-azure-webapp-using-cli/_static/app_test.png)

## <a name="create-the-azure-app-service-instance"></a>Azure App Service 인스턴스 만들기

[Azure Cloud Shell](/azure/cloud-shell/quickstart)을 사용하여 리소스 그룹, App Service 계획 및 App Service 웹앱을 만듭니다.

```azurecli-interactive
# Generate a unique Web App name
let randomNum=$RANDOM*$RANDOM
webappname=tutorialApp$randomNum

# Create the DotNetAzureTutorial resource group
az group create --name DotNetAzureTutorial --location EastUS

# Create an App Service plan.
az appservice plan create --name $webappname --resource-group DotNetAzureTutorial --sku FREE

# Create the Web App
az webapp create --name $webappname --resource-group DotNetAzureTutorial --plan $webappname
```

배포 전에 다음 명령을 사용하여 계정 수준 배포 자격 증명을 설정합니다.

```azurecli-interactive
az webapp deployment user set --user-name <desired user name> --password <desired password>
```

Git을 사용하여 앱을 배포하려면 배포 URL이 필요합니다. 다음과 같이 URL을 검색합니다.

```azurecli-interactive
az webapp deployment source config-local-git -n $webappname -g DotNetAzureTutorial --query [url] -o tsv
```

표시된 URL이 `.git`으로 끝나는 것을 알 수 있습니다. 다음 단계에서 사용됩니다.

## <a name="deploy-the-app-using-git"></a>Git를 사용하여 앱 배포

Git을 사용하여 로컬 컴퓨터에서 배포할 준비가 되었습니다.

> [!NOTE]
> 줄 끝에 대한 Git 경고는 무시해도 됩니다.

# <a name="windowstabwindows"></a>[Windows](#tab/windows)

```cmd
REM Initialize the local Git repository
git init

REM Add the contents of the working directory to the repo
git add --all

REM Commit the changes to the local repo
git commit -a -m "Initial commit"

REM Add the URL as a Git remote repository
git remote add azure <THE GIT URL YOU NOTED EARLIER>

REM Push the local repository to the remote
git push azure master
```

# <a name="othertabother"></a>[기타](#tab/other)

```bash
# Initialize the local Git repository
git init

# Add the contents of the working directory to the repo
git add --all

# Commit the changes to the local repo
git commit -a -m "Initial commit"

# Add the URL as a Git remote repository
git remote add azure <THE GIT URL YOU NOTED EARLIER>

# Push the local repository to the remote
git push azure master
```

---

Git은 이전에 설정된 배포 자격 증명을 요구합니다. 인증 후에 앱은 원격 위치로 푸시되고, 빌드되며 배포됩니다.

![Git 배포 출력](publish-to-azure-webapp-using-cli/_static/post_deploy.png)

## <a name="test-the-app"></a>앱 테스트

`https://<web app name>.azurewebsites.net`으로 이동하여 앱을 테스트합니다. Cloud Shell(또는 Azure CLI)에 주소를 표시하려면 다음을 사용합니다.

```azurecli-interactive
az webapp show -n $webappname -g DotNetAzureTutorial --query defaultHostName -o tsv
```

![Azure에서 실행 중인 앱](publish-to-azure-webapp-using-cli/_static/app_deployed.png)

## <a name="clean-up"></a>정리

앱 테스트와 코드 및 리소스를 검사가 끝나면 리소스 그룹을 삭제하여 웹앱 및 계획을 삭제합니다.

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 방법을 학습했습니다.

> [!div class="checklist"]
> * Azure CLI를 사용하여 Azure App Service 웹 사이트 만들기
> * Git 명령줄 도구를 사용하여 ASP.NET Core 앱을 Azure App Service에 배포

다음으로, 명령줄을 사용하여 CosmosDB를 사용하는 기존 웹앱을 배포하는 방법을 알아보세요.

> [!div class="nextstepaction"]
> [.NET Core를 사용하여 명령줄에서 Azure에 배포](/dotnet/azure/dotnet-quickstart-xplat)
