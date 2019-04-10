---
title: Razor 구성 요소 및 Blazor 호스트 및 배포
author: guardrex
description: Razor 구성 요소 및 Blazor 앱을 호스트하고 배포하는 방법을 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 03/28/2019
uid: host-and-deploy/razor-components-blazor/index
ms.openlocfilehash: eeaa27bef584523b77d8b47000b310fe0cac7341
ms.sourcegitcommit: 6bde1fdf686326c080a7518a6725e56e56d8886e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59070310"
---
# <a name="host-and-deploy-razor-components-and-blazor"></a><span data-ttu-id="6aa12-103">Razor 구성 요소 및 Blazor 호스트 및 배포</span><span class="sxs-lookup"><span data-stu-id="6aa12-103">Host and deploy Razor Components and Blazor</span></span>

<span data-ttu-id="6aa12-104">작성자: [Luke Latham](https://github.com/guardrex), [Rainer Stropek](https://www.timecockpit.com) 및 [Daniel Roth](https://github.com/danroth27)</span><span class="sxs-lookup"><span data-stu-id="6aa12-104">By [Luke Latham](https://github.com/guardrex), [Rainer Stropek](https://www.timecockpit.com), and [Daniel Roth](https://github.com/danroth27)</span></span>

## <a name="publish-the-app"></a><span data-ttu-id="6aa12-105">앱 게시</span><span class="sxs-lookup"><span data-stu-id="6aa12-105">Publish the app</span></span>

<span data-ttu-id="6aa12-106">앱은 [dotnet publish](/dotnet/core/tools/dotnet-publish) 명령을 사용하여 릴리스 구성으로 배포하기 위해 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aa12-106">Apps are published for deployment in Release configuration with the [dotnet publish](/dotnet/core/tools/dotnet-publish) command.</span></span> <span data-ttu-id="6aa12-107">IDE(통합 개발 환경)는 기본 제공 게시 기능을 사용하여 자동으로 `dotnet publish` 명령의 실행을 처리할 수 있으므로, 사용 중인 개발 도구에 따라 명령 프롬프트에서 수동으로 명령을 실행할 필요가 없을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aa12-107">An integrated development environment (IDE) may handle executing the `dotnet publish` command automatically using its built-in publishing features, so it might not be necessary to manually execute the command from a command prompt depending on the development tools in use.</span></span>

```console
dotnet publish -c Release
```

`dotnet publish` <span data-ttu-id="6aa12-108">는 배포할 자산을 만들기 전에 프로젝트 종속성의 [복원](/dotnet/core/tools/dotnet-restore)과 프로젝트의 [빌드](/dotnet/core/tools/dotnet-build)를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa12-108">triggers a [restore](/dotnet/core/tools/dotnet-restore) of the project's dependencies and [builds](/dotnet/core/tools/dotnet-build) the project before creating the assets for deployment.</span></span> <span data-ttu-id="6aa12-109">빌드 프로세스의 일부로 앱 다운로드 크기와 로드 시간을 줄이기 위해 사용하지 않는 메서드와 어셈블리를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6aa12-109">As part of the build process, unused methods and assemblies are removed to reduce app download size and load times.</span></span> <span data-ttu-id="6aa12-110">배포는 */bin/Release/{대상 프레임워크}/publish* 폴더에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aa12-110">The deployment is created in the */bin/Release/{TARGET FRAMEWORK}/publish* folder.</span></span>

<span data-ttu-id="6aa12-111">*publish* 폴더의 자산은 웹 서버에 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aa12-111">The assets in the *publish* folder are deployed to the web server.</span></span> <span data-ttu-id="6aa12-112">배포는 사용 중인 개발 도구에 따라 수동 프로세스일 수도 있고 자동 프로세스일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aa12-112">Deployment might be a manual or automated process depending on the development tools in use.</span></span>

## <a name="deployment"></a><span data-ttu-id="6aa12-113">배포</span><span class="sxs-lookup"><span data-stu-id="6aa12-113">Deployment</span></span>

<span data-ttu-id="6aa12-114">배포 지침은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6aa12-114">For deployment guidance, see the following topics:</span></span>

* [<span data-ttu-id="6aa12-115">클라이언트 쪽 Blazor</span><span class="sxs-lookup"><span data-stu-id="6aa12-115">Client-side Blazor</span></span>](xref:host-and-deploy/razor-components-blazor/blazor)
* [<span data-ttu-id="6aa12-116">서버 쪽 ASP.NET Core Razor 구성 요소</span><span class="sxs-lookup"><span data-stu-id="6aa12-116">Server-side ASP.NET Core Razor Components</span></span>](xref:host-and-deploy/razor-components-blazor/razor-components)
