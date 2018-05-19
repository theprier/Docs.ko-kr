---
title: ASP.NET Core에서 Razor 뷰 컴파일 및 미리 컴파일
author: rick-anderson
description: ASP.NET Core 앱에서 MVC Razor 뷰 컴파일 및 미리 컴파일을 사용하도록 설정하는 방법에 대해 알아봅니다.
manager: wpickett
ms.author: riande
ms.date: 12/13/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: article
uid: mvc/views/view-compilation
ms.openlocfilehash: 013ca0d149c6415b5e6825aa5a48e93ae48f6728
ms.sourcegitcommit: 0063338c2e130409081bb60fcffa0c3f190cd46a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/12/2018
---
# <a name="razor-file-cshtml-compilation-in-aspnet-core"></a><span data-ttu-id="524d8-103">ASP.NET Core의 Razor 파일(.cshtml) 컴파일</span><span class="sxs-lookup"><span data-stu-id="524d8-103">Razor file (.cshtml) compilation in ASP.NET Core</span></span>

<span data-ttu-id="524d8-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="524d8-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="524d8-105">Razor 뷰는 뷰를 호출할 때 런타임에서 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-105">Razor views are compiled at runtime when the view is invoked.</span></span> <span data-ttu-id="524d8-106">ASP.NET Core 2.1.0 이상은 [Razor Sdk](/aspnetcore/mvc/razor-pages/sdk)를 사용하여 빌드 및 게시 시점에 보기를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-106">ASP.NET Core 2.1.0 or later compile views at build and publish time using [Razor Sdk](/aspnetcore/mvc/razor-pages/sdk).</span></span> <span data-ttu-id="524d8-107">ASP.NET Core 1.1 및 ASP.NET Core 2.0에서 보기는 필요에 따라 미리 컴파일 도구를 사용하여 &mdash; 앱 게시 및 배포 시 컴파일될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-107">In ASP.NET Core 1.1, and ASP.NET Core 2.0, views can optionally be compiled at publish and deployed with the app &mdash; using the precompilation tool.</span></span> 



<span data-ttu-id="524d8-108">미리 컴파일 고려 사항:</span><span class="sxs-lookup"><span data-stu-id="524d8-108">Precompilation considerations:</span></span>

* <span data-ttu-id="524d8-109">뷰를 미리 컴파일하면 게시된 번들 크기는 작아지고 시작 시간은 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-109">Precompiling views results in a smaller published bundle and faster startup time.</span></span>
* <span data-ttu-id="524d8-110">뷰를 미리 컴파일한 후에는 Razor 파일을 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-110">You can't edit Razor files after you precompile views.</span></span> <span data-ttu-id="524d8-111">편집된 뷰는 게시된 번들에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-111">The edited views won't be present in the published bundle.</span></span> 

<span data-ttu-id="524d8-112">미리 컴파일된 뷰를 배포하려면</span><span class="sxs-lookup"><span data-stu-id="524d8-112">To deploy precompiled views:</span></span>

# <a name="aspnet-core-21tabaspnetcore21"></a>[<span data-ttu-id="524d8-113">ASP.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="524d8-113">ASP.NET Core 2.1</span></span>](#tab/aspnetcore21/)
<span data-ttu-id="524d8-114">Razor 파일의 빌드 및 게시 시점 컴파일은 Razor Sdk에서 기본적으로 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-114">Build and publish time compilation of Razor files is enabled by default by the Razor Sdk.</span></span> <span data-ttu-id="524d8-115">업데이트된 후에 Razor 파일을 편집하는 작업은 빌드 시 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-115">Editing Razor files after they are updated is supported at build time.</span></span> <span data-ttu-id="524d8-116">기본적으로 컴파일된 *Views.dll*만이 응용 프로그램과 함께 배포되고 cshtml 파일은 배포되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-116">By default, only the compiled *Views.dll* and no cshtml files are deployed with your application.</span></span> 
    
> [!IMPORTANT]
> <span data-ttu-id="524d8-117">Razor Sdk는 미리 컴파일 특정 속성이 프로젝트 파일에서 설정되지 않은 경우에만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-117">The Razor Sdk is only effective when no precompilation specific properties are set in your project file.</span></span> <span data-ttu-id="524d8-118">예를 들어 *.csproj* 파일에서 `MvcRazorCompileOnPublish`를 설정하면 Razor Sdk를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-118">For instance, setting `MvcRazorCompileOnPublish` in your *.csproj* file will disable the Razor Sdk.</span></span>

# <a name="aspnet-core-20tabaspnetcore20"></a>[<span data-ttu-id="524d8-119">ASP.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="524d8-119">ASP.NET Core 2.0</span></span>](#tab/aspnetcore20/)

<span data-ttu-id="524d8-120">프로젝트가 .NET Framework를 대상으로 하는 경우 [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/)에 대한 패키지 참조를 포함시킵니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-120">If your project targets .NET Framework, include a package reference to [Microsoft.AspNetCore.Mvc.Razor.ViewCompilation](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc.Razor.ViewCompilation/):</span></span>

```xml
<PackageReference Include="Microsoft.AspNetCore.Mvc.Razor.ViewCompilation" Version="2.0.0" PrivateAssets="All" />
```

<span data-ttu-id="524d8-121">프로젝트가 .NET Core를 대상으로 하는 경우 변경 작업이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-121">If your project targets .NET Core, no changes are necessary.</span></span>

<span data-ttu-id="524d8-122">ASP.NET Core 2.x 프로젝트 템플릿은 기본적으로 `MvcRazorCompileOnPublish`를 `true`로 암시적으로 설정하므로 이 노드를 *.csproj* 파일에서 안전하게 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-122">The ASP.NET Core 2.x project templates implicitly sets `MvcRazorCompileOnPublish` to `true` by default, which means this node can be safely removed from the *.csproj* file.</span></span>
    
> [!IMPORTANT]
> <span data-ttu-id="524d8-123">ASP.NET Core 2.0에서 [SCD(자체 포함 배포)](/dotnet/core/deploying/#self-contained-deployments-scd)를 수행하는 경우 Razor 보기 미리 컴파일은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-123">Razor view precompilation in not available when performing a [self-contained deployment (SCD)](/dotnet/core/deploying/#self-contained-deployments-scd) in ASP.NET Core 2.0.</span></span> 

<span data-ttu-id="524d8-124">[.NET Core CLI 게시 명령](/dotnet/core/tools/dotnet-publish)을 사용하여 [프레임워크 종속 배포](/dotnet/core/deploying/#framework-dependent-deployments-fdd)에 대한 앱을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-124">Prepare the app for a [framework-dependent deployment](/dotnet/core/deploying/#framework-dependent-deployments-fdd) with the [.NET Core CLI publish command](/dotnet/core/tools/dotnet-publish).</span></span> <span data-ttu-id="524d8-125">예를 들어 프로젝트 루트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-125">For example, execute the following command at the project root:</span></span>

```console
dotnet publish -c Release
```

<span data-ttu-id="524d8-126">미리 컴파일에 성공하면 컴파일된 Razor 뷰가 포함된 *<project_name>.PrecompiledViews.dll* 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-126">A *<project_name>.PrecompiledViews.dll* file, containing the compiled Razor views, is produced when precompilation succeeds.</span></span> <span data-ttu-id="524d8-127">예를 들어 아래 스크린샷은 *WebApplication1.PrecompiledViews.dll* 내부에서 *Index.cshtml*의 내용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-127">For example, the screenshot below depicts the contents of *Index.cshtml* inside of *WebApplication1.PrecompiledViews.dll*:</span></span>

![DLL 내에서 Razor 뷰](view-compilation/_static/razor-views-in-dll.png)

# <a name="aspnet-core-1xtabaspnetcore1x"></a>[<span data-ttu-id="524d8-129">ASP.NET Core 1.x</span><span class="sxs-lookup"><span data-stu-id="524d8-129">ASP.NET Core 1.x</span></span>](#tab/aspnetcore1x/)

<span data-ttu-id="524d8-130">`MvcRazorCompileOnPublish`를 `true`로 설정하고 `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation`에 대한 패키지 참조를 포함시킵니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-130">Set `MvcRazorCompileOnPublish` to `true` and include a package reference to `Microsoft.AspNetCore.Mvc.Razor.ViewCompilation`.</span></span> <span data-ttu-id="524d8-131">다음 *.csproj* 샘플은 이러한 설정을 강조 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="524d8-131">The following *.csproj* sample highlights these settings:</span></span>

[!code-xml[](view-compilation/sample/MvcRazorCompileOnPublish.csproj?highlight=5,12)]

---

