---
title: ASP.NET Core 2.1 이상용 Microsoft.AspNetCore.App 메타패키지
author: Rick-Anderson
description: Microsoft.AspNetCore.App 메타패키지에는 지원되는 모든 ASP.NET Core 및 Entity Framework Core 패키지가 포함됩니다.
monikerRange: '>= aspnetcore-2.1'
ms.author: riande
ms.date: 09/20/2017
uid: fundamentals/metapackage-app
ms.openlocfilehash: d27c3aa53d6edd235006dc136f09558395e15b6e
ms.sourcegitcommit: a742b55e4b8276a48b8b4394784554fecd883c84
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45538455"
---
# <a name="microsoftaspnetcoreapp-metapackage-for-aspnet-core-21"></a><span data-ttu-id="2a13f-103">ASP.NET Core 2.1용 Microsoft.AspNetCore.App 메타패키지</span><span class="sxs-lookup"><span data-stu-id="2a13f-103">Microsoft.AspNetCore.App metapackage for ASP.NET Core 2.1</span></span>

<span data-ttu-id="2a13f-104">이 기능을 사용하려면 .NET Core 2.1 이상을 대상으로 하는 ASP.NET Core 2.1 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-104">This feature requires ASP.NET Core 2.1 and later targeting .NET Core 2.1 and later.</span></span>

<span data-ttu-id="2a13f-105">ASP.NET Core용 [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App) [메타패키지](/dotnet/core/packages#metapackages):</span><span class="sxs-lookup"><span data-stu-id="2a13f-105">The [Microsoft.AspNetCore.App](https://www.nuget.org/packages/Microsoft.AspNetCore.App) [metapackage](/dotnet/core/packages#metapackages) for ASP.NET Core:</span></span>

* <span data-ttu-id="2a13f-106">[Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/), [Remotion.Linq](https://www.nuget.org/packages/Remotion.Linq/) 및 [IX-Async](https://www.nuget.org/packages/System.Interactive.Async/)를 제외한 타사 종속성을 포함하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="2a13f-106">Does not include third-party dependencies except for [Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/), [Remotion.Linq](https://www.nuget.org/packages/Remotion.Linq/), and [IX-Async](https://www.nuget.org/packages/System.Interactive.Async/).</span></span> <span data-ttu-id="2a13f-107">이러한 타사 종속성은 주요 프레임워크 기능이 작동하도록 하는 데 필요한 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-107">These 3rd-party dependencies are deemed necessary to ensure the major frameworks features function.</span></span>
* <span data-ttu-id="2a13f-108">이전에 언급한 것 이외의 타사 종속성을 포함하는 것을 제외하고 ASP.NET Core 팀에서 지원하는 모든 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-108">Includes all supported packages by the ASP.NET Core team except those that contain third-party dependencies (other than those previously mentioned).</span></span>
* <span data-ttu-id="2a13f-109">이전에 언급한 것 이외의 타사 종속성을 포함하는 것을 제외하고 Entity Framework 팀에서 지원하는 모든 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-109">Includes all supported packages by the Entity Framework Core team except those that contain third-party dependencies (other than those previously mentioned).</span></span>

<span data-ttu-id="2a13f-110">ASP.NET Core 2.1 이상 Entity Framework Core 2.1 이상의 모든 기능은 `Microsoft.AspNetCore.App` 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-110">All the features of ASP.NET Core 2.1 and later and Entity Framework Core 2.1 and later are included in the `Microsoft.AspNetCore.App` package.</span></span> <span data-ttu-id="2a13f-111">ASP.NET Core 2.1 이상을 대상으로 하는 기본 프로젝트 템플릿에는 이 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-111">The default project templates targeting ASP.NET Core 2.1 and later use this package.</span></span> <span data-ttu-id="2a13f-112">ASP.NET Core 2.1 이상과 Entity Framework Core 2.1 이상을 대상으로 하는 응용 프로그램은 `Microsoft.AspNetCore.App` 패키지를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-112">We recommend applications targeting ASP.NET Core 2.1 and later and Entity Framework Core 2.1 and later use the `Microsoft.AspNetCore.App` package.</span></span>

<span data-ttu-id="2a13f-113">`Microsoft.AspNetCore.App` 메타패키지의 버전 번호는 ASP.NET Core 버전 및 Entity Framework Core 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-113">The version number of the `Microsoft.AspNetCore.App` metapackage represents the ASP.NET Core version and Entity Framework Core version.</span></span>

<span data-ttu-id="2a13f-114">`Microsoft.AspNetCore.App` 메타패키지 사용 시에는 앱을 보호하기 위한 버전 제한 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-114">Using the `Microsoft.AspNetCore.App` metapackage provides version restrictions that protect your app:</span></span>

* <span data-ttu-id="2a13f-115">`Microsoft.AspNetCore.App`에 패키지에 대한 전이적인(직접적이지 않은) 종속성을 가진 패키지가 포함되어 있고, 이러한 버전 번호가 서로 다를 경우 NuGet에서 오류를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-115">If a package is included that has a transitive (not direct) dependency on a package in `Microsoft.AspNetCore.App`, and those version numbers differ, NuGet will generate an error.</span></span>
* <span data-ttu-id="2a13f-116">앱에 추가된 다른 패키지는 `Microsoft.AspNetCore.App`에 포함된 패키지 버전을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-116">Other packages added to your app cannot change the version of packages included in `Microsoft.AspNetCore.App`.</span></span>
* <span data-ttu-id="2a13f-117">버전 일관성은 안정적인 환경을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-117">Version consistency ensures a reliable experience.</span></span> <span data-ttu-id="2a13f-118">`Microsoft.AspNetCore.App`은 동일한 앱에서 함께 사용되는 관련 비트의 테스트되지 않은 버전 조합을 방지하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-118">`Microsoft.AspNetCore.App` was designed to prevent untested version combinations of related bits being used together in the same app.</span></span>

<span data-ttu-id="2a13f-119">`Microsoft.AspNetCore.App` 메타패키지를 사용하는 응용 프로그램은 ASP.NET Core 공유 프레임워크를 자동으로 활용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-119">Applications that use the `Microsoft.AspNetCore.App` metapackage automatically take advantage of the ASP.NET Core shared framework.</span></span> <span data-ttu-id="2a13f-120">`Microsoft.AspNetCore.App` 메타패키지를 사용할 경우, 참조되는 ASP.NET Core NuGet 패키지의 자산이 응용 프로그램을 사용하여 배포되지 **않습니다**. 이러한 자산은 &mdash; ASP.NET Core 공유 프레임워크에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-120">When you use the `Microsoft.AspNetCore.App` metapackage, **no** assets from the referenced ASP.NET Core NuGet packages are deployed with the application&mdash;the ASP.NET Core shared framework contains these assets.</span></span> <span data-ttu-id="2a13f-121">공유 프레임워크의 자산은 응용 프로그램 시작 시간 단축을 위해 미리 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-121">The assets in the shared framework are precompiled to improve application startup time.</span></span> <span data-ttu-id="2a13f-122">자세한 내용은 [.NET Core 배포 패키징](/dotnet/core/build/distribution-packaging)의 "공유 프레임워크"를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a13f-122">For more information, see "shared framework" in [.NET Core distribution packaging](/dotnet/core/build/distribution-packaging).</span></span>

<span data-ttu-id="2a13f-123">다음 프로젝트 파일은 ASP.NET Core용 `Microsoft.AspNetCore.App` 메타패키지를 참조하며 일반적인 ASP.NET Core 2.1 템플릿을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-123">The following project file references the `Microsoft.AspNetCore.App` metapackage for ASP.NET Core and represents a typical ASP.NET Core 2.1 template:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp2.1</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.App" Version="2.1.4" />
  </ItemGroup>

</Project>
```

<span data-ttu-id="2a13f-124">`Microsoft.AspNetCore.App` 참조의 버전 번호는 해당 버전의 공유 프레임워크가 선택된다고 보장할 수 **없습니다**.</span><span class="sxs-lookup"><span data-stu-id="2a13f-124">The version number on the `Microsoft.AspNetCore.App` reference does **not** guarantee that version of the shared framework will be used.</span></span> <span data-ttu-id="2a13f-125">예를 들어 `2.1.1` 버전을 지정했는데 `2.1.3`이 설치되는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-125">For example, suppose version `2.1.1` is specified, but `2.1.3` is installed.</span></span> <span data-ttu-id="2a13f-126">이 경우 앱은 `2.1.3`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-126">In that case, the app uses `2.1.3`.</span></span> <span data-ttu-id="2a13f-127">권장되는 방법은 아니지만 롤포워드 동작을 비활성화할 수 있습니다(패치 및/또는 부 버전).</span><span class="sxs-lookup"><span data-stu-id="2a13f-127">Although not recommended, you can disable roll-forward behavior (patch and/or minor).</span></span> <span data-ttu-id="2a13f-128">패키지 버전 롤포워드 동작에 대한 자세한 내용은 [dotnet 호스트 롤포워드](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a13f-128">For more information on package version roll-forward behavior, see [dotnet host roll forward](https://github.com/dotnet/core-setup/blob/master/Documentation/design-docs/roll-forward-on-no-candidate-fx.md).</span></span>

## <a name="update-aspnet-core"></a><span data-ttu-id="2a13f-129">ASP.NET Core 업데이트</span><span class="sxs-lookup"><span data-stu-id="2a13f-129">Update ASP.NET Core</span></span>

<span data-ttu-id="2a13f-130">`Microsoft.AspNetCore.App` [메타패키지](/dotnet/core/packages#metapackages)는 NuGet에서 업데이트된 기존 패키지가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-130">The `Microsoft.AspNetCore.App` [metapackage](/dotnet/core/packages#metapackages) isn't a traditional package that's updated from NuGet.</span></span> <span data-ttu-id="2a13f-131">`Microsoft.NETCore.App`과 유사한 `Microsoft.AspNetCore.App`은 공유 런타임을 나타내며, NuGet 외부에서 처리되는 특별한 버전 관리 의미 체계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-131">Similar to `Microsoft.NETCore.App`, `Microsoft.AspNetCore.App` represents a shared runtime, which has special versioning semantics handled outside of NuGet.</span></span> <span data-ttu-id="2a13f-132">자세한 내용은 [패키지, 메타패키지 및 프레임워크](/dotnet/core/packages)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a13f-132">For more information, see [Packages, metapackages and frameworks](/dotnet/core/packages).</span></span>

<span data-ttu-id="2a13f-133">ASP.NET Core를 업데이트하려면:</span><span class="sxs-lookup"><span data-stu-id="2a13f-133">To update ASP.NET Core:</span></span>

* <span data-ttu-id="2a13f-134">개발 머신 및 빌드 서버: 다운로드 및 설치 합니다 [.NET Core SDK](https://www.microsoft.com/net/download)를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-134">On development machines and build servers: Download and install the [.NET Core SDK](https://www.microsoft.com/net/download).</span></span>
* <span data-ttu-id="2a13f-135">배포 서버: [.NET Core 런타임](https://www.microsoft.com/net/download)을 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-135">On deployment servers: Download and install the [.NET Core runtime](https://www.microsoft.com/net/download).</span></span>

 <span data-ttu-id="2a13f-136">응용 프로그램을 다시 시작하면 응용 프로그램이 최신 설치 버전으로 롤포워드됩니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-136">Applications will roll forward to the latest installed version on application restart.</span></span> <span data-ttu-id="2a13f-137">프로젝트 파일에서 `Microsoft.AspNetCore.App` 버전 번호를 업데이트할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2a13f-137">It's not necessary to update the `Microsoft.AspNetCore.App` version number in the project file.</span></span> <span data-ttu-id="2a13f-138">자세한 내용은 [Framework 종속 앱 롤포워드](/dotnet/core/versions/selection#framework-dependent-apps-roll-forward)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a13f-138">For more information, see [Framework-dependent apps roll forward](/dotnet/core/versions/selection#framework-dependent-apps-roll-forward).</span></span>

<span data-ttu-id="2a13f-139">응용 프로그램에서 이전에 `Microsoft.AspNetCore.All`을 사용한 경우 [Microsoft.AspNetCore.All에서 Microsoft.AspNetCore.App으로 마이그레이션](xref:fundamentals/metapackage#migrate)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2a13f-139">If your application previously used `Microsoft.AspNetCore.All`, see [Migrating from Microsoft.AspNetCore.All to Microsoft.AspNetCore.App](xref:fundamentals/metapackage#migrate).</span></span>
