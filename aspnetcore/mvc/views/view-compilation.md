---
title: ASP.NET Core에서 Razor 파일 컴파일 및 미리 컴파일
author: rick-anderson
description: Razor 파일을 미리 컴파일할 경우의 이점과 ASP.NET Core 앱에서 Razor 파일 미리 컴파일을 구현하는 방법에 대해 알아보세요.
monikerRange: '>= aspnetcore-1.1'
ms.author: riande
ms.custom: mvc
ms.date: 02/13/2019
uid: mvc/views/view-compilation
ms.openlocfilehash: c4e8f722fdf3d3f64807cc35ff9f349af7f32abd
ms.sourcegitcommit: 6ba5fb1fd0b7f9a6a79085b0ef56206e462094b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56248188"
---
# <a name="razor-file-compilation-in-aspnet-core"></a><span data-ttu-id="7ff14-103">ASP.NET Core의 Razor 파일 컴파일</span><span class="sxs-lookup"><span data-stu-id="7ff14-103">Razor file compilation in ASP.NET Core</span></span>

<span data-ttu-id="7ff14-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="7ff14-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

::: moniker range="= aspnetcore-1.1"

<span data-ttu-id="7ff14-105">Razor 파일은 런타임 시 관련 MVC 뷰가 호출되면 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-105">A Razor file is compiled at runtime, when the associated MVC view is invoked.</span></span> <span data-ttu-id="7ff14-106">빌드 시 Razor 파일 게시는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-106">Build-time Razor file publishing is unsupported.</span></span> <span data-ttu-id="7ff14-107">Razor 파일은 필요에 따라 미리 컴파일 도구를 사용하여 앱 게시 및 배포 시 컴파일될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-107">Razor files can optionally be compiled at publish time and deployed with the app&mdash;using the precompilation tool.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="7ff14-108">Razor 파일은 런타임 시 관련 Razor 페이지 또는 MVC 뷰가 호출되면 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-108">A Razor file is compiled at runtime, when the associated Razor Page or MVC view is invoked.</span></span> <span data-ttu-id="7ff14-109">빌드 시 Razor 파일 게시는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-109">Build-time Razor file publishing is unsupported.</span></span> <span data-ttu-id="7ff14-110">Razor 파일은 필요에 따라 미리 컴파일 도구를 사용하여 앱 게시 및 배포 시 컴파일될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-110">Razor files can optionally be compiled at publish time and deployed with the app&mdash;using the precompilation tool.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="7ff14-111">Razor 파일은 런타임 시 관련 Razor 페이지 또는 MVC 뷰가 호출되면 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-111">A Razor file is compiled at runtime, when the associated Razor Page or MVC view is invoked.</span></span> <span data-ttu-id="7ff14-112">Razor 파일은 [Razor SDK](xref:razor-pages/sdk)를 사용하여 빌드 및 게시 시 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-112">Razor files are compiled at both build and publish time using the [Razor SDK](xref:razor-pages/sdk).</span></span>

::: moniker-end

## <a name="precompilation-considerations"></a><span data-ttu-id="7ff14-113">미리 컴파일 고려 사항</span><span class="sxs-lookup"><span data-stu-id="7ff14-113">Precompilation considerations</span></span>

<span data-ttu-id="7ff14-114">다음은 Razor 파일을 미리 컴파일할 경우의 부작용입니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-114">The following are side effects of precompiling Razor files:</span></span>

* <span data-ttu-id="7ff14-115">더 작게 게시되는 번들</span><span class="sxs-lookup"><span data-stu-id="7ff14-115">A smaller published bundle</span></span>
* <span data-ttu-id="7ff14-116">더 빠른 시작 시간</span><span class="sxs-lookup"><span data-stu-id="7ff14-116">A faster startup time</span></span>
* <span data-ttu-id="7ff14-117">게시된 번들에 연관 콘텐츠가 없기 때문에 Razor 파일을 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-117">You can't edit Razor files&mdash;the associated content is absent from the published bundle.</span></span>

## <a name="deploy-precompiled-files"></a><span data-ttu-id="7ff14-118">미리 컴파일된 파일 배포</span><span class="sxs-lookup"><span data-stu-id="7ff14-118">Deploy precompiled files</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="7ff14-119">Razor 파일의 빌드 및 게시 시점 컴파일은 Razor SDK에서 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-119">Build- and publish-time compilation of Razor files is enabled by default by the Razor SDK.</span></span> <span data-ttu-id="7ff14-120">업데이트된 후에 Razor 파일을 편집하는 작업은 빌드 시 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-120">Editing Razor files after they're updated is supported at build time.</span></span> <span data-ttu-id="7ff14-121">기본적으로 컴파일된 *Views.dll*만이 앱과 함께 배포되고 *cshtml* 파일은 배포되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-121">By default, only the compiled *Views.dll* and no *.cshtml* files are deployed with your app.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ff14-122">미리 컴파일 도구는 ASP.NET Core 3.0에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-122">The precompilation tool will be removed in ASP.NET Core 3.0.</span></span> <span data-ttu-id="7ff14-123">[Razor Sdk](xref:razor-pages/sdk)로 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-123">We recommend migrating to [Razor Sdk](xref:razor-pages/sdk).</span></span>
>
> <span data-ttu-id="7ff14-124">Razor SDK는 미리 컴파일 특정 속성이 프로젝트 파일에서 설정되지 않은 경우에만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-124">The Razor SDK is effective only when no precompilation-specific properties are set in the project file.</span></span> <span data-ttu-id="7ff14-125">예를 들어 *.csproj* 파일의 `MvcRazorCompileOnPublish` 속성을 `true`로 설정하면 Razor SDK가 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-125">For instance, setting the *.csproj* file's `MvcRazorCompileOnPublish` property to `true` disables the Razor SDK.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="7ff14-126">프로젝트가 .NET Framework를 대상으로 하는 경우 [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet 패키지를 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="7ff14-126">If your project targets .NET Framework, install the [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet package:</span></span>

[!code-xml[](view-compilation/sample/DotNetFrameworkProject.csproj?name=snippet_ViewCompilationPackage)]

<span data-ttu-id="7ff14-127">프로젝트가 .NET Core를 대상으로 하는 경우 변경 작업이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-127">If your project targets .NET Core, no changes are necessary.</span></span>

<span data-ttu-id="7ff14-128">ASP.NET Core 2.x 프로젝트 템플릿은 기본적으로 `MvcRazorCompileOnPublish` 속성을 암시적으로 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-128">The ASP.NET Core 2.x project templates implicitly set the `MvcRazorCompileOnPublish` property to `true` by default.</span></span> <span data-ttu-id="7ff14-129">다라서 이 요소는 *.csproj* 파일에서 안전하게 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-129">Consequently, this element can be safely removed from the *.csproj* file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ff14-130">미리 컴파일 도구는 ASP.NET Core 3.0에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-130">The precompilation tool will be removed in ASP.NET Core 3.0.</span></span> <span data-ttu-id="7ff14-131">[Razor Sdk](xref:razor-pages/sdk)로 마이그레이션하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-131">We recommend migrating to [Razor Sdk](xref:razor-pages/sdk).</span></span>
>
> <span data-ttu-id="7ff14-132">ASP.NET Core 2.0에서 [SCD(자체 포함 배포)](/dotnet/core/deploying/#self-contained-deployments-scd)를 수행하는 경우 Razor 파일 미리 컴파일은 사용 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-132">Razor file precompilation is unavailable when performing a [self-contained deployment (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) in ASP.NET Core 2.0.</span></span>

::: moniker-end

::: moniker range="= aspnetcore-1.1"

<span data-ttu-id="7ff14-133">`MvcRazorCompileOnPublish` 속성을 `true`로 설정하고 [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet 패키지를 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="7ff14-133">Set the `MvcRazorCompileOnPublish` property to `true`, and install the [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/) NuGet package.</span></span> <span data-ttu-id="7ff14-134">다음 *.csproj* 샘플은 이러한 설정을 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-134">The following *.csproj* sample highlights these settings:</span></span>

[!code-xml[](view-compilation/sample/MvcRazorCompileOnPublish.csproj?highlight=4,10)]

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="7ff14-135">[.NET Core CLI 게시 명령](/dotnet/core/tools/dotnet-publish)을 사용하여 [프레임워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd)에 대한 앱을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-135">Prepare the app for a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd) with the [.NET Core CLI publish command](/dotnet/core/tools/dotnet-publish).</span></span> <span data-ttu-id="7ff14-136">예를 들어 프로젝트 루트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-136">For example, execute the following command at the project root:</span></span>

```console
dotnet publish -c Release
```

<span data-ttu-id="7ff14-137">미리 컴파일에 성공하면 컴파일된 Razor 파일이 포함된 *<project_name>.PrecompiledViews.dll* 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-137">A *<project_name>.PrecompiledViews.dll* file, containing the compiled Razor files, is produced when precompilation succeeds.</span></span> <span data-ttu-id="7ff14-138">예를 들어 아래 스크린샷은 *WebApplication1.PrecompiledViews.dll* 내부에서 *Index.cshtml*의 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-138">For example, the screenshot below depicts the contents of *Index.cshtml* within *WebApplication1.PrecompiledViews.dll*:</span></span>

![DLL 내에서 Razor 뷰](view-compilation/_static/razor-views-in-dll.png)

::: moniker-end

## <a name="recompile-razor-files-on-change"></a><span data-ttu-id="7ff14-140">변경 시 Razor 파일 다시 컴파일</span><span class="sxs-lookup"><span data-stu-id="7ff14-140">Recompile Razor files on change</span></span>

<span data-ttu-id="7ff14-141"><xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions> <xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions.AllowRecompilingViewsOnFileChange>는 디스크의 파일이 변경되면 Razor 파일(Razor 뷰 및 Razor Pages)이 컴파일되고 업데이트되는지 여부를 결정하는 값을 가져오거나 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-141">The <xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions> <xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions.AllowRecompilingViewsOnFileChange> gets or sets a value that determines if Razor files (Razor views and Razor Pages) are recompiled and updated if files change on disk.</span></span>

<span data-ttu-id="7ff14-142">`true`로 설정하면 [IFileProvider.Watch](xref:Microsoft.Extensions.FileProviders.IFileProvider.Watch*)는 구성된 <xref:Microsoft.Extensions.FileProviders.IFileProvider> 인스턴스에서 Razor 파일의 변경 내용을 감시합니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-142">When set to `true`, [IFileProvider.Watch](xref:Microsoft.Extensions.FileProviders.IFileProvider.Watch*) watches for changes to Razor files in configured <xref:Microsoft.Extensions.FileProviders.IFileProvider> instances.</span></span>

<span data-ttu-id="7ff14-143">다음의 경우 기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-143">The default value is `true` for:</span></span>

* <span data-ttu-id="7ff14-144">ASP.NET Core 2.1 또는 이전 버전의 앱.</span><span class="sxs-lookup"><span data-stu-id="7ff14-144">ASP.NET Core 2.1 or earlier apps.</span></span>
* <span data-ttu-id="7ff14-145">개발 환경의 ASP.NET Core 2.2 이상의 앱.</span><span class="sxs-lookup"><span data-stu-id="7ff14-145">ASP.NET Core 2.2 or later apps in the Development environment.</span></span>

<span data-ttu-id="7ff14-146"><xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions.AllowRecompilingViewsOnFileChange>는 호환성 스위치와 연결되어 있으며 앱에 대해 구성된 호환성 버전에 따라 다른 동작을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-146"><xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions.AllowRecompilingViewsOnFileChange> is associated with a compatibility switch and can provide different behavior depending on the configured compatibility version for the app.</span></span> <span data-ttu-id="7ff14-147"><xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions.AllowRecompilingViewsOnFileChange>를 설정하여 앱을 구성하면 앱의 호환성 버전에 의해 암시된 값보다 우선 순위가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-147">Configuring the app by setting <xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions.AllowRecompilingViewsOnFileChange> takes precedence over the value implied by the app's compatibility version.</span></span>

<span data-ttu-id="7ff14-148">앱의 호환성 버전이 <xref:Microsoft.AspNetCore.Mvc.CompatibilityVersion.Version_2_1> 또는 이전 버전으로 설정된 경우 명시적으로 구성하지 않는 한 <xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions.AllowRecompilingViewsOnFileChange>는 `true`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-148">If the app's compatibility version is set to <xref:Microsoft.AspNetCore.Mvc.CompatibilityVersion.Version_2_1> or earlier, <xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions.AllowRecompilingViewsOnFileChange> is set to `true` unless explicitly configured.</span></span>

<span data-ttu-id="7ff14-149">앱의 호환성 버전이 <xref:Microsoft.AspNetCore.Mvc.CompatibilityVersion.Version_2_2> 이상으로 설정된 경우 환경이 개발이 아니거나 값이 명시적으로 구성되지 않은 경우 <xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions.AllowRecompilingViewsOnFileChange>가 `false`로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ff14-149">If the app's compatibility version is set to <xref:Microsoft.AspNetCore.Mvc.CompatibilityVersion.Version_2_2> or later, <xref:Microsoft.AspNetCore.Mvc.Razor.RazorViewEngineOptions.AllowRecompilingViewsOnFileChange> is set to `false` unless the environment is Development or the value is explicitly configured.</span></span>

<span data-ttu-id="7ff14-150">앱의 호환성 버전 설정에 대한 지침과 예는 <xref:mvc/compatibility-version>을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ff14-150">For guidance and examples of setting the app's compatibility version, see <xref:mvc/compatibility-version>.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7ff14-151">추가 자료</span><span class="sxs-lookup"><span data-stu-id="7ff14-151">Additional resources</span></span>

::: moniker range="= aspnetcore-1.1"

* <xref:mvc/views/overview>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

* <xref:razor-pages/index>
* <xref:mvc/views/overview>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

* <xref:razor-pages/index>
* <xref:mvc/views/overview>
* <xref:razor-pages/sdk>

::: moniker-end
