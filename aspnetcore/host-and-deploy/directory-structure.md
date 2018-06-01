---
title: ASP.NET Core 디렉터리 구조
author: guardrex
description: 게시된 ASP.NET Core 앱의 디렉터리 구조에 대해 알아봅니다.
manager: wpickett
ms.author: riande
ms.custom: mvc
ms.date: 04/09/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: host-and-deploy/directory-structure
ms.openlocfilehash: a5cc1f23d624643facddc9e2006fb246e5ae66dc
ms.sourcegitcommit: 477d38e33530a305405eaf19faa29c6d805273aa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33838438"
---
# <a name="aspnet-core-directory-structure"></a><span data-ttu-id="a5001-103">ASP.NET Core 디렉터리 구조</span><span class="sxs-lookup"><span data-stu-id="a5001-103">ASP.NET Core directory structure</span></span>

<span data-ttu-id="a5001-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="a5001-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="a5001-105">ASP.NET Core에서 게시된 응용 프로그램 디렉터리인 *publish*는 응용 프로그램 파일, 구성 파일, 정적 자산, 패키지 및 런타임([자체 포함 배포](/dotnet/core/deploying/#self-contained-deployments-scd)의 경우)으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5001-105">In ASP.NET Core, the published application directory, *publish*, is comprised of application files, config files, static assets, packages, and the runtime (for [self-contained deployments](/dotnet/core/deploying/#self-contained-deployments-scd)).</span></span>


| <span data-ttu-id="a5001-106">앱 형식</span><span class="sxs-lookup"><span data-stu-id="a5001-106">App Type</span></span> | <span data-ttu-id="a5001-107">디렉터리 구조</span><span class="sxs-lookup"><span data-stu-id="a5001-107">Directory Structure</span></span> |
| -------- | ------------------- |
| [<span data-ttu-id="a5001-108">프레임워크 종속 배포</span><span class="sxs-lookup"><span data-stu-id="a5001-108">Framework-dependent Deployment</span></span>](/dotnet/core/deploying/#framework-dependent-deployments-fdd) | <ul><li><span data-ttu-id="a5001-109">publish&dagger;</span><span class="sxs-lookup"><span data-stu-id="a5001-109">publish&dagger;</span></span><ul><li><span data-ttu-id="a5001-110">logs&dagger;(stdout 로그를 수신하는 데 필요한 경우가 아니면 선택 사항)</span><span class="sxs-lookup"><span data-stu-id="a5001-110">logs&dagger; (optional unless required to receive stdout logs)</span></span></li><li><span data-ttu-id="a5001-111">Views&dagger;(MVC 앱, 뷰가 미리 컴파일되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="a5001-111">Views&dagger; (MVC apps; if views aren't precompiled)</span></span></li><li><span data-ttu-id="a5001-112">Pages&dagger;(MVC 또는 Razor 페이지 앱, 페이지가 미리 컴파일되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="a5001-112">Pages&dagger; (MVC or Razor Pages apps; if pages aren't precompiled)</span></span></li><li><span data-ttu-id="a5001-113">wwwroot&dagger;</span><span class="sxs-lookup"><span data-stu-id="a5001-113">wwwroot&dagger;</span></span></li><li><span data-ttu-id="a5001-114">\*\.dll 파일</span><span class="sxs-lookup"><span data-stu-id="a5001-114">\*\.dll files</span></span></li><li><span data-ttu-id="a5001-115">\<assembly-name>.deps.json</span><span class="sxs-lookup"><span data-stu-id="a5001-115">\<assembly-name>.deps.json</span></span></li><li><span data-ttu-id="a5001-116">\<assembly-name>.dll</span><span class="sxs-lookup"><span data-stu-id="a5001-116">\<assembly-name>.dll</span></span></li><li><span data-ttu-id="a5001-117">\<assembly-name>.pdb</span><span class="sxs-lookup"><span data-stu-id="a5001-117">\<assembly-name>.pdb</span></span></li><li><span data-ttu-id="a5001-118">\<assembly-name>.PrecompiledViews.dll</span><span class="sxs-lookup"><span data-stu-id="a5001-118">\<assembly-name>.PrecompiledViews.dll</span></span></li><li><span data-ttu-id="a5001-119">\<assembly-name>.PrecompiledViews.pdb</span><span class="sxs-lookup"><span data-stu-id="a5001-119">\<assembly-name>.PrecompiledViews.pdb</span></span></li><li><span data-ttu-id="a5001-120">\<assembly-name>.runtimeconfig.json</span><span class="sxs-lookup"><span data-stu-id="a5001-120">\<assembly-name>.runtimeconfig.json</span></span></li><li><span data-ttu-id="a5001-121">web.config(IIS 배포)</span><span class="sxs-lookup"><span data-stu-id="a5001-121">web.config (IIS deployments)</span></span></li></ul></li></ul> |
| [<span data-ttu-id="a5001-122">자체 포함 배포</span><span class="sxs-lookup"><span data-stu-id="a5001-122">Self-contained Deployment</span></span>](/dotnet/core/deploying/#self-contained-deployments-scd) | <ul><li><span data-ttu-id="a5001-123">publish&dagger;</span><span class="sxs-lookup"><span data-stu-id="a5001-123">publish&dagger;</span></span><ul><li><span data-ttu-id="a5001-124">logs&dagger;(stdout 로그를 수신하는 데 필요한 경우가 아니면 선택 사항)</span><span class="sxs-lookup"><span data-stu-id="a5001-124">logs&dagger; (optional unless required to receive stdout logs)</span></span></li><li><span data-ttu-id="a5001-125">refs&dagger;</span><span class="sxs-lookup"><span data-stu-id="a5001-125">refs&dagger;</span></span></li><li><span data-ttu-id="a5001-126">Views&dagger;(MVC 앱, 뷰가 미리 컴파일되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="a5001-126">Views&dagger; (MVC apps; if views aren't precompiled)</span></span></li><li><span data-ttu-id="a5001-127">Pages&dagger;(MVC 또는 Razor 페이지 앱, 페이지가 미리 컴파일되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="a5001-127">Pages&dagger; (MVC or Razor Pages apps; if pages aren't precompiled)</span></span></li><li><span data-ttu-id="a5001-128">wwwroot&dagger;</span><span class="sxs-lookup"><span data-stu-id="a5001-128">wwwroot&dagger;</span></span></li><li><span data-ttu-id="a5001-129">\*.dll 파일</span><span class="sxs-lookup"><span data-stu-id="a5001-129">\*.dll files</span></span></li><li><span data-ttu-id="a5001-130">\<assembly-name>.deps.json</span><span class="sxs-lookup"><span data-stu-id="a5001-130">\<assembly-name>.deps.json</span></span></li><li><span data-ttu-id="a5001-131">\<assembly-name>.exe</span><span class="sxs-lookup"><span data-stu-id="a5001-131">\<assembly-name>.exe</span></span></li><li><span data-ttu-id="a5001-132">\<assembly-name>.pdb</span><span class="sxs-lookup"><span data-stu-id="a5001-132">\<assembly-name>.pdb</span></span></li><li><span data-ttu-id="a5001-133">\<assembly-name>.PrecompiledViews.dll</span><span class="sxs-lookup"><span data-stu-id="a5001-133">\<assembly-name>.PrecompiledViews.dll</span></span></li><li><span data-ttu-id="a5001-134">\<assembly-name>.PrecompiledViews.pdb</span><span class="sxs-lookup"><span data-stu-id="a5001-134">\<assembly-name>.PrecompiledViews.pdb</span></span></li><li><span data-ttu-id="a5001-135">\<assembly-name>.runtimeconfig.json</span><span class="sxs-lookup"><span data-stu-id="a5001-135">\<assembly-name>.runtimeconfig.json</span></span></li><li><span data-ttu-id="a5001-136">web.config(IIS 배포)</span><span class="sxs-lookup"><span data-stu-id="a5001-136">web.config (IIS deployments)</span></span></li></ul></li></ul> |

<span data-ttu-id="a5001-137">&dagger;디렉터리를 나타냄</span><span class="sxs-lookup"><span data-stu-id="a5001-137">&dagger;Indicates a directory</span></span>

<span data-ttu-id="a5001-138">*publish* 디렉터리는 배포의 *응용 프로그램 기본 경로*라고도 하는 *콘텐츠 루트 경로*를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a5001-138">The *publish* directory represents the *content root path*, also called the *application base path*, of the deployment.</span></span> <span data-ttu-id="a5001-139">서버에 배포된 앱의 *publish* 디렉터리에 어떤 이름을 지정하더라도 해당 위치는 호스트된 앱에 대한 서버의 실제 경로로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5001-139">Whatever name is given to the *publish* directory of the deployed app on the server, its location serves as the server's physical path to the hosted app.</span></span>

<span data-ttu-id="a5001-140">*wwwroot* 디렉터리(있는 경우)에는 정적 자산만 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5001-140">The *wwwroot* directory, if present, only contains static assets.</span></span>

<span data-ttu-id="a5001-141">다음 두 가지 방법 중 하나를 사용하여 stdout *logs* 디렉터리를 배포용으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5001-141">The stdout *logs* directory can be created for the deployment using one of the following two approaches:</span></span>

* <span data-ttu-id="a5001-142">다음 `<Target>` 요소를 프로젝트 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5001-142">Add the following `<Target>` element to the project file:</span></span>

   ```xml
   <Target Name="CreateLogsFolder" AfterTargets="Publish">
     <MakeDir Directories="$(PublishDir)Logs" 
              Condition="!Exists('$(PublishDir)Logs')" />
     <WriteLinesToFile File="$(PublishDir)Logs\.log" 
                       Lines="Generated file" 
                       Overwrite="True" 
                       Condition="!Exists('$(PublishDir)Logs\.log')" />
   </Target>
   ```

   <span data-ttu-id="a5001-143">`<MakeDir>` 요소는 게시된 출력에 빈 *Logs* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5001-143">The `<MakeDir>` element creates an empty *Logs* folder in the published output.</span></span> <span data-ttu-id="a5001-144">이 요소는 `PublishDir` 속성을 사용하여 폴더를 만들 대상 위치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a5001-144">The element uses the `PublishDir` property to determine the target location for creating the folder.</span></span> <span data-ttu-id="a5001-145">웹 배포와 같은 여러 배포 방법에서는 배포 중에 빈 폴더를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="a5001-145">Several deployment methods, such as Web Deploy, skip empty folders during deployment.</span></span> <span data-ttu-id="a5001-146">`<WriteLinesToFile>` 요소는 파일이 서버에 배포되도록 *Logs* 폴더에 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a5001-146">The `<WriteLinesToFile>` element generates a file in the *Logs* folder, which guarantees deployment of the folder to the server.</span></span> <span data-ttu-id="a5001-147">대상 폴더에 대한 쓰기 권한이 작업자 프로세스에 없는 경우에는 폴더 만들기에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5001-147">Note that folder creation may still fail if the worker process doesn't have write access to the target folder.</span></span>

* <span data-ttu-id="a5001-148">배포 시 서버에서 *Logs* 디렉터리를 실제로 만드세요.</span><span class="sxs-lookup"><span data-stu-id="a5001-148">Physically create the *Logs* directory on the server in the deployment.</span></span>

<span data-ttu-id="a5001-149">배포 디렉터리에는 읽기/실행 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a5001-149">The deployment directory requires Read/Execute permissions.</span></span> <span data-ttu-id="a5001-150">*Logs* 디렉터리에는 읽기/쓰기 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a5001-150">The *Logs* directory requires Read/Write permissions.</span></span> <span data-ttu-id="a5001-151">파일이 작성되는 추가 디렉터리에는 읽기/쓰기 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a5001-151">Additional directories where files are written require Read/Write permissions.</span></span>
