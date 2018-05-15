---
title: ASP.NET Core Razor SDK
author: Rick-Anderson
description: ASP.NET Core의 Razor 페이지를 통해 MVC를 사용하는 것보다 더 쉽고 더 생산적으로 코딩 페이지에 초점을 맞춘 시나리오를 만드는 방법을 알아봅니다.
manager: wpickett
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 4/12/2018
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: content
uid: mvc/razor-pages/sdk
ms.openlocfilehash: 2cbebb12ccd1098e1950aa7eeb22fab4ffc689e6
ms.sourcegitcommit: c79fd3592f444d58e17518914f8873d0a11219c0
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="aspnet-core-razor-sdk"></a><span data-ttu-id="d73ef-103">ASP.NET Core Razor SDK</span><span class="sxs-lookup"><span data-stu-id="d73ef-103">ASP.NET Core Razor SDK</span></span>

<span data-ttu-id="d73ef-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="d73ef-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[](~/includes/2.1.md)]

<span data-ttu-id="d73ef-105">[!INCLUDE[](~/includes/2.1-SDK.md)]에는 `Microsoft.NET.Sdk.Razor` MSBuild SDK(Razor SDK)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-105">The [!INCLUDE[](~/includes/2.1-SDK.md)] includes the `Microsoft.NET.Sdk.Razor` MSBuild SDK (Razor SDK).</span></span> <span data-ttu-id="d73ef-106">Razor SDK:</span><span class="sxs-lookup"><span data-stu-id="d73ef-106">The Razor SDK:</span></span>

* <span data-ttu-id="d73ef-107">ASP.NET Core MVC 기반 프로젝트용 [Razor](xref:mvc/views/razor) 파일을 포함하는 프로젝트의 빌드, 패키징 및 게시와 관련된 환경을 표준화합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-107">Standardizes the experience around building, packaging, and publishing projects containing [Razor](xref:mvc/views/razor) files for ASP.NET Core MVC-based projects.</span></span>
* <span data-ttu-id="d73ef-108">Razor 파일 컴파일의 사용자 지정을 허용하는 사전 정의된 대상, 속성 및 항목 집합이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-108">Includes a set of predefined targets, properties, and items that allow customizing the compilation of Razor files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d73ef-109">전제 조건</span><span class="sxs-lookup"><span data-stu-id="d73ef-109">Prerequisites</span></span>

[!INCLUDE[](~/includes/2.1-SDK.md)]

## <a name="using-the-razor-sdk"></a><span data-ttu-id="d73ef-110">Razor SDK 사용</span><span class="sxs-lookup"><span data-stu-id="d73ef-110">Using the Razor SDK</span></span>

<span data-ttu-id="d73ef-111">대부분의 웹앱은 Razor SDK를 명시적으로 참조할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-111">Most web apps don't need to expressly reference the Razor SDK.</span></span> 

<span data-ttu-id="d73ef-112">Razor SDK를 사용하여 Razor 보기 또는 Razor 페이지를 포함하는 클래스 라이브러리를 빌드하려면:</span><span class="sxs-lookup"><span data-stu-id="d73ef-112">To use the Razor SDK to build class libraries containing Razor views or Razor Pages:</span></span>

* <span data-ttu-id="d73ef-113">`Microsoft.NET.Sdk` 대신 `Microsoft.NET.Sdk.Razor`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-113">Use `Microsoft.NET.Sdk.Razor` instead of `Microsoft.NET.Sdk`:</span></span>
```xml
<Project SDK="Microsoft.NET.Sdk.Razor">
  ...
</Project>
```

* <span data-ttu-id="d73ef-114">일반적으로 Razor 페이지 및 Razor 보기를 빌드하고 컴파일하는 데 필요한 추가 종속성을 가져오려면 `Microsoft.AspNetCore.Mvc`에 대한 패키지 참조가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-114">Typically a package reference to `Microsoft.AspNetCore.Mvc` is required to bring in additional dependencies required to build and compile Razor Pages and Razor views.</span></span> <span data-ttu-id="d73ef-115">최소한 프로젝트는 다음에 패키지 참조를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-115">At minimum, your project needs to add package references to:</span></span>

    * `Microsoft.AspNetCore.Razor.Design` 
    * `Microsoft.AspNetCore.Mvc.Razor.Extensions`
    
 <span data-ttu-id="d73ef-116">이전 패키지는 `Microsoft.AspNetCore.Mvc`에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-116">The preceding packages are included in `Microsoft.AspNetCore.Mvc`.</span></span> <span data-ttu-id="d73ef-117">다음 표시에서는 Razor SDK를 사용하여 ASP.NET Core Razor 페이지 앱용 Razor 파일을 빌드하는 기본 *.csproj* 파일을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-117">The following markup shows a basic *.csproj* file that uses the Razor SDK to build Razor files for an ASP.NET Core Razor Pages app:</span></span>
    
 [!code-xml[Main](sdk/sample/RazorSDK.csproj)]

### <a name="properties"></a><span data-ttu-id="d73ef-118">속성</span><span class="sxs-lookup"><span data-stu-id="d73ef-118">Properties</span></span>

<span data-ttu-id="d73ef-119">다음 속성은 Razor의 SDK 동작을 프로젝트 빌드의 일부로 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-119">The following properties control the Razor's SDK behavior as part of a project build:</span></span>

* <span data-ttu-id="d73ef-120">`RazorCompileOnBuild`: `true`인 경우, 프로젝트 빌드 중에 Razor 어셈블리를 컴파일하고 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-120">`RazorCompileOnBuild` : When `true`, compiles and emits the Razor assembly as part of building the project.</span></span> <span data-ttu-id="d73ef-121">기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-121">Defaults to `true`.</span></span>
* <span data-ttu-id="d73ef-122">`RazorCompileOnPublish`: `true`인 경우, 프로젝트 게시 중에 Razor 어셈블리를 컴파일하고 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-122">`RazorCompileOnPublish` : When `true`, compiles and emits the Razor assembly as part of publishing the project.</span></span> <span data-ttu-id="d73ef-123">기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-123">Defaults to `true`.</span></span>

<span data-ttu-id="d73ef-124">다음 속성 및 항목은 Razor SDK에 대한 입력 및 출력을 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-124">The following properties and items are used to configure inputs and output to the Razor SDK:</span></span>

| <span data-ttu-id="d73ef-125">항목</span><span class="sxs-lookup"><span data-stu-id="d73ef-125">Items</span></span>                                         | <span data-ttu-id="d73ef-126">설명</span><span class="sxs-lookup"><span data-stu-id="d73ef-126">Description</span></span>                                                                   |
| ------------                                  | -------------                                                                 |
| <span data-ttu-id="d73ef-127">RazorGenerate</span><span class="sxs-lookup"><span data-stu-id="d73ef-127">RazorGenerate</span></span>                                 | <span data-ttu-id="d73ef-128">코드 생성 대상에 입력되는 항목 요소(*.cshtml* 파일).</span><span class="sxs-lookup"><span data-stu-id="d73ef-128">Item elements (*.cshtml* files) that are inputs to code generation targets.</span></span> |
| <span data-ttu-id="d73ef-129">RazorCompile</span><span class="sxs-lookup"><span data-stu-id="d73ef-129">RazorCompile</span></span>                                  | <span data-ttu-id="d73ef-130">Razor 컴파일 대상에 입력되는 항목 요소(.cs 파일).</span><span class="sxs-lookup"><span data-stu-id="d73ef-130">Item elements (.cs files) that are inputs to  Razor compilation targets.</span></span> <span data-ttu-id="d73ef-131">이 ItemGroup을 사용하여 Razor 어셈블리에 컴파일할 추가 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-131">Use this ItemGroup to specify additional files to be compiled in to the Razor assembly.</span></span> |
| <span data-ttu-id="d73ef-132">RazorAssemblyAttribute</span><span class="sxs-lookup"><span data-stu-id="d73ef-132">RazorAssemblyAttribute</span></span>                        | <span data-ttu-id="d73ef-133">코드에 사용된 항목 요소는 Razor 어셈블리의 특성을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-133">Item elements used to code generate attributes for the Razor assembly.</span></span> <span data-ttu-id="d73ef-134">예:</span><span class="sxs-lookup"><span data-stu-id="d73ef-134">For example:</span></span>  <br />`<RazorAssemblyAttribute ` <br />  `Include="System.Reflection.AssemblyMetadataAttribute"`<br />`  _Parameter1="BuildSource" _Parameter2="https://docs.asp.net/">` |
| <span data-ttu-id="d73ef-135">RazorEmbeddedResource</span><span class="sxs-lookup"><span data-stu-id="d73ef-135">RazorEmbeddedResource</span></span>                         | <span data-ttu-id="d73ef-136">생성된 Razor 어셈블리에 포함 리소스로 추가된 항목 요소</span><span class="sxs-lookup"><span data-stu-id="d73ef-136">Item elements added as embedded resources to the generated Razor assembly</span></span> |

| <span data-ttu-id="d73ef-137">속성</span><span class="sxs-lookup"><span data-stu-id="d73ef-137">Property</span></span>                                      | <span data-ttu-id="d73ef-138">설명</span><span class="sxs-lookup"><span data-stu-id="d73ef-138">Description</span></span>                                                                   |
| ------------                                  | -------------                                                                 |
| <span data-ttu-id="d73ef-139">RazorTargetName</span><span class="sxs-lookup"><span data-stu-id="d73ef-139">RazorTargetName</span></span>                               | <span data-ttu-id="d73ef-140">Razor에서 생성한 어셈블리의 파일 이름(확장명 제외).</span><span class="sxs-lookup"><span data-stu-id="d73ef-140">File name (without extension) of the assembly produced by Razor.</span></span> | 
| <span data-ttu-id="d73ef-141">RazorOutputPath</span><span class="sxs-lookup"><span data-stu-id="d73ef-141">RazorOutputPath</span></span>                               | <span data-ttu-id="d73ef-142">Razor 출력 디렉터리.</span><span class="sxs-lookup"><span data-stu-id="d73ef-142">The Razor output directory.</span></span>                                      |
| <span data-ttu-id="d73ef-143">RazorCompileToolset</span><span class="sxs-lookup"><span data-stu-id="d73ef-143">RazorCompileToolset</span></span>                           | <span data-ttu-id="d73ef-144">Razor 어셈블리를 빌드하는 데 사용되는 도구 집합을 결정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-144">Used to determine the toolset used to build the Razor assembly.</span></span> <span data-ttu-id="d73ef-145">유효한 값은 `Implicit` 및 `PrecompilationTool`입니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-145">Valid values are `Implicit`, , and `PrecompilationTool`.</span></span> |
| <span data-ttu-id="d73ef-146">EnableDefaultContentItems</span><span class="sxs-lookup"><span data-stu-id="d73ef-146">EnableDefaultContentItems</span></span>                     | <span data-ttu-id="d73ef-147">`true`인 경우, *.cshtml* 파일과 같은 특정 파일 형식이 프로젝트의 콘텐츠로 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-147">When `true`, includes certain file types, such as *.cshtml* files, as content in the project.</span></span> <span data-ttu-id="d73ef-148">Microsoft.NET.Sdk.Web을 통해 참조하면 *wwwroot* 및 구성 파일에 있는 모든 파일도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-148">When referenced via Microsoft.NET.Sdk.Web, also includes all files under *wwwroot*, and config files.</span></span>         |
| <span data-ttu-id="d73ef-149">EnableDefaultRazorGenerateItems</span><span class="sxs-lookup"><span data-stu-id="d73ef-149">EnableDefaultRazorGenerateItems</span></span>               | <span data-ttu-id="d73ef-150">`true`인 경우, `RazorGenerate` 항목의 `Content` 항목에서 *.cshtml* 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-150">When `true`, includes *.cshtml* files from `Content` items in `RazorGenerate` items.</span></span> |
| <span data-ttu-id="d73ef-151">GenerateRazorTargetAssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="d73ef-151">GenerateRazorTargetAssemblyInfo</span></span>               | <span data-ttu-id="d73ef-152">`true`인 경우, `RazorAssemblyAttribute`로 지정된 특성을 포함하는 *.cs* 파일을 생성하고 이를 컴파일 출력에 포함시킵니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-152">When `true`, generates a *.cs* file containing attributes specified by `RazorAssemblyAttribute` and includes it in the compile output.</span></span> |
| <span data-ttu-id="d73ef-153">EnableDefaultRazorTargetAssemblyInfoAttributes</span><span class="sxs-lookup"><span data-stu-id="d73ef-153">EnableDefaultRazorTargetAssemblyInfoAttributes</span></span> | <span data-ttu-id="d73ef-154">`true`인 경우, `RazorAssemblyAttribute`에 어셈블리 특성의 기본 집합을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-154">When `true`, adds a default set of assembly attributes to `RazorAssemblyAttribute`.</span></span> |
| <span data-ttu-id="d73ef-155">CopyRazorGenerateFilesToPublishDirectory</span><span class="sxs-lookup"><span data-stu-id="d73ef-155">CopyRazorGenerateFilesToPublishDirectory</span></span>       | <span data-ttu-id="d73ef-156">`true`인 경우, RazorGenerate 항목(*.cshtml*) 파일을 게시 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-156">When `true`, copies RazorGenerate items (*.cshtml*) files to the publish directory.</span></span> <span data-ttu-id="d73ef-157">일반적으로 Razor 파일은 빌드 시간 또는 게시 시간에 컴파일에 참여하는 경우 게시된 응용 프로그램에 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-157">Typically Razor files are not needed for a published application if they participate in compilation at build-time or publish-time.</span></span> <span data-ttu-id="d73ef-158">기본값은 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-158">Defaults to `false`.</span></span> |
| <span data-ttu-id="d73ef-159">CopyRefAssembliesToPublishDirectory</span><span class="sxs-lookup"><span data-stu-id="d73ef-159">CopyRefAssembliesToPublishDirectory</span></span>            | <span data-ttu-id="d73ef-160">`true`인 경우, 참조 어셈블리 항목을 게시 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-160">When `true`, copy reference assembly items to the publish directory.</span></span> <span data-ttu-id="d73ef-161">일반적으로 참조 어셈블리는 Razor 컴파일이 빌드 시간 또는 게시 시간에 발생하는 경우 게시된 응용 프로그램에 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-161">Typically reference assemblies are not needed for a published application if Razor compilation occurs at build-time or publish-time.</span></span> <span data-ttu-id="d73ef-162">게시된 응용 프로그램에 런타임 컴파일이 필요한 경우(예: 런타임에 cshtml 파일을 수정하거나 포함된 보기를 사용하는 경우) `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-162">Set to `true`, if your published application requires runtime compilation, for example, modifies cshtml files at runtime, or uses embedded views.</span></span> <span data-ttu-id="d73ef-163">기본값은 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-163">Defaults to `false`.</span></span> |
| <span data-ttu-id="d73ef-164">IncludeRazorContentInPack</span><span class="sxs-lookup"><span data-stu-id="d73ef-164">IncludeRazorContentInPack</span></span>                      | <span data-ttu-id="d73ef-165">`true`인 경우, 모든 Razor 콘텐츠 항목(*.cshtml* 파일)은 생성된 NuGet 패키지에 포함되도록 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-165">When `true`, all Razor content items (*.cshtml* files) will be marked for inclusion in the generated NuGet package.</span></span> <span data-ttu-id="d73ef-166">기본값은 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-166">Defaults to `false`.</span></span> |
| <span data-ttu-id="d73ef-167">EmbedRazorGenerateSources</span><span class="sxs-lookup"><span data-stu-id="d73ef-167">EmbedRazorGenerateSources</span></span> | <span data-ttu-id="d73ef-168">`true`인 경우, 생성된 Razor 어셈블리에 포함된 파일로 RazorGenerate(*.cshtml*) 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-168">When `true`, adds RazorGenerate (*.cshtml*) items as embedded files to the generated Razor assembly.</span></span> <span data-ttu-id="d73ef-169">기본값은 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-169">Defaults to `false`.</span></span> |
| <span data-ttu-id="d73ef-170">UseRazorBuildServer</span><span class="sxs-lookup"><span data-stu-id="d73ef-170">UseRazorBuildServer</span></span>                           | <span data-ttu-id="d73ef-171">`true`인 경우, 영구적 빌드 서버 프로세스를 사용하여 코드 생성 작업을 오프로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-171">When `true`, uses a persistent build server process to offload code generation work.</span></span> <span data-ttu-id="d73ef-172">기본값은 `UseSharedCompilation`입니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-172">Defaults to the value of `UseSharedCompilation`.</span></span> |

### <a name="targets"></a><span data-ttu-id="d73ef-173">대상</span><span class="sxs-lookup"><span data-stu-id="d73ef-173">Targets</span></span>
<span data-ttu-id="d73ef-174">Razor SDK는 두 기본 대상을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-174">The Razor SDK defines two primary targets:</span></span>

* <span data-ttu-id="d73ef-175">`RazorGenerate` - 코드는 RazorGenerate 항목 요소에서 *.cs* 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-175">`RazorGenerate` - Code generates *.cs* files from RazorGenerate item elements.</span></span> <span data-ttu-id="d73ef-176">이 대상 전후에 실행할 수 있는 추가 대상을 지정하려면 `RazorGenerateDependsOn` 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-176">Use `RazorGenerateDependsOn` property to specify additional targets that can run before or after this target.</span></span>
* <span data-ttu-id="d73ef-177">`RazorCompile` - 생성된 *.cs* 파일을 Razor 어셈블리로 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-177">`RazorCompile` - Compiles generated *.cs* files in to a Razor assembly.</span></span> <span data-ttu-id="d73ef-178">이 대상 전후에 실행할 수 있는 추가 대상을 지정하려면 `RazorCompileDependsOn`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d73ef-178">Use `RazorCompileDependsOn` to specify additional targets that can run before or after this target.</span></span>