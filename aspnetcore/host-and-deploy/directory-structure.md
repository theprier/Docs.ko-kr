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
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="aspnet-core-directory-structure"></a><span data-ttu-id="175a3-103">ASP.NET Core 디렉터리 구조</span><span class="sxs-lookup"><span data-stu-id="175a3-103">ASP.NET Core directory structure</span></span>

<span data-ttu-id="175a3-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="175a3-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="175a3-105">ASP.NET Core, 게시 된 응용 프로그램 디렉터리에서에서 *게시*, 응용 프로그램 파일, config 파일, 정적 자산, 패키지 및 런타임 구성 됩니다 (에 대 한 [자체 포함된 배포](/dotnet/core/deploying/#self-contained-deployments-scd)).</span><span class="sxs-lookup"><span data-stu-id="175a3-105">In ASP.NET Core, the published application directory, *publish*, is comprised of application files, config files, static assets, packages, and the runtime (for [self-contained deployments](/dotnet/core/deploying/#self-contained-deployments-scd)).</span></span>


| <span data-ttu-id="175a3-106">앱 유형</span><span class="sxs-lookup"><span data-stu-id="175a3-106">App Type</span></span> | <span data-ttu-id="175a3-107">디렉터리 구조</span><span class="sxs-lookup"><span data-stu-id="175a3-107">Directory Structure</span></span> |
| -------- | ------------------- |
| [<span data-ttu-id="175a3-108">프레임 워크 종속 배포</span><span class="sxs-lookup"><span data-stu-id="175a3-108">Framework-dependent Deployment</span></span>](/dotnet/core/deploying/#framework-dependent-deployments-fdd) | <ul><li><span data-ttu-id="175a3-109">publish&dagger;</span><span class="sxs-lookup"><span data-stu-id="175a3-109">publish&dagger;</span></span><ul><li><span data-ttu-id="175a3-110">로그&dagger; (stdout 로그를 받을 수 필요로 하지 않는 경우 선택 사항)</span><span class="sxs-lookup"><span data-stu-id="175a3-110">logs&dagger; (optional unless required to receive stdout logs)</span></span></li><li><span data-ttu-id="175a3-111">뷰&dagger; (MVC 앱; 뷰 아닌 미리 컴파일하는 경우)</span><span class="sxs-lookup"><span data-stu-id="175a3-111">Views&dagger; (MVC apps; if views aren't precompiled)</span></span></li><li><span data-ttu-id="175a3-112">페이지&dagger; (MVC 또는 Razor 페이지 앱; 페이지가 아닌 미리 컴파일하는 경우)</span><span class="sxs-lookup"><span data-stu-id="175a3-112">Pages&dagger; (MVC or Razor Pages apps; if pages aren't precompiled)</span></span></li><li><span data-ttu-id="175a3-113">wwwroot&dagger;</span><span class="sxs-lookup"><span data-stu-id="175a3-113">wwwroot&dagger;</span></span></li><li><span data-ttu-id="175a3-114">\*\.dll 파일</span><span class="sxs-lookup"><span data-stu-id="175a3-114">\*\.dll files</span></span></li><li><span data-ttu-id="175a3-115">\<어셈블리 이름 >. deps.json</span><span class="sxs-lookup"><span data-stu-id="175a3-115">\<assembly-name>.deps.json</span></span></li><li><span data-ttu-id="175a3-116">\<어셈블리 이름 >.dll</span><span class="sxs-lookup"><span data-stu-id="175a3-116">\<assembly-name>.dll</span></span></li><li><span data-ttu-id="175a3-117">\<어셈블리 이름 >.pdb</span><span class="sxs-lookup"><span data-stu-id="175a3-117">\<assembly-name>.pdb</span></span></li><li><span data-ttu-id="175a3-118">\<어셈블리 이름 >. PrecompiledViews.dll</span><span class="sxs-lookup"><span data-stu-id="175a3-118">\<assembly-name>.PrecompiledViews.dll</span></span></li><li><span data-ttu-id="175a3-119">\<어셈블리 이름 >. PrecompiledViews.pdb</span><span class="sxs-lookup"><span data-stu-id="175a3-119">\<assembly-name>.PrecompiledViews.pdb</span></span></li><li><span data-ttu-id="175a3-120">\<어셈블리 이름 >. runtimeconfig.json</span><span class="sxs-lookup"><span data-stu-id="175a3-120">\<assembly-name>.runtimeconfig.json</span></span></li><li><span data-ttu-id="175a3-121">web.config (IIS 배포)</span><span class="sxs-lookup"><span data-stu-id="175a3-121">web.config (IIS deployments)</span></span></li></ul></li></ul> |
| [<span data-ttu-id="175a3-122">자체 포함된 배포</span><span class="sxs-lookup"><span data-stu-id="175a3-122">Self-contained Deployment</span></span>](/dotnet/core/deploying/#self-contained-deployments-scd) | <ul><li><span data-ttu-id="175a3-123">publish&dagger;</span><span class="sxs-lookup"><span data-stu-id="175a3-123">publish&dagger;</span></span><ul><li><span data-ttu-id="175a3-124">로그&dagger; (stdout 로그를 받을 수 필요로 하지 않는 경우 선택 사항)</span><span class="sxs-lookup"><span data-stu-id="175a3-124">logs&dagger; (optional unless required to receive stdout logs)</span></span></li><li><span data-ttu-id="175a3-125">refs&dagger;</span><span class="sxs-lookup"><span data-stu-id="175a3-125">refs&dagger;</span></span></li><li><span data-ttu-id="175a3-126">뷰&dagger; (MVC 앱; 뷰 아닌 미리 컴파일하는 경우)</span><span class="sxs-lookup"><span data-stu-id="175a3-126">Views&dagger; (MVC apps; if views aren't precompiled)</span></span></li><li><span data-ttu-id="175a3-127">페이지&dagger; (MVC 또는 Razor 페이지 앱; 페이지가 아닌 미리 컴파일하는 경우)</span><span class="sxs-lookup"><span data-stu-id="175a3-127">Pages&dagger; (MVC or Razor Pages apps; if pages aren't precompiled)</span></span></li><li><span data-ttu-id="175a3-128">wwwroot&dagger;</span><span class="sxs-lookup"><span data-stu-id="175a3-128">wwwroot&dagger;</span></span></li><li><span data-ttu-id="175a3-129">\*.dll 파일</span><span class="sxs-lookup"><span data-stu-id="175a3-129">\*.dll files</span></span></li><li><span data-ttu-id="175a3-130">\<어셈블리 이름 >. deps.json</span><span class="sxs-lookup"><span data-stu-id="175a3-130">\<assembly-name>.deps.json</span></span></li><li><span data-ttu-id="175a3-131">\<어셈블리 이름 >.exe</span><span class="sxs-lookup"><span data-stu-id="175a3-131">\<assembly-name>.exe</span></span></li><li><span data-ttu-id="175a3-132">\<어셈블리 이름 >.pdb</span><span class="sxs-lookup"><span data-stu-id="175a3-132">\<assembly-name>.pdb</span></span></li><li><span data-ttu-id="175a3-133">\<어셈블리 이름 >. PrecompiledViews.dll</span><span class="sxs-lookup"><span data-stu-id="175a3-133">\<assembly-name>.PrecompiledViews.dll</span></span></li><li><span data-ttu-id="175a3-134">\<어셈블리 이름 >. PrecompiledViews.pdb</span><span class="sxs-lookup"><span data-stu-id="175a3-134">\<assembly-name>.PrecompiledViews.pdb</span></span></li><li><span data-ttu-id="175a3-135">\<어셈블리 이름 >. runtimeconfig.json</span><span class="sxs-lookup"><span data-stu-id="175a3-135">\<assembly-name>.runtimeconfig.json</span></span></li><li><span data-ttu-id="175a3-136">web.config (IIS 배포)</span><span class="sxs-lookup"><span data-stu-id="175a3-136">web.config (IIS deployments)</span></span></li></ul></li></ul> |

<span data-ttu-id="175a3-137">&dagger;디렉터리를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="175a3-137">&dagger;Indicates a directory</span></span>

<span data-ttu-id="175a3-138">*게시* 디렉터리를 나타냅니다는 *콘텐츠 루트 경로*라고도 하는 *응용 프로그램 기본 경로*를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="175a3-138">The *publish* directory represents the *content root path*, also called the *application base path*, of the deployment.</span></span> <span data-ttu-id="175a3-139">에 원하는 이름이 지정 됩니다는 *게시* 서버에 배포 된 응용 프로그램의 디렉터리를 해당 위치 역할을 서버의 실제 경로 호스팅된 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="175a3-139">Whatever name is given to the *publish* directory of the deployed app on the server, its location serves as the server's physical path to the hosted app.</span></span>

<span data-ttu-id="175a3-140">*wwwroot* 디렉터리에 있는 경우 정적 자산이 포함만 합니다.</span><span class="sxs-lookup"><span data-stu-id="175a3-140">The *wwwroot* directory, if present, only contains static assets.</span></span>

<span data-ttu-id="175a3-141">stdout *로그* 다음 두 가지 방법 중 하나를 사용 하 여 배포에 대 한 디렉터리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="175a3-141">The stdout *logs* directory can be created for the deployment using one of the following two approaches:</span></span>

* <span data-ttu-id="175a3-142">다음 추가 `<Target>` 프로젝트 파일에는 요소:</span><span class="sxs-lookup"><span data-stu-id="175a3-142">Add the following `<Target>` element to the project file:</span></span>

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

   <span data-ttu-id="175a3-143">`<MakeDir>` 요소는 빈 만듭니다 *로그* 게시 된 출력에는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="175a3-143">The `<MakeDir>` element creates an empty *Logs* folder in the published output.</span></span> <span data-ttu-id="175a3-144">요소를 사용 하 여는 `PublishDir` 폴더를 만들기 위한 대상 위치를 확인 하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="175a3-144">The element uses the `PublishDir` property to determine the target location for creating the folder.</span></span> <span data-ttu-id="175a3-145">웹 배포와 같은 몇 가지 배포 방법, 배포 하는 동안 빈 폴더를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="175a3-145">Several deployment methods, such as Web Deploy, skip empty folders during deployment.</span></span> <span data-ttu-id="175a3-146">`<WriteLinesToFile>` 에 파일을 생성 하는 요소는 *로그* 폴더를이 서버에 폴더의 배포를 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="175a3-146">The `<WriteLinesToFile>` element generates a file in the *Logs* folder, which guarantees deployment of the folder to the server.</span></span> <span data-ttu-id="175a3-147">작업자 프로세스가 대상 폴더에 대 한 쓰기 권한이 하지 않는 경우 폴더 만들기 오류가 여전히 발생할 수 있는 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="175a3-147">Note that folder creation may still fail if the worker process doesn't have write access to the target folder.</span></span>

* <span data-ttu-id="175a3-148">실제로 만들지는 *로그* 디렉터리는 배포의 서버에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="175a3-148">Physically create the *Logs* directory on the server in the deployment.</span></span>

<span data-ttu-id="175a3-149">배포 디렉터리에 읽기/Execute 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="175a3-149">The deployment directory requires Read/Execute permissions.</span></span> <span data-ttu-id="175a3-150">*로그* 디렉터리에 대 한 읽기/쓰기 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="175a3-150">The *Logs* directory requires Read/Write permissions.</span></span> <span data-ttu-id="175a3-151">추가 디렉터리를이 파일은 읽기/쓰기 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="175a3-151">Additional directories where files are written require Read/Write permissions.</span></span>
