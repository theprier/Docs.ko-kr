---
title: Visual Studio Tools for Docker 및 ASP.NET Core
author: spboyer
description: Visual Studio 2017 도구 및 Windows용 Docker를 사용하여 ASP.NET Core 앱을 컨테이너화하는 방법에 대해 알아봅니다.
ms.author: scaddie
ms.custom: mvc
ms.date: 07/18/2018
uid: host-and-deploy/docker/visual-studio-tools-for-docker
ms.openlocfilehash: afa7b05820ba021c50d9c23804095f7edd8b71f1
ms.sourcegitcommit: ee2b26c7d08b38c908c668522554b52ab8efa221
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39146886"
---
# <a name="visual-studio-tools-for-docker-with-aspnet-core"></a>Visual Studio Tools for Docker 및 ASP.NET Core

[Visual Studio 2017](https://www.visualstudio.com/)에서는 .NET Core를 대상으로 하는 컨테이너화된 ASP.NET Core 앱의 빌드, 디버그 및 실행을 지원합니다. Windows 및 Linux 컨테이너가 모두 지원됩니다.

## <a name="prerequisites"></a>전제 조건

* **.NET Core 플랫폼 간 개발** 워크로드가 있는 [Visual Studio 2017](https://www.visualstudio.com/)
* [Windows용 Docker](https://docs.docker.com/docker-for-windows/install/)

## <a name="installation-and-setup"></a>설치 및 설정

Docker 설치의 경우 [Windows용 Docker: 설치하기 전에 알아야 할 사항](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install)의 정보를 검토하고 [Windows용 Docker](https://docs.docker.com/docker-for-windows/install/)를 설치합니다.

Windows용 Docker에서 **[공유 드라이브](https://docs.docker.com/docker-for-windows/#shared-drives)** 는 볼륨 매핑 및 디버깅을 지원하도록 구성되어야 합니다. 시스템 트레이의 Docker 아이콘을 마우스 오른쪽 단추로 클릭하고 **설정...** 을 선택한 다음, **공유 드라이브**를 선택합니다. Docker에서 파일을 저장하는 드라이브를 선택합니다. **적용**을 선택합니다.

![공유 드라이브](./visual-studio-tools-for-docker/_static/settings-shared-drives-win.png)

> [!TIP]
> Visual Studio 2017 버전 15.6 이상은 **공유 드라이브**가 구성되지 않은 경우 메시지를 표시합니다.

## <a name="add-docker-support-to-an-app"></a>앱에 Docker 지원 추가

ASP.NET Core 프로젝트에 Docker 지원을 추가하려면 프로젝트가 .NET Core를 대상으로 해야 합니다. Linux 및 Windows 컨테이너가 둘 다 지원됩니다.

프로젝트에 Docker 지원을 추가할 때 Windows 또는 Linux 컨테이너를 선택할 수 있습니다. Docker 호스트는 동일한 컨테이너 형식을 실행 중이어야 합니다. 실행 중인 Docker 인스턴스에서 컨테이너 형식을 변경하려면 시스템 트레이의 Docker 아이콘을 마우스 오른쪽 단추로 클릭하고 **Windows 컨테이너로 전환** 또는 **Linux 컨테이너로 전환**을 선택합니다.

### <a name="new-app"></a>새 앱

**ASP.NET Core 웹 응용 프로그램** 프로젝트 템플릿을 사용하여 새 앱을 만들 때 **Docker 지원 사용** 확인란을 선택합니다.

![Docker 지원 사용 확인란](visual-studio-tools-for-docker/_static/enable-docker-support-check box.png)

대상 프레임워크가 .NET Core인 경우 **OS** 드롭다운에서 컨테이너 유형을 선택할 수 있습니다.

### <a name="existing-app"></a>기존 앱

Visual Studio Tools for Docker는 .NET Framework를 대상으로 하는 기존 ASP.NET Core 프로젝트에 Docker 추가를 지원하지 않습니다. .NET Core를 대상으로 하는 ASP.NET Core 프로젝트의 경우 도구를 통해 Docker 지원을 추가하는 두 가지 옵션이 있습니다. Visual Studio에서 프로젝트를 열고 다음 옵션 중 하나를 선택합니다.

* **프로젝트** 메뉴에서 **Docker 지원**을 선택합니다.
* 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **Docker 지원**을 선택합니다.

## <a name="docker-assets-overview"></a>Docker 자산 개요

Visual Studio Tools for Docker는 다음 파일을 포함하여 솔루션에 *docker-compose* 프로젝트를 추가합니다.

* *.dockerignore*: 빌드 컨텍스트를 생성할 때 제외할 파일 및 디렉터리 패턴의 목록을 포함합니다.
* *docker-compose.yml*: 빌드되어 `docker-compose build` 및 `docker-compose run`으로 각각 실행할 이미지 컬렉션을 정의하는 데 사용되는 기본 [Docker Compose](https://docs.docker.com/compose/overview/) 파일입니다.
* *docker-compose.override.yml*: 서비스에 대한 구성 재정의를 포함하는 Docker Compose에서 읽는 옵션 파일입니다. Visual Studio는 `docker-compose -f "docker-compose.yml" -f "docker-compose.override.yml"`을 실행하여 이러한 파일을 병합합니다.

최종 Docker 이미지를 만들기 위한 레시피인 *Dockerfile*은 프로젝트 루트에 추가됩니다. 그 안의 명령을 이해하려면 [Dockerfile 참조](https://docs.docker.com/engine/reference/builder/)를 참조하세요. 이 특정 *Dockerfile*은 빌드 단계라는 네 개의 단계를 포함하는 [다단계 빌드](https://docs.docker.com/engine/userguide/eng-image/multistage-build/)를 사용합니다.

[!code-dockerfile[](visual-studio-tools-for-docker/samples/HelloDockerTools/HelloDockerTools/Dockerfile?highlight=1,5,14,17)]

*Dockerfile*은 [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore) 이미지를 기반으로 합니다. 이 기본 이미지는 시작 성능을 개선하도록 prejit된 ASP.NET Core NuGet 패키지를 포함합니다.

*docker-compose.yml* 파일에는 프로젝트를 실행할 때 생성되는 이미지의 이름이 포함됩니다.

[!code-yaml[](visual-studio-tools-for-docker/samples/HelloDockerTools/docker-compose.yml?highlight=5)]

앞의 예제에서 `image: hellodockertools`는 앱이 **디버그** 모드에서 실행될 때 `hellodockertools:dev` 이미지를 생성합니다. 앱이 **릴리스** 모드에서 실행될 때 `hellodockertools:latest` 이미지가 생성됩니다.

레지스트리에 이미지를 푸시하는 경우 이미지 이름 앞에 [Docker 허브](https://hub.docker.com/) 사용자 이름을 추가합니다(예: `dockerhubusername/hellodockertools`). 또는 구성에 따라 개인 레지스트리 URL을 포함하도록 이미지 이름을 변경합니다(예: `privateregistry.domain.com/hellodockertools`).

## <a name="debug"></a>디버그

도구 모음의 디버그 드롭다운에서 **Docker**를 선택하고 앱에서 디버깅을 시작합니다. **출력** 창의 **Docker** 뷰는 진행 중인 다음 작업을 표시합니다.

* *microsoft/aspnetcore* 런타임 이미지를 가져옵니다(캐시에 아직 없는 경우).
* *microsoft/aspnetcore-build* compile/publish 이미지를 가져옵니다(캐시에 아직 없는 경우).
* *ASPNETCORE_ENVIRONMENT* 환경 변수는 컨테이너 내에서 `Development`로 설정됩니다.
* 포트 80이 공개되고 localhost의 동적으로 할당된 포트에 매핑됩니다. 포트는 Docker 호스트에 의해 결정되며 `docker ps` 명령을 사용하여 쿼리할 수 있습니다.
* 앱이 컨테이너에 복사됩니다.
* 컨테이너에 연결된 디버거와 함께 기본 브라우저가 시작되며 동적으로 할당된 포트를 사용합니다.

결과 Docker 이미지는 앱의 *dev* 이미지이며 *microsoft/aspnetcore* 이미지가 기본 이미지입니다. **패키지 관리자 콘솔**(PMC) 창에서 `docker images` 명령을 실행합니다. 컴퓨터의 이미지가 표시됩니다.

```console
REPOSITORY                   TAG                   IMAGE ID            CREATED             SIZE
hellodockertools             latest                f8f9d6c923e2        About an hour ago   391MB
hellodockertools             dev                   85c5ffee5258        About an hour ago   389MB
microsoft/aspnetcore-build   2.0-nanoserver-1709   d7cce94e3eb0        15 hours ago        1.86GB
microsoft/aspnetcore         2.0-nanoserver-1709   8872347d7e5d        40 hours ago        389MB
```

> [!NOTE]
> **디버그** 구성은 볼륨 탑재를 사용하여 반복 환경을 제공하므로 dev 이미지에는 앱 콘텐츠가 없습니다. 이미지를 푸시하려면 **Release** 구성을 사용합니다.

PMC에서 `docker ps` 명령을 실행합니다. 앱은 컨테이너를 사용하여 실행됩니다.

```console
CONTAINER ID        IMAGE                  COMMAND                   CREATED             STATUS              PORTS                   NAMES
baf9a678c88d        hellodockertools:dev   "C:\\remote_debugge..."   21 seconds ago      Up 19 seconds       0.0.0.0:37630->80/tcp   dockercompose4642749010770307127_hellodockertools_1
```

## <a name="edit-and-continue"></a>편집하며 계속하기

정적 파일 및 Razor 뷰에 대한 변경 사항은 자동으로 업데이트되므로 컴파일 단계가 필요하지 않습니다. 내용을 변경 및 저장하고 브라우저를 새로 고쳐 업데이트를 확인합니다.

코드 파일을 수정하려면 컨테이너 내에서 컴파일하고 Kestrel을 다시 시작해야 합니다. 변경 후 컨테이너 내에서 `CTRL+F5`를 사용하여 프로세스를 수행하고 앱을 시작합니다. Docker 컨테이너는 다시 빌드되거나 중지되지 않습니다. PMC에서 `docker ps` 명령을 실행합니다. 원래 컨테이너는 10분 이전을 기준으로 여전히 실행됩니다.

```console
CONTAINER ID        IMAGE                  COMMAND                   CREATED             STATUS              PORTS                   NAMES
baf9a678c88d        hellodockertools:dev   "C:\\remote_debugge..."   10 minutes ago      Up 10 minutes       0.0.0.0:37630->80/tcp   dockercompose4642749010770307127_hellodockertools_1
```

## <a name="publish-docker-images"></a>Docker 이미지 게시

앱의 개발 및 디버그 주기를 완료한 후 앱의 프로덕션 이미지를 만들 때 Visual Studio Tools for Docker를 사용할 수 있습니다. 구성 드롭다운을 **릴리스**로 변경하고 앱을 빌드합니다. 도구에서 ‘최신’ 태그로 이미지를 생성하면 이를 개인 레지스트리 또는 Docker Hub에 푸시할 수 있습니다.

PMC에서 `docker images` 명령을 실행하여 이미지의 목록을 봅니다.

```console
REPOSITORY                   TAG                   IMAGE ID            CREATED             SIZE
hellodockertools             latest                4cb1fca533f0        19 seconds ago      391MB
hellodockertools             dev                   85c5ffee5258        About an hour ago   389MB
microsoft/aspnetcore-build   2.0-nanoserver-1709   d7cce94e3eb0        16 hours ago        1.86GB
microsoft/aspnetcore         2.0-nanoserver-1709   8872347d7e5d        40 hours ago        389MB
```

> [!NOTE]
> `docker images` 명령은 *\<없음>*(위에 나열되지 않음)으로 식별된 리포지토리 이름 및 태그로 매개자 이미지를 반환합니다. 이러한 이름이 지정되지 않는 이미지는 [다단계 빌드](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) *Dockerfile*에 의해 생성됩니다. 최종 이미지 빌드의 효율성을 향상시키며&mdash;변경될 때 필요한 레이어만 다시 빌드됩니다. 더 이상 매개자 이미지가 필요하지 않은 경우 [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/) 명령을 사용하여 삭제합니다.

*dev* 이미지와 비교하여 프로덕션 또는 릴리스 이미지의 크기가 작을 수 있습니다. 볼륨 매핑으로 인해 디버거 및 앱은 컨테이너 내부가 아닌 로컬 컴퓨터에서 실행되었습니다. *최신* 이미지는 호스트 컴퓨터에서 앱을 실행하는 데 필요한 앱 코드를 패키징했습니다. 따라서 델타는 앱 코드의 크기입니다.

## <a name="additional-resources"></a>추가 자료

* [Docker 관련 Visual Studio 2017 개발 문제 해결](/azure/vs-azure-tools-docker-troubleshooting-docker-errors)
* [Visual Studio Tools for Docker GitHub 리포지토리](https://github.com/Microsoft/DockerTools)
