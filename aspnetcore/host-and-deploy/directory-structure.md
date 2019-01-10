---
title: ASP.NET Core 디렉터리 구조
author: guardrex
description: 게시된 ASP.NET Core 앱의 디렉터리 구조에 대해 알아봅니다.
monikerRange: '>= aspnetcore-2.2'
ms.author: riande
ms.custom: mvc
ms.date: 12/11/2018
uid: host-and-deploy/directory-structure
ms.openlocfilehash: ee0bebb8b5c688f8471d6420d1641b87ac271f6c
ms.sourcegitcommit: b34b25da2ab68e6495b2460ff570468f16a9bf0d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53284567"
---
# <a name="aspnet-core-directory-structure"></a><span data-ttu-id="9ae01-103">ASP.NET Core 디렉터리 구조</span><span class="sxs-lookup"><span data-stu-id="9ae01-103">ASP.NET Core directory structure</span></span>

<span data-ttu-id="9ae01-104">[Luke Latham](https://github.com/guardrex)으로</span><span class="sxs-lookup"><span data-stu-id="9ae01-104">By [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="9ae01-105">*게시* 디렉터리에는 [dotnet 게시](/dotnet/core/tools/dotnet-publish) 명령에 의해 생성된 앱의 배포 가능한 자산이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae01-105">The *publish* directory contains the app's deployable assets produced by the [dotnet publish](/dotnet/core/tools/dotnet-publish) command.</span></span> <span data-ttu-id="9ae01-106">디렉터리에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ae01-106">The directory contains:</span></span>

* <span data-ttu-id="9ae01-107">애플리케이션 파일</span><span class="sxs-lookup"><span data-stu-id="9ae01-107">Application files</span></span>
* <span data-ttu-id="9ae01-108">구성 파일</span><span class="sxs-lookup"><span data-stu-id="9ae01-108">Configuration files</span></span>
* <span data-ttu-id="9ae01-109">정적 자산</span><span class="sxs-lookup"><span data-stu-id="9ae01-109">Static assets</span></span>
* <span data-ttu-id="9ae01-110">패키지</span><span class="sxs-lookup"><span data-stu-id="9ae01-110">Packages</span></span>
* <span data-ttu-id="9ae01-111">런타임([자체 포함 배포](/dotnet/core/deploying/#self-contained-deployments-scd)만 해당)</span><span class="sxs-lookup"><span data-stu-id="9ae01-111">A runtime ([self-contained deployment](/dotnet/core/deploying/#self-contained-deployments-scd) only)</span></span>

| <span data-ttu-id="9ae01-112">앱 형식</span><span class="sxs-lookup"><span data-stu-id="9ae01-112">App Type</span></span> | <span data-ttu-id="9ae01-113">디렉터리 구조</span><span class="sxs-lookup"><span data-stu-id="9ae01-113">Directory Structure</span></span> |
| -------- | ------------------- |
| [<span data-ttu-id="9ae01-114">프레임워크 종속 배포</span><span class="sxs-lookup"><span data-stu-id="9ae01-114">Framework-dependent Deployment</span></span>](/dotnet/core/deploying/#framework-dependent-deployments-fdd) | <ul><li><span data-ttu-id="9ae01-115">publish&dagger;</span><span class="sxs-lookup"><span data-stu-id="9ae01-115">publish&dagger;</span></span><ul><li><span data-ttu-id="9ae01-116">Logs&dagger;(stdout 로그를 수신하는 데 필요한 경우가 아니면 선택 사항)</span><span class="sxs-lookup"><span data-stu-id="9ae01-116">Logs&dagger; (optional unless required to receive stdout logs)</span></span></li><li><span data-ttu-id="9ae01-117">Views&dagger;(MVC 앱, 뷰가 미리 컴파일되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="9ae01-117">Views&dagger; (MVC apps; if views aren't precompiled)</span></span></li><li><span data-ttu-id="9ae01-118">Pages&dagger;(MVC 또는 Razor 페이지 앱, 페이지가 미리 컴파일되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="9ae01-118">Pages&dagger; (MVC or Razor Pages apps; if pages aren't precompiled)</span></span></li><li><span data-ttu-id="9ae01-119">wwwroot&dagger;</span><span class="sxs-lookup"><span data-stu-id="9ae01-119">wwwroot&dagger;</span></span></li><li><span data-ttu-id="9ae01-120">\*\.dll 파일</span><span class="sxs-lookup"><span data-stu-id="9ae01-120">\*\.dll files</span></span></li><li><span data-ttu-id="9ae01-121">{ASSEMBLY NAME}.deps.json</span><span class="sxs-lookup"><span data-stu-id="9ae01-121">{ASSEMBLY NAME}.deps.json</span></span></li><li><span data-ttu-id="9ae01-122">{ASSEMBLY NAME}.dll</span><span class="sxs-lookup"><span data-stu-id="9ae01-122">{ASSEMBLY NAME}.dll</span></span></li><li><span data-ttu-id="9ae01-123">{ASSEMBLY NAME}.pdb</span><span class="sxs-lookup"><span data-stu-id="9ae01-123">{ASSEMBLY NAME}.pdb</span></span></li><li><span data-ttu-id="9ae01-124">{ASSEMBLY NAME}.Views.dll</span><span class="sxs-lookup"><span data-stu-id="9ae01-124">{ASSEMBLY NAME}.Views.dll</span></span></li><li><span data-ttu-id="9ae01-125">{ASSEMBLY NAME}.Views.pdb</span><span class="sxs-lookup"><span data-stu-id="9ae01-125">{ASSEMBLY NAME}.Views.pdb</span></span></li><li><span data-ttu-id="9ae01-126">{ASSEMBLY NAME}.runtimeconfig.json</span><span class="sxs-lookup"><span data-stu-id="9ae01-126">{ASSEMBLY NAME}.runtimeconfig.json</span></span></li><li><span data-ttu-id="9ae01-127">web.config(IIS 배포)</span><span class="sxs-lookup"><span data-stu-id="9ae01-127">web.config (IIS deployments)</span></span></li></ul></li></ul> |
| [<span data-ttu-id="9ae01-128">자체 포함 배포</span><span class="sxs-lookup"><span data-stu-id="9ae01-128">Self-contained Deployment</span></span>](/dotnet/core/deploying/#self-contained-deployments-scd) | <ul><li><span data-ttu-id="9ae01-129">publish&dagger;</span><span class="sxs-lookup"><span data-stu-id="9ae01-129">publish&dagger;</span></span><ul><li><span data-ttu-id="9ae01-130">Logs&dagger;(stdout 로그를 수신하는 데 필요한 경우가 아니면 선택 사항)</span><span class="sxs-lookup"><span data-stu-id="9ae01-130">Logs&dagger; (optional unless required to receive stdout logs)</span></span></li><li><span data-ttu-id="9ae01-131">Views&dagger;(MVC 앱, 뷰가 미리 컴파일되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="9ae01-131">Views&dagger; (MVC apps; if views aren't precompiled)</span></span></li><li><span data-ttu-id="9ae01-132">Pages&dagger;(MVC 또는 Razor 페이지 앱, 페이지가 미리 컴파일되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="9ae01-132">Pages&dagger; (MVC or Razor Pages apps; if pages aren't precompiled)</span></span></li><li><span data-ttu-id="9ae01-133">wwwroot&dagger;</span><span class="sxs-lookup"><span data-stu-id="9ae01-133">wwwroot&dagger;</span></span></li><li><span data-ttu-id="9ae01-134">\*.dll 파일</span><span class="sxs-lookup"><span data-stu-id="9ae01-134">\*.dll files</span></span></li><li><span data-ttu-id="9ae01-135">{ASSEMBLY NAME}.deps.json</span><span class="sxs-lookup"><span data-stu-id="9ae01-135">{ASSEMBLY NAME}.deps.json</span></span></li><li><span data-ttu-id="9ae01-136">{ASSEMBLY NAME}.dll</span><span class="sxs-lookup"><span data-stu-id="9ae01-136">{ASSEMBLY NAME}.dll</span></span></li><li><span data-ttu-id="9ae01-137">{ASSEMBLY NAME}.exe</span><span class="sxs-lookup"><span data-stu-id="9ae01-137">{ASSEMBLY NAME}.exe</span></span></li><li><span data-ttu-id="9ae01-138">{ASSEMBLY NAME}.pdb</span><span class="sxs-lookup"><span data-stu-id="9ae01-138">{ASSEMBLY NAME}.pdb</span></span></li><li><span data-ttu-id="9ae01-139">{ASSEMBLY NAME}.Views.dll</span><span class="sxs-lookup"><span data-stu-id="9ae01-139">{ASSEMBLY NAME}.Views.dll</span></span></li><li><span data-ttu-id="9ae01-140">{ASSEMBLY NAME}.Views.pdb</span><span class="sxs-lookup"><span data-stu-id="9ae01-140">{ASSEMBLY NAME}.Views.pdb</span></span></li><li><span data-ttu-id="9ae01-141">{ASSEMBLY NAME}.runtimeconfig.json</span><span class="sxs-lookup"><span data-stu-id="9ae01-141">{ASSEMBLY NAME}.runtimeconfig.json</span></span></li><li><span data-ttu-id="9ae01-142">web.config(IIS 배포)</span><span class="sxs-lookup"><span data-stu-id="9ae01-142">web.config (IIS deployments)</span></span></li></ul></li></ul> |

<span data-ttu-id="9ae01-143">&dagger;디렉터리를 나타냄</span><span class="sxs-lookup"><span data-stu-id="9ae01-143">&dagger;Indicates a directory</span></span>

<span data-ttu-id="9ae01-144">*publish* 디렉터리는 배포의 *애플리케이션 기본 경로*라고도 하는 *콘텐츠 루트 경로*를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9ae01-144">The *publish* directory represents the *content root path*, also called the *application base path*, of the deployment.</span></span> <span data-ttu-id="9ae01-145">서버에 배포된 앱의 *publish* 디렉터리에 어떤 이름을 지정하더라도 해당 위치는 호스트된 앱에 대한 서버의 실제 경로로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ae01-145">Whatever name is given to the *publish* directory of the deployed app on the server, its location serves as the server's physical path to the hosted app.</span></span>

<span data-ttu-id="9ae01-146">*wwwroot* 디렉터리(있는 경우)에는 정적 자산만 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ae01-146">The *wwwroot* directory, if present, only contains static assets.</span></span>

<span data-ttu-id="9ae01-147">다음 두 가지 방법 중 하나를 사용하여 stdout *Logs* 디렉터리를 배포용으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ae01-147">The stdout *Logs* directory can be created for the deployment using one of the following two approaches:</span></span>

* <span data-ttu-id="9ae01-148">다음 `<Target>` 요소를 프로젝트 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae01-148">Add the following `<Target>` element to the project file:</span></span>

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

   <span data-ttu-id="9ae01-149">`<MakeDir>` 요소는 게시된 출력에 빈 *Logs* 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9ae01-149">The `<MakeDir>` element creates an empty *Logs* folder in the published output.</span></span> <span data-ttu-id="9ae01-150">이 요소는 `PublishDir` 속성을 사용하여 폴더를 만들 대상 위치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae01-150">The element uses the `PublishDir` property to determine the target location for creating the folder.</span></span> <span data-ttu-id="9ae01-151">웹 배포와 같은 여러 배포 방법에서는 배포 중에 빈 폴더를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="9ae01-151">Several deployment methods, such as Web Deploy, skip empty folders during deployment.</span></span> <span data-ttu-id="9ae01-152">`<WriteLinesToFile>` 요소는 파일이 서버에 배포되도록 *Logs* 폴더에 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae01-152">The `<WriteLinesToFile>` element generates a file in the *Logs* folder, which guarantees deployment of the folder to the server.</span></span> <span data-ttu-id="9ae01-153">대상 폴더에 대한 쓰기 권한이 작업자 프로세스에 없는 경우 이 방법을 사용한 폴더 만들기가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae01-153">Folder creation using this approach fails if the worker process doesn't have write access to the target folder.</span></span>

* <span data-ttu-id="9ae01-154">배포 시 서버에서 *Logs* 디렉터리를 실제로 만드세요.</span><span class="sxs-lookup"><span data-stu-id="9ae01-154">Physically create the *Logs* directory on the server in the deployment.</span></span>

<span data-ttu-id="9ae01-155">배포 디렉터리에는 읽기/실행 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae01-155">The deployment directory requires Read/Execute permissions.</span></span> <span data-ttu-id="9ae01-156">*Logs* 디렉터리에는 읽기/쓰기 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae01-156">The *Logs* directory requires Read/Write permissions.</span></span> <span data-ttu-id="9ae01-157">파일이 작성되는 추가 디렉터리에는 읽기/쓰기 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9ae01-157">Additional directories where files are written require Read/Write permissions.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ae01-158">추가 자료</span><span class="sxs-lookup"><span data-stu-id="9ae01-158">Additional resources</span></span>

* [<span data-ttu-id="9ae01-159">dotnet publish</span><span class="sxs-lookup"><span data-stu-id="9ae01-159">dotnet publish</span></span>](/dotnet/core/tools/dotnet-publish)
* [<span data-ttu-id="9ae01-160">.NET Core 애플리케이션 배포</span><span class="sxs-lookup"><span data-stu-id="9ae01-160">.NET Core application deployment</span></span>](/dotnet/core/deploying/)
* [<span data-ttu-id="9ae01-161">대상 프레임워크</span><span class="sxs-lookup"><span data-stu-id="9ae01-161">Target frameworks</span></span>](/dotnet/standard/frameworks)
* [<span data-ttu-id="9ae01-162">.NET Core RID 카탈로그</span><span class="sxs-lookup"><span data-stu-id="9ae01-162">.NET Core RID Catalog</span></span>](/dotnet/core/rid-catalog)
