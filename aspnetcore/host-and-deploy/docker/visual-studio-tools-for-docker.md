---
title: "Visual Studio Tools for Docker 및 ASP.NET Core"
author: spboyer
description: "Visual Studio 2017 도구 및 Windows용 Docker를 사용하여 ASP.NET Core 앱을 컨테이너화하는 방법에 대해 알아봅니다."
manager: wpickett
ms.author: scaddie
ms.custom: mvc
ms.date: 12/12/2017
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/docker/visual-studio-tools-for-docker
ms.openlocfilehash: b2a3c369a22d50fcefdb96914f5bf84bfafab7cb
ms.sourcegitcommit: 6fa546140575b3eb279eabae12d9acad966f70e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2018
---
# <a name="visual-studio-tools-for-docker-with-aspnet-core"></a><span data-ttu-id="ab16e-103">Visual Studio Tools for Docker 및 ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ab16e-103">Visual Studio Tools for Docker with ASP.NET Core</span></span>

<span data-ttu-id="ab16e-104">[Visual Studio 2017](https://www.visualstudio.com/) 빌드, 디버깅 및 실행 중인 컨테이너 화 된 ASP.NET Core.NET Core를 대상으로 하는 응용 프로그램을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-104">[Visual Studio 2017](https://www.visualstudio.com/) supports building, debugging, and running containerized ASP.NET Core apps targeting .NET Core.</span></span> <span data-ttu-id="ab16e-105">Windows 및 Linux 컨테이너가 모두 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-105">Both Windows and Linux containers are supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab16e-106">전제 조건</span><span class="sxs-lookup"><span data-stu-id="ab16e-106">Prerequisites</span></span>

* <span data-ttu-id="ab16e-107">**.NET Core 플랫폼 간 개발** 워크로드가 있는 [Visual Studio 2017](https://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="ab16e-107">[Visual Studio 2017](https://www.visualstudio.com/) with the **.NET Core cross-platform development** workload</span></span>
* [<span data-ttu-id="ab16e-108">Windows용 Docker</span><span class="sxs-lookup"><span data-stu-id="ab16e-108">Docker for Windows</span></span>](https://docs.docker.com/docker-for-windows/install/)

## <a name="installation-and-setup"></a><span data-ttu-id="ab16e-109">설치 및 설정</span><span class="sxs-lookup"><span data-stu-id="ab16e-109">Installation and setup</span></span>

<span data-ttu-id="ab16e-110">Docker 설치의 경우 [Windows용 Docker: 설치하기 전에 알아야 할 사항](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install)의 정보를 검토하고 [Windows용 Docker](https://docs.docker.com/docker-for-windows/install/)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-110">For Docker installation, review the information at [Docker for Windows: What to know before you install](https://docs.docker.com/docker-for-windows/install/#what-to-know-before-you-install) and install [Docker For Windows](https://docs.docker.com/docker-for-windows/install/).</span></span>

<span data-ttu-id="ab16e-111">Windows용 Docker에서 **[공유 드라이브](https://docs.docker.com/docker-for-windows/#shared-drives)**는 볼륨 매핑 및 디버깅을 지원하도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-111">**[Shared Drives](https://docs.docker.com/docker-for-windows/#shared-drives)** in Docker for Windows must be configured to support volume mapping and debugging.</span></span> <span data-ttu-id="ab16e-112">시스템 트레이 Docker 아이콘을 마우스 오른쪽 단추로 클릭을 선택 **설정 중...** 를 선택 하 고 **드라이브 공유**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-112">Right-click the System Tray's Docker icon, select **Settings...**, and select **Shared Drives**.</span></span> <span data-ttu-id="ab16e-113">Docker 파일을 저장 하는 드라이브를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-113">Select the drive where Docker stores files.</span></span> <span data-ttu-id="ab16e-114">선택 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-114">Select **Apply**.</span></span>

![공유 드라이브](./visual-studio-tools-for-docker/_static/settings-shared-drives-win.png)

> [!TIP]
> <span data-ttu-id="ab16e-116">Visual Studio 2017 15.6 이후 버전 확인 될 때 **드라이브 공유** 하도록 구성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-116">Visual Studio 2017 versions 15.6 and later prompt when **Shared Drives** aren't configured.</span></span>

## <a name="add-docker-support-to-an-app"></a><span data-ttu-id="ab16e-117">앱에 Docker 지원 추가</span><span class="sxs-lookup"><span data-stu-id="ab16e-117">Add Docker support to an app</span></span>

<span data-ttu-id="ab16e-118">ASP.NET Core 프로젝트에 Docker 지원을 추가 하기 위해 프로젝트.NET Core를 대상으로 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-118">In order to add Docker support to an ASP.NET Core project, the project must target .NET Core.</span></span> <span data-ttu-id="ab16e-119">Linux 및 Windows 컨테이너를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-119">Both Linux and Windows containers are supported.</span></span>

<span data-ttu-id="ab16e-120">Docker 지원에는 프로젝트를 추가할 때는 Windows 또는 Linux 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-120">When adding Docker support to a project, choose either a Windows or a Linux container.</span></span> <span data-ttu-id="ab16e-121">Docker 호스트는 동일한 컨테이너 형식을 실행 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-121">The Docker host must be running the same container type.</span></span> <span data-ttu-id="ab16e-122">실행 중인 Docker 인스턴스에서 컨테이너 형식을 변경하려면 시스템 트레이의 Docker 아이콘을 마우스 오른쪽 단추로 클릭하고 **Windows 컨테이너로 전환** 또는 **Linux 컨테이너로 전환**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-122">To change the container type in the running Docker instance, right-click the System Tray's Docker icon and choose **Switch to Windows containers...** or **Switch to Linux containers...**.</span></span>

### <a name="new-app"></a><span data-ttu-id="ab16e-123">새 앱</span><span class="sxs-lookup"><span data-stu-id="ab16e-123">New app</span></span>

<span data-ttu-id="ab16e-124">**ASP.NET Core 웹 응용 프로그램** 프로젝트 템플릿을 사용하여 새 앱을 만들 때 **Docker 지원 활성화** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-124">When creating a new app with the **ASP.NET Core Web Application** project templates, select the **Enable Docker Support** checkbox:</span></span>

![Docker 지원 활성화 확인란](visual-studio-tools-for-docker/_static/enable-docker-support-checkbox.png)

<span data-ttu-id="ab16e-126">대상 프레임 워크가.NET Core 하는 경우는 **OS** 드롭 다운 컨테이너 유형을 선택이 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-126">If the target framework is .NET Core, the **OS** drop-down allows for the selection of a container type.</span></span>

### <a name="existing-app"></a><span data-ttu-id="ab16e-127">기존 앱</span><span class="sxs-lookup"><span data-stu-id="ab16e-127">Existing app</span></span>

<span data-ttu-id="ab16e-128">Visual Studio Tools for Docker는 .NET Framework를 대상으로 하는 기존 ASP.NET Core 프로젝트에 Docker 추가를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-128">The Visual Studio Tools for Docker don't support adding Docker to an existing ASP.NET Core project targeting .NET Framework.</span></span> <span data-ttu-id="ab16e-129">.NET Core를 대상으로 하는 ASP.NET Core 프로젝트의 경우 도구를 통해 Docker 지원을 추가하는 두 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-129">For ASP.NET Core projects targeting .NET Core, there are two options for adding Docker support via the tooling.</span></span> <span data-ttu-id="ab16e-130">Visual Studio에서 프로젝트를 열고 다음 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-130">Open the project in Visual Studio, and choose one of the following options:</span></span>

* <span data-ttu-id="ab16e-131">**프로젝트** 메뉴에서 **Docker 지원**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-131">Select **Docker Support** from the **Project** menu.</span></span>
* <span data-ttu-id="ab16e-132">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **Docker 지원**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-132">Right-click the project in Solution Explorer and select **Add** > **Docker Support**.</span></span>

## <a name="docker-assets-overview"></a><span data-ttu-id="ab16e-133">Docker 자산 개요</span><span class="sxs-lookup"><span data-stu-id="ab16e-133">Docker assets overview</span></span>

<span data-ttu-id="ab16e-134">Visual Studio Tools for Docker는 다음을 포함하여 솔루션에 *docker-compose* 프로젝트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-134">The Visual Studio Tools for Docker add a *docker-compose* project to the solution, containing the following:</span></span>

* <span data-ttu-id="ab16e-135">*.dockerignore*: 빌드 컨텍스트를 생성할 때 제외할 파일 및 디렉터리 패턴의 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-135">*.dockerignore*: Contains a list of file and directory patterns to exclude when generating a build context.</span></span>
* <span data-ttu-id="ab16e-136">*docker-compose.yml*: 빌드되어 `docker-compose build` 및 `docker-compose run`으로 각각 실행할 이미지 컬렉션을 정의하는 데 사용되는 기본 [Docker Compose](https://docs.docker.com/compose/overview/) 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-136">*docker-compose.yml*: The base [Docker Compose](https://docs.docker.com/compose/overview/) file used to define the collection of images to be built and run with `docker-compose build` and `docker-compose run`, respectively.</span></span>
* <span data-ttu-id="ab16e-137">*docker-compose.override.yml*: 서비스에 대한 구성 재정의를 포함하는 Docker Compose에서 읽는 옵션 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-137">*docker-compose.override.yml*: An optional file, read by Docker Compose, containing configuration overrides for services.</span></span> <span data-ttu-id="ab16e-138">Visual Studio는 `docker-compose -f "docker-compose.yml" -f "docker-compose.override.yml"`을 실행하여 이러한 파일을 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-138">Visual Studio executes `docker-compose -f "docker-compose.yml" -f "docker-compose.override.yml"` to merge these files.</span></span>

<span data-ttu-id="ab16e-139">최종 Docker 이미지를 만들기 위한 레시피인 *Dockerfile*은 프로젝트 루트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-139">A *Dockerfile*, the recipe for creating a final Docker image, is added to the project root.</span></span> <span data-ttu-id="ab16e-140">그 안의 명령을 이해하려면 [Dockerfile 참조](https://docs.docker.com/engine/reference/builder/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab16e-140">Refer to [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for an understanding of the commands within it.</span></span> <span data-ttu-id="ab16e-141">이 특정 *Dockerfile*은 빌드 단계라는 네 개의 단계를 포함하는 [다단계 빌드](https://docs.docker.com/engine/userguide/eng-image/multistage-build/)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-141">This particular *Dockerfile* uses a [multi-stage build](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) containing four distinct, named build stages:</span></span>

[!code-dockerfile[](visual-studio-tools-for-docker/samples/HelloDockerTools/HelloDockerTools/Dockerfile?highlight=1,5,14,17)]

<span data-ttu-id="ab16e-142">*Dockerfile*은 [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore) 이미지를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-142">The *Dockerfile* is based on the [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore) image.</span></span> <span data-ttu-id="ab16e-143">이 기본 이미지는 시작 성능을 개선하도록 prejit된 ASP.NET Core NuGet 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-143">This base image includes the ASP.NET Core NuGet packages, which have been pre-jitted to improve startup performance.</span></span>

<span data-ttu-id="ab16e-144">*docker compose.yml* 파일 프로젝트를 실행할 때 만들어진 이미지의 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-144">The *docker-compose.yml* file contains the name of the image that's created when the project runs:</span></span>

[!code-yaml[](visual-studio-tools-for-docker/samples/HelloDockerTools/docker-compose.yml?highlight=5)]

<span data-ttu-id="ab16e-145">앞의 예제에서 `image: hellodockertools`는 앱이 **디버그** 모드에서 실행될 때 `hellodockertools:dev` 이미지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-145">In the preceding example, `image: hellodockertools` generates the image `hellodockertools:dev` when the app runs in **Debug** mode.</span></span> <span data-ttu-id="ab16e-146">앱이 **릴리스** 모드에서 실행될 때 `hellodockertools:latest` 이미지가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-146">The `hellodockertools:latest` image is generated when the app runs in **Release** mode.</span></span>

<span data-ttu-id="ab16e-147">이미지 이름 앞의 [Docker 허브](https://hub.docker.com/) 사용자 이름 (예를 들어 `dockerhubusername/hellodockertools`) 경우 이미지 레지스트리에 밀어넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-147">Prefix the image name with the [Docker Hub](https://hub.docker.com/) username (for example, `dockerhubusername/hellodockertools`) if the image will be pushed to the registry.</span></span> <span data-ttu-id="ab16e-148">또는 개인 레지스트리 URL을 포함 하도록 이미지 이름 변경 (예를 들어 `privateregistry.domain.com/hellodockertools`) 구성에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-148">Alternatively, change the image name to include the private registry URL (for example, `privateregistry.domain.com/hellodockertools`) depending on the configuration.</span></span>

## <a name="debug"></a><span data-ttu-id="ab16e-149">디버그</span><span class="sxs-lookup"><span data-stu-id="ab16e-149">Debug</span></span>

<span data-ttu-id="ab16e-150">도구 모음의 디버그 드롭다운에서 **Docker**를 선택하고 앱에서 디버깅을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-150">Select **Docker** from the debug drop-down in the toolbar, and start debugging the app.</span></span> <span data-ttu-id="ab16e-151">**출력** 창의 **Docker** 뷰는 진행 중인 다음 작업을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-151">The **Docker** view of the **Output** window shows the following actions taking place:</span></span>

* <span data-ttu-id="ab16e-152">*microsoft/aspnetcore* 런타임 이미지 (아직 있는 경우 캐시) 획득 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-152">The *microsoft/aspnetcore* runtime image is acquired (if not already in the cache).</span></span>
* <span data-ttu-id="ab16e-153">*microsoft/aspnetcore 빌드* 이미지 컴파일/게시 (아직 있는 경우 캐시) 획득 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-153">The *microsoft/aspnetcore-build* compile/publish image is acquired (if not already in the cache).</span></span>
* <span data-ttu-id="ab16e-154">*ASPNETCORE_ENVIRONMENT* 환경 변수는 컨테이너 내에서 `Development`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-154">The *ASPNETCORE_ENVIRONMENT* environment variable is set to `Development` within the container.</span></span>
* <span data-ttu-id="ab16e-155">포트 80이 노출되고 동적으로 할당된 localhost용 포트에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-155">Port 80 is exposed and mapped to a dynamically-assigned port for localhost.</span></span> <span data-ttu-id="ab16e-156">포트는 Docker 호스트에 의해 결정되며 `docker ps` 명령을 사용하여 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-156">The port is determined by the Docker host and can be queried with the `docker ps` command.</span></span>
* <span data-ttu-id="ab16e-157">응용 프로그램 컨테이너에 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-157">The app is copied to the container.</span></span>
* <span data-ttu-id="ab16e-158">기본 브라우저에서 동적으로 할당 된 포트를 사용 하 여 컨테이너에 연결 된 디버거가으로 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-158">The default browser is launched with the debugger attached to the container using the dynamically-assigned port.</span></span> 

<span data-ttu-id="ab16e-159">결과 Docker 이미지를는 *dev* 응용 프로그램의 이미지는 *microsoft/aspnetcore* 기본 이미지로 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-159">The resulting Docker image is the *dev* image of the app with the *microsoft/aspnetcore* images as the base image.</span></span> <span data-ttu-id="ab16e-160">**패키지 관리자 콘솔**(PMC) 창에서 `docker images` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-160">Run the `docker images` command in the **Package Manager Console** (PMC) window.</span></span> <span data-ttu-id="ab16e-161">컴퓨터에 이미지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-161">The images on the machine are displayed:</span></span>

```console
REPOSITORY                   TAG                   IMAGE ID            CREATED             SIZE
hellodockertools             latest                f8f9d6c923e2        About an hour ago   391MB
hellodockertools             dev                   85c5ffee5258        About an hour ago   389MB
microsoft/aspnetcore-build   2.0-nanoserver-1709   d7cce94e3eb0        15 hours ago        1.86GB
microsoft/aspnetcore         2.0-nanoserver-1709   8872347d7e5d        40 hours ago        389MB
```

> [!NOTE]
> <span data-ttu-id="ab16e-162">Dev 이미지로 앱 콘텐츠를 없는 **디버그** 구성 볼륨 탑재를 사용 하 여 반복 환경을 제공 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-162">The dev image lacks the app contents, as **Debug** configurations use volume mounting to provide the iterative experience.</span></span> <span data-ttu-id="ab16e-163">이미지를 푸시하려면 **Release** 구성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-163">To push an image, use the **Release** configuration.</span></span>

<span data-ttu-id="ab16e-164">PMC에서 `docker ps` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-164">Run the `docker ps` command in PMC.</span></span> <span data-ttu-id="ab16e-165">앱은 컨테이너를 사용하여 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-165">Notice the app is running using the container:</span></span>

```console
CONTAINER ID        IMAGE                  COMMAND                   CREATED             STATUS              PORTS                   NAMES
baf9a678c88d        hellodockertools:dev   "C:\\remote_debugge..."   21 seconds ago      Up 19 seconds       0.0.0.0:37630->80/tcp   dockercompose4642749010770307127_hellodockertools_1
```

## <a name="edit-and-continue"></a><span data-ttu-id="ab16e-166">편집하며 계속하기</span><span class="sxs-lookup"><span data-stu-id="ab16e-166">Edit and continue</span></span>

<span data-ttu-id="ab16e-167">정적 파일 및 Razor 뷰에 대한 변경 사항은 자동으로 업데이트되므로 컴파일 단계가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-167">Changes to static files and Razor views are automatically updated without the need for a compilation step.</span></span> <span data-ttu-id="ab16e-168">내용을 변경 및 저장하고 브라우저를 새로 고쳐 업데이트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-168">Make the change, save, and refresh the browser to view the update.</span></span>  

<span data-ttu-id="ab16e-169">코드 파일을 수정하려면 컨테이너 내에서 컴파일하고 Kestrel을 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-169">Modifications to code files requires compiling and a restart of Kestrel within the container.</span></span> <span data-ttu-id="ab16e-170">변경 후 컨테이너 내에서 CTRL + F5를 사용하여 프로세스를 수행하고 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-170">After making the change, use CTRL + F5 to perform the process and start the app within the container.</span></span> <span data-ttu-id="ab16e-171">Docker 컨테이너는 다시 작성 되거나 중지 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-171">The Docker container isn't rebuilt or stopped.</span></span> <span data-ttu-id="ab16e-172">PMC에서 `docker ps` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-172">Run the `docker ps` command in PMC.</span></span> <span data-ttu-id="ab16e-173">원래 컨테이너는 10분 이전을 기준으로 여전히 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-173">Notice the original container is still running as of 10 minutes ago:</span></span>

```console
CONTAINER ID        IMAGE                  COMMAND                   CREATED             STATUS              PORTS                   NAMES
baf9a678c88d        hellodockertools:dev   "C:\\remote_debugge..."   10 minutes ago      Up 10 minutes       0.0.0.0:37630->80/tcp   dockercompose4642749010770307127_hellodockertools_1
```

## <a name="publish-docker-images"></a><span data-ttu-id="ab16e-174">Docker 이미지 게시</span><span class="sxs-lookup"><span data-stu-id="ab16e-174">Publish Docker images</span></span>

<span data-ttu-id="ab16e-175">응용 프로그램의 개발 및 디버그 주기가 완료 되 면 Docker 용 Visual Studio Tools 만드는 데 도움이 되는 앱의 프로덕션 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-175">Once the develop and debug cycle of the app is completed, the Visual Studio Tools for Docker assist in creating the production image of the app.</span></span> <span data-ttu-id="ab16e-176">구성 드롭다운을 **릴리스**로 변경하고 앱을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-176">Change the configuration drop-down to **Release** and build the app.</span></span> <span data-ttu-id="ab16e-177">도구를 사용 하 여 이미지 생성의 *최신* 태그 개인 레지스트리 또는 Docker 허브에 밀어넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-177">The tooling produces the image with the *latest* tag, which can be pushed to the private registry or Docker Hub.</span></span> 

<span data-ttu-id="ab16e-178">PMC에서 `docker images` 명령을 실행하여 이미지의 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-178">Run the `docker images` command in PMC to see the list of images:</span></span>

```console
REPOSITORY                   TAG                   IMAGE ID            CREATED             SIZE
hellodockertools             latest                4cb1fca533f0        19 seconds ago      391MB
hellodockertools             dev                   85c5ffee5258        About an hour ago   389MB
microsoft/aspnetcore-build   2.0-nanoserver-1709   d7cce94e3eb0        16 hours ago        1.86GB
microsoft/aspnetcore         2.0-nanoserver-1709   8872347d7e5d        40 hours ago        389MB
```

> [!NOTE]
> <span data-ttu-id="ab16e-179">`docker images` 명령은 *\<없음>*(위에 나열되지 않음)으로 식별된 리포지토리 이름 및 태그로 매개자 이미지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-179">The `docker images` command returns intermediary images with repository names and tags identified as *\<none>* (not listed above).</span></span> <span data-ttu-id="ab16e-180">이러한 이름이 지정되지 않는 이미지는 [다단계 빌드](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) *Dockerfile*에 의해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-180">These unnamed images are produced by the [multi-stage build](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) *Dockerfile*.</span></span> <span data-ttu-id="ab16e-181">최종 이미지 빌드의 효율성을 향상시키며&mdash;변경될 때 필요한 레이어만 다시 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-181">They improve the efficiency of building the final image&mdash;only the necessary layers are rebuilt when changes occur.</span></span> <span data-ttu-id="ab16e-182">중간 이미지 필요 없게 된 경우 삭제를 사용 하는 [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-182">When the intermediary images are no longer needed, delete them using the [docker rmi](https://docs.docker.com/engine/reference/commandline/rmi/) command.</span></span>

<span data-ttu-id="ab16e-183">*dev* 이미지와 비교하여 프로덕션 또는 릴리스 이미지의 크기가 작을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-183">There may be an expectation for the production or release image to be smaller in size by comparison to the *dev* image.</span></span> <span data-ttu-id="ab16e-184">볼륨 매핑에 때문에 디버거 및 앱 실행 중이 던 로컬 컴퓨터에서 및 컨테이너 내에 있지 합니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-184">Because of the volume mapping, the debugger and app were running from the local machine and not within the container.</span></span> <span data-ttu-id="ab16e-185">*최신* 이미지는 호스트 컴퓨터에서 앱을 실행하는 데 필요한 앱 코드를 패키징했습니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-185">The *latest* image has packaged the necessary app code to run the app on a host machine.</span></span> <span data-ttu-id="ab16e-186">따라서 델타 앱 코드의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="ab16e-186">Therefore, the delta is the size of the app code.</span></span>
